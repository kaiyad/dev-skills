---
name: test
description: Write tests that pin behavior — test-first for new work, characterization tests before changing untested code. Use when adding tests, doing TDD or red-green-refactor, or asked to cover or verify behavior. Python/pytest.
---

Write tests that would fail if the behavior broke and survive if the code is merely restructured. See `../../references/python-conventions.md` for pytest idioms.

## Steps

1. **Test the behavior at the seam.** Assert on observable outputs and effects through the public interface, not on internal calls or private state. A test coupled to the implementation breaks on every refactor and guards nothing — that's the failure mode to avoid.
2. **For new work, go test-first (red-green-refactor).**
   - **Red**: write one test that states the next increment of behavior and fails for the right reason. Run it; see it fail.
   - **Green**: write the simplest code that passes it.
   - **Refactor**: improve the shape with the test holding the line.
3. **For untested code you're about to change, characterize first.** Write tests that capture what it *currently* does, so a later change that alters behavior shows up as a failing test rather than a silent regression.
4. **Shape each test.** One behavior per test. Arrange–act–assert. Names that read as sentences (`test_rejects_expired_token`). Fixtures for setup, `parametrize` for cases, no logic in the test body.
5. **Cover the edges that bite.** Empty, boundary, duplicate, error paths, and concurrency where it's real — not only the happy path. Keep every test deterministic: no wall-clock, no network, no ordering or sleep dependence.

## Completion

Each new behavior has a test that failed before the code existed; changed legacy code has characterization tests around it; edge and error paths are covered; the suite is green and deterministic — stated with the command you ran.
