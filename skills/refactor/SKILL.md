---
name: refactor
description: Improve structure without changing behavior — establish a test net, make one mechanical move at a time, stay green throughout. Use when asked to refactor, clean up, simplify, or restructure, or to extract, rename, inline, or move code without adding features.
---

Change the shape, never the behavior, in steps small enough that the tests prove you didn't break anything. Steer toward `../../references/design-principles.md` (deeper modules, clearer seams) and `../../references/python-conventions.md`.

## Steps

1. **Net first.** Confirm tests cover the behavior you're about to move. If the code is untested, write characterization tests before you touch it (hand to the `test` skill). Refactoring without a net is rewriting — a different, riskier activity.
2. **Map the blast radius.** Find everything that depends on what you're changing before you change it, so a rename or a moved seam doesn't break a caller you didn't know about.
3. **One move at a time.** Each step is a single reversible transformation — rename, extract function/class, inline, move, change signature. Run the suite after each. It stays green the whole way; if it goes red, you've changed behavior — back out and reconsider.
4. **Never smuggle.** Do not mix a behavior change into a refactor commit. If you discover a bug mid-refactor, note it and fix it separately so the diff stays honest and the review stays cheap.
5. **Name the target.** State which principle each move serves — a deeper module, a seam at a stabler boundary, duplication collapsed to one source of truth — so the change is justified, not just rearranged.

## Completion

Behavior is provably identical (suite green at every step); the structure is measurably better against a named principle; no feature change or bug fix rode along in the diff.
