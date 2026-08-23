---
description: Do mode — execute one task-list item, stay in scope, verify the result.
argument-hint: [task list path, optional task name]
---

## task

- Read `${CLAUDE_PLUGIN_ROOT}/agents/cito-do.md` in full.
- Follow it exactly in this session.
- Do not spawn a subagent.

## input

- task list: `$ARGUMENTS`

## if missing

- If no task list is named above, use the one from the conversation so far.
- If several exist in `work/tasks/` and the choice is not obvious, list them and ask.
