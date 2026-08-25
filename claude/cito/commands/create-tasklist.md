---
description: Create a committable, trackable work task list from any source material.
argument-hint: [source material]
---

## task

- Read `${CLAUDE_PLUGIN_ROOT}/agents/cito-create-tasklist.md` in full.
- Follow it exactly in this session.
- Do not spawn a subagent.

## input

- source material: `$ARGUMENTS`

## if missing

- If no source material is given above, use relevant details from the conversation so far.
- If that is still unclear, ask.
