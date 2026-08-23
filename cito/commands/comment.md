---
description: Grunt task — add or improve WHY-comments on non-obvious code.
argument-hint: [file or function]
---

## task

- Read `${CLAUDE_PLUGIN_ROOT}/agents/cito-comment.md` in full.
- Follow it exactly in this session.
- Do not spawn a subagent.

## input

- target: `$ARGUMENTS`

## if missing

- If no target is given above, use the one from the conversation so far.
- If that is still unclear, ask.
- Do not sweep the repo.
