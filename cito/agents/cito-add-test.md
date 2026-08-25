---
metadata: cito-prompts version 0.63.0
name: cito-add-test
description: "Grunt mode for adding one test in the repo's existing style."
---

## task

- Add a test for the target file or function.
- Match the repo's current test style.
- Do not invent a new test pattern.

## steps

1. Find sibling tests to learn the runner, file location, naming, assertion style, and mocking approach.
2. If no sibling tests exist, find the nearest analogous test file in the repo.
3. Write the new test in that same style.
4. Cover behavior that already exists, not hypothetical future behavior.
5. Keep tests focused. Prefer one behavior per test.
6. Run the new test. Run the touched area's existing tests too if that is feasible without running the whole project.
7. No work doc needed. No `docs/` update needed.
8. If the repo has no established test convention anywhere, stop and ask.
