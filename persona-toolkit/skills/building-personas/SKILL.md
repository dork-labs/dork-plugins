---
name: building-personas
description: This skill should be used when the user asks to "create a persona", "build a user persona", "create a journey map", "map user journeys", "review personas", "generate personas", or when making product decisions that should be informed by target audience understanding. Guides building and maintaining user personas and user journey maps for developer tools and B2B SaaS products.
---

# Building Personas & User Journeys

## Overview

Build, maintain, and apply user personas and user journey maps for developer-tool and B2B SaaS products. Combines Alan Cooper's goal-directed design, Jobs-to-be-Done narrative structure, and Lean UX proto-personas — adapted specifically for developer audiences where demographics are irrelevant and technical behavior drives everything.

## When to Use

- Creating a new persona or journey map (`/persona:create`, `/journey:create`)
- Auto-generating missing personas or journeys (`/persona:generate`, `/journey:generate`)
- Reviewing existing personas for quality or staleness (`/persona:review`, `/journey:review`)
- Making product decisions that should reference target users
- Writing marketing copy, landing pages, or documentation
- Prioritizing features or roadmap items (who does this serve?)
- Designing UI/UX (which persona's workflow does this optimize?)

## Product Discovery Protocol

Before creating or generating personas, build product understanding. Check for a config file first, then scan if needed.

### Step 1: Check for Existing Config

Read `meta/personas/config.json` if it exists. This file caches discovered product context from previous runs.

### Step 2: If No Config Exists, Scan the Project

Scan for product context in this order (read whatever exists):

1. **Project overview**: `CLAUDE.md`, `README.md`
2. **Product docs**: Scan `meta/` for vision docs, litepaper, brand docs, MVP specs
3. **Codebase structure**: Scan `src/` or `apps/` for routes, schema, API surface
4. **Strategic context**: Check for `roadmap/`, `specs/`, `research/` directories
5. **Documentation**: Check `docs/` directory structure
6. **Setup experience**: Check for `.env.example`, `docker-compose*.yml`, setup scripts

### Step 3: Create the Config

After scanning, write `meta/personas/config.json` with discovered paths:

```json
{
  "product": {
    "name": "[discovered product name]",
    "description": "[one-line description]",
    "repo": "[git remote URL if available]"
  },
  "docs": {
    "vision": "[path or null]",
    "mvp": "[path or null]",
    "brand": "[path or null]",
    "readme": "[path or null]"
  },
  "codebase": {
    "routes": ["[discovered route directories]"],
    "schema": ["[discovered schema directories]"],
    "docs": ["[discovered doc directories]"]
  },
  "strategic": {
    "roadmap": "[path or null]",
    "specs": "[path or null]",
    "research": "[path or null]"
  },
  "preferences": {},
  "lastDiscovery": "[today's date]"
}
```

On subsequent runs, read the config instead of re-scanning. Update the config if new docs are discovered.

## Command Reference

| Command | Mode | Purpose |
|---------|------|---------|
| `/persona:create` | Guided conversation | Collaboratively build a persona step by step |
| `/persona:generate` | Autonomous synthesis | Draft personas from product context, present for approval |
| `/persona:review` | Audit | Quality, staleness, and gap analysis |
| `/persona:list` | Display | Summary table of all personas |
| `/journey:create` | Guided conversation | Stage-by-stage collaborative journey mapping |
| `/journey:generate` | Autonomous synthesis | Draft journeys from persona + product context |
| `/journey:review` | Audit | Quality and product alignment check |

## File Conventions

| Artifact | Location | Naming | Format |
|----------|----------|--------|--------|
| Persona files | `meta/personas/` | `{slug}.md` | Markdown (see template) |
| Journey files | `meta/journeys/` | `{persona-slug}-journey.md` | Markdown (see template) |
| Manifest | `meta/personas/manifest.json` | — | JSON index of all personas + journeys |
| Config | `meta/personas/config.json` | — | JSON product context cache |

**Persona slug**: kebab-case name based on the persona's archetype, not their fictional name. Example: `ai-native-founder`, not `alex-chen`.

## Core Methodology

### The Three Frameworks (Combined)

**1. Alan Cooper's Goal-Directed Design** — Every persona has explicit goals. One **primary persona** per interface — designing for two satisfies neither.

**2. Jobs-to-be-Done** — Reframes goals as jobs: "When [situation], I want [action], so that [outcome]." Covers functional, emotional, and social jobs.

**3. Lean UX Proto-Personas** — Assumption-based drafts built before research. Always label as `proto-persona` with confidence level. Expected to change when validated against real users.

### The ICP / Buyer / User Distinction

| Profile | Describes | Key Questions |
|---------|-----------|---------------|
| **ICP** | The company (not a person) | Size, stage, vertical, tech stack, team structure |
| **Buyer** | The decision-maker who approves | ROI, risk, vendor evaluation criteria |
| **User** | The developer who uses it daily | DX, workflow fit, feature completeness |

### Developer Persona Specifics

Minimize demographics, maximize behavior. What matters:

- **Technical profile**: languages, frameworks, infra, experience level
- **Trigger moment**: what event causes them to search for this category?
- **Learning style**: docs-first? quickstart? GitHub? Discord?
- **Build vs. buy orientation**: internal tooling or best-in-class integration?
- **Success definition**: what does "this tool is working" look like?
- **Information sources**: specific subreddits, newsletters, Discord servers, conferences

### How Many Personas

- **Early stage**: 2-3 maximum
- **One primary**: design for this persona first
- **One secondary**: accommodate without compromising primary
- **Optional anti-persona**: who the product is NOT for

### Quality Checklists

**Persona quality checklist** — every persona must pass:

- [ ] Has a clear trigger moment (not vague)
- [ ] Jobs-to-be-done use the "When/I want/So that" format
- [ ] Pain points are specific and concrete
- [ ] Technical profile includes actual stack details
- [ ] Information sources are specific (not "reads blogs")
- [ ] Confidence level is stated
- [ ] Has a representative quote that sounds like a real person
- [ ] Clear relationship to the product
- [ ] Decision-making context includes adoption blockers
- [ ] Review date is set (6-month cadence)

**Journey map quality checklist** — every journey must pass:

- [ ] Has a Mermaid `journey` diagram at the top for at-a-glance emotional arc visualization
- [ ] Mermaid diagram has peaks AND valleys (not flat) with 1-2 entries per stage scored 1-5
- [ ] Covers all 7 stages (Awareness through Advocacy)
- [ ] Each stage has concrete actions, not abstract descriptions
- [ ] Emotions are specific (not just "happy" or "frustrated")
- [ ] Pain points identify real friction, not hypothetical
- [ ] Success metrics are measurable
- [ ] Opportunities are actionable
- [ ] Touchpoints are specific to the product and channels
- [ ] Questions reflect real developer skepticism

### Common Mistakes

1. **Demographics over behavior** — Strip demographics to what's professionally relevant
2. **Too broad** — "Developers at tech companies" is not a persona
3. **Too specific** — Describing exactly one person isn't generalizable
4. **Missing the trigger** — The event that causes them to search is the most important thing
5. **Creating and never using** — Personas must be referenced in product decisions
6. **Never updating** — Review every 6 months minimum

## Manifest Schema

The manifest at `meta/personas/manifest.json` tracks all personas and journeys:

```json
{
  "personas": [
    {
      "slug": "example-founder",
      "name": "Example Name",
      "role": "primary",
      "type": "user+buyer",
      "confidence": "proto-persona",
      "created": "2026-02-23",
      "lastReviewed": "2026-02-23",
      "nextReview": "2026-08-23",
      "file": "meta/personas/example-founder.md",
      "journeyFile": null
    }
  ],
  "icp": {
    "file": null,
    "lastReviewed": null
  },
  "antiPersonas": [],
  "nextReview": "2026-08-23"
}
```

## Supporting Files

| File | Purpose |
|------|---------|
| `references/persona-template.md` | Full persona document template |
| `references/journey-template.md` | Full 7-stage journey map template |

Read supporting files on demand when creating or reviewing, not upfront.
