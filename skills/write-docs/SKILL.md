---
name: document
description: Write documentation that stays true — READMEs, module/API docs, ADRs, runbooks, design docs — pitched at its reader and limited to what won't rot. Use when asked to document, write a README/ADR/runbook, or explain a system in prose for others.
---

Documentation earns its keep only when a reader can act on it and it's still true. Write for one named reader, and cache only what they can't get by looking at the code.

## Steps

1. **Pick the type and its reader — they decide everything:**
   - **README** → first-time user: what it is, why it exists, the quickstart that works.
   - **API / module doc** → the caller: the contract (inputs, outputs, errors, guarantees), not the internals.
   - **ADR** → the future maintainer: the decision, the forces behind it, the alternatives considered, and the consequence. (Format in `../../references/design-principles.md`.)
   - **Runbook** → on-call at 3am: numbered steps, exact commands, how to tell it worked, who to escalate to.
   - **Design doc** → the reviewer: forces, approach, alternatives, tradeoffs (pairs with `shape-design`).
2. **Cache only the non-obvious.** Write down the *why*, the gotcha, the convention no config states. Don't restate what the code, signatures, or config already say — that duplicate goes stale the moment the code changes and becomes a lie.
3. **Show, don't assert.** A runnable example or a real command beats a paragraph of description. Verify every command and snippet actually runs.
4. **Fit the repo.** Match where existing docs live and how they're styled; one more doc in the house style beats a lone masterpiece nobody finds.

## Completion

The named reader can act without reading the source; every claim and example is current and runs; the doc records the non-obvious *why*, not a copy of the code. It lives where that kind of doc belongs in this repo.
