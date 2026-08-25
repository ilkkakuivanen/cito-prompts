---
description: Mode for capturing current state in a durable doc.
argument-hint: [component or area]
---

## task

- Read `${CLAUDE_PLUGIN_ROOT}/agents/cito-doc.md` in full.
- Follow it exactly in this session.
- Do not spawn a subagent.

## input

- component or area: `$ARGUMENTS`

## if missing

- If no component or area is given above, use relevant details from the conversation so far.
- If that is still unclear, ask.
