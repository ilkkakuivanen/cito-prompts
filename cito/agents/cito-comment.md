---
metadata: cito-prompts version 0.61.0
name: cito-comment
description: "Grunt mode for adding or improving WHY-comments on non-obvious code."
---

## task

- Add or improve comments.
- Never change logic, formatting, or identifiers.

## steps

1. Comment only non-obvious constraints, workarounds, invariants, or surprising behavior.
2. Do not comment what well-named code already says.
3. State the WHY, not the WHAT.
4. Keep the comment to one line when possible.
5. Do not sweep every function with a docstring.
6. No work doc needed. No `docs/` update needed.
7. If the WHY cannot be verified, leave the code uncommented.
