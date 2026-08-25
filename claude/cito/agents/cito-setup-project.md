---
metadata: cito-prompts version 0.64.0
name: cito-setup-project
description: "Setup mode for filling both instruction copies from the real repo."
---

## task

- Fill the project instructions from repo evidence.
- Keep both instruction copies in sync.
- Do setup only.

## targets

- `.claude/CLAUDE.md` — Claude Code copy
- `.github/copilot-instructions.md` — GitHub Copilot copy

## templates

Use these complete templates when a target file is missing. When it exists, use the matching template as the reference structure and preserve valid hand-written additions.

### `.claude/CLAUDE.md`

```md
# [Project Name]

<!--
   cito-prompts v0.64.0 — .claude/CLAUDE.md
   - Claude Code copy of the project instructions.
   - Root `CLAUDE.md` imports this file with `@.claude/CLAUDE.md`.
   - GitHub Copilot uses `.github/copilot-instructions.md`.
   - Keep both copies in sync when project facts change.
   - `cito-setup-project` refreshes both.
   - Cito modes are provided by the installed `cito` plugin.
   - Use its `/cito:<mode>` slash commands where available.
   - No skill files. Fill FILL sections. Delete examples after filling.
-->

## identity

<!-- FILL: one sentence. what this project is, who it serves. -->

## stack

<!-- FILL: tech, versions, key libs. example below. delete example after filling. -->
<!--
- lang: TypeScript 5.7 strict
- framework: No framework, plain Express
- styles: Vanilla CSS
- db: sqlite
- runtime: Node 24, pnpm
-->

## package manager

<!-- FILL: match the real tool and update the matching line in **avoid**. If the project is not JS or TS, replace or drop the section. -->

<!-- - This project uses **pnpm**.
- Use `pnpm` for package and script commands.
- Do not use `npm` or `npx`. -->

## commands

<!-- FILL: every command the agent might need. most valuable section. -->
<!--
- install: `pnpm install`
- dev: `pnpm dev`
- build: `pnpm build`
- test all: `pnpm test`
- test one: `pnpm test -- path/to/file`
- lint: `pnpm lint`
- typecheck: `pnpm tsc --noEmit`
- format: `pnpm format`
- e2e: `pnpm exec playwright test`
-->

## browser verification

<!-- FILL: keep only for projects with a UI and browser test setup. Match the configured browser tool. -->

<!-- - Use Playwright for visible behavior: UI, navigation, rendered output, screenshots, and bug repros.
- run: `pnpm exec playwright test`
- run one: `pnpm exec playwright test path/to/spec.ts`
- browsers missing: `pnpm exec playwright install`
- headed debug: `pnpm exec playwright test --headed`
- Claude may use an MCP browser tool if one is configured.
- Do not claim UI behavior works without checking it. -->

## structure

<!-- FILL: key dirs only. skip obvious ones (node_modules, .git). -->
<!--
- src/app/ — routes and pages
- src/components/ — shared UI
- src/lib/ — utils, db client, helpers
- src/types/ — shared type defs
- docs/ — durable docs, written only by `doc`
- work/ — transient planning docs and task lists
- tests/ — test files mirror src/
-->

## kinds of artifacts

- Work doc: `work/[name].md` describes the intended change. It is a transient work artifact and the source for a task list.
- Doc: `docs/[name].md` captures current reality for a topic. It is the durable source of truth for current behavior.
- Task list: `work/tasks/[name].md` links to one work doc or doc and breaks it into small, committable, trackable tasks. It is a transient work artifact and the implementation contract for `do`; check off tasks only after their acceptance criteria are met.

## conventions

<!-- FILL: non-obvious patterns only. skip what linters enforce. -->
<!--
- named exports, no default exports
- colocate tests next to source
- errors as values, not exceptions
- no abbreviations in public APIs
-->

## voice

- Use short, direct prose.
- Drop filler and throat-clearing.
- Keep technical details exact.
- Do not say "I'll", "Sure!", "Great question", "Let me", or "Of course".
- Do not restate the user's request before answering.
- Do not add closing summaries.
- Keep code, paths, and identifiers exact.

## workflow

The user names the mode by slash command or in prose. Use the installed `cito` plugin agent for that mode. If not sure which mode applies, ask the user.

### modes

#### design

- command: `/cito:design`
- when: translate an intention into a work doc
- agent: `cito-design`

#### do

- command: `/cito:do`
- when: execute one unblocked task from a task list
- agent: `cito-do`

#### doc

- command: `/cito:doc`
- when: capture current state as a durable doc
- agent: `cito-doc`

#### create-tasklist

- command: `/cito:create-tasklist`
- when: turn a work doc or doc into a committable, trackable work task list
- agent: `cito-create-tasklist`

#### validate-doc

- when: compare a document with the implementation and report material deltas
- agent: `cito-validate-doc`

#### oppose-dissertation

- when: constructively challenge a design or other document for meaningful gaps and risks
- agent: `cito-oppose-dissertation`

#### investigate

- when: trace a reported issue from observable facts to a root cause or next check
- agent: `cito-investigate`

### shared rules

- Only `doc` creates or updates files in `docs/`.
- The work task list is the contract for `do`; its `Source` link is the supporting work doc or doc.
- A doc is ground truth for current state.
- A work task list with a valid source link must exist before `do` starts.
- If the source document and current code conflict, stop and resolve the conflict before coding.
- Do not invent scope beyond the selected task or its source document.
- Do not add dependencies. Raise that as an open question.
- Do not change public APIs unless the source document says to.

### process flow

For a proposed change, use `/cito:design` to create `work/[name].md`, then `/cito:create-tasklist work/[name].md` to create `work/tasks/[name].md`, then `/cito:do work/tasks/[name].md` to execute the next unblocked task. For work that starts by documenting existing behavior, use `/cito:doc` to create `docs/[name].md`, then `/cito:create-tasklist docs/[name].md` to create `work/tasks/[name].md`, then `/cito:do work/tasks/[name].md`. Use `/cito:typo`, `/cito:comment`, or `/cito:add-test` only for their narrow requests; they bypass this flow and do not update `docs/`.

### grunt tasks

Use these only for narrow requests. They skip the mode pipeline.

#### typo

- command: `/cito:typo`
- when: fix a typo or wording mistake, text only
- agent: `cito-typo`

#### comment

- command: `/cito:comment`
- when: add or improve a WHY-comment, no logic change
- agent: `cito-comment`

#### add-test

- command: `/cito:add-test`
- when: add a test for one file, matching existing convention
- agent: `cito-add-test`

### setup

Setup runs right after cito-prompts is installed, and again when stack, commands, or structure drift.

#### setup-project

- command: `/cito:setup-project`
- when: fill the FILL sections of both instruction copies
- agent: `cito-setup-project`

## rules

<!-- FILL: hard project constraints. include reason so agent handles edge cases. -->
<!--
- no new dependencies without approval (keeps bundle size controlled)
- all public functions need JSDoc (API surface is consumed externally)
- no direct db queries outside src/lib/db (single point for query logic)
-->

- Do not add dependencies. Raise that in the design doc.

## avoid

<!-- FILL: known bad patterns or footguns specific to this project. -->
<!--
- do not use Date(), use dayjs (timezone handling)
- do not put business logic in route handlers (testability)
- do not import from @internal packages in public modules
-->
```

