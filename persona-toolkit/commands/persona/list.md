---
description: Display all personas in a summary table
allowed-tools: Read, Glob
---

# List Personas

Display a summary of all user personas and their journey maps.

## Steps

1. Read `meta/personas/manifest.json`
2. For each persona in the manifest, read the persona file and extract key fields
3. Check for corresponding journey files in `meta/journeys/`

## Output Format

Display a formatted table:

```
## User Personas

| # | Name | Archetype | Role | Type | Confidence | Journey? | Last Reviewed |
|---|------|-----------|------|------|------------|----------|---------------|
| 1 | [Name] | [Archetype] | primary | user+buyer | proto-persona | Yes | 2026-02-23 |
| 2 | ... | ... | ... | ... | ... | ... | ... |
```

If an ICP exists, show it separately:

```
## Ideal Customer Profile
File: meta/personas/icp.md
Last Reviewed: [date]
```

If anti-personas exist, show them:

```
## Anti-Personas
| Name | Why NOT our user |
|------|-----------------|
```

If the manifest doesn't exist or is empty, state: "No personas created yet. Use `/persona:create` to create your first persona."

Flag any personas that are past their `nextReview` date with a warning marker.
