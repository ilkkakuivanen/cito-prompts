---
description: Grunt task — fix typos and wording mistakes. Text only.
argument-hint: [file, area, or the typo itself]
---

## task

- Read `${CLAUDE_PLUGIN_ROOT}/agents/cito-typo.md` in full.
- Follow it exactly in this session.
- Do not spawn a subagent.

## input

- target: `$ARGUMENTS`

## if missing

- If no target is given above, use the one from the conversation so far.
- If that is still unclear, ask.
- Do not sweep the repo.
