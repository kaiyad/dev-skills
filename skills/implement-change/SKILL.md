---
name: implement
description: Write Python to an elegant, idiomatic standard — reuse what exists, pick the cleanest construct, keep the change minimal, and verify it. Use when implementing a feature, function, or module from a spec, plan, or clear request.
---

Turn a decided design into code that reads like the rest of the codebase wrote it. Follow `../../references/python-conventions.md` for the standard. If the approach isn't decided yet, stop and run `shape-design` first.

## Steps

1. **Orient.** Read the target file and its neighbors. Match their imports, naming, error handling, and structure before adding anything. Search for an existing utility before writing one; search for an existing dependency before adding one.
2. **Choose, don't drift.** When a non-trivial construct is in play — data shape, library vs stdlib, sync vs async, where the seam goes — name the options in a line and take the cleanest that fits *this* codebase (the conventions file lists the common forks and their heuristics). Don't silently commit to the first thing that compiles.
3. **Write to the standard.** Precise types on the public surface, specific exceptions, small pure functions, deep modules. Idiomatic Python, not translated-from-another-language Python.
4. **Hold the scope.** Make the smallest change that satisfies the spec. Don't refactor code the task doesn't require — note it and move on. One logical change at a time; never bundle a rename or a refactor into a behavior change.
5. **Verify.** While iterating, run the single test covering the change. Before calling it done, run the project's real lint, typecheck, and test commands (find them in `pyproject.toml`/`Makefile`/CI — don't guess). Report each command and its result.

## Completion

The change meets the spec, follows the conventions and the surrounding style, and the project's lint, types, and tests are green — stated with the commands you ran. Never say a test passed unless you ran it and read the output; if something couldn't be verified, say so plainly.
