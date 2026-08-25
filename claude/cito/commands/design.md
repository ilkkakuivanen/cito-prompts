---
description: Mode for turning an intention into a design doc under work/.
argument-hint: [what to design]
---

## task

- Read `${CLAUDE_PLUGIN_ROOT}/agents/cito-design.md` in full.
- Follow it exactly in this session.
- Do not spawn a subagent.

## input

- intention: `$ARGUMENTS`

## if missing

- If no intention is given above, use relevant details from the conversation so far.
- If that is still unclear, ask.
