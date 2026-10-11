---
name: prototype
description: Build a throwaway POC, spike, or demo to answer one question fast — polish and robustness traded deliberately for speed. Use when the user wants to sanity-check an approach, validate a library, explore a UI, or produce a POC or demo, and the code is not meant to ship.
---

A prototype exists to answer a question, not to become the product. Its value is the answer and the learning; the code is disposable. Treating it as production is the one way to waste it.

## Steps

1. **Name the question.** Write, in one sentence, the single thing this prototype must settle — "does this state model handle concurrent edits", "is this library fast enough", "does this flow feel right". Everything the prototype does serves that question; everything else is cut.
2. **Cut ruthlessly, on purpose.** Hardcode values, skip error handling, mock the boundaries, ignore edge cases. The shortcuts *are* the method — but name them, so no one mistakes the prototype for a finished thing.
3. **Quarantine it.** Keep it in a scratch directory, a throwaway branch, or a notebook — isolated so disposable code can't leak into the real codebase and quietly become load-bearing.
4. **Get to the answer fast.** Run it, observe, iterate. The moment the question is answered, stop — a prototype polished past its answer is wasted effort.
5. **Report the learning.** State what the prototype proved and didn't, and what a production version would actually need (the error handling, edges, and tests you deliberately skipped). The output is a decision, not a deliverable.

## Completion

The named question is answered with running evidence; the throwaway code is isolated from the real codebase; the report names what was proven and what production would still require. If it turns out to be worth keeping, it gets rebuilt properly — the prototype is not promoted.
