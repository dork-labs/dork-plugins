---
description: Automatically identify persona gaps and generate draft personas from product context
allowed-tools: Read, Write, Edit, Glob, Grep, Bash(ls:*), AskUserQuestion, Task, WebSearch
---

# Generate Missing Personas

Automatically analyze the product, identify which personas are missing, draft them from product context, and present for user approval. This is the **autonomous** counterpart to `/persona:create` (guided conversation).

**Philosophy**: Synthesize personas from everything known about the product — not guessing. Every claim in a generated persona should trace back to something concrete in the product docs, codebase, or competitive landscape. Mark all outputs as `proto-persona` (assumption-based) and flag the key assumptions that need validation.

## Phase 1: Deep Product Immersion

Read ALL available product context. The quality of generated personas depends entirely on how deeply the product is understood.

### Load Product Context

1. Check if `meta/personas/config.json` exists
   - If yes: read it for cached product context
   - If no: run the Product Discovery Protocol (see the `building-personas` skill) to scan the project

2. Using the config (or fresh scan results), read ALL available documentation:

**Product vision and architecture:**
- Product vision/litepaper docs
- MVP or product scope docs
- Brand or positioning docs
- CLAUDE.md / README.md

**Product reality (what's actually built):**
- Database schema directories — the data model reveals who the product serves
- API route directories — the API surface reveals supported workflows
- UI/dashboard route directories — reveals what users see and do

**Strategic context:**
- Roadmap files (if they exist) — planned features imply planned audience
- Spec directories — active specs reveal near-term direction
- Research directories — existing research on users, market, or competitors

**Existing persona landscape:**
- `meta/personas/manifest.json`
- All existing persona and journey files

**Methodology:**
- The `building-personas` skill for quality criteria and frameworks
- The persona template from the skill's `references/persona-template.md`

3. Update `meta/personas/config.json` with any newly discovered paths

## Phase 2: Gap Analysis

Analyze what's missing from the current persona set:

### Coverage Gaps

| Gap Type | Check | Why It Matters |
|----------|-------|----------------|
| **No primary persona** | Is there a persona with `role: primary`? | Can't design without knowing who to design for first |
| **No secondary persona** | Is there at least one `secondary`? | Forces tradeoff thinking |
| **No anti-persona** | Is there anyone in `antiPersonas`? | Clarifies scope — who the product is NOT for |
| **No ICP** | Is `icp` populated? | Company-level targeting for go-to-market |
| **Buyer ≠ User gap** | Are buyer and user perspectives both covered? | They diverge as the product scales |
| **Feature-segment gaps** | Do major product features each map to a user type? | Each integration/feature implies a user |
| **Stage gap** | Are early-stage and growth-stage companies both considered? | Different stages have different needs |

### Synthesis Sources

Map product features to the user types they imply. For each major feature, integration, or capability in the product, identify what kind of user it serves and what their role/motivation would be.

## Phase 3: Draft Personas

For each identified gap, draft a complete persona using the template.

**Drafting rules:**

1. **Derive, don't invent.** Every detail should trace back to a product signal.
2. **Be specific, not generic.** Don't write "uses modern tools" — list actual technologies.
3. **The trigger is sacred.** Must be a concrete event, not a general feeling.
4. **JTBD must be functional.** "When [concrete situation], I want [specific capability], so that [measurable outcome]." Reference actual product features.
5. **Name the anti-patterns.** For each persona, state what would make them NOT adopt the product.
6. **Quote should sound human.** Not marketing copy.

### Persona Ordering

Generate personas in this priority order:
1. **Primary persona** (if missing) — design the entire product for this person
2. **Secondary persona** (if missing) — meaningfully different user to accommodate
3. **Anti-persona** (if missing) — who the product is explicitly NOT for
4. **ICP** (if missing) — the company profile, not a person

## Phase 4: Present for Approval

Present EACH generated persona to the user individually. Do not batch them.

For each persona:

1. **Explain the reasoning**: "I generated this persona because [gap identified] + [product signals that informed it]"
2. **Present the full draft** section by section
3. **Flag key assumptions**: "The three assumptions I'm least confident about are: [1], [2], [3]"
4. **Ask for approval**: Use AskUserQuestion:
   - "Approve and save as-is"
   - "Approve with modifications" (then collaborate on changes)
   - "Reject — this isn't a real user segment for us"
   - "Skip for now — come back to this one"

**Critical: Do NOT save any persona without explicit user approval.**

## Phase 5: Save Approved Personas

For each approved persona:
1. Generate the slug (kebab-case archetype)
2. Write to `meta/personas/{slug}.md`
3. Update `meta/personas/manifest.json`
4. Update `meta/personas/config.json` with any new preferences
5. Set `confidence: "proto-persona"`
6. Set review dates (6-month cadence from today)

## Phase 6: Summary and Next Steps

After all personas are processed, present:

1. **What was created**: Table of approved personas with roles
2. **What was rejected**: Brief note on why
3. **What's still missing**: Any remaining gaps
4. **Recommended next step**: Typically `/journey:generate` to create journey maps

```
## Persona Coverage Summary

| Slot | Status | Persona |
|------|--------|---------|
| Primary | ✓ Created | [name] — [archetype] |
| Secondary | ✓ Created | [name] — [archetype] |
| Anti-persona | ✗ Rejected | [reason] |
| ICP | ✓ Created | [description] |

Missing journeys: [list personas without journey maps]
→ Run `/journey:generate` to create them
```
