---
metadata: cito-prompts version 0.64.0
name: cito-create-tasklist
description: "Create a committable, trackable work task list from any source material."
---

## task

- Create or update `work/tasks/[name].md` from the source material the user provides, such as a document, chat contents, log snippet, issue, command output, or code review.
- Stay in planning mode. Do not implement code.
- Make each task independently committable and trackable.
- Match the task list's depth to the work's size: keep small checks concise, and structure larger features into a complete, dependency-ordered plan.

## steps

1. If no source material is supplied, ask the user to provide or identify it. Accept material pasted into the conversation as a source; do not require it to exist as a workspace file.
2. Read all provided source material and any files it explicitly names. For a workspace source, record its path; for conversation-only or external material, give it a concise descriptive label. Do not infer work from unrelated sources.
3. Assess the scope before drafting:

- For a small, well-defined check or fix, produce only the necessary verification and follow-up tasks.
- For a feature, multi-file change, or uncertain request, separate discovery or decisions, implementation stages, tests, documentation, and validation as applicable.

4. Create `work/tasks/[name].md`, using a clear name derived from the source material unless the user specifies another. Read the full task list before updating an existing one.
5. Add one unchecked task per cohesive implementation step. Order tasks by dependency, and keep each task small enough for one focused commit.
6. Each implementation task must name the expected files when the source supports identifying them and concrete acceptance criteria. For unknown files, state the discovery needed rather than inventing paths.
7. Preserve uncertainty as an unchecked decision or blocker. Do not invent scope, files, APIs, or solutions not supported by the source material.
8. Leave every task unchecked. Implementation work, not this agent, marks tasks complete.

## required sections

- `# Task List: [Name]`
- `## Source`
  - Identify the source material the list is derived from. Link workspace files; otherwise use its descriptive label and a brief context note.
- `## Tasks`
  - Use `- [ ]` checkboxes, one task per item.
  - Under each task, include `Files:` and `Acceptance:` bullets.
  - For a small source, omit stages and keep the list to the work actually required.
  - For larger work, group tasks under short dependency-oriented headings when that improves execution clarity.
- `## Decisions / Blockers`
  - Unresolved questions or dependencies that prevent a task from starting.
