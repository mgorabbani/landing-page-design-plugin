---
name: landing-page-design
description: Build a landing page or full website that looks professionally designed, not AI-generated. Use whenever the user asks to build, design, create, scaffold, or improve a website, landing page, marketing site, homepage, portfolio, product site, or any web front-end surface — including triggers like "build a landing page", "design a website", "make a site for my startup", "I need a homepage", or "/landing-page-design". Avoids the generic Inter-plus-purple-gradient aesthetic by reasoning from the site's domain (medical, SaaS, agency, e-commerce, portfolio, restaurant, creator, nonprofit, local service, crypto, AI, real estate) down to sections, components, and assets. The skill is library-agnostic — it teaches a discovery pattern so the agent finds *today's* trending shadcn-compatible component registries (shadcn, Magic UI, Aceternity, Kibo UI, Launch UI, Skiper, 21st.dev, and whatever else is current) by browsing curated directories and library docs live, then installs via the shadcn CLI.
license: MIT
---

# Landing Page Design

This is an **instruction for you, the agent.** It's not a script. Its job is to make you ask the right questions and point at the right places to look, so the site you produce is genuinely designed — not the default AI-slop (Inter everywhere, purple gradient hero, three feature cards).

You get there by reasoning in a strict order:

**domain → single-page vs multi-page → section list → what goes inside each section → components → assets (icons, illustrations, photos, patterns, 3D, video) → design tokens → build**

At each step, **ask the user only what you can't infer**, check the filesystem for what you can, and — critically — **look up what's current on the web** before you pick any library or component. This skill bundles no MCP, no frozen catalog, no vendored code. It teaches you a discovery pattern and seeds you with a starting list of libraries and sources. The ecosystem moves fast (shadcn/ui, Magic UI, Aceternity, Kibo UI, Launch UI, Skiper, 21st.dev, and new entrants every quarter) — always verify before committing.

## The pattern in one glance

The single most important diagram in this skill. Every invocation follows this path:

```
1. Detect domain            → references/domains.md
2. Single-page or multi?    → inferred from domain (ask only if ambiguous)
3. Section list             → domain recipe gives the ordered list
4. Section anatomy          → for each section, what content slots it needs
                              (headline, sub, visual, CTA, testimonial count...)
5. Components per section   → browse current libraries, shortlist, pick
                              (references/components-by-section.md seeds it)
6. Assets per section       → icon pack, illustration pack, photo source,
                              patterns, 3D, and — only if the domain
                              calls for it — video (options: user
                              footage / Lottie / Rive / Remotion, etc.)
                              (references/assets.md)
7. Design tokens            → colors, fonts, radius, shadow, motion — BEFORE install
8. Build                    → shadcn CLI install, edit for tokens, compose pages
9. llms.txt                 → auto-generated from what was built
10. Handoff                 → hand SEO off to /seo skill if the user has it
```

Don't skip steps. Each one narrows the decision space for the next — that's how the output stays coherent.

## Core philosophy

Keep these principles in mind at every step:

1. **Domain is the master key.** The type of site (doctor, SaaS, agency, restaurant, crypto...) determines sections, aesthetic, components, assets, copy, and CTA. Never skip this.
2. **Value thinking over aesthetic thinking.** For the specific visitor, ask: *what do they need to feel, know, and do?* Pick sections and components that serve that.
3. **Let the agent think.** Only ask the user questions they genuinely know better than you. Infer everything else from context and domain.
4. **Coherence before components.** Define design tokens FIRST — colors, fonts, radius, shadow, motion — then install components, then edit each to consume the tokens.
5. **Real components from real libraries via the shadcn CLI.** No reinventing effects from scratch. Live registries, versioned, maintained.
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

### Phase 3 — Sections and section anatomy

This is the most skipped phase and the one that separates thoughtful output from AI-slop. Two sub-steps:

**3a — Pick the section list.** Load `references/domains.md`, find the recipe for the user's domain, and use it as the starting section flow. Each recipe gives you:

- Typical sections in order
- The critical CTA
- Aesthetic defaults
- Recommended component choices per section
- Asset style
- llms.txt focus

Internally reason: *what does this visitor need to feel, know, and do?* Examples:

- **Doctor** — trust (credentials, real portraits, reviews), clarity (services, insurance), low-friction booking
- **SaaS** — proof it works (logos, metrics, demo), 5-second understanding, free-trial CTA
- **Agency** — evidence of taste and past work, clear offering, easy inquiry
- **E-commerce** — browseable products, trust, fast checkout path
- **Crypto** — bold and technical, audited/verified signals, connect-wallet CTA
- **Creator** — testimonials, curriculum preview, enrollment

Adapt the recipe to the user's specifics. Recipes are starting points, not scripts.

**3b — Decide what each section should have.** For every section in your list, specify the **content anatomy** before you think about components:

- Hero → eyebrow (optional), headline, sub-headline, 1 primary + 0–1 secondary CTA, visual (image / video / 3D / animated block)
- Feature section → section heading, 3–6 features each with icon + title + 1-line description
- Social proof → logo row (6–10) OR metric row (3–4 numbers) OR quote row
- Testimonials → quote count, with-photo or without, marquee vs grid vs carousel
- Pricing → tier count (2–4), feature list per tier, one highlighted tier
- FAQ → 4–8 Q&A pairs
- Team → headshot + name + role + short bio (optional)
- CTA section → single focused headline + one button, contrast background
- Footer → column count, social links, legal

