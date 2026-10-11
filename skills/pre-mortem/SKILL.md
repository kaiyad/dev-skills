---
name: pre-mortem
description: Before building something risky, assume it has already failed in production and work backward to the guardrails that prevent it. Use before a risky launch, migration, or architectural bet, or when the user wants failure modes surfaced early while they're still cheap to fix.
---

Catch the failure while it's still hypothetical and cheap. The move is a deliberate inversion: don't ask "what could go wrong" — stand in a future where it *has* gone wrong and explain how. That framing surfaces failure modes the forward question never reaches.

## Steps

1. **Jump to the failure.** State it as fact: "it's three months later and this blew up." Make it vivid and specific — the concrete scene unlocks honest failure modes that a sanitized "what are the risks" conversation politely avoids.
2. **Enumerate the paths, broad first.** List the distinct ways it failed across every axis: **technical** (load, data corruption, a dependency outage), **product** (nobody used it, it solved the wrong problem), **operational** (couldn't debug it, couldn't roll it back). Don't stop at the first obvious one — breadth is the point.
3. **Rank by likelihood × blast radius.** Push the cheap-and-harmless to the bottom; raise the plausible-and-catastrophic to the top. You act on the top of the list, not all of it.
4. **Convert each top risk into a guardrail.** A test, an alert (hand to `observe`), a feature flag, a rate limit, a rollback plan, a scope cut, or a decision not to build it. A named risk with no guardrail is just anxiety on a slide.
5. **Decide and record.** Separate must-have-before-launch from monitor-after, and write the decision down so it survives the enthusiasm of launch day.

## Completion

The plausible high-impact failure modes are enumerated across technical, product, and operational axes and ranked; each top risk has a concrete guardrail or an explicit, recorded decision to accept it; must-have-before-launch is separated from monitor-after.
