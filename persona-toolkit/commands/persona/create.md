---
description: Create a new user persona through guided conversation
argument-hint: '[optional: brief persona concept, e.g., "technical founder using AI agents"]'
allowed-tools: Read, Write, Edit, Glob, Grep, Bash(ls:*), AskUserQuestion, Task
---

# Create a User Persona

Guide the user through building a user persona for this product. This is a **guided conversation** — collaborate on each aspect, bringing product knowledge to the table.

## Context: $ARGUMENTS

## Phase 0: Product Immersion

Before asking a single question, build deep product understanding.

### Load Product Context

1. Check if `meta/personas/config.json` exists
   - If yes: read it for cached product context (doc paths, product name, etc.)
   - If no: run the Product Discovery Protocol (see the `building-personas` skill)
2. Read the product documentation discovered in config (vision docs, MVP specs, brand docs, README, CLAUDE.md — whatever exists)
3. Read the `building-personas` skill for methodology and quality criteria
4. Read the persona template from the skill's `references/persona-template.md`
5. Check for existing personas: `meta/personas/manifest.json` (if it exists)
6. If existing personas exist, read them to understand the current landscape

**Complete this reading before asking the first question.** This is what makes the conversation valuable — deep product knowledge enables challenging assumptions and suggesting connections.

## Phase 1: Discovery (Guided Conversation)

Ask questions **one at a time**. After each answer, synthesize what you've learned and ask the next question. Use AskUserQuestion with multiple-choice options where possible.

**Question flow** (adapt based on answers — skip questions that have been answered):

1. **The archetype**: "Who is this persona? What's their role and context?" — Suggest archetypes based on the product context
2. **The trigger**: "What specific event or frustration causes this persona to start looking for something like this?" — Push for specificity. "Things break" is not specific enough.
3. **The current state**: "How are they handling this problem today?" — Understanding the workaround reveals the pain.
4. **The technical profile**: "What's their stack? What AI tools are they using? How do they learn new tools?"
5. **Jobs to be done**: "When [their trigger situation], what do they actually want to happen?" — Guide through 2-3 JTBD using "When/I want/So that" format.
6. **Goals and success**: "What does 'this is working' look like for them?"
7. **Information sources**: "Where does this persona hang out? Where would they first hear about us?"
8. **Decision-making**: "What would stop them from adopting? What's the biggest blocker?"
9. **Persona role**: "Is this our primary persona or secondary? Are they also the buyer, or just the user?" — Reference existing personas if any.

**Throughout the conversation:**
- Propose ideas and connections the user might not have considered
- Challenge vague answers: "Can you be more specific?"
- Reference the product: connect persona details to actual product features
- Surface tensions: "This conflicts with what you said about X — which is more accurate?"

## Phase 2: Draft

After gathering enough information (typically 6-8 questions), draft the full persona using the template.

Present the draft to the user section by section:
1. Identity + Quote
2. Technical Profile
3. Jobs to be Done
4. Goals + Pain Points
5. Triggers + Information Sources
6. Relationship to Product + Decision-Making

After each section, ask: "Does this capture it accurately, or should we adjust?"

## Phase 3: Finalize

1. Generate the persona slug (kebab-case archetype, not the fictional name)
2. Write the persona file to `meta/personas/{slug}.md`
3. Update `meta/personas/manifest.json`:
   - If manifest doesn't exist, create it with the schema from the skill
   - If it exists, add the new persona entry
4. Update `meta/personas/config.json` with any new preferences discovered during the conversation
5. Set `confidence: "proto-persona"` (assumption-based until validated by research)
6. Set `nextReview` to 6 months from today

## Phase 4: Next Steps

After saving, ask:

"The persona is saved. Would you like to:"
- Create a journey map for this persona (`/journey:create`)
- Create another persona
- Review what we have so far (`/persona:list`)

## Quality Gate

Before saving, verify against the checklist in the skill. If any item fails, fix it before saving.
