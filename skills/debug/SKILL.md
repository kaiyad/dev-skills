---
name: debug
description: Diagnose a bug or regression by reproducing it first, then isolating the cause before changing anything. Use when something is broken, failing, crashing, flaky, slow, or regressed, or when asked to debug or find the root cause of a failure.
---

Find the cause before touching the fix. The discipline is a loop that goes **red** — fails reliably on the bug — and only goes green once a change addresses the named cause, not the symptom.

## Steps

1. **Reproduce.** Build the smallest reliable trigger — a failing test or a single command that shows the bug every time. The loop is *red* when it fails on demand. Do not attempt a fix while the bug is intermittent or unreproduced; you'd be guessing.
2. **Observe the evidence.** Gather the actual error text, full stack trace, logs, and the exact inputs. Reproduce them verbatim in your notes — never paraphrase a stack trace or round off an error message; the precise wording is the clue.
3. **Isolate.** Form one hypothesis about the mechanism. Make the *cheapest* observation that would disprove it — a bisect, a log line, an assertion, a breakpoint. Let the result kill or keep the hypothesis, then narrow again. Continue until the cause is a single mechanism you can state in one sentence.
4. **Confirm.** Change the code that addresses that mechanism. The fix is real only when it flips the loop red→green *and* you can explain why — a change that merely makes the symptom disappear is a new bug in disguise.
5. **Guard.** Leave the reproduction behind as a regression test so this exact failure can't return silently.

## Completion

The cause is named as a mechanism (not "something with the data"); the fix flips the reproduction from red to green with an explanation of why; a regression test is committed. For a performance regression, the same loop applies with a measurement as the red/green signal — profile, don't guess.
