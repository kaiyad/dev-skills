---
name: spec
description: Turn a request or conversation into a spec with testable acceptance criteria before any code. Use when the user wants to define, scope, or write up what to build, or when a task is too fuzzy to implement or review against directly.
---

A spec is the **contract** that `implement` builds to and `review` measures against. Write it so "done" is a fact anyone can check, not an opinion.

## Steps

1. **Capture the goal as an outcome.** State the problem and the user behind it, and the result that would solve it — not a solution. "Users can recover a deleted draft within 30 days" is a goal; "add a `restore()` method" is a guess at the solution.
2. **Write testable acceptance criteria.** List the observable conditions that make it done, each one a thing a test could assert. If a criterion can't be checked without someone's judgment, sharpen it until it can.
3. **Draw the scope boundary.** State explicitly what's in, what's out, and what's deferred to later. The out-of-scope list prevents scope creep in implementation and endless argument in review.
4. **Surface the unknowns.** Where you can't answer something, write it as an open question rather than quietly assuming. Resolve the *blocking* unknowns with the user before any code starts; the non-blocking ones can be noted and carried.
5. **Keep it short.** A spec is the smallest contract that pins the behavior — not a design doc (that's `shape-design`) and not an essay. If it's deciding *how*, it's drifted out of scope.

## Completion

Every acceptance criterion is observable and testable; in-scope and out-of-scope are explicit; no blocking unknown is left silently assumed. The spec could be handed to someone who wasn't in the conversation and they'd build the right thing.
