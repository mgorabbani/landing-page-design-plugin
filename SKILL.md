---
name: landing-page-design
description: Build a landing page or full website that looks professionally designed, not AI-generated. Use whenever the user asks to build, design, create, scaffold, or improve a website, landing page, marketing site, homepage, portfolio, product site, or any web front-end surface — including triggers like "build a landing page", "design a website", "make a site for my startup", "I need a homepage", or "/landing-page-design". Avoids the generic Inter-plus-purple-gradient aesthetic by reasoning from the site's domain (medical, SaaS, agency, e-commerce, portfolio, restaurant, creator, nonprofit, local service, crypto, AI, real estate) down to sections, components, and assets, then pulls real components from shadcn, Magic UI, Aceternity, Kibo UI, Launch UI, and Skiper via the shadcn CLI and MCP servers.
license: MIT
---

# Landing Page Design

You are helping the user build a real landing page or website that looks professionally designed. Your job is to avoid the default AI-slop aesthetic (Inter font everywhere, purple gradient hero, three feature cards in a row) by reasoning from domain → value → sections → components → tokens, then assembling real components pulled live from the shadcn ecosystem.

## Core philosophy

Keep these principles in mind at every step:

1. **Domain is the master key.** The type of site (doctor, SaaS, agency, restaurant, crypto...) determines sections, aesthetic, components, assets, copy, and CTA. Never skip this.
2. **Value thinking over aesthetic thinking.** For the specific visitor, ask: *what do they need to feel, know, and do?* Pick sections and components that serve that.
3. **Let the agent think.** Only ask the user questions they genuinely know better than you. Infer everything else from context and domain.
4. **Coherence before components.** Define design tokens FIRST — colors, fonts, radius, shadow, motion — then install components, then edit each to consume the tokens.
5. **Real components from real libraries via real CLIs and MCPs.** No reinventing effects from scratch. Live registries, versioned, maintained.
6. **Ship AI-discoverable by default.** Every generated site includes an `llms.txt` at the project root.
7. **SEO is a handoff.** This skill builds. If the user has `/seo`, recommend running it after.

## The flow

Follow these phases in order. Do NOT skip phases — each one narrows the decision space for the next.

### Phase 1 — Silent context sensing

Before asking anything, inspect the project:

- Read `package.json` if it exists. Detect framework (Next.js, Vite, Astro, Remix, SvelteKit) and Tailwind version.
- Check for `components.json` (shadcn initialized) and `tailwind.config.*` / `src/app/globals.css` (Tailwind v4 CSS vars).
- Look for existing pages in `app/`, `src/app/`, `src/pages/`, or `pages/`.
- Note any existing design system (colors in `globals.css`, custom fonts loaded, brand tokens).

Skip any later question that the filesystem already answered.

### Phase 2 — Ask only what matters

Ask these three questions, in order, and only if context didn't already answer them. Bundle them into a single user message when possible.

**Q1: Domain / type of site.** *(Master key. Always ask if unclear.)*

> "What kind of site is this? e.g. medical practice, SaaS / dev tool, agency, e-commerce, personal portfolio, restaurant, creator / course, nonprofit, local service, crypto or DeFi, AI product, real estate — or describe it if none of those fit."

**Q2: Single page or multi-page?** *(Often inferable — portfolio is usually multi, a launch page is usually single, SaaS is usually multi. Only ask if genuinely ambiguous.)*

**Q3: Section count.** *(Suggest a default per domain and let the user nudge.)*

> "Doctor sites usually work well with 4–5 sections — hero, services, about/credentials, testimonials, booking CTA. Go with that, or want more or less?"

Infer everything else: aesthetic direction, header style (full hero on homepage, compact nav on subpages), which sections belong, asset style, motion intensity. If the user volunteered aesthetic hints ("clean", "bold", "playful", brand colors, references), incorporate them — but don't interrogate for them.

### Phase 3 — Value-driven section planning

Load `references/domains.md` and find the recipe for the user's domain. The recipe gives you:

- Typical sections in order
- The critical CTA
- Aesthetic defaults
- Recommended component choices per section
- Asset style
- llms.txt focus

Internally reason: *what does this visitor need to feel, know, and do?* Examples the skill bakes in:

- **Doctor** — trust (credentials, real portraits, reviews), clarity (services, insurance), low-friction booking
- **SaaS** — proof it works (logos, metrics, demo), 5-second understanding, free-trial CTA
- **Agency** — evidence of taste and past work, clear offering, easy inquiry
- **E-commerce** — browseable products, trust, fast checkout path
- **Crypto** — bold and technical, audited/verified signals, connect-wallet CTA
- **Creator** — testimonials, curriculum preview, enrollment

Adapt the recipe to the user's specifics. Recipes are starting points, not scripts.

### Phase 4 — Component shortlisting

For each section, choose 1 component. Use these sources, in order:

1. **MCP servers** (preferred, live). If `shadcn`, `magicui`, or `kibo-ui` MCP servers are configured, query them for current components.
2. **Fit matrix** in `references/components-by-section.md` — a curated table tagging components by section and suitable domain aesthetic. Use this when MCP isn't available or to pre-filter candidates.
3. **Registries reference** in `references/registries.md` — the exact shadcn CLI commands and namespace URLs.

Shortlist 3–5 candidates per section. Pick the best fit based on domain aesthetic, or present 2–3 options to the user if you're genuinely torn. **Not every cool effect for every site** — a calm lamp + portrait works for a doctor hero; meteors + globe + number tickers work for crypto.

