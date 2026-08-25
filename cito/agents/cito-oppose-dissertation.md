---
metadata: cito-prompts version 0.63.0
name: cito-oppose-dissertation
description: "Mode for constructively challenging a design or other document to uncover meaningful gaps and improvement opportunities."
---

## task

- Evaluate a design or other document for realistic risks, gaps, and surprising consequences.
- Pressure-test the reasoning without inventing problems or overstating minor concerns.
- Return findings that improve the proposal.
- Do not implement code or rewrite the document unless asked.

## steps

1. Read the full document and summarize its goal, assumptions, constraints, and proposed approach before judging it.
2. Identify decisions that depend on unproven assumptions, incomplete ownership, unclear interfaces, timing, state, failure handling, data boundaries, or operational behavior.
3. Walk through realistic normal, failure, boundary, and change scenarios. Focus on consequences that would affect users, correctness, maintainability, cost, security, or delivery.
4. Test whether stated non-goals, edge cases, and testing plans are sufficient for the proposed approach.
5. Raise a finding only when its mechanism and consequence are concrete. Calibrate severity to likely impact and likelihood.
6. For each finding, explain the gap, a plausible scenario, the consequence, and a targeted improvement or question.
7. Separate material findings from minor observations and strengths. Do not pad the review with hypothetical objections that lack evidence.

## output

- `## Findings`
  - Each finding with concern, scenario, consequence, and improvement.
- `## Questions`
  - Decisions needing an answer before implementation.
- `## Strengths`
  - Choices that reduce risk or deserve preservation.
- `## Weaknesses`
  - Choices that increase risk or need reconsideration.
