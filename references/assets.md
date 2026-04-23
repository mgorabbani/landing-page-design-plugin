# Assets — icons, illustrations, photos, patterns, 3D

Don't default to Lucide + stock photos for every site. Match asset style to domain aesthetic.

## Icon sets

| Source | Style | Best for | URL |
|---|---|---|---|
| **Lucide** | Clean line icons | Medical, legal, fintech, SaaS defaults | https://lucide.dev |
| **Iconify** | 200k+ icon sets, many styles | Search-first, when you need a specific icon | https://iconify.design |
| **Icons8** | Colorful, illustrated, 3D variants | Playful, creator, SaaS marketing | https://icons8.com |
| **Phosphor** | Multi-weight line (thin, regular, bold, fill) | Editorial, portfolio | https://phosphoricons.com |
| **Tabler** | Consistent line icons | Agency, technical | https://tabler.io/icons |
| **Heroicons** | Tailwind-paired line / solid | Anywhere Tailwind is used | https://heroicons.com |
| **Simple Icons** | 3000+ brand logos (monochrome) | "As featured in" / customer logo rows | https://simpleicons.org |
| **Radix Icons** | Tiny, geometric | Dense UIs | https://www.radix-ui.com/icons |

### Using via React

Pick a single icon library per project for UI icons (consistency matters). Separately, Simple Icons is fine for brand logos alongside your UI icon set.

```bash
npm install lucide-react
# or
npm install @iconify/react
# or
npm install @phosphor-icons/react
```

## Illustration sets

| Source | Style | Best for | URL |
|---|---|---|---|
| **unDraw** | Flat single-color illustrations | SaaS, tech, onboarding | https://undraw.co |
| **Storyset** | Editable flat illustrations (7 styles) | Nonprofit, creator, AI | https://storyset.com |
| **DrawKit** | Friendly illustrations, hand-drawn | Creator, wellness, lifestyle | https://drawkit.com |
| **Humaaans** | Mix-and-match people illustrations | Nonprofit, creator, people-forward | https://humaaans.com |
| **Open Peeps** | Hand-drawn library | Warm, friendly, community | https://openpeeps.com |
| **Blush** | Diverse people illustrations | Creator, lifestyle, wellness | https://blush.design |
| **IRA Design** | Modular Bauhaus-style | Editorial, bold design sites | https://iradesign.io |

### Asset-by-domain guidance

- **Medical / real estate / agency / restaurant** — minimize or skip illustrations. Real photography and iconography only.
- **SaaS / AI / dev tools** — unDraw and abstract patterns work. Avoid cutesy people illustrations.
- **Nonprofit / creator / local service** — Storyset, Humaaans, Blush can add warmth — but flag to user if they'd prefer real photos.
- **Crypto** — skip flat illustrations; reach for 3D abstract.

## Photography — Unsplash API workflow (no placeholders)

Placeholder gray boxes and `<TODO: swap this>` comments are unshipped work. The skill's default is to use **real Unsplash images fetched via the public API**, attributed per their guidelines, so the site is visually complete on first render. If the user later has original photography, they can swap.

There are three tiers depending on what the project needs. Default to **Tier 1** unless the user asks otherwise.

### Tier 1 — Session-time curation (default, no API key needed at runtime)

During the build conversation, the agent searches Unsplash for domain-appropriate photos and hardcodes the curated permalink URLs into the site. No runtime dependency, no env var, no API call from the deployed page.

**How the agent does it:**

1. For each section that needs photography, form a specific search query based on the domain, e.g. for a dermatologist:
   - Hero: `"minimalist clinic interior"` or `"bright medical office"`
   - About: the user's own portrait if provided, else `"professional doctor portrait"`
   - Testimonials: skip photos or use user-provided
