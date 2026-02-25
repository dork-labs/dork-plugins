---
description: Automatically generate journey maps for personas that don't have one
allowed-tools: Read, Write, Edit, Glob, Grep, Bash(ls:*), AskUserQuestion, Task, WebSearch
---

# Generate Missing Journey Maps

Automatically identify personas without journey maps, draft journey maps by synthesizing product knowledge with persona profiles, and present for user approval.

**Philosophy**: A journey map is only as good as its specificity. "Visits the website" is not a journey stage — "Reads the README, checks the last commit date, scans for integration docs, and decides whether to clone the repo" is. Every touchpoint, emotion, and friction point must trace back to something real in the product or a reasonable inference from the persona.

## Phase 1: Load Full Context

Journey maps require the deepest product knowledge because they map the user's experience across every surface of the product.

### Load Product Context

1. Check if `meta/personas/config.json` exists
   - If yes: read it for cached product context
   - If no: run the Product Discovery Protocol (see the `building-personas` skill) to scan the project

2. Using the config (or fresh scan results), read ALL available documentation:

**Persona context:**
- `meta/personas/manifest.json` — identify personas WITHOUT `journeyFile` entries
- Read ALL persona files (even ones that have journeys — for cross-reference)
- Read ALL existing journey files (for consistency)

**Product surface (what the user actually touches):**
- Product vision/scope docs, brand docs
- UI/dashboard route directories — what users see and do
- Marketing site structure (if present)
- Documentation directory structure
- CLAUDE.md / README.md — API endpoints are touchpoints for developer personas

**Setup and onboarding surface:**
- `.env.example` files — what configuration is required?
- `package.json` scripts — what's the setup experience?
- `docker-compose*.yml` — is Docker involved?
- Any quickstart or getting-started documentation

**Methodology:**
- The `building-personas` skill
- The journey template from the skill's `references/journey-template.md`

3. Update `meta/personas/config.json` with any newly discovered paths

## Phase 2: Identify Missing Journeys

Check the manifest for personas where `journeyFile` is null or the file doesn't exist.

If ALL personas already have journey maps, report this and ask if the user wants to regenerate any.

If NO personas exist at all, stop and suggest: "No personas exist yet. Run `/persona:generate` first to create personas, then come back for journey maps."

## Phase 3: Draft Journey Maps

For each persona missing a journey, draft the complete 7-stage map.

### Stage-by-Stage Synthesis Guide

For each stage, draw from specific sources:

**Stage 1: Awareness** — Derive from the persona's trigger moment and information sources. The trigger IS the start of awareness. Research: What would this persona Google? What community threads would they find?

**Stage 2: Evaluation** — Derive from the persona's learning style and evaluation criteria. Map actual product surfaces they'd examine: GitHub repo, README, docs, API reference. Developers are skeptical — emotions should reflect that.

**Stage 3: Acquisition** — Map the ACTUAL setup flow from the codebase. How many steps from "clone" to "running"? Every real friction point is a pain point. The persona's technical profile determines how they experience this.

**Stage 4: Activation** — Define the "aha moment" specifically for THIS persona based on their primary JTBD. Map actual views they'd see. Empty state UX is critical here.

**Stage 5: Retention** — Derive from the persona's usage frequency and goals. What makes them come back? What would make them STOP? Customization is likely the retention inflection point.

**Stage 6: Expansion** — Different for each persona type. Map where buyer and user journeys intersect. Consider what's NOT built yet that blocks expansion.

**Stage 7: Advocacy** — Derive from the persona's information sources (they advocate where they consume). What would make this persona write a tweet, blog post, or conference talk?

### Drafting Rules

1. **Reference actual product surfaces.** Don't say "visits the dashboard" — name the specific view or page.
2. **Emotions must be specific and honest.** Include both positive and negative emotions.
3. **Pain points must be real.** Cross-reference against the actual codebase.
4. **Success metrics must be measurable.**
5. **Opportunities must be actionable.** Not "improve the onboarding" but specific, buildable improvements.
6. **The summary table tells a coherent story.** If emotions are flat, the journey isn't specific enough.
7. **Include a Mermaid `journey` diagram.** Every journey map MUST include a Mermaid emotional arc diagram immediately after the frontmatter and before the summary table. Use 1-2 entries per stage with emotion scores from 1-5. Labels should be concrete moments. The arc must have peaks AND valleys. See the journey template for syntax and scoring guide.

## Phase 4: Present for Approval

Present EACH journey map to the user individually.

For each journey:

1. **State which persona this is for** and briefly summarize the persona
2. **Present stage by stage** — show 2-3 stages at a time, ask for feedback, continue
3. **Present the summary table** at the end
4. **Highlight insights**: "Here are the product gaps this journey reveals..."
5. **Ask for approval**: Use AskUserQuestion:
   - "Approve and save as-is"
   - "Approve with modifications" (collaborate on specific stages)
   - "This journey doesn't feel right — let's redo it via `/journey:create`"
   - "Skip for now"

**Critical: Do NOT save any journey without explicit user approval.**

## Phase 5: Save Approved Journeys

For each approved journey:
1. Write to `meta/journeys/{persona-slug}-journey.md`
2. Update the persona's entry in `meta/personas/manifest.json` with the `journeyFile` path
3. Match confidence level to the persona's confidence level

## Phase 6: Cross-Journey Analysis

After all journeys are generated, perform a cross-journey analysis:

1. **Intersection points**: Where do different personas' journeys overlap?
2. **Systemic friction**: Are there stages where ALL personas struggle?
3. **Content gaps**: What content/docs are needed across multiple journeys?
4. **Quick wins**: Low-effort improvements that would help multiple personas
5. **Critical moments**: The 1-2 moments where failure means losing the user permanently

Present this analysis and ask if the user wants to create issues or roadmap items for any findings.

```
## Journey Generation Summary

| Persona | Journey | Status | Key Insight |
|---------|---------|--------|-------------|
| [name] | [slug]-journey.md | ✓ Created | [one-line insight] |
| [name] | [slug]-journey.md | ✗ Skipped | [reason] |

### Cross-Journey Insights
- **Systemic friction at [stage]**: [description]
- **Content gap**: [what's missing]
- **Quick win**: [actionable improvement]

→ Run `/journey:review` periodically to keep journeys aligned with product changes
```
