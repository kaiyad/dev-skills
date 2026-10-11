---
name: calibrate
description: Derive this repo's real conventions, design patterns, and review priorities from its own code, and write them into the references so every other skill follows the team's actual standard. Use when setting these skills up in a new repo, or refreshing the standard after the codebase has drifted.
---

Make the skill library a mirror of this team's best code, not a set of imported opinions. This reads the repo and rewrites `../../references/python-conventions.md`, `../../references/design-principles.md`, and `../../references/review-rubric.md` to match what the code actually does — so `implement`, `review`, `refactor`, and `test` inherit the real standard automatically.

## Steps

1. **Sample what's load-bearing.** Delegate a broad read (use `explore` / a subagent) across a representative slice — the core modules, the most-changed files, the test suite, and the tooling config (`pyproject.toml`/CI). Read what carries weight, not every file.
2. **Infer, don't impose.** Extract the patterns the code *actually* follows: error-handling style, typing discipline, module and seam boundaries, naming, test idioms, the tool stack. The standard comes from the code; your defaults are only the fallback where the code is silent.
3. **Separate convention from accident.** A pattern repeated across modules by different authors is a convention — promote it. A one-off is noise — leave it out. Where the dominant pattern has exceptions, record both.
4. **Write the references with citations.** Update the three reference files to describe the repo's real conventions, each anchored to a real `file:line` example so the standard is grounded and auditable, not asserted.
5. **Surface the tensions.** Where the codebase contradicts itself, or a dominant pattern looks like tech debt, list it for a human to rule on rather than silently canonizing it as "the standard."

## Completion

The three references describe the repo's real, dominant conventions with cited `file:line` examples; contradictions and suspected debt are surfaced for a decision, not hidden; the other skills now measure against this repo's standard instead of generic defaults. Re-run after a major change so the standard tracks reality instead of rotting.
