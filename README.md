# dev-skills

A small, composable set of software-development skills for AI coding agents. Python-oriented, but the shape transfers to any stack. Built to reduce *variance* — so every engineer's agent follows the same process — not to automate thinking away.

## The one principle that shapes everything here

**A skill guides; it does not enforce.** An agent can ignore or fail to trigger a skill. So the division of labor is:

| Layer | Mechanism | Holds | Enforced by |
|---|---|---|---|
| Invariants (must always hold) | **CI + git/pre-commit hooks** | tests pass, types, lint, no secrets, branch protection | machine — a hard gate |
| Always-on facts | **`CLAUDE.md` / `AGENTS.md`** | stack, package manager, layout, conventions | loaded every turn |
| Triggered processes | **these skills** | how we design, review, debug, ship | agent — advisory |
| Per-feature intent | **specs / tickets** | what to build, acceptance criteria | humans |
| Shared tools & data | **MCP servers** | issue tracker, internal APIs, docs | infra |

Put anything mandatory in CI, not in a skill. These skills cover the judgment-heavy process CI can't check.

## Why it's organized this way (context budgeting)

- **13 skills, not 40.** Each one earns its place. A sprawling library over-triggers, collides on descriptions, and burns context. Prune first; add only when a real inconsistency demands it.
- **Descriptions are trigger-first and lean.** A skill's description is loaded *every turn* whether it fires or not, so it states the trigger up front and carries no filler.
- **Shared knowledge lives once, in `references/`.** The Python standard, the design vocabulary, and the review rubric are each a single source of truth, loaded on demand by the skills that point to them — never duplicated across skill bodies. Change a convention in one place.
- **Bodies load only when a skill fires** (progressive disclosure), so the standing cost is just the descriptions.

## Skills

**Define & design**
- `spec` — request → spec with testable acceptance criteria (the contract).
- `shape-design` — frame forces, survey proven patterns, lay out real alternatives with tradeoffs, recommend one, record it.

**Build**
- `implement` — write idiomatic Python to the standard; reuse first, minimal change, verified.
- `test` — test-first (red-green-refactor) and characterization tests; pin behavior, not implementation.
- `refactor` — change shape without changing behavior, one green step at a time.
- `prototype` — a throwaway POC/spike/demo to answer one question fast.

**Verify & ship**
- `review` — six-axis diff review (correctness, design, spec, quality, security, tests) with a fix for every finding.
- `debug` — reproduce → isolate to a named mechanism → confirm → guard with a regression test.
- `pr` — a PR body a reviewer can act on.
- `incident` — production response: stabilize → preserve evidence → diagnose → prevent.

**Understand & carry**
- `explore` — map an unfamiliar codebase without pulling it all into context.
- `document` — READMEs, API docs, ADRs, runbooks, design docs that stay true.
- `handoff` — compact a session so another agent can resume cold.

**Learn & explain**
- `explain-doc` — read a doc/Confluence/article/PDF/link and explain it from zero context, ELI5, with a visual.
- `name-the-concept` — given a problem, name the standard concept behind it, map it to the problem, show how to apply it.
- `explain-term` — explain a technical term from zero, with a visual, a worked example, and a contrasting non-example.

## References (loaded on demand)

- `references/python-conventions.md` — the elegant Python standard + the "name the alternatives" habit.
- `references/design-principles.md` — deep modules, seams, the pattern catalog, the alternatives format.
- `references/review-rubric.md` — the six review axes and the finding format.
- `references/explain-visually.md` — the ELI5 writing rules and how to pick/draw the right visual.

## How they compose

A typical feature flows:

```
spec → shape-design → implement ⇄ test → review → pr
```

with `debug`, `refactor`, `prototype`, `explore`, `document`, `handoff`, and `incident` pulled in as the situation calls. Skills point at each other and at the shared references rather than repeating content.

## Install

**As a Claude Code plugin** (updates as a unit): add this folder to a marketplace, or symlink `skills/*` into `.claude/skills/`.

**Copied into a repo** (team-shared, PR-reviewed — recommended for teams): copy `skills/` and `references/` into the project and commit them, so the whole team's agents run the same version and changes go through code review. Keep the paths relative so the cross-references resolve.

## Adapt it to your team

- Swap `python-conventions.md` for your stack's standard — the skills reference it by path, so they follow automatically.
- Tune the `review-rubric.md` axes to what your team actually cares about.
- Give one person ownership and a delete-first habit, or it will rot.
- Move your non-negotiables into CI and hooks. These skills make the agent *want* to do the right thing; CI makes sure it *did*.