`references/components-by-section.md` has a more detailed "section anatomy" quick reference. Load it before Phase 4. Decide the anatomy first, pick components second — components are in service of the content, not the other way around.

### Phase 4 — Discover current libraries, then shortlist components

Do NOT skip straight to the seed examples. The shadcn-compatible component ecosystem moves fast — libraries rise and fall, components get renamed, new registries appear. Follow this pattern every time:

**Step 4a. Discover what's current.** Open `references/registries.md` for the discovery procedure. In short:

1. Fetch one or more **curated directories** (e.g. `registry.directory`, shadcn.io's awesome list, shadcn's own registry directory page). These list live shadcn-compatible registries with their namespaces.
2. Skim the results. Note any registry that looks relevant to the domain (e.g. "animation effects" for SaaS/AI, "blocks" for marketing pages, "charts" for dashboards).
3. Cross-check against the seed list in `references/registries.md` — use seeds as familiar anchors, but don't miss anything new.

**Step 4b. Browse the library's own docs.** For each candidate library, fetch its `/docs` or `/components` page and note which components exist today under what names. Component names drift; don't invent.

**Step 4c. Shortlist per section.** Use `references/components-by-section.md` as a domain-aesthetic-aware filter. It's a seed opinion — treat as a starting shortlist, then refine using what you actually found in steps 4a–4b.

**Step 4d. Pick.** 3–5 candidates per section, then pick the best fit. If genuinely torn, present 2–3 options to the user. **Not every cool effect for every site** — a calm lamp + portrait works for a doctor hero; meteors + globe + number tickers work for crypto.

If you don't have web access (sandboxed, offline), say so to the user, fall back to the seeds in the references, and flag that the list may be behind the current ecosystem.

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
3. **Pick the asset sources** for this site — see `references/assets.md`. Match the domain aesthetic:
   - Icon pack (one UI set: Lucide / Phosphor / Iconify / Icons8 / Tabler / Heroicons — plus Simple Icons for brand logos)
   - Illustration pack (unDraw / Storyset / Humaaans / Blush / IRA Design — or skip if the domain wants photography instead)
   - Photography source (user-provided preferred; Unsplash/Pexels flagged as placeholder)
   - Patterns or shapes (Hero Patterns / Haikei / SVG Backgrounds)
   - 3D (Shapefest / 3DIcons / Spline) only when the domain calls for it
   - **Video** — most sites don't need it. Ask first: does this domain actually benefit from moving footage? (SaaS product demo, creator intro reel, restaurant atmosphere, real estate walkthrough — yes. Medical, agency portfolio, local service, most nonprofits — usually no.) If yes, the options range from user-provided footage, to vector animation (Lottie / Rive) when something is small and UI-adjacent, to programmatic tools like Remotion when the video itself should be designed in React and share the site's brand tokens. See `references/assets.md` for the trade-offs. It's awareness, not a default.
4. Write the page files. Prefer composing in `app/page.tsx` (homepage) and `app/<route>/page.tsx` (subpages). Each section is its own component under `components/sections/`.
5. Wire up navigation between pages if multi-page. Subpage header is compact (logo + nav + single CTA); homepage header can be the immersive hero variant.

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

- `references/domains.md` — always load for Phase 3a. 12 domain recipes.
- `references/components-by-section.md` — load for Phase 3b and Phase 4. Section anatomy (content slots) + component fit matrix.
- `references/registries.md` — load for Phase 4. The discovery pattern, shadcn CLI commands, namespace URLs, and the doc pages to browse.
- `references/assets.md` — load for Phase 6. Icons, illustrations, photos, patterns, 3D, and video options (only relevant if the domain calls for motion footage).
- `references/llms-txt-template.md` — load for Phase 7.

## Example libraries (seed list — not exhaustive, not canonical)

These are starting points as of April 2026. **Always run Phase 4a discovery** — new registries appear constantly, and what's trending today may not be tomorrow.

| Library | Typical role | Good starting picks |
|---|---|---|
| **shadcn/ui** | Foundation primitives | Button, Card, Input, Dialog, Form, Accordion |
| **Aceternity UI** | Hero effects & full-section blocks | Lamp, Spotlight, Hero Parallax, Bento, Globe, Macbook Scroll |
| **Magic UI** | Effects & text animation | Animated Beam, Meteors, Border Beam, Number Ticker, Marquee |
| **Launch UI** | Complete landing sections | Hero, Bento, Feature, Social Proof, FAQ, Pricing, CTA, Footer |
| **Kibo UI** | Complex blocks | Gantt, Kanban, Editor + Hero, Pricing, FAQ, Testimonial, Team |
| **Skiper UI** | Signature micro-interactions | Image reveal, dynamic island, cursor trails |
| **21st.dev** | Marketplace of community registries | Many independent registries; browse their directory |
| **Motion Primitives** | Animation recipes | Core motion patterns |
| **ElevenLabs UI** | Voice/agent UI | Orbs, waveforms — only if building a voice app |

If you find a library not on this list that clearly fits, use it. The list is illustrative.

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
