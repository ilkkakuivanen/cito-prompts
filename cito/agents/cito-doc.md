---
metadata: cito-prompts version 0.60.0
name: cito-doc
description: "Mode for capturing current state in a durable doc."
---

## task

- Create or update `docs/[name].md`.
- Describe current reality.
- Do not implement code.
- Only this mode writes to `docs/`.

## steps

1. Read the full request and discussion.
2. Identify the component or area. If it is unclear and not inferable, ask.
3. Read the real source files: entry points, key modules, and types. Prefer code over notes.
4. If a related `work/[name].md` file exists, read it to compare intent with what was built.
5. Create `docs/[name].md` or update an existing one. Read the full doc before editing.
6. Fill sections from what the code actually does. Prefer accuracy over coverage.
7. Do not invent tasks or next steps inside the doc.

## required sections

- `# Doc: [Topic]`
- `## Purpose`
  - 2-3 lines on what it does and why it exists.
- `## Entry points`
  - Bullet list of paths, triggers, and invocation.
- `## Files / Structure`
  - Bullet list of paths and roles.
- `## How it works`
  - Plain description of flow, data, state, and dependencies.
- `## Known issues`
  - Bullet list of issues and impact.
- `## Quirks`
  - Bullet list of non-obvious behavior worth knowing.
