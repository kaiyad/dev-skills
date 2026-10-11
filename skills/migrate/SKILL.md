---
name: migrate
description: Change a database schema or migrate data safely — zero-downtime, reversible, via expand-contract and batched backfill. Use when altering a schema, renaming or dropping a column, moving data, or any change where old and new code or data must coexist during rollout.
---

A schema change is the highest-blast-radius thing a team ships: it touches live data, it can't always be rolled back, and old and new code run side by side during the deploy. The discipline that makes it safe is **expand-contract** — never change in place.

## Steps

1. **Expand-contract is the spine.** Split every change into separate deploys: **expand** (add the new column/table, keep the old), **migrate** (code reads and writes both), **backfill** (fill the new from the old), **contract** (remove the old). One step per deploy, never collapsed.
2. **Survive the dual-running window.** During rollout, old and new code run at the same time. Every intermediate state must be correct for *both* — a change that's only valid once all instances have updated will break mid-deploy. This is the rule most in-place migrations violate.
3. **Backfill in batches.** Migrate existing rows in resumable, idempotent batches off the hot path. Never a single locking statement over a large table — that's an outage, not a migration.
4. **Stay reversible.** Each step has a rollback that loses no data. The one destructive step (the drop) runs only *after* the new path is proven in production, and never in the same deploy that introduced it.
5. **Guard the data.** Back up first. Verify row counts and invariants before and after each step. Rehearse on a production-sized copy — a migration that's only ever run against an empty dev database is untested.

## Completion

The change rolls forward and back with no downtime and no data loss; old and new code coexist correctly through every intermediate deploy; the destructive step runs only after the new path is confirmed in production; data invariants were verified before and after and the migration was rehearsed on prod-sized data.
