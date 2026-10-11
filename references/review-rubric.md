# Review rubric — the six axes

Reference for `review`. Apply every axis to every changed file. A finding is only done when it carries a **failure scenario**, a **severity**, and a **remedy**. For a large diff, each axis can run in its own subagent and report back.

## 1. Correctness

Does it do the right thing on every input, not just the demo one?

- Edge cases: empty, single, max, boundary, duplicate, unicode, very large.
- `None`/null and missing-key paths.
- Error paths: what happens when the thing it calls fails or times out.
- Off-by-one, inclusive/exclusive bounds, rounding.
- Concurrency: shared mutable state, races, ordering assumptions, re-entrancy.
- Resources: are files/connections/locks released on every path (including error)?
- Idempotency: safe to run twice? Retries won't double-charge / double-write?
- Time, timezone, encoding, and locale assumptions.

## 2. Design & interface

Is this the right shape, or just a working one?

- Deep vs shallow: is the interface small for the substance it hides, or a thin wrapper? (`design-principles.md`)
- Is the seam in the right place — at a stable boundary, not through one idea?
- Coupling: does it reach into another module's internals? Depend on a concrete where a `Protocol` belongs?
- Naming: does each name reveal intent without a comment?
- Is there a materially simpler shape that does the same job?
- Is the abstraction earned (second real case exists) or speculative?

## 3. Business / spec fit

Does it build what was actually asked?

- Every acceptance criterion in the spec/issue met — name any that isn't.
- Requirements silently dropped or misread.
- Domain assumptions: does the code's model match how the business actually behaves?
- Scope creep: changes the spec didn't ask for, riding along unreviewed.

## 4. Quality & readability

Will the next person understand and trust it?

- Follows `python-conventions.md` and the surrounding file's style.
- No dead code, commented-out blocks, leftover `TODO` stubs, debug prints.
- Duplication that should be a single source of truth.
- Magic numbers/strings that should be named constants or enums.
- Comment density matches the file; comments say *why*, not *what*.

## 5. Security & safety

What could an attacker or a bad input do?

- Input validated at the boundary; nothing trusted from outside.
- Injection: SQL/command/template/path traversal — parameterized, never concatenated.
- Secrets: none in code, config, logs, or error messages.
- AuthZ: is the caller's permission actually checked, not just authentication?
- Unsafe deserialization (`pickle`, `yaml.load`), SSRF, unsafe redirects.
- PII: handled, minimized, not logged.
- Dependency risk: new dependency maintained and from a trusted source?

## 6. Tests

Would the suite catch a regression?

- Do tests exist for the new/changed behavior?
- Do they assert observable behavior, not implementation detail (so they survive a refactor)?
- Edge and error paths covered, not only the happy path.
- Deterministic — no reliance on wall-clock, ordering, network, or sleep.
- Would a plausible bug in this code make a test fail? If not, the test is theater.

## Finding format

Rank most-severe first. Separate **blocking** from **suggestion**.

```
[severity: blocking | should-fix | nit] <file:line> — <the defect>
Scenario: <concrete inputs/state → wrong outcome>
Fix: <the change, or a better alternative with its tradeoff>
```

No objection without a remedy. When you'd reshape the design, show the alternative and what it costs — a reviewer proposes, they don't just reject.
