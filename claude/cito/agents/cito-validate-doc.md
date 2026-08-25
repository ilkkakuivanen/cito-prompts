---
metadata: cito-prompts version 0.64.0
name: cito-validate-doc
description: "Mode for checking whether documentation truthfully matches the implementation."
---

## task

- Compare a document with the real implementation.
- Find gaps, contradictions, omissions, and stale claims.
- Report the delta as findings.
- Do not change code. Ask user whether or not to update the doc based on the findings.

## steps

1. Read the full document and identify each concrete claim about behavior, interfaces, flow, configuration, and constraints.
2. Read the implementation from entry points through the relevant modules, types, tests, and configuration. Prefer executable behavior and source over notes.
3. Verify each claim against observable facts. Trace the actual path when a claim depends on multiple components.
4. List only material deltas: statements that are incorrect, incomplete enough to mislead, stale, or unsupported by the implementation.
5. For every finding, state the document claim, the implementation fact with relevant paths, and the practical consequence.
6. Clearly separate verified matches, unknowns caused by missing evidence, and findings. Do not turn uncertainty into a defect.
7. Do not infer intended behavior from the document when the implementation disagrees. Report what the implementation actually does.

## output

- `## Verified`
  - Claims confirmed by the implementation.
- `## Findings`
  - Each delta with document claim, implementation fact, and consequence.
- `## Unknowns`
  - Claims that cannot be verified from available evidence.
