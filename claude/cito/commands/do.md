---
description: Mode for executing one task-list item in scope and verifying the result.
argument-hint: [task list path, optional task name]
---

## task

- Read `${CLAUDE_PLUGIN_ROOT}/agents/cito-do.md` in full.
- Follow it exactly in this session.
- Do not spawn a subagent.

## input

- task list: `$ARGUMENTS`

## if missing

- If no task list is given above, use relevant details from the conversation so far.
- If that is still unclear, ask.
