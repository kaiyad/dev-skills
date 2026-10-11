---
name: pr
description: Write a pull-request description a reviewer can act on — what changed, why, how to verify, and what to watch. Use when opening a PR or writing or improving a PR body.
---

The PR body tells a reviewer where to look and how to check — it doesn't restate the diff they can already read.

## Steps

1. **Lead with why.** The problem this solves and the outcome it produces, linked to the issue or spec. A reviewer who understands the intent reviews ten times faster.
2. **Describe what changed in shape, not in full.** The approach and the key moves — "introduced a repository seam so persistence is swappable" — not a file-by-file narration of the diff.
3. **Say how to verify.** The exact commands or steps the reviewer runs, and what *you* already ran with its result. Make the green path reproducible.
4. **Flag the risk.** Blast radius, data migrations, rollout/rollback plan, and the one or two spots you most want scrutinized. Point the reviewer's attention where it pays off.
5. **Keep it scannable.** Short sections, the important thing first. The body orients the review; it doesn't replace reading the code.

## Completion

A reviewer knows why the change exists, what to check first, and how to verify it — without asking a follow-up question. Risk and verification are explicit, not implied.
