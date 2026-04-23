# Section anatomy & component fit matrix

Two things in one file:

1. **Section anatomy** — for each section type, the content slots it needs. Decide anatomy before you pick components.
2. **Component fit matrix** — example components tagged by section × aesthetic. A seed shortlist, not a canonical list; always cross-check against the library's current docs (see `registries.md` for the discovery pattern).

## Section anatomy (fill these slots before picking components)

| Section | Required content | Optional | Notes |
|---|---|---|---|
| **Hero** | Headline, 1 primary CTA, a visual | Eyebrow, sub-headline, secondary CTA, badge / announcement bar | The visual is usually the single biggest design decision — image, product screenshot, abstract 3D, animated effect, or pure typography. |
| **Features grid / bento** | Section heading, 3–6 feature items (each: icon + title + 1-line description) | Section sub-heading, per-feature visual or animation | Bento sizes matter — mix one "hero" tile with 3–5 smaller ones. |
| **Social proof (logos)** | 6–10 brand logos (monochrome), optional "as featured in" label | — | Keep it one row, marquee or static. |
| **Social proof (metrics)** | 3–4 big numbers + labels | Background accent | Use number ticker when motion fits. |
| **Testimonials** | 3–9 quotes, each with name + role/company | Photo, company logo, star rating | Decide layout: marquee (high volume, low commitment), grid (medium density), carousel (if the quotes are long), single hero quote (premium). |
| **Pricing** | 2–4 tiers, each with name + price + feature list + CTA | One highlighted tier, annual/monthly toggle, comparison table | Clarity of tier differentiation matters more than the visual. |
| **FAQ** | 4–8 Q&A pairs | Category grouping | Accordion by default. |
| **Team** | Headshot + name + role for each member | Short bio, social links | 3–12 members feels right for most sites. |
| **About / founder story** | Narrative text, photo | Pull quotes, timeline, founding-date badge | Split-layout (image + text) is the safe default. |
| **Case study / work item** | Client name, 1-line challenge, 2–4 lines outcome, visual | Metrics, testimonial, link to full case | For agency / portfolio sites. |
| **Blog / resources preview** | 3–6 recent posts (title + date + excerpt + thumbnail) | Category pills, featured post | Link to `/blog` for full list. |
| **Newsletter capture** | Headline, 1-line promise, email input + button | Privacy note, subscriber count | Usually goes above the footer. |
| **CTA section** | Focused headline, 1 primary CTA | Sub-headline, secondary action | Contrast background. One decision, not five. |
| **Footer** | Logo, nav columns, legal links | Social links, newsletter, contact, language switcher | Column count depends on site scale. |
| **Nav / header** | Logo, 3–6 nav links, 1 CTA | Announcement bar, mega menu, search, user menu | Homepage may use hero-embedded nav; subpages use compact sticky nav. |

## Component fit matrix

Which components fit which section, tagged by suitable domain aesthetic. Use as a shortlist, not a prescription — always verify the component still exists in the library's current docs before installing.

## How to read

Each row is a **section type × component candidate**. Aesthetic tags tell you when it fits:

- `calm` — medical, nonprofit, hospitality, real estate
- `editorial` — agency, portfolio, premium commerce, creator
- `technical` — SaaS, dev tools, AI product
- `bold` — crypto, AI product, launch pages, consumer apps
- `warm` — creator, nonprofit, local service, restaurant
- `product-led` — e-commerce, hospitality, real estate
- `universal` — works almost anywhere with tokens

## Hero sections

| Component | Registry | Tags | Notes |
|---|---|---|---|
| Spotlight | `@aceternity/spotlight` | calm, editorial, universal | Subtle radial light. Safe default. |
| Lamp | `@aceternity/lamp` | calm, editorial, technical | Soft gradient lamp above title. |
| Hero Parallax | `@aceternity/hero-parallax` | editorial, product-led, bold | Scrolling image rows. Heavy — needs good images. |
| Background Beams | `@aceternity/background-beams` | technical, bold, AI | Animated SVG beams. |
| Macbook Scroll | `@aceternity/macbook-scroll` | technical, SaaS | Dramatic product reveal. |
| Container Scroll Animation | `@aceternity/container-scroll-animation` | technical, SaaS | Card scales in on scroll. |
| Wavy Background | `@aceternity/wavy-background` | warm, creator, bold | Animated gradient waves. |
| Meteors | `@magicui/meteors` | bold, crypto, AI | Overlay with shooting stars. Often paired. |
| Border Beam | `@magicui/border-beam` | technical, AI, bold | Animated border. Pair with a product card. |
| Globe | `@aceternity/globe` or `@magicui/globe` | crypto, SaaS, enterprise | Rotating 3D globe. |
| Launch UI Hero | Launch UI | universal | Composable marketing hero block. |
| Custom type hero | — | editorial, agency, portfolio | Pure typography. Often the best choice for taste-driven sites. |

## Feature / bento sections

| Component | Registry | Tags | Notes |
|---|---|---|---|
| Bento Grid | `@aceternity/bento-grid` | technical, SaaS, AI | Mixed card sizes. Current default for feature sections. |
| Launch UI Bento | Launch UI | technical, SaaS | Alt bento with section wrapper. |
| Kibo Feature | `@kibo-ui/feature` | universal | Straightforward feature grid. |
| Launch UI Feature | Launch UI | universal | Alternating image + text. |
| Sticky Scroll Reveal | `@aceternity/sticky-scroll-reveal` | editorial, SaaS | Scroll-triggered feature narration. |
| Tabs (shadcn) | `@shadcn/tabs` | universal | Tab-switched feature display. |
| Animated Beam | `@magicui/animated-beam` | technical, AI, crypto | "Data flow" diagrams between nodes. |

