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
