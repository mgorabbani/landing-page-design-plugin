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

## Photography

| Source | Best for | URL |
|---|---|---|
| **Unsplash** | General stock — good curation | https://unsplash.com |
| **Pexels** | Stock alternative | https://pexels.com |
| **Pixabay** | Backup | https://pixabay.com |
| **User-provided** | Always preferred for portfolio / agency / restaurant / real estate / product | — |

**Flag stock usage.** If you're reaching for Unsplash for a doctor portrait, tell the user: *"I'm using a placeholder portrait from Unsplash — swap this for a real photo of the practitioner before shipping. Stock portraits undercut the trust message."*

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
- Every photograph is either user-provided or flagged as placeholder.
- Patterns are subtle — they should support the content, not compete.
- 3D is used at most once per page, in the hero.
- Fonts are self-hosted (next/font or @fontsource) — no render-blocking CDN link tags.
