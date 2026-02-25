---
description: Review journey maps for completeness, quality, and gaps
allowed-tools: Read, Write, Edit, Glob, Grep, AskUserQuestion
---

# Review Journey Maps

Review all existing journey maps for quality, completeness, and alignment with current product state.

## Step 1: Load Context

1. Read the `building-personas` skill for quality criteria
2. Read `meta/personas/manifest.json` to get the inventory
3. Read all journey files listed in the manifest
4. Read the associated persona files (journeys without persona context are meaningless)
5. Read `meta/personas/config.json` for product context
6. Read the product documentation referenced in the config

## Step 2: Quality Audit

For each journey map, evaluate against the journey quality checklist from the skill:

- [ ] Has a Mermaid `journey` diagram at the top
- [ ] Mermaid diagram has peaks AND valleys (not flat) with 1-2 entries per stage scored 1-5
- [ ] Covers all 7 stages
- [ ] Each stage has concrete actions, not abstract descriptions
- [ ] Emotions are specific (not just "happy" or "frustrated")
- [ ] Pain points identify real friction, not hypothetical
- [ ] Success metrics are measurable
- [ ] Opportunities are actionable
- [ ] Touchpoints are specific to the product and channels
- [ ] Questions reflect real developer skepticism

Score each journey: `pass`, `needs-update`, `needs-rebuild`.

## Step 3: Product Alignment

Check whether journey maps reflect the current product reality:
- Have new features been built that should appear in touchpoints?
- Have any touchpoints become obsolete (features removed/changed)?
- Do the "Our content/UX" sections reflect what actually exists now?
- Are the identified opportunities still relevant?

## Step 4: Cross-Journey Analysis

If multiple journeys exist:
- Where do different personas' journeys intersect? (especially buyer + user)
- Are there stages where ALL personas struggle? (systemic issue)
- Are there contradictions between personas' journeys?
- Which persona's journey is most critical to get right first?

## Step 5: Report

Present findings and recommendations. Ask the user how they'd like to address any issues found.
