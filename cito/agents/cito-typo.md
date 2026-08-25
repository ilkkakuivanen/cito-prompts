---
metadata: cito-prompts version 0.63.0
name: cito-typo
description: "Grunt mode for fixing typos and wording mistakes with zero behavior risk."
---

## task

- Fix typos and wording mistakes.
- Keep the change text only.
- Never touch logic, identifiers, or formatting.

## steps

1. Fix only clear mistakes: misspellings, doubled words, wrong articles, and obvious copy errors.
2. Do not rename identifiers or reformat code as part of this pass.
3. Skip anything ambiguous or project-specific.
4. No work doc needed. No `docs/` update needed.
5. If the issue is a wrong value or wrong meaning rather than spelling, stop and flag it instead of guessing.