## Social proof / logo sections

| Component | Registry | Tags | Notes |
|---|---|---|---|
| Marquee | `@magicui/marquee` | universal | Infinite scrolling logos or testimonials. |
| Logo Cloud (custom) | — | calm, editorial | Static centered logos. Often classier. |
| Launch UI Social Proof | Launch UI | universal | Opinionated logo row. |

## Testimonials

| Component | Registry | Tags | Notes |
|---|---|---|---|
| Kibo Testimonial | `@kibo-ui/testimonial` | universal | Clean cards. |
| Marquee of testimonial cards | `@magicui/marquee` | technical, bold, warm | Scrolling testimonial wall. |
| Animated Testimonials | `@aceternity/animated-testimonials` | editorial, creator | Image + quote with transitions. |
| Launch UI Social Proof | Launch UI | universal | Testimonial variants included. |

## Pricing

| Component | Registry | Tags | Notes |
|---|---|---|---|
| Launch UI Pricing | Launch UI | SaaS, creator, AI | 2–4 tier block with feature lists. |
| Kibo Pricing | `@kibo-ui/pricing` | SaaS, creator | Alt pricing block. |
| Custom with shadcn Card + Badge | — | editorial | When you want taste-forward pricing. |

## FAQ

| Component | Registry | Tags | Notes |
|---|---|---|---|
| shadcn Accordion | `@shadcn/accordion` | universal | Standard accordion FAQ. |
| Kibo FAQ | `@kibo-ui/faq` | universal | Pre-composed FAQ block. |
| Launch UI FAQ | Launch UI | universal | Section-wrapped FAQ. |

## CTA / final conversion

| Component | Registry | Tags | Notes |
|---|---|---|---|
| Launch UI CTA | Launch UI | universal | Big centered CTA with background treatment. |
| shadcn Card + Button | `@shadcn/card` + `@shadcn/button` | universal | Simple, always works. |
| Aceternity BackgroundLines + CTA | `@aceternity/background-lines` | bold, AI | Dramatic final CTA. |

## Stats / metrics

| Component | Registry | Tags | Notes |
|---|---|---|---|
| Number Ticker | `@magicui/number-ticker` | technical, SaaS, AI, crypto, nonprofit | Counts up on viewport enter. |
| Stat row (custom with shadcn) | — | universal | When motion would be overkill. |

## Team / about

| Component | Registry | Tags | Notes |
|---|---|---|---|
| Kibo Team | `@kibo-ui/team` | universal | Team grid with photos + bios. |
| shadcn Card + Avatar | `@shadcn/card` + `@shadcn/avatar` | calm, local | Simple team card. |
| Split layout (image + bio) | — | editorial, medical, creator | Custom, works everywhere. |

## Navigation / header

| Component | Registry | Tags | Notes |
|---|---|---|---|
| shadcn Navigation Menu | `@shadcn/navigation-menu` | universal | Foundation. |
| Floating Nav | `@aceternity/floating-nav` | technical, bold | Reveals on scroll. |
| Dock | `@magicui/dock` | creator, editorial, product | macOS-style dock nav. |
| Launch UI Header | Launch UI | universal | Full header with mobile menu. |

## Footer

| Component | Registry | Tags | Notes |
|---|---|---|---|
| Launch UI Footer | Launch UI | universal | Multi-column footer with social. |
| Custom (shadcn primitives) | — | editorial, minimal | Hand-rolled, tightest fit. |

## Signature "moment" components (use sparingly)

One per page max. Used well, they're what people remember.

| Component | Registry | Tags | Notes |
|---|---|---|---|
| Orbiting Circles | `@magicui/orbiting-circles` | SaaS, AI, crypto | Integration / partners display. |
| Dynamic Island | `@skiper-ui/*` | creator, product | iOS-style animated bar. |
| Image Reveal | `@skiper-ui/*` | editorial, portfolio | Cursor-driven image reveal. |
| Cursor Trail | `@skiper-ui/*` | bold, agency | Trailing cursor effect. |
| Card Swap (stack) | `@skiper-ui/*` | creator, product | Stacked card carousel. |
| Text Reveal | `@magicui/text-reveal` | editorial, bold | Scroll-triggered text fill. |
| Animated Gradient Text | `@magicui/animated-gradient-text` | bold, AI, crypto | Use ONCE if at all. |

## Forms

| Component | Registry | Tags | Notes |
|---|---|---|---|
| shadcn Form + Input + Textarea | `@shadcn/form` | universal | Always the baseline. |
| shadcn Select, Checkbox, RadioGroup | `@shadcn/*` | universal | Standard form primitives. |
| Booking iframe (Calendly / Cal.com) | — | medical, creator, local | Embed rather than build. |

## Galleries / media

| Component | Registry | Tags | Notes |
|---|---|---|---|
| shadcn Carousel | `@shadcn/carousel` | universal | Foundation carousel. |
| Hero Parallax | `@aceternity/hero-parallax` | editorial, product-led | Scrolling grid reveals. |
| Masonry (custom) | — | editorial | For irregular galleries. |

## Rules of thumb

- **One signature effect per page.** Meteors + lamp + border-beam + cursor trail + animated beam is noise.
- **If you use a marquee, slow it down.** Default speeds are too fast for calm domains.
- **Match motion to domain.** Crypto can handle meteors; a dermatologist can't.
- **Edit after install.** Every pulled component gets a pass to consume design tokens — no hardcoded hex, radius, or font.
