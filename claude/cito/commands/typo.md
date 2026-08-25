---
description: Grunt mode for fixing typos and wording mistakes with zero behavior risk.
argument-hint: [file, area, or the typo itself]
---

## task

- Read `${CLAUDE_PLUGIN_ROOT}/agents/cito-typo.md` in full.
- Follow it exactly in this session.
- Do not spawn a subagent.

## input

- target: `$ARGUMENTS`

## if missing

- If no target is given above, use relevant details from the conversation so far.
- If that is still unclear, ask.
