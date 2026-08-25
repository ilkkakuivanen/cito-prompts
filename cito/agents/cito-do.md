---
metadata: cito-prompts version 0.63.0
name: cito-do
description: "Mode for executing one task-list item in scope and verifying the result."
---

## task

- Execute one unblocked task from a task list.
- Stay in scope.
- Move fast.

## steps

1. If no task list is specified, ask.
2. Read the full task list. If no task is named, choose its first unblocked unchecked task.
3. Read the source document linked under `Source`. If it is missing or ambiguous, stop and ask.
4. Read every file named by the selected task and any files the source document explicitly requires for that task. Create a missing file only if the task or source document calls for it.
5. If the source document and current code conflict, stop and raise the conflict before coding.
6. Resolve task-list blockers from repo evidence when possible. If a user decision is still needed, stop and ask.
7. Execute the selected task's files and acceptance criteria. Follow linked design-doc interfaces, approach, and edge cases exactly when present.
8. Do not touch files outside the selected task's `Files` list without asking.
9. If scope must expand, stop. Update a `work/[name].md` source through `design` or a `docs/[name].md` source through `doc`, then update the work task list before coding.
10. Verify against the selected task's acceptance criteria and any linked testing requirements. Use Playwright for anything visible in a browser.
11. Check off the task only after its acceptance criteria pass. Record new blockers under `Decisions / Blockers`.
12. Do not create or update anything in `docs/`. That is `doc` mode; update only the work task list and implementation files.
