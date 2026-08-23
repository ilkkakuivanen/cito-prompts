---
description: Create a committable, trackable work task list from a work or docs document.
argument-hint: [path to work or docs document]
---

## task

- Read `${CLAUDE_PLUGIN_ROOT}/agents/cito-create-tasklist.md` in full.
- Follow it exactly in this session.
- Do not spawn a subagent.

## input

- source document: `$ARGUMENTS`

## if missing

- If no source document is given above, use a work or docs document named in the conversation so far.
- If no source document is clear, ask.
