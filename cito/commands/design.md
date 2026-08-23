---
description: Design mode — turn an intention into a work doc.
argument-hint: [what to design]
---

## task

- Read `${CLAUDE_PLUGIN_ROOT}/agents/cito-design.md` in full.
- Follow it exactly in this session.
- Do not spawn a subagent.

## input

- intention: `$ARGUMENTS`

## if missing

- If no intention is given above, use the request from the conversation so far.
- If that is still unclear, ask.
