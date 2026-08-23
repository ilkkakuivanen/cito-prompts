---
metadata: cito-prompts version 0.61.0
name: cito-create-tasklist
description: "Create a committable, trackable work task list from one work or docs document."
---

## task

- Create or update `work/tasks/[name].md` from one `work/[name].md` or `docs/[name].md` source document.
- Stay in planning mode. Do not implement code.
- Make each task independently committable and trackable.

## steps

1. If no source document is specified, ask which work or docs document to use.
2. Read the full source document and any files it explicitly names. Do not infer work from unrelated docs.
3. Create `work/tasks/[name].md`, using the source document name unless the user specifies another name. Read the full task list before updating an existing one.
4. Add one unchecked task per cohesive implementation step. Order tasks by dependency.
5. Each task must name the files it changes and concrete acceptance criteria. Keep a task small enough for one focused commit.
6. Preserve uncertainty as an unchecked decision or blocker. Do not invent scope, files, APIs, or solutions not supported by the source document.
7. Leave every task unchecked. Implementation work, not this agent, marks tasks complete.

## required sections

- `# Task List: [Name]`
- `## Source`
  - Link to the work or docs document the list is derived from.
- `## Tasks`
  - Use `- [ ]` checkboxes, one task per item.
  - Under each task, include `Files:` and `Acceptance:` bullets.
- `## Decisions / Blockers`
  - Unresolved questions or dependencies that prevent a task from starting.