2. Query the Unsplash API — or, if no API key is available, use the agent's web-search/fetch tool against `https://unsplash.com/s/photos/<query>` and pick photos manually:

   ```
   GET https://api.unsplash.com/search/photos?query=<query>&orientation=landscape&per_page=6
   Authorization: Client-ID <UNSPLASH_ACCESS_KEY>
   ```

   Each result has `id`, `urls.regular` (permalink), `user.name` and `user.links.html` for attribution, and `links.download_location` (which must be pinged once per image per Unsplash's ToS).

3. Pick one photo per slot. Prefer photos with clean composition and matching color temperature. Avoid ones with heavy visual noise that will fight the site's tokens.

4. Embed the permalink URL directly in the generated code. Use the `images.unsplash.com/photo-<id>` form with query params:

   ```
   https://images.unsplash.com/photo-<ID>?w=1600&q=80&auto=format&fit=crop
   ```

5. Write a small wrapper component so every Unsplash image renders with the required attribution:

   ```tsx
   // components/ui/unsplash-image.tsx
   import Image from 'next/image'
   import type { ComponentProps } from 'react'

   type Props = {
     src: string
     alt: string
     photographer: string
     photographerUrl: string
     className?: string
   } & Omit<ComponentProps<typeof Image>, 'src' | 'alt'>

   export function UnsplashImage({
     src, alt, photographer, photographerUrl, className, ...rest
   }: Props) {
     return (
       <figure className={className}>
         <Image src={src} alt={alt} {...rest} />
         <figcaption className="text-xs text-muted-foreground mt-1">
           Photo by{' '}
           <a href={photographerUrl} className="underline" rel="nofollow">
             {photographer}
           </a>{' '}
           on{' '}
           <a href="https://unsplash.com" className="underline" rel="nofollow">
             Unsplash
           </a>
         </figcaption>
       </figure>
     )
   }
   ```

   For hero/background uses where a visible caption doesn't fit, move the attribution to a compact credits strip in the footer that lists all Unsplash photographers used on the page.

6. For Next.js, add `images.unsplash.com` to `next.config.js`:

   ```js
   module.exports = {
     images: { remotePatterns: [{ protocol: 'https', hostname: 'images.unsplash.com' }] },
   }
   ```

7. Ping the download endpoint **once per selected photo** to honor Unsplash's tracking requirement (required by their API ToS):

   ```bash
   curl -H "Authorization: Client-ID $UNSPLASH_ACCESS_KEY" \
     "https://api.unsplash.com/photos/<ID>/download"
   ```

   If no API key is available for this step, note it in the handoff — the user can set `UNSPLASH_ACCESS_KEY` and re-run a small ping script later.

### Tier 2 — Runtime fetch (dynamic photos, requires API key in env)

For sites where photos should rotate or be driven by data (a gallery page, a blog), the Unsplash fetch happens server-side at request time. Use a Next.js route handler:

```ts
// app/api/unsplash/route.ts
import { NextRequest } from 'next/server'

export async function GET(req: NextRequest) {
  const q = req.nextUrl.searchParams.get('query') ?? ''
  const res = await fetch(
    `https://api.unsplash.com/search/photos?query=${encodeURIComponent(q)}&per_page=6`,
    {
      headers: { Authorization: `Client-ID ${process.env.UNSPLASH_ACCESS_KEY}` },
      next: { revalidate: 3600 },
    }
  )
  return Response.json(await res.json())
}
```

User sets `UNSPLASH_ACCESS_KEY` in `.env.local` (get one free at https://unsplash.com/developers). Consumers call `/api/unsplash?query=...` and render the results through the same `<UnsplashImage>` wrapper.

### Tier 3 — Build-time prefetch (best performance, requires API key)

For maximum performance, prefetch the curated images at build time, download them to `public/unsplash/`, and reference local paths. Script:

```ts
// scripts/prefetch-unsplash.ts
import { writeFile, mkdir } from 'node:fs/promises'
import { fetch } from 'undici'

const QUERIES = [
  { slot: 'hero',  query: 'minimalist clinic interior' },
  { slot: 'about', query: 'professional doctor portrait' },
]

const key = process.env.UNSPLASH_ACCESS_KEY!
await mkdir('public/unsplash', { recursive: true })

