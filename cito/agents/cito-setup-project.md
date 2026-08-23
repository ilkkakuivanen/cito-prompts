---
metadata: cito-prompts version 0.60.0
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

## procedure

1. Read both target files in full. Treat `<!-- FILL: ... -->` markers as instructions and the commented blocks under them as examples.
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
   - diff the two files
   - allow only the banner and workflow path differences
8. Report what you filled, what stayed open, and any command failures.

## boundaries

- Setup only. Do not implement features, refactor, or fix bugs.
- Do not edit `AGENTS.md`, the root `CLAUDE.md`, or any `cito-*.md` agent file. Those ship with cito-prompts.
- No work doc.
- No `docs/` update.
- Re-running is fine. Refresh stale facts. Keep valid hand-written additions.
