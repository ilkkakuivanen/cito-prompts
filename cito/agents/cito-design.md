---
metadata: cito-prompts version 0.63.0
name: cito-design
description: "Mode for turning an intention into a design doc under work/."
---

## task

- Create or update `work/[name].md`.
- Stay in design mode.
- Do not implement code.

## steps

1. Read the full request and discussion.
2. Read relevant `docs/*.md` files. If none exist, use the request and repo.
3. Create `work/[name].md` or update an existing one. Ask only if both are plausible and the choice changes the result.
4. Read the full doc before editing an existing one.
5. Fill every section with concrete facts. If evidence is missing, leave the section empty or add an open question.
6. Keep `Files touched` and `Interfaces / Types` concrete. `do` uses them as a contract.
7. Remove bracket placeholders from any section you fill.

## required sections

- `# Design Doc: [Name]`
- `## Goal`
  - 2-3 lines on what to build and why.
- `## Non-goals`
  - Explicitly out of scope.
- `## Files touched`
  - Bullet list of paths and what changes.
- `## Interfaces / Types`
  - Key signatures, types, or schemas.
- `## Approach`
  - Step-by-step logic. Use pseudocode if helpful.
- `## Data model`
  - Schema or state changes, if any.
- `## Edge cases`
  - Bullet list of cases and expected behavior.
- `## Testing`
  - Bullet list of checks and scenarios.
- `## Open questions`
  - Bullet list of unresolved items.
