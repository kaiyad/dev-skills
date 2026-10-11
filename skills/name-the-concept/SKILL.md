---
name: name-the-concept
description: Given a problem the user describes, identify the standard technical concept or pattern behind it, explain what that concept is, map it onto their problem, and show how to apply it. Use when the user has a problem and wants to know the established concept, pattern, or term that addresses it.
---

Connect a concrete problem to the named, established concept the field already has for it — so the user gains the canonical term to search, the theory behind it, and a concrete way to apply it. The point is to hand them a lever, not a definition.

## Steps

1. **Strip to the shape.** Restate the problem as its structural core, with the domain specifics removed. "I keep recomputing the same result" is *memoization/caching*; "requests spike and overwhelm the service" is *backpressure / rate limiting / queueing*; "two writers clobber each other" is *concurrency control*. The shape points at the concept.
2. **Name it canonically.** Give the established concept with the exact term the field uses, so the user can search it and read further. If more than one fits, name the closest and list the alternatives with the condition that selects each.
3. **Explain the concept itself.** Briefly and from the ground up: what it is, and the problem it was invented to solve — the ELI5 rules in `../../references/explain-visually.md` apply. Ground it before mapping it.
4. **Map it onto their problem.** Draw the correspondence explicitly: *this* part of your problem is the thing the concept calls X. Say where the fit is tight and where it isn't — a concept applied past its fit is a new bug.
5. **Show how to apply it.** The concrete move in their situation, the standard tool/library/pattern that implements it in their stack, and the one gotcha that bites people. A small diagram or example where it earns its place (`explain-visually.md`).
6. **Point onward.** The canonical name to search and one high-trust primary source to go deeper.

## Completion

The standard concept is named with the term the field actually uses; the concept is explained from the ground up; the mapping onto the user's problem is explicit about where it fits and where it doesn't; the application is a concrete next move with the real tool named — not just a definition.