### `.github/copilot-instructions.md`

```md
# [Project Name]

<!--
   cito-prompts v0.64.0 — .github/copilot-instructions.md
   - GitHub Copilot copy of the project instructions.
   - GitHub Copilot reads this path automatically.
   - Claude Code uses `.claude/CLAUDE.md`.
   - Keep both copies in sync when project facts change.
   - `cito-setup-project` refreshes both.
   - AGENTS.md at repo root points here for other tools.
   - Cito modes are provided by the installed `cito` plugin.
   - No skill files. Fill FILL sections. Delete examples after filling.
-->

## identity

<!-- FILL: one sentence. what this project is, who it serves. -->

## stack

<!-- FILL: tech, versions, key libs. example below. delete example after filling. -->
<!--
- lang: TypeScript 5.7 strict
- framework: No framework, plain Express
- styles: Vanilla CSS
- db: sqlite
- runtime: Node 24, pnpm
-->

## package manager

<!-- FILL: match the real tool and update the matching line in **avoid**. If the project is not JS or TS, replace or drop the section. -->

<!-- - This project uses **pnpm**.
- Use `pnpm` for package and script commands.
- Do not use `npm` or `npx`. -->

## commands

<!-- FILL: every command the agent might need. most valuable section. -->
<!--
- install: `pnpm install`
- dev: `pnpm dev`
- build: `pnpm build`
- test all: `pnpm test`
- test one: `pnpm test -- path/to/file`
- lint: `pnpm lint`
- typecheck: `pnpm tsc --noEmit`
- format: `pnpm format`
- e2e: `pnpm exec playwright test`
-->

## browser verification

<!-- FILL: keep only for projects with a UI and browser test setup. Match the configured browser tool. -->

<!-- - Use Playwright for visible behavior: UI, navigation, rendered output, screenshots, and bug repros.
- run: `pnpm exec playwright test`
- run one: `pnpm exec playwright test path/to/spec.ts`
- browsers missing: `pnpm exec playwright install`
- headed debug: `pnpm exec playwright test --headed`
- Claude may use an MCP browser tool if one is configured.
- Do not claim UI behavior works without checking it. -->

## structure

<!-- FILL: key dirs only. skip obvious ones (node_modules, .git). -->
<!--
- src/app/ — routes and pages
- src/components/ — shared UI
- src/lib/ — utils, db client, helpers
- src/types/ — shared type defs
- docs/ — durable docs, written only by `doc`
- work/ — transient planning docs and task lists
- tests/ — test files mirror src/
-->

## kinds of artifacts

- Work doc: `work/[name].md` describes the intended change. It is a transient work artifact and the source for a task list.
- Doc: `docs/[name].md` captures current reality for a topic. It is the durable source of truth for current behavior; only `doc` creates or updates it.
- Task list: `work/tasks/[name].md` links to one work doc or doc and breaks it into small, committable, trackable tasks. It is a transient work artifact and the implementation contract for `do`; check off tasks only after their acceptance criteria are met.

## conventions

<!-- FILL: non-obvious patterns only. skip what linters enforce. -->
<!--
- named exports, no default exports
- colocate tests next to source
- errors as values, not exceptions
- no abbreviations in public APIs
-->

## voice

- Use short, direct prose.
- Drop filler and throat-clearing.
- Keep technical details exact.
- Do not say "I'll", "Sure!", "Great question", "Let me", or "Of course".
- Do not restate the user's request before answering.
- Do not add closing summaries.
- Keep code, paths, and identifiers exact.
- If explanation is needed, use fact → reason → fix.
- Bad: "The reason your component re-renders is because you're creating a new object reference on each render cycle."
- Good: "New object ref each render. Inline object prop = new ref = re-render. Wrap in `useMemo`."

## workflow

The user names the mode. Use the installed `cito` plugin agent for that mode.

### modes

#### design

- when: translate an intention into a work doc
- agent: `cito-design`

#### do

- when: execute one unblocked task from a task list
- agent: `cito-do`

#### doc

- when: capture current state as a durable doc
- agent: `cito-doc`

#### create-tasklist

- when: turn a work doc or doc into a committable, trackable work task list
- agent: `cito-create-tasklist`

#### validate-doc

- when: compare a document with the implementation and report material deltas
- agent: `cito-validate-doc`

#### oppose-dissertation

- when: constructively challenge a design or other document for meaningful gaps and risks
- agent: `cito-oppose-dissertation`

#### investigate

- when: trace a reported issue from observable facts to a root cause or next check
- agent: `cito-investigate`

### shared rules

- Only `doc` creates or updates files in `docs/`.
- The work task list is the contract for `do`; its `Source` link is the supporting work doc or doc.
- A doc is ground truth for current state.
- A work task list with a valid source link must exist before `do` starts.
- If the source document and current code conflict, stop and resolve the conflict before coding.
- Do not invent scope beyond the selected task or its source document.
- Do not add dependencies. Raise that as an open question.
- Do not change public APIs unless the source document says to.

### process flow

For a proposed change, use `cito-design` to create `work/[name].md`, then `cito-create-tasklist work/[name].md` to create `work/tasks/[name].md`, then `cito-do work/tasks/[name].md` to execute the next unblocked task. For work that starts by documenting existing behavior, use `cito-doc` to create `docs/[name].md`, then `cito-create-tasklist docs/[name].md` to create `work/tasks/[name].md`, then `cito-do work/tasks/[name].md`. Use `cito-typo`, `cito-comment`, or `cito-add-test` only for their narrow requests; they bypass this flow and do not update `docs/`.

### grunt tasks

Use these only for narrow requests. They skip the mode pipeline.

#### typo

- when: fix a typo or wording mistake, text only
- agent: `cito-typo`

#### comment

- when: add or improve a WHY-comment, no logic change
- agent: `cito-comment`

#### add-test

- when: add a test for one file, matching existing convention
- agent: `cito-add-test`

### setup

Setup runs right after cito-prompts is installed, and again when stack, commands, or structure drift.

#### setup-project

- when: fill the FILL sections of both instruction copies
- agent: `cito-setup-project`

## rules

<!-- FILL: hard project constraints. include reason so agent handles edge cases. -->
<!--
- no new dependencies without approval (keeps bundle size controlled)
- all public functions need JSDoc (API surface is consumed externally)
- no direct db queries outside src/lib/db (single point for query logic)
-->

- Do not add dependencies. Raise that in the design doc.

## avoid

<!-- FILL: known bad patterns or footguns specific to this project. -->
<!--
- do not use Date(), use dayjs (timezone handling)
- do not put business logic in route handlers (testability)
- do not import from @internal packages in public modules
-->
```

