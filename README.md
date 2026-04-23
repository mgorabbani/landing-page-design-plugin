# landing-page-design

A cross-agent Skill that turns any Claude Code / Codex CLI / Cursor session into a thoughtful landing page and website generator — without the generic AI-slop aesthetic.

**Status:** v0.1.0 — April 2026. Works on Claude Code (plugin) and any agent that reads SKILL.md (Codex CLI, Cursor, Gemini CLI, Antigravity IDE).

## What this is

An **instruction manual for AI agents.** Not a template pack. Not an MCP server. Not a frozen catalog of components.

When the user says *"build a landing page for a dermatologist in Dubai"* or *"I need a site for my indie SaaS launch"*, this skill makes the agent:

1. **Detect the domain** first (the master key).
2. **Ask only the questions it can't answer** from the filesystem or the request.
3. **Walk a strict pattern**: domain → single-page or multi → section list → per-section content anatomy → components → assets → design tokens → build → `llms.txt`.
4. **Discover what's current on the web** before picking components — the shadcn-compatible ecosystem (shadcn/ui, Magic UI, Aceternity, Kibo UI, Launch UI, Skiper, 21st.dev, and newer entrants) changes monthly, so any frozen list in this repo is a starting point, never the source of truth.
5. **Lock coherence with design tokens** — colors, fonts, radius, shadow, motion — *before* installing any component.
6. **Install via the shadcn CLI** (universal path for every library above).
7. **Reach for the right media tool** based on the domain, not reflexively. Icon pack, illustration pack, photography, patterns, 3D, and — only when the domain genuinely calls for it — video (where options like user footage, Lottie, Rive, or Remotion are each awareness-level suggestions, not defaults).
8. **Ship AI-discoverable** by auto-generating `llms.txt` for every site.
9. **Hand SEO off** to a separate `/seo` skill rather than doing it here.

## The pattern the skill enforces

```
1. Detect domain            → references/domains.md
2. Single-page or multi?    → default single-page; branch only on
                              strong signal or explicit request
3. Section list             → domain recipe gives the ordered list
4. Section anatomy          → for each section, what content slots it needs
5. Write the copy           → specific, not generic — references/copy.md
6. Components per section   → browse current libraries, shortlist, pick
7. Assets per section       → icons, illustrations, photos via Unsplash
                              API (no placeholders), patterns, 3D, and
                              video only if the domain calls for it
8. Design tokens            → colors, fonts, radius, shadow, motion — BEFORE install
9. Build + responsive/a11y  → shadcn CLI install, edit for tokens,
                              compose pages, test mobile + reduced-motion
10. llms.txt                → auto-generated from what was built
11. Deploy handoff          → suggest vercel / netlify / cloudflare pages
12. SEO handoff             → hand off to /seo skill
```

## Repo layout

```
landing-page-design/
├── SKILL.md                           # the skill (lean router, ~290 lines)
├── references/
│   ├── domains.md                     # 12 domain recipes
│   ├── copy.md                        # headline/sub/CTA patterns + phrase blacklist
│   ├── registries.md                  # discovery pattern + seed libraries
│   ├── components-by-section.md       # section anatomy + fit matrix
│   ├── assets.md                      # icons, illustrations, Unsplash API workflow, patterns, 3D, optional video
│   └── llms-txt-template.md           # llms.txt generator spec
├── .claude-plugin/
│   └── plugin.json                    # Claude Code plugin wrapper
├── evals/
│   └── evals.json                     # test prompts for eval loops
└── README.md
```

**No bundled MCP.** This repo ships no `.mcp.json`. The skill tells the agent to use *its own* web-fetch / search tool to browse library docs directly. If you want to add MCP servers (shadcn's, Magic UI's, etc.) to your own environment, that's a separate choice you make in your own `.mcp.json` — this skill doesn't require or ship one.

**No frozen catalog.** Components listed in `references/components-by-section.md` are seed examples as of April 2026. The skill instructs the agent to verify current names against each library's docs before installing.

## Install

### Claude Code (plugin)

Clone into your plugins directory:

```bash
mkdir -p ~/.claude/plugins
git clone https://github.com/<your-username>/landing-page-design-skill ~/.claude/plugins/landing-page-design
```

Or per-project:

```bash
mkdir -p .claude/plugins
git clone https://github.com/<your-username>/landing-page-design-skill .claude/plugins/landing-page-design
```

Restart Claude Code. The skill auto-triggers on website / landing-page requests, or invoke it explicitly:

```
/landing-page-design
```

### Codex CLI

Copy `SKILL.md` + `references/` into `.skills/landing-page-design/` in your project (or `~/.codex/skills/` for global):

```bash
mkdir -p .skills/landing-page-design
cp -r SKILL.md references/ .skills/landing-page-design/
```

### Cursor

Copy `SKILL.md` + `references/` into `.cursor/skills/landing-page-design/`. Cursor picks them up automatically.

### Other SKILL.md-compatible agents (Gemini CLI, Antigravity IDE)

Drop `SKILL.md` + `references/` into the agent's skills directory — check each agent's docs for the exact path.

## Philosophy

1. **Domain is the master key.** Sections, components, assets, and copy all cascade from what type of site it is.
2. **Value thinking, not aesthetic thinking.** *What does the visitor need to feel / know / do?* Then pick the sections and components that serve that.
3. **Pattern, not prescription.** The skill gives the agent a decision flow and reference material; the agent reasons the specifics.
4. **Ask the right questions.** Only ask the user what they genuinely know better than the agent. Infer everything else.
5. **Browse for current truth.** Libraries change. Always check the live docs before picking a component.
6. **Coherence before components.** Design tokens first, installs second, edits third.
7. **Real components via the shadcn CLI.** No reinventing effects from scratch. No stale catalogs.
8. **Ship AI-discoverable by default.** Every generated site includes `llms.txt`.
9. **SEO is a handoff, not a feature.** Keep this skill focused.

## Dev & iteration

### Evaluate with the skill-creator loop (Claude Code)

[`anthropics/skills`](https://github.com/anthropics/skills) ships a `skill-creator` skill with an eval framework. Install it and point it at this repo, using `evals/evals.json` as the prompt set:

```bash
python -m scripts.aggregate_benchmark <workspace>/iteration-1 --skill-name landing-page-design
python <skill-creator-path>/eval-viewer/generate_review.py <workspace>/iteration-1 --skill-name "landing-page-design"
```

### Dogfood

Invoke `/landing-page-design` on a real project (your own portfolio, a friend's business) and honestly evaluate the output. If it feels generic or AI-slop, iterate — the skill is specifically tuned to avoid that.

## Contributing

Pull requests welcome. Especially:

- New domain recipes (12 isn't enough — B2B marketplaces, dating apps, gaming, edtech, fitness SaaS, etc.)
- Additional discovery sources for `references/registries.md` (new curated directories, aggregators, awesome-lists)
- New section types in the anatomy table (comparison tables, trust bar, demo iframe, etc.)
- Better anti-pattern examples for the AI-slop detection list
- Notes for new SKILL.md-compatible agents

## License

MIT.
