---
description: Setup mode for filling both instruction copies from the real repo.
argument-hint: [extra project facts, optional]
---

## task

- Read `${CLAUDE_PLUGIN_ROOT}/agents/cito-setup-project.md` in full.
- Follow it exactly in this session.
- Do not spawn a subagent.

## input

- extra facts from the user: `$ARGUMENTS`

## if missing

- If no extra facts from the user is given above, use relevant details from the conversation so far.
- If that is still unclear, ask.
