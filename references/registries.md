# Registries, CLI, and MCP servers

Everything the agent needs to pull real components from real libraries — live.

## The core idea

The shadcn CLI (v3+) supports **namespaced registries**. Every library below publishes a registry endpoint in shadcn's format, so the same `npx shadcn@latest add @namespace/component` command works for all of them. Don't copy-paste components from docs — always install via CLI so users get the current version and the CLI wires up dependencies.

## Namespace table

| Namespace | Library | Registry URL pattern | Notes |
|---|---|---|---|
| `@shadcn` | shadcn/ui (default) | `https://ui.shadcn.com/r/{name}.json` | Default. No prefix needed: `npx shadcn add button` works. |
| `@magicui` | Magic UI | `https://magicui.design/r/{name}.json` | Effects, text, number-ticker, marquee, beams. |
| `@aceternity` | Aceternity UI | `https://ui.aceternity.com/registry/{name}.json` | Heroes, bento, hero-parallax, globe, lamp, spotlight. |
| `@kibo-ui` | Kibo UI | `https://www.kibo-ui.com/r/{name}.json` | Complex blocks, gantt, kanban, pricing, testimonial, team. |
| `@skiper-ui` | Skiper UI | — (install via CLI: `npx shadcn add @skiper-ui/<name>`) | Signature micro-interactions, image reveals, cursor trails. |

### Launch UI (whole-registry init pattern)

Launch UI doesn't (as of 2026) use a single namespaced item syntax — it uses the shadcn init-from-URL pattern. Install in one of two ways:

```bash
# New project — init from the Launch UI registry root
npx shadcn@latest init 'https://launchuicomponents.com/r'

# Existing shadcn project — add from the registry root
npx shadcn@latest add 'https://launchuicomponents.com/r'
```

When prompted for base color, **choose Zinc** — that matches downstream components.

## Configuring namespaces in `components.json`

To use `@magicui/*`, `@aceternity/*`, etc., the user's project needs them registered in `components.json`. If the project has been shadcn-initialized, extend `components.json`:

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

If the URL for a namespace isn't known with certainty, omit it and fall back to the absolute-URL install form:

```bash
npx shadcn@latest add 'https://www.kibo-ui.com/r/testimonial.json'
```

## CLI command cookbook

```bash
# Initialize shadcn (new project). Choose Zinc as base color by default.
npx shadcn@latest init

# Install a single component from a registered namespace
npx shadcn@latest add @magicui/marquee
npx shadcn@latest add @aceternity/hero-parallax
npx shadcn@latest add @kibo-ui/pricing

# Install default shadcn primitives
npx shadcn@latest add button card input dialog form accordion sheet tabs avatar

# Install from an absolute URL (bypasses namespace config)
npx shadcn@latest add 'https://magicui.design/r/border-beam.json'

# Install Launch UI (whole-registry, existing project)
npx shadcn@latest add 'https://launchuicomponents.com/r'
```

## MCP servers

Live MCP servers let the agent query current components instead of relying on a stale catalog. These get configured in `.mcp.json` at the project root (universal format — Claude Code auto-loads, Cursor reads from `.cursor/mcp.json`, Codex CLI reads from its own config file). See the project README for per-agent install notes.

### shadcn MCP

```json
{
  "mcpServers": {
    "shadcn": {
      "command": "npx",
      "args": ["shadcn@latest", "mcp"]
    }
  }
}
```

Uses the project's `components.json` registries. Once the namespace registrations above are in place, this MCP can list, search, and install components from any of them.

### Magic UI MCP

```json
{
  "mcpServers": {
    "magicui": {
      "command": "npx",
      "args": ["-y", "@magicuidesign/mcp@latest"]
    }
  }
}
```

Exposes Magic UI's component list, source, and install metadata.

### Kibo UI MCP

```json
{
  "mcpServers": {
    "kibo-ui": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://www.kibo-ui.com/api/mcp/mcp"]
    }
  }
}
```

Remote server bridged through `mcp-remote`. Exposes Kibo UI component metadata.

### Combined `.mcp.json`

The skill ships a combined `.mcp.json` at the repo root — see `/.mcp.json` for the canonical block. Users merge it into their project's `.mcp.json` (or copy as-is if no existing one).

## When to query MCP vs use local matrix

- **Use MCP** when it's configured and the user wants the absolute latest component list, or you need to search by keyword.
- **Use the fit matrix** (`components-by-section.md`) when MCP isn't available, when you're pre-filtering candidates by domain aesthetic, or when you want a curated opinion rather than an alphabetical list.

Most of the time, combine both: matrix shortlists, MCP confirms current names and URLs.

## Gotchas

- **Tailwind version.** Magic UI and Aceternity target Tailwind v4 by default. If the project is on v3, components may need a tailwind.config tweak. Check `package.json` and flag to the user.
- **React 19 / RSC.** Some effects rely on client-only hooks. If the project is all-server-components, confirm each component has `"use client"` at the top after install.
- **CSS variable shape.** Default shadcn uses HSL tokens; Magic UI and Aceternity use the same pattern. If the user already has `oklch` tokens, normalize to one format — don't mix.
- **Font loading.** Launch UI and Aceternity may assume specific fonts are loaded. Check `app/layout.tsx` after install.
- **Post-install edit pass.** After every `npx shadcn add`, open the installed file and replace hardcoded colors / radii / fonts with your tokens. This is required for coherence.
