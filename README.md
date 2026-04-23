# landing-page-design

A cross-agent Skill that turns any Claude Code / Codex CLI / Cursor session into a landing page and website generator — without the generic AI-slop aesthetic.

**Status:** v0.1.0 — April 2026. Works on Claude Code (plugin) and any agent that reads SKILL.md (Codex CLI, Cursor, Gemini CLI, Antigravity IDE).

## What it does

Given a request like *"build a landing page for a dermatologist in Dubai"* or *"I need a site for my indie SaaS launch"*, this skill:

1. **Reasons from domain first** — the type of site (medical, SaaS, agency, e-commerce, portfolio, restaurant, creator, nonprofit, local service, crypto, AI product, real estate) is the master key for sections, aesthetic, and CTAs.
2. **Asks only what matters** — three questions max; everything else is inferred.
3. **Locks coherence with design tokens** — colors, fonts, radius, shadow, motion — *before* installing any components.
4. **Pulls real components live** via the shadcn CLI and MCP servers from shadcn/ui, Magic UI, Aceternity, Kibo UI, Launch UI, and Skiper.
5. **Edits every installed component** to consume the tokens, so multi-library compositions feel like one designed site.
6. **Ships AI-discoverable** by auto-generating an `llms.txt` for every site.
7. **Hands off SEO** rather than doing it — meant to pair with a separate `/seo` skill.

## Repo layout

```
landing-page-design/
├── SKILL.md                           # the skill (lean router, <500 lines)
├── references/
│   ├── domains.md                     # 12 domain recipes
│   ├── registries.md                  # shadcn CLI + MCP server configs
│   ├── components-by-section.md       # fit matrix
│   ├── assets.md                      # icons, illustrations, photos, patterns, 3D
│   └── llms-txt-template.md           # llms.txt generator spec
├── .mcp.json                          # universal MCP server config
├── .claude-plugin/
│   └── plugin.json                    # Claude Code plugin wrapper (optional)
├── evals/
│   └── evals.json                     # test prompts for the skill-creator eval loop
└── README.md
```

## Install

### Claude Code (plugin)

Clone the repo (or a fork) into your Claude Code plugins directory:

```bash
# Global install
mkdir -p ~/.claude/plugins
git clone https://github.com/<your-username>/landing-page-design-skill ~/.claude/plugins/landing-page-design

# Or per-project
mkdir -p .claude/plugins
git clone https://github.com/<your-username>/landing-page-design-skill .claude/plugins/landing-page-design
```

Restart Claude Code. The skill auto-triggers on website/landing-page requests, or invoke it explicitly:

```
/landing-page-design
```

MCP servers (shadcn, Magic UI, Kibo UI) are wired up automatically via `.claude-plugin/plugin.json`.

### Codex CLI

Copy `SKILL.md` and the `references/` folder into `.skills/landing-page-design/` in your project (or global `~/.codex/skills/`):

```bash
mkdir -p .skills/landing-page-design
cp -r SKILL.md references/ .skills/landing-page-design/
```

Copy `.mcp.json` into your project root (Codex CLI reads MCP config from the standard location — check your Codex CLI docs for the exact path; as of April 2026 the universal `.mcp.json` is honored).

### Cursor

Copy `SKILL.md` and `references/` into `.cursor/skills/landing-page-design/` (Cursor picks them up automatically).

For MCP, merge the `mcpServers` block from `.mcp.json` into `.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "shadcn": { "command": "npx", "args": ["shadcn@latest", "mcp"] },
    "magicui": { "command": "npx", "args": ["-y", "@magicuidesign/mcp@latest"] },
    "kibo-ui": { "command": "npx", "args": ["-y", "mcp-remote", "https://www.kibo-ui.com/api/mcp/mcp"] }
  }
}
```

Restart Cursor.

### Other SKILL.md-compatible agents (Gemini CLI, Antigravity IDE)

Drop `SKILL.md` + `references/` into the agent's skills directory (check each agent's docs for the exact path). Manually register the MCP servers using the agent's MCP config format.

## How it works, in one paragraph

The SKILL.md is a lean router (~2000 tokens) that orients the agent: philosophy, the 8-phase flow (context → questions → domain → components → tokens → assembly → llms.txt → handoff), the library map, anti-patterns, and a done-checklist. The deep knowledge lives in `references/` and is progressively loaded — the agent only reads `references/domains.md` when it enters Phase 3, `references/registries.md` and `components-by-section.md` when it enters Phase 4, and so on. This keeps the main context window lean while making the full design library available on demand.

## Philosophy

1. **Domain is the master key.** Sections, components, assets, and copy all cascade from what type of site it is.
2. **Value thinking, not aesthetic thinking.** *What does the visitor need to feel / know / do?* Then pick components that serve that.
3. **Let the agent think.** Give it frameworks, not scripts. Only ask questions the agent genuinely can't answer from context.
4. **Coherence before components.** Design tokens first, installs second, edits third.
5. **Real components from real libraries via real CLIs and MCPs.** No reinventing effects from scratch. No stale catalogs. Live, versioned, maintained.
6. **Ship AI-discoverable by default.** Every generated site includes `llms.txt`.
7. **SEO is a handoff, not a feature.** Keep this skill focused.

## Dev & iteration

### Test with the skill-creator eval loop (Claude Code)

[`anthropics/skills`](https://github.com/anthropics/skills) ships a `skill-creator` skill with an eval framework. Install it, then point it at this repo:

```bash
# From your skill-creator directory
python -m scripts.aggregate_benchmark <workspace>/iteration-1 --skill-name landing-page-design
python <skill-creator-path>/eval-viewer/generate_review.py <workspace>/iteration-1 --skill-name "landing-page-design"
```

Use `evals/evals.json` as the prompt set.

### Dogfood

Invoke `/landing-page-design` on a real project (your own portfolio, a friend's business) and honestly evaluate the output. If it feels generic or AI-slop, iterate — the skill is specifically tuned to avoid that.

## Contributing

Pull requests welcome. Especially:

- New domain recipes (12 isn't enough — B2B marketplaces, dating apps, gaming, edtech, fitness SaaS, etc.)
- Updated registry namespace URLs when libraries change theirs
- Better anti-pattern examples for the "AI-slop detection" section in SKILL.md
- MCP config notes for new agents

## License

MIT.