for (const { slot, query } of QUERIES) {
  const r = await fetch(
    `https://api.unsplash.com/search/photos?query=${encodeURIComponent(query)}&per_page=1`,
    { headers: { Authorization: `Client-ID ${key}` } }
  )
  const { results } = (await r.json()) as any
  const photo = results[0]
  const img = await fetch(photo.urls.regular).then(res => res.arrayBuffer())
  await writeFile(`public/unsplash/${slot}.jpg`, Buffer.from(img))
  // Ping download tracking per Unsplash ToS
  await fetch(photo.links.download_location, {
    headers: { Authorization: `Client-ID ${key}` },
  })
  // Save attribution
  await writeFile(
    `public/unsplash/${slot}.json`,
    JSON.stringify({
      photographer: photo.user.name,
      photographerUrl: photo.user.links.html,
    }, null, 2)
  )
}
```

Wire to `package.json`: `"prebuild": "tsx scripts/prefetch-unsplash.ts"`.

### Domain-keyed search queries (starting points)

For the agent's Tier 1 curation. Adjust based on the specific practice/product/brand.

| Domain | Hero query | Supporting queries |
|---|---|---|
| Medical | `minimalist clinic interior`, `bright medical office` | `doctor consultation`, `dermatology closeup`, `medical instruments neutral` |
| SaaS | `laptop clean workspace`, `developer screen` | `office team collaborating`, `abstract tech pattern` |
| Agency | `studio workspace monochrome`, `design desk` | `creative team meeting`, `color palette swatches` |
| E-commerce (fashion) | `editorial fashion product`, `minimalist garment` | `lifestyle shot <product category>`, `studio on-model` |
| E-commerce (home) | `minimalist living room`, `product lifestyle home` | `close-up textile`, `natural light interior` |
| Portfolio | User's own work only — do not auto-curate | — |
| Restaurant | `restaurant interior warm lighting`, `chef plating` | `restaurant dish close-up`, `wine pour`, `dining table night` |
| Creator | User's own photo if provided, else `home studio setup`, `creator workspace` | `laptop with notebook`, `podcast microphone` |
| Nonprofit | Real work photos strongly preferred; if not: `community volunteers`, `hands planting` | Domain-specific (education → `classroom diverse`; environmental → `forest sunlight`) |
| Local service | `professional trade worker`, `clean uniform service` | `truck <service type>`, `before after <service>` |
| Crypto / DeFi | Skip photography entirely — use 3D abstract instead | — |
| AI product | `abstract light pattern`, `minimalist screen` | Skip people photos; use abstract |
| Real estate | User-provided property images strongly preferred; if demo: `luxury home interior`, `modern living room` | `architectural detail`, `natural light bedroom` |

### When photography is the wrong call

- **Crypto, DeFi, AI product** — photos of people feel off. Use 3D abstract or generated patterns.
- **Agency / portfolio** — only the user's own work; generic stock undercuts the "taste" message.
- **Medical portraits** — if the user hasn't provided a real practitioner photo, *say so in the handoff*: *"I'm using a stock portrait for now. A real photo of the practitioner before launch is important for trust — stock portraits read as fake on medical sites."*

### Attribution — do it properly

Every Unsplash photo used must credit the photographer. Unsplash's ToS require:

- Photographer name linked to their Unsplash profile
- Link to `https://unsplash.com`
- Download-tracking ping per image (Tier 3 does this in script; Tier 1 should do it manually or via a small one-off script after selection)

A site without attribution is technically in breach of Unsplash's ToS. The `<UnsplashImage>` wrapper above handles it automatically when inline; for hero/background use, place a compact credits strip in the footer.


## Patterns & backgrounds

| Source | Style | Best for | URL |
|---|---|---|---|
| **Hero Patterns** | SVG repeating patterns | Section dividers, subtle backgrounds | https://heropatterns.com |
| **SVG Backgrounds** | Generated SVG backgrounds | Hero backdrops | https://svgbackgrounds.com |
| **Haikei** | Generated shapes (blobs, waves, gradients) | Modern organic sections | https://haikei.app |
| **Shape Divider** | Section transition shapes | Softening hard edges | https://shapedivider.app |
| **BGJar** | SVG backgrounds generator | Alt to Haikei | https://bgjar.com |
| **Mesh gradients (CSS)** | Custom CSS / Haikei export | Hero backgrounds when not using Aceternity | — |

## 3D assets

| Source | Style | Best for | URL |
|---|---|---|---|
| **Shapefest** | 3D abstract shapes, free | Crypto, AI, bold | https://shapefest.com |
| **3DIcons** | 3D icons, many packs | Crypto, creator, playful | https://3dicons.co |
| **Spline** | Interactive 3D scenes | Hero interactive 3D | https://spline.design |

### Spline in React

```bash
npm install @splinetool/react-spline
```

Import a Spline scene URL into a hero. Performance-heavy — only if the domain calls for it (crypto, AI, agency with a bold signature).

## Video / motion — awareness, not a default

**First ask: does this domain actually benefit from video?** Most sites don't. A landing page that reads for 10 seconds and then asks for an action rarely needs a moving hero. Defaulting to video is how you get AI-slop with a side of bandwidth bill.

Domains where video often earns its place:

