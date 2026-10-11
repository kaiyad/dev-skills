# Design principles — deep modules and the pattern catalog

Reference for designing and judging structure. Loaded on demand by `shape-design`, `review`, and `refactor`. The goal of every design decision: a system that is simple to understand and cheap to change, not one that is clever.

## Deep modules (the core idea)

A **module** (function, class, package, service) has an *interface* — what a caller must know — and an *implementation* — what it hides. A **deep** module presents a small interface over a substantial implementation: much hidden, little asked of the caller. A **shallow** module is the smell: a wide interface over little substance (a thin wrapper that just forwards, a class whose methods are all getters/setters, a "manager" that only delegates).

- The interface is a cost paid on every use, forever. The hidden implementation is the value. Maximize what you hide behind the smallest honest interface.
- **Information hiding**: each module owns a decision and hides how it makes it, so changing that decision touches one place.
- **Design it twice**: sketch two genuinely different interfaces before committing. The second one teaches you what the first got wrong.
- **Design from the caller's side**: write the call site you wish existed, then build the interface that makes it real.
- **Define errors out of existence**: an interface that makes the error case impossible (or trivial) beats one that documents how to handle it.

## Seams

A **seam** is where you'd cut to test, swap, or reason about a part in isolation. Put seams at stable boundaries (a domain concept, an external dependency), not through the middle of one idea. A good seam is where behavior changes when requirements change — align module boundaries with the axes of likely change.

## Coupling & cohesion

- **Low coupling**: modules depend on each other's interfaces, not internals. Depend on a `Protocol`, not a concrete class, at a boundary you'll want to swap.
- **High cohesion**: things that change together live together; things that change for different reasons don't.
- Dependencies point inward, toward stable abstractions, away from volatile detail (frameworks, IO, UI).

## Pattern catalog — reach for the boring, proven one first

Before inventing, name the established solution that fits. Prefer the well-understood pattern a new teammate will recognize over a novel construction. One line each on when it earns its place:

- **Layered / hexagonal (ports & adapters)** — isolate domain logic from IO/framework; the default shape for an app with external dependencies.
- **Repository** — hide persistence behind a collection-like interface; swap DB or mock it in tests.
- **Dependency injection** — pass collaborators in rather than constructing them inside; the cheapest testability win there is.
- **Strategy** — a family of interchangeable algorithms chosen at runtime; kills a branching `if type ==` chain.
- **Adapter** — wrap a mismatched external interface in the one your domain wants.
- **Factory / builder** — centralize construction when it's non-trivial or varies.
- **State machine** — model anything with explicit states and legal transitions (orders, jobs, connections); replaces scattered boolean flags.
- **Pipeline** — a sequence of pure stages over a stream; natural for data transforms.
- **Event-driven / pub-sub** — decouple producers from consumers when fan-out or async is real; don't add the indirection speculatively.
- **CQRS** — split read and write models *only* when their shapes genuinely diverge; premature CQRS is pure cost.
- **Idempotency + retry + circuit breaker** — the baseline trio for any call across a network boundary.
- **Feature flag** — decouple deploy from release; the safe path for risky or gradual changes.

## Presenting alternatives (how `shape-design` and `review` surface options)

When a decision has more than one defensible answer, lay out **2–3 real contenders** — never a strawman next to the one you want. For each:

- **What it is** — one line.
- **What it optimizes** — simplicity / changeability / performance / operability.
- **What it costs** — the price you pay to get that.
- **When it wins** — the condition that makes it the right call.

Then **recommend one**, tied to the forces of *this* problem, and name the **reversal condition**: the fact that, if it changed, would flip the choice. A recommendation without a reversal condition is an assertion, not a design.

## Tradeoff vocabulary

Name which axis you're buying when you choose:

- **Simplicity** — fewest moving parts, easiest to hold in the head.
- **Changeability** — cheapest to modify along the expected axis of change.
- **Performance** — latency/throughput/memory, measured not assumed.
- **Operability** — how it behaves at 3am: observable, recoverable, debuggable.

You cannot maximize all four. Say which one this decision prioritizes and which you're spending.

## When not to abstract

- **YAGNI**: don't build the general case before the second real instance exists. One use case is not a pattern.
- **Rule of three**: duplication is cheaper than the wrong abstraction. Extract on the third occurrence, when the shape is clear.
- The reverse is also a smell: hardcoding past the point where the variation is obviously real. Abstract when the second case arrives, not before, not after.
