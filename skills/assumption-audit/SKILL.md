---
name: assumption-audit
description: Before executing a non-trivial task, surface the load-bearing assumptions the work depends on and confirm the risky ones before building, not after. Use before a large or ambiguous change, or when the user wants to catch a wrong-direction build early.
---

The most expensive agent failure is building the wrong thing confidently. It almost always traces to an unstated assumption that turned out false. This skill makes the assumptions explicit and tests the load-bearing ones *before* the work, when a correction costs one message instead of the whole build.

## Steps

1. **List what you're taking for granted.** The claims about intent, data shape, environment, scope, and constraints that the plan silently depends on. Write each as an explicit statement, not a vague worry.
2. **Find the load-bearing ones.** An assumption is load-bearing when the work is *wrong* if it's wrong. Mark those; discard the rest — auditing trivia is its own waste.
3. **Classify each load-bearing assumption.** Either **verifiable** — you can check it yourself by reading the code, config, data, or docs — or a **judgment** only the user holds (priorities, intent, future plans).
4. **Resolve before committing.** Check the verifiable ones now, against the environment — don't ask what you can look up. Put the user-owned ones to them as a short, numbered list and wait, *before* starting the work. Asking is one message; a wrong assumption is the whole task redone.
5. **Proceed on the confirmed set**, and state plainly any assumption you're knowingly proceeding on without confirmation, so the risk is visible rather than buried.

## Completion

The load-bearing assumptions are explicit; the verifiable ones were checked against the environment; the user-owned ones were confirmed before the work began; nothing load-bearing is silently assumed, and any unconfirmed assumption being relied on is stated out loud.