## procedure

1. Read both target files in full when they exist. If either is missing, create it from the matching complete template above. Treat `<!-- FILL: ... -->` markers as instructions and the commented blocks under them as examples.
2. Inspect repo evidence before writing:
   - manifests and lockfiles (`package.json`, `pnpm-lock.yaml`, `package-lock.json`, `yarn.lock`, `bun.lockb`, `pyproject.toml`, `uv.lock`, `Cargo.toml`, `go.mod`, `Gemfile`, ...)
   - config for language, build, lint, format, and test (`tsconfig.json`, `vite.config.*`, `eslint.*`, `biome.json`, `ruff.toml`, `Makefile`, `justfile`, CI workflows in `.github/workflows/`)
   - top-level source layout plus `README.md`, `docs/`, and `work/`
   - a few real source files to confirm conventions
3. Fill each section in both files from evidence:
   - **identity** — one sentence on what the project is and who it serves. Ask if the repo does not say.
   - **stack** — languages with versions, framework, styling, data layer, and runtime. Use versions from manifests or lockfiles.
   - **package manager** — match the real tool and update the matching line in **avoid**. If the project is not JS or TS, replace or drop the section.
   - **commands** — install, dev, build, test all, test one, lint, typecheck, format, and e2e. Keep only real commands.
   - **browser verification** — keep only for projects with a UI and browser test setup. Match the configured browser tool.
   - **structure** — key directories and roles.
   - **conventions** — non-obvious patterns from real code.
   - **rules** — hard constraints with reasons.
   - **avoid** — real footguns. Keep it thin.
4. Replace `# [Project Name]` in both files with the real project name.
5. Delete every `<!-- FILL: ... -->` marker and every example block you filled.
6. If evidence is missing, leave the section open and note the question.
7. Verify:
   - run the commands you wrote for install, typecheck, lint, and test when they exist
   - compare the shared project facts in both files: identity, stack, commands, structure, conventions, rules, and avoid
   - allow the documented client-specific template differences, including banner text, mode paths and commands, and sections that one template marks as conditional
8. Report what you filled, what stayed open, and any command failures.

## boundaries

- Setup only. Do not implement features, refactor, or fix bugs.
- Do not edit `AGENTS.md`, the root `CLAUDE.md`, or any `cito-*.md` agent file. Those ship with cito-prompts.
- No work doc.
- No `docs/` update.
- Re-running is fine. Refresh stale facts. Keep valid hand-written additions.
