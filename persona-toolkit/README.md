# Persona Toolkit

Build and maintain user personas and journey maps for developer tools and B2B SaaS products.

Combines Alan Cooper's Goal-Directed Design, Jobs-to-be-Done narrative structure, and Lean UX Proto-Personas — adapted for developer audiences where demographics are irrelevant and technical behavior drives everything.

## Features

- **Guided persona creation** — Collaborative conversation that challenges assumptions and builds deep personas
- **Autonomous persona generation** — Scans your codebase and product docs to draft personas automatically
- **7-stage journey mapping** — Awareness through Advocacy with Mermaid emotional arc diagrams
- **Quality auditing** — Reviews personas and journeys for staleness, gaps, and alignment
- **Product Discovery Protocol** — Automatically scans your project for docs and caches context for future runs

## Commands

| Command | Description |
|---------|-------------|
| `/persona:create` | Guided conversation to build a persona step by step |
| `/persona:generate` | Auto-generate missing personas from product context |
| `/persona:list` | Display all personas in a summary table |
| `/persona:review` | Audit personas for quality, staleness, and gaps |
| `/journey:create` | Stage-by-stage collaborative journey mapping |
| `/journey:generate` | Auto-generate journeys from persona + product context |
| `/journey:review` | Audit journeys for quality and product alignment |

## File Conventions

The plugin creates and manages files in your project:

```
meta/
├── personas/
│   ├── manifest.json       # Index of all personas and journeys
│   ├── config.json         # Cached product context (auto-generated)
│   ├── {slug}.md           # Individual persona files
│   └── icp.md              # Ideal Customer Profile
└── journeys/
    └── {slug}-journey.md   # Journey maps with Mermaid diagrams
```

## How It Works

### First Run

On the first `/persona:generate` or `/persona:create`, the plugin scans your project for product documentation (README, CLAUDE.md, vision docs, codebase structure, roadmap, etc.) and caches the discovered paths in `meta/personas/config.json`.

### Subsequent Runs

On future runs, the plugin reads the cached config instead of re-scanning, making it faster and consistent. The config also stores user preferences discovered during conversations.

### Methodology

Every persona includes:
- **Technical profile** (stack, tools, experience)
- **Trigger moment** (the event that starts the search)
- **Jobs to be Done** (When/I want/So that format)
- **Adoption blockers** (what stops them)
- **Quality checklist** (10 items, enforced before saving)

Every journey map includes:
- **Mermaid emotional arc diagram** (peaks and valleys, scored 1-5)
- **7 stages** with concrete actions, touchpoints, emotions, pain points
- **Summary table** showing the narrative arc
- **Product gap analysis** and actionable opportunities

## Installation

```bash
# Via marketplace
/plugin marketplace add dork-labs/claude-plugins
/plugin install persona-toolkit@dork-labs

# Via local development
claude --plugin-dir /path/to/persona-toolkit
```

## License

MIT
