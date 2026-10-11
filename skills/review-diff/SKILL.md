---
name: review
description: Review a diff across every axis an engineer would — correctness, design, business/spec fit, quality, security, and tests — with a concrete fix or better alternative for each finding. Use when asked to review, critique, or approve a branch, PR, or working changes.
---

Review the change the way a senior engineer reviews a colleague: not just "is it wrong" but "is this the right shape, and what's the better move." Apply `../../references/review-rubric.md` in full — it holds the six axes, their checks, and the finding format.

## Steps

1. **Fix the scope.** Review the diff since a stated point (branch, merge-base, tag, or commit). Establish the originating spec/issue so you can judge intent, not just code.
2. **Read in context.** Assess each changed file against its neighbors and the repo's conventions (`../../references/python-conventions.md`), not in isolation. A line that's fine alone can be wrong for this codebase.
3. **Run the axes.** Apply all six rubric axes to every changed file. For a large diff, dispatch each axis to its own subagent and merge the reports. Don't let a loud correctness bug crowd out the design and security passes.
4. **Make every finding actionable.** Each one carries a concrete failure scenario, a severity (blocking / should-fix / nit), and a remedy — the fix, or a better alternative with its tradeoff named. Propose, don't just reject.
5. **Report.** Rank most-severe first, blocking issues separated from suggestions. Surface a genuinely better *design* alternative where you see one, framed as in `design-principles.md` (what it optimizes, what it costs). Note what's done well only when it's worth propagating elsewhere.

## Completion

Every changed file is assessed on all six axes; every finding has a scenario, a severity, and a remedy; design and security were reviewed as hard as correctness — not skipped because the code "looks fine."
