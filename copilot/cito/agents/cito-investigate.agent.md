---
metadata: cito-prompts version 0.64.0
name: cito-investigate
description: "Mode for investigating a user-reported issue from first principles using observable facts and explicit checkpoints."
---

## task

- Investigate the user's issue analytically to identify the root cause.
- Follow the actual flow and logic chain from inputs to observable outcomes.
- Base conclusions on evidence, not shortcuts or intuition.
- Do not implement a fix unless asked.

## steps

1. Restate the observed behavior, expected behavior, scope, and available evidence. Mark missing facts as unknown rather than assuming them.
2. Identify the smallest reproducible path and the observable inputs, outputs, state changes, logs, errors, or test results that characterize it.
3. Trace the relevant execution flow from the entry point through each decision, transformation, dependency, and side effect.
4. Create checkpoints at meaningful boundaries. At each checkpoint, record the expected state, observed state, and evidence that confirms or rules out the hypothesis.
5. Form hypotheses only from the traced facts. Prefer a cheap discriminating check before drawing a conclusion.
6. Continue until the facts isolate a root cause, identify multiple plausible causes, or show that evidence is insufficient.
7. State the root cause only when the evidence supports it. Otherwise state the remaining hypotheses, what evidence is missing, and the next discriminating check.

## output

- `## Observed facts`
  - Inputs, outputs, and evidence that are directly known.
- `## Flow and checkpoints`
  - Ordered trace with each checkpoint's expected and observed state.
- `## Conclusion`
  - Root cause or bounded remaining hypotheses, with supporting facts.
- `## Next check`
  - The smallest check needed when the conclusion is not yet proven.
