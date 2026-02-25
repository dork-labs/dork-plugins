---
description: Create a user journey map for an existing persona
argument-hint: '[persona-slug, e.g., "ai-native-founder"]'
allowed-tools: Read, Write, Edit, Glob, Grep, AskUserQuestion, Task
---

# Create a User Journey Map

Guide the user through mapping the user journey for a specific persona through the product. This is a **guided conversation** — collaborate on each stage, bringing product knowledge to the table.

## Context: $ARGUMENTS

## Phase 0: Load Context

1. Check if `meta/personas/config.json` exists
   - If yes: read it for cached product context
   - If no: run the Product Discovery Protocol (see the `building-personas` skill)
2. Read `meta/personas/manifest.json` to find the persona
3. Read the persona file (the one specified in the argument, or ask the user which persona)
4. Read the product documentation referenced in the config — deep product knowledge is needed to map touchpoints
5. Read the `building-personas` skill for methodology
6. Read the journey template from the skill's `references/journey-template.md`
7. Check for existing journeys in `meta/journeys/` for consistency

If no persona slug is provided, list available personas and ask the user to choose.

## Phase 1: Stage-by-Stage Guided Conversation

Walk through each of the 7 stages one at a time. For each stage:

1. **Set the scene**: Describe what typically happens at this stage for this persona, based on what is known about them and the product
2. **Propose a draft**: Based on the persona's profile, propose concrete details for each dimension (actions, touchpoints, emotions, etc.)
3. **Collaborate**: Ask the user to validate, adjust, or add to the draft
4. **Record**: Capture the agreed details

**The 7 stages:**

1. **Awareness** — How do they discover the problem or the product?
   - Focus on the trigger moment from the persona
   - Map specific channels where this persona would encounter the product

2. **Evaluation** — How do they assess this product vs alternatives?
   - Developers evaluate through the product, not marketing
   - Consider: README quality, docs, GitHub health, time-to-understand

3. **Acquisition** — How do they get started?
   - Map the actual setup flow (CLI install, Docker, config, first project)
   - Identify every friction point

4. **Activation** — When do they first get real value?
   - This is the "aha moment" — define it precisely for this persona
   - Consider what "first success" looks like for them

5. **Retention** — What keeps them using it?
   - What's the daily/weekly habit?
   - What would cause them to stop using it?

6. **Expansion** — How do they bring others in?
   - Team adoption, additional projects, deeper integration
   - Where does buyer persona diverge from user persona?

7. **Advocacy** — How do they tell others?
   - Developer word-of-mouth specifics
   - Community contributions, blog posts, social proof

**Throughout**: Challenge generic answers. "Visits the website" is not specific enough — WHERE on the website? What are they looking for? What would make them bounce?

## Phase 2: Journey Summary

After completing all 7 stages:

1. **Create a Mermaid `journey` diagram** showing the emotional arc at a glance. Use 1-2 entries per stage with emotion scores from 1-5. Labels should be concrete moments. The arc must have peaks AND valleys. See the journey template for syntax and scoring guide.

2. **Create a summary table** showing the emotional arc:

```
| Stage | Key Emotion | Biggest Friction | Top Opportunity |
```

Present both the Mermaid diagram and table to the user and ask if the overall narrative feels right.

## Phase 3: Finalize

1. Write the journey file to `meta/journeys/{persona-slug}-journey.md` using the template (Mermaid diagram goes immediately after frontmatter, before the summary table)
2. Update `meta/personas/manifest.json` to add the `journeyFile` path to the persona entry
3. Set confidence and review dates matching the persona

## Phase 4: Insights

After saving, highlight:
- **Product gaps**: Where the journey reveals something that hasn't been built yet
- **Content needs**: What content/documentation is missing at each stage
- **Quick wins**: Low-effort improvements that would reduce friction
- **Critical moments**: The 1-2 moments where the product absolutely cannot fail

Ask if the user would like to create issues for any of the identified gaps.