- SaaS / dev tools — product demo or interactive preview
- AI product — showing the model do something
- Creator / course — personal intro reel, sample lesson
- Restaurant / hospitality — atmosphere, chef at work
- Real estate — property walkthrough
- E-commerce with physical products — fit, movement, scale

Domains where video is usually the wrong call:

- Medical, legal, most local services — trust comes from stillness, not motion
- Agency / portfolio — let the work images speak; reels feel overproduced
- Nonprofit — real photos of real work tell the story better
- Crypto / DeFi — a number-ticker on live data says more than a pre-rendered explainer

If — and only if — video fits, here are the options the agent should know about. Pick the lightest tool that gets it done.

| Option | When it fits | Notes |
|---|---|---|
| **User-provided MP4 / WebM** | User already has footage. | Always the first choice. Embed with a native `<video>` tag + poster frame, or host on Mux / Cloudflare Stream for adaptive bitrate. |
| **Lottie / Lottiefiles** | Small, UI-adjacent vector animations — a logo reveal, an illustrated icon that moves, a micro-animation in a hero. Tiny JSON payloads. | https://lottiefiles.com |
| **Rive** | Interactive animations the user can drive (hover, scroll, input). A step up from Lottie when the motion needs state. | https://rive.app |
| **Remotion** | When the video itself should be *designed in React* so it inherits brand tokens, fonts, and can be generated from data. Render to MP4 (sidecar project) or embed `@remotion/player` for live playback. Best for data-driven explainers, animated stats, templated cut-downs. | https://remotion.dev |
| **Spline scene** | 3D hero element, interactive. Heavier — only on bold-aesthetic sites. | https://spline.design |
| **Mux / Cloudflare Stream** | Hosting layer when self-hosting a large MP4 is a problem. | https://mux.com · https://cloudflare.com/products/stream |

### When motion isn't really video

Before reaching for any of the above, check whether the need is actually video at all:

- Static hero that needs "life" → CSS animation, a Magic UI effect, or a subtle pattern — not video
- Logo reveal → Lottie, not a rendered clip
- Stats counting up → a number-ticker component, not a pre-rendered MP4
- Scroll-triggered feature reveal → a scroll component, not video
- "Products moving" feel on an e-commerce hero → parallax or looping GIF-sized WebM, not a full video player

Match the tool to the actual motion need. Nine times out of ten, a non-video path is lighter, faster, and reads better.

## Font loading

| Source | Notes |
|---|---|
| **Next/font** (Next.js) | Automatic, self-hosted. Use `next/font/google` or `next/font/local`. |
| **Fontsource** | `npm install @fontsource/<font>` — self-hosted for any framework. |
| **Google Fonts** | Last resort via `<link>`. |
| **Typewolf** | Font pairing inspiration (not a host) — https://typewolf.com |

### Recommended pairings by domain

| Domain | Display | Body |
|---|---|---|
| Medical | Fraunces / Source Serif / Cormorant | Inter / Geist |
| SaaS | Geist / Inter Display / Satoshi | Inter / Geist |
| Agency | Playfair / Fraunces / PP Neue Montreal | Inter / Neue Haas clone |
| E-commerce (luxury) | Cormorant / Didone (Playfair) | Inter |
| E-commerce (streetwear) | Archivo Black / Space Grotesk | Inter |
| Portfolio | Editorial choice | Inter / Geist |
| Restaurant | Cormorant / Fraunces | Quiet sans |
| Creator | Plus Jakarta / Inter Display | Inter |
| Nonprofit | DM Sans / Plus Jakarta | Inter |
| Local service | Archivo / Montserrat | Inter |
| Crypto | Geist / JetBrains Mono (display) / Space Grotesk | Inter / Geist |
| AI | Geist / Inter Display | Inter / Geist |
| Real estate | Playfair / Fraunces | Inter |

## Audit before ship

- Every icon comes from **one** icon library (plus Simple Icons for brand logos, separately).
- No mixed illustration styles on one page.
- Every photograph is either user-provided or curated via the Unsplash API workflow above — no placeholder gray boxes, no `<TODO>` comments. Every Unsplash photo has attribution rendered either inline or in a footer credits strip, and its download endpoint was pinged once.
- Patterns are subtle — they should support the content, not compete.
- 3D is used at most once per page, in the hero.
- Fonts are self-hosted (next/font or @fontsource) — no render-blocking CDN link tags.
