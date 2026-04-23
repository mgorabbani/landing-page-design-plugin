# Registries — discovery pattern, seed list, install

This skill is **library-agnostic and time-aware**. Component libraries in the shadcn ecosystem rise, fall, and rebrand constantly. A frozen list here would be stale in weeks. Instead, follow the **discovery pattern** below every time you enter Phase 4 of SKILL.md.

## The discovery pattern (run this every time)

### Step 1 — Fetch a curated directory

Use your web fetch / search tool against one or more of these. They maintain lists of currently-active shadcn-compatible registries and usually update faster than any static doc:

| Directory | What it lists | URL |
|---|---|---|
| **registry.directory** | Community-maintained explorer of shadcn registries with filters | https://registry.directory |
| **shadcn registry directory** | Official-ish list of featured registries | https://ui.shadcn.com/docs/directory |
| **shadcn.io / awesome** | Curated awesome list of shadcn-adjacent projects | https://www.shadcn.io/awesome |
| **awesome-shadcn-ui (GitHub)** | Community awesome list | https://github.com/birobirobiro/awesome-shadcn-ui |
| **21st.dev** | Marketplace of community component registries and blocks | https://21st.dev |

Fetch one or two of these, skim for libraries relevant to the domain, and note their registry names and docs URLs.

### Step 2 — Browse each candidate library's docs

For each library you're considering, fetch its `/docs` or `/components` page and note:

- Which components exist today
- Their current names (naming drifts — don't rely on memory)
- Their install syntax (most are `@namespace/component`; some are whole-registry init)
- Any domain-fit signal from the screenshots or demos

### Step 3 — Confirm via the fit matrix

Open `components-by-section.md` and pre-filter your shortlist by domain aesthetic (calm, editorial, technical, bold, warm, product-led). If you found new components in steps 1–2 that the matrix doesn't know about, add them to the shortlist — the matrix is a seed opinion, not a rulebook.

### Step 4 — Install via shadcn CLI

See the cookbook below. `npx shadcn@latest add ...` is the universal install path.

## Seed list of libraries (as of April 2026)

Starting anchors. Always verify against steps 1–2 — any of these can change names, URLs, or disappear.

| Namespace | Library | Registry URL pattern | Browse here |
|---|---|---|---|
| `@shadcn` | shadcn/ui (default) | `https://ui.shadcn.com/r/{name}.json` | https://ui.shadcn.com/docs/components |
| `@magicui` | Magic UI | `https://magicui.design/r/{name}.json` | https://magicui.design/docs |
| `@aceternity` | Aceternity UI | `https://ui.aceternity.com/registry/{name}.json` | https://ui.aceternity.com/components |
| `@kibo-ui` | Kibo UI | `https://www.kibo-ui.com/r/{name}.json` | https://www.kibo-ui.com/components |
| `@skiper-ui` | Skiper UI | Namespaced install via shadcn CLI | https://skiper-ui.com |
| Launch UI | Launch UI | `https://launchuicomponents.com/r` (whole-registry init) | https://www.launchuicomponents.com/components |
| `@21st-dev` (or per-publisher) | 21st.dev marketplace | Per-component registry URL (varies by publisher) | https://21st.dev |

### 21st.dev specifics

21st.dev is a **marketplace**, not a single library — community publishers put up their own components under their own namespaces. When you browse it, pick components by their individual publisher/registry URL; the install command is still `npx shadcn@latest add 'https://21st.dev/.../r/name.json'` or the namespaced form if a publisher registered one. Always copy the exact install command shown on the component's 21st.dev page — it's the source of truth for that component.

### Launch UI (whole-registry init pattern)

Launch UI (as of April 2026) uses the shadcn init-from-URL pattern, not namespaced items:

```bash
# New project — init from the Launch UI registry root
npx shadcn@latest init 'https://launchuicomponents.com/r'

# Existing shadcn project — add from the registry root
npx shadcn@latest add 'https://launchuicomponents.com/r'
```

When prompted for base color, **choose Zinc** — that matches downstream components. Note: this can overwrite `globals.css` in an existing project — warn the user and offer to merge manually.

## Configuring namespaces in `components.json`

To use `@magicui/*`, `@aceternity/*`, `@kibo-ui/*`, etc., register the namespaces in `components.json`:

```json
{
  "$schema": "https://ui.shadcn.com/schema.json",
  "style": "new-york",
  "rsc": true,
  "tsx": true,
  "tailwind": {
    "config": "",
    "css": "src/app/globals.css",
    "baseColor": "zinc",
    "cssVariables": true
  },
  "aliases": {
    "components": "@/components",
    "utils": "@/lib/utils",
    "ui": "@/components/ui",
    "hooks": "@/hooks",
    "lib": "@/lib"
  },
  "registries": {
    "@magicui": "https://magicui.design/r/{name}.json",
    "@aceternity": "https://ui.aceternity.com/registry/{name}.json",
    "@kibo-ui": "https://www.kibo-ui.com/r/{name}.json",
    "@skiper-ui": "https://skiper-ui.com/r/{name}.json"
  }
}
```

**If a URL you copied here is no longer right,** fall back to the absolute-URL install form — that always works:

```bash
npx shadcn@latest add 'https://magicui.design/r/border-beam.json'
```

## CLI command cookbook

```bash
# Initialize shadcn (new project). Choose Zinc as base color by default.
npx shadcn@latest init

# Install default shadcn primitives (almost always needed)
npx shadcn@latest add button card input dialog form accordion sheet tabs avatar

# Install a single component from a registered namespace
npx shadcn@latest add @magicui/marquee
npx shadcn@latest add @aceternity/hero-parallax
npx shadcn@latest add @kibo-ui/pricing

# Install from an absolute URL (bypasses namespace config)
npx shadcn@latest add 'https://magicui.design/r/border-beam.json'

# Install a Launch-UI-style whole registry
npx shadcn@latest add 'https://launchuicomponents.com/r'
```

## Gotchas

- **Verify names live.** If a component you remember doesn't exist by that name anymore, browse the library's docs page and find the current equivalent. Don't fake it.
- **New libraries appear.** If step 1 surfaces something clearly better than the seed list for the domain, use it.
- **Tailwind version.** Many animation-heavy libraries target Tailwind v4 by default. If the project is on v3, components may need a tailwind.config tweak. Check `package.json` and flag to the user.
- **React 19 / RSC.** Some effects rely on client-only hooks. If the project is all-server-components, confirm each component has `"use client"` at the top after install.
- **CSS variable shape.** Default shadcn uses HSL tokens; most others follow the same pattern. If the user already has `oklch` tokens, normalize to one format — don't mix.
- **Font loading.** Landing-section libraries may assume specific fonts are loaded. Check `app/layout.tsx` after install.
- **Post-install edit pass.** After every `npx shadcn add`, open the installed file and replace hardcoded colors / radii / fonts with your tokens. This is required for coherence.

## When you have no web access

Fall back entirely to `components-by-section.md` and the seed list above, and tell the user:

> "I'm working from a seed list in this skill — for the most current components I'd normally browse each library's docs page. If you see a component in their docs that's not here, let me know and I'll install it."