### Phase 5 — Coherence lock (CRITICAL — do not skip)

**Before installing anything**, write the design tokens to `src/app/globals.css` (Tailwind v4) or `tailwind.config.ts` (v3). Tokens to define:

- **Palette** — 3–5 colors with explicit roles: `--background`, `--foreground`, `--primary`, `--accent`, `--muted`. Derive from the domain aesthetic. No arbitrary hexes later.
- **Typography** — one display font, one body font. Load via `next/font` (Next.js) or `@fontsource` / Google Fonts `<link>` (everything else). Set `--font-display` and `--font-sans` tokens.
- **Radius** — single scale (`--radius` → `sm`, `md`, `lg`, `xl`). No freelancing.
- **Shadow** — single scale (`--shadow-sm`, `--shadow`, `--shadow-lg`).
- **Motion** — easing curves and duration range (e.g. `--ease-out-quint`, fast = 150ms, default = 300ms, slow = 600ms).

Only now start pulling components. **After each `npx shadcn add`**, open the installed file and replace any hardcoded colors, radii, fonts, or shadows with the tokens. When you're done, grep the final code for raw hex colors, arbitrary `rounded-[...]`, or inline font-family — those are coherence leaks.

### Phase 6 — Assembly

1. Scaffold missing infrastructure only if needed (new Next.js app, install Tailwind, init shadcn). Use `npx shadcn@latest init` with Zinc as the base color when starting fresh.
2. Run `npx shadcn@latest add @<registry>/<component>` for each picked component. See `references/registries.md` for namespace URLs and CLI patterns.
3. Write the page files. Prefer composing in `app/page.tsx` (homepage) and `app/<route>/page.tsx` (subpages). Each section is its own component under `components/sections/`.
4. Wire up navigation between pages if multi-page. Subpage header is compact (logo + nav + single CTA); homepage header can be the immersive hero variant.
5. Assets: see `references/assets.md` for icon sets, illustrations, photos, and patterns matched to domain aesthetic. Default to Lucide for icons; reach for Iconify / Icons8 / 3D sets when the domain calls for it.

### Phase 7 — llms.txt generation

Generate `llms.txt` at the project root. Follow `references/llms-txt-template.md`. The file describes the site for AI crawlers — site purpose, key pages, primary CTAs, and any structured content (product list, service menu, team). Auto-populate it from what you just built.

### Phase 8 — Handoff

End with a short summary:

- What was built (pages, sections, component sources)
- Where the design tokens live
- How to run the dev server
- One-liner: *"Want this SEO-optimized? If you have the `/seo` skill installed, run it now — it handles meta, schema.org, sitemap, Open Graph images, and performance."*

## When to load references

Read these only when you need them — keep context lean.

- `references/domains.md` — always load for Phase 3. 12 domain recipes.
- `references/registries.md` — load for Phase 4/6. Shadcn CLI commands, MCP configs, namespace URLs.
- `references/components-by-section.md` — load for Phase 4. Fit matrix: which components suit which section × domain.
- `references/assets.md` — load for Phase 6. Icons, illustrations, photos, patterns, 3D.
- `references/llms-txt-template.md` — load for Phase 7.

## Libraries at a glance

| Library | Role | When to use |
|---|---|---|
| **shadcn/ui** | Foundation primitives | Always — Button, Card, Input, Dialog |
| **Aceternity UI** | Hero effects & blocks | Lamp, Spotlight, Hero Parallax, Bento, Globe, Macbook Scroll |
| **Magic UI** | Effects & text animation | Animated Beam, Meteors, Border Beam, Number Ticker, Marquee |
| **Launch UI** | Landing page sections | Hero, Bento, Feature, Social Proof, FAQ, Pricing, CTA, Footer |
| **Kibo UI** | Complex blocks | Gantt, Kanban, Editor + Hero, Pricing, FAQ, Testimonial, Team |
| **Skiper UI** | Signature moments | Image reveal, dynamic island, cursor trails |
| **Motion Primitives** | Animation recipes | Core motion patterns |
| **ElevenLabs UI** | Voice/agent UI only | Orbs, waveforms — skip unless building a voice app |

## Anti-patterns to refuse

These produce AI-slop. Catch yourself and choose differently.

- Inter as the only font, for every domain. Pair it with a display serif, mono, or editorial sans matched to the domain.
- Purple → pink gradient hero on a site that isn't crypto, AI, or creator. Default gradient is a tell.
- Three-card feature grid as the only way to show features. Bento, alternating splits, tabs, and scroll-triggered reveals exist.
- Generic stock photo of a smiling team in an office. Either use real photos or stylized illustrations; don't fake warmth.
- Purple/blue gradient CTA button. Use the token's `--primary`, full stop.
- Over-animating. One signature motion per page is usually enough.
- Ignoring the domain — every SaaS doesn't look the same, every agency doesn't look the same.

## Checklist before you declare done

- [ ] Domain reasoning is visible in the section choices and aesthetic
- [ ] Design tokens exist in globals.css / tailwind config before any component was installed
- [ ] Every installed component reads from tokens — no hardcoded hex / radius / font
- [ ] Section count matches the user's answer (or the recipe default)
- [ ] Homepage uses hero header; subpages use compact header
- [ ] Critical CTA for the domain is present above the fold AND repeated at the bottom
- [ ] `llms.txt` exists at project root and describes the site
- [ ] Dev server runs without errors (`npm run dev`)
- [ ] You did not add SEO (meta, schema, sitemap) — that's the `/seo` handoff
