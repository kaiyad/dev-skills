---
name: explore
description: Build an accurate mental map of an unfamiliar codebase or module fast, without pulling every file into context. Use when onboarding, asked how something works or where something lives, or before changing code you don't yet understand.
---

Understand the system well enough to change it safely, while keeping the bulk of the reading *out* of the working context. The deliverable is a map, not a pile of files.

## Steps

1. **Start from the edges.** Entry points, public interfaces, the config, and the tests state intent more cheaply than the implementation does. The test suite is the cheapest spec of how the system is meant to behave — read it early.
2. **Delegate the broad reading.** Send the wide, exploratory reading to a subagent or search and pull back only the findings — the map — not the raw files. Stale file dumps in the main context are charged on every later turn; the summary isn't.
3. **Trace one real path end to end.** Follow a single request, command, or data flow from entry to effect, rather than reading breadth-first. One complete trace teaches the architecture faster than ten partial skims.
4. **Name the seams.** Identify the module boundaries, the core data model, and where behavior changes — i.e. where a given change would actually go. That's the map worth keeping.

## Completion

You can state the main components, how data flows between them, and where a specific change belongs — each claim anchored with a `file:line`. The context holds the map, not the whole codebase.
