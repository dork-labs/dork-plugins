---
description: Review existing personas for quality, staleness, and gaps
allowed-tools: Read, Write, Edit, Glob, Grep, AskUserQuestion
---

# Review Personas

Review all existing personas for quality, staleness, and gaps.

## Step 1: Load Context

1. Read the `building-personas` skill for quality criteria
2. Read `meta/personas/manifest.json` to get the persona inventory
3. Read all persona files listed in the manifest
4. Read `meta/personas/config.json` for product context
5. Read the product documentation referenced in the config (to check alignment)

## Step 2: Quality Audit

For each persona, evaluate against the quality checklist from the skill:

- [ ] Has a clear trigger moment (not vague)
- [ ] Jobs-to-be-done use the "When/I want/So that" format
- [ ] Pain points are specific and concrete
- [ ] Technical profile includes actual stack details
- [ ] Information sources are specific
- [ ] Confidence level is stated
- [ ] Has a representative quote
- [ ] Clear relationship to the product
- [ ] Decision-making context includes adoption blockers
- [ ] Review date is set

Score each persona: `pass` (all checks), `needs-update` (1-3 failures), `needs-rebuild` (4+ failures).

## Step 3: Staleness Check

- Compare `lastReviewed` dates against current date
- Flag any persona past its `nextReview` date as `stale`
- Check if the product has changed significantly since the persona was written (new features, pivots, etc.)

## Step 4: Gap Analysis

Analyze whether the persona set covers the product adequately:

- Is there a clear primary persona?
- Does the persona set cover both buyer and user perspectives?
- Are there obvious user segments not represented?
- Is there an anti-persona (who the product is NOT for)?
- Do the personas align with the current roadmap priorities?

## Step 5: Report

Present findings as a table:

```
| Persona | Role | Quality | Staleness | Issues |
|---------|------|---------|-----------|--------|
```

Then provide specific recommendations:
- Which personas need updates (and what specifically)
- Whether new personas should be created
- Whether any personas should be retired

Ask the user how they'd like to proceed with any identified issues.
