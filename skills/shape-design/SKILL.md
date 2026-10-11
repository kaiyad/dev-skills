---
name: shape-design
description: Design a feature or module before coding — frame the forces, survey the proven approaches, lay out real alternatives with tradeoffs, recommend one, and record it. Use when the user wants to design, architect, or decide the approach for something non-trivial, or asks how they should build it.
---

Design the approach before a line of code, so the implementation inherits a decision instead of improvising one. Read `../../references/design-principles.md` — it carries the deep-module vocabulary, the pattern catalog, and the alternatives format this skill drives toward.

## Steps

1. **Frame the forces.** Restate the problem as the constraints the solution must satisfy — load, change rate, failure modes, the team's skills, what must stay simple — not as a solution in disguise. Read the surrounding code first so the design fits the grain of what exists.
2. **Survey.** Name the established, boring patterns that fit these forces before inventing anything (pattern catalog in the reference). A new teammate recognizing the shape is worth more than cleverness.
3. **Branch.** Put up **2–3 real alternatives**, each one a competent engineer would defend. For each: what it is, what it optimizes, what it costs, when it wins. No strawman standing next to the favorite.
4. **Resolve the open decisions.** Where a choice depends on something only the user knows (priorities, future plans, constraints), ask — one numbered round of questions, each with your recommended answer, worded so "yes" accepts it. Find *facts* yourself (read the code, the config); put only *decisions* to the user.
5. **Recommend.** Pick one approach, justified in terms of the framed forces, and name the **reversal condition** — the fact that would flip the choice.
6. **Record.** Capture the decision as a short design doc or ADR (hand to the `document` skill): forces, alternatives considered, choice, consequence. A design nobody can find was never made.

## Completion

Every framed force is answered by the recommendation; every alternative was a genuine contender; the choice is recorded with the condition that would reverse it. Do not start implementing until the user confirms the shape.
