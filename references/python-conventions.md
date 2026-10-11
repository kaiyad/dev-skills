# Python conventions — the elegant standard

Reference for writing and reviewing Python. Loaded on demand by `implement`, `review`, `refactor`, and `test`. These are defaults, not laws: when the project's own config or surrounding code sets a different convention, that wins — match the grain of the code you're in.

## Tooling (use what the project configures)

Read `pyproject.toml` / `setup.cfg` / CI before assuming. The modern default stack, if the project has none:

- **ruff** for lint + format (replaces black, isort, flake8). One tool, one config.
- **mypy** or **pyright** in strict mode for types.
- **pytest** for tests.
- **uv** (or pip-tools / poetry) for dependency management, pinned.
- **src layout** (`src/package/…`) so tests run against the installed package, not the working tree.

Never guess a command — find the real `test`/`lint`/`typecheck` invocation in `pyproject.toml`, `Makefile`, `tox.ini`, or CI.

## Types

- Annotate every public signature. Internal helpers too when the type isn't obvious.
- Prefer precise types over `Any`: `Literal`, `Protocol` (structural, for seams), `TypedDict`, `Enum`, generics. `Any` is an escape hatch you justify, not a default.
- `X | None` over `Optional[X]`, `list[X]` over `List[X]` (3.10+).
- `Protocol` over ABCs when you want duck-typed seams without inheritance coupling.

## Data shapes

Pick the lightest that carries the meaning:

- **`@dataclass`** (often `frozen=True`) for plain internal data. Default choice.
- **pydantic** `BaseModel` for data crossing a boundary that needs validation (API input, config, external payloads). Validate once, at the edge; trust it inside.
- **`Enum`** over string/int constants — the type documents the domain and the checker guards it.
- **`NamedTuple`/`TypedDict`** for lightweight fixed records; `TypedDict` when it's really a dict you're typing.
- Reach for a plain `dict`/`tuple` only for the genuinely anonymous. A named shape beats a tuple whose fields you have to remember.

## Functions

- Small, one responsibility, pure where you can make it pure (no hidden IO/state) — pure functions are the testable seam.
- Early return over nested `if`; guard clauses at the top.
- Keyword-only (`*,`) for booleans and optional config so call sites read: `connect(host, *, retries=3)` not `connect(host, True, 3)`.
- Explicit parameters over `**kwargs` unless you're genuinely forwarding.

## Errors

- Raise **specific** exceptions; define your own domain exceptions over reusing `ValueError` for everything.
- Catch **narrow** and near the thing that can fail. Never bare `except:`; `except Exception` only at a top-level boundary that logs and re-raises or converts.
- Exceptions for the exceptional; return values (or a `Result`-style type) for outcomes the caller routinely handles.
- Context managers (`with`) for every resource — files, locks, connections, sessions.
- Define errors out of existence where you can: an API that returns an empty list beats one that raises on "nothing found".

## Modules (deep, not shallow)

- A module is a **seam**: a simple interface hiding a substantial implementation. The interface is the cost you pay forever; the hidden implementation is the value. See `design-principles.md`.
- Keep internals private (`_name`), expose a small surface, use `__all__` to state it.
- No circular imports — if two modules need each other, the shared thing belongs in a third.

## Idioms

- `pathlib.Path` over `os.path`.
- f-strings over `%` / `.format`.
- Comprehensions when they read in one breath; a plain loop when the comprehension would need a comment.
- `enumerate`, `zip`, `dict.get`, `collections.defaultdict`/`Counter` over hand-rolled equivalents.
- Generators/iterators for large or streaming data — don't materialize a list you'll consume once.
- `functools.cached_property`, `lru_cache` for memoization instead of hand-rolled caches.

## Concurrency

- `asyncio` for IO-bound concurrency; processes (`concurrent.futures.ProcessPoolExecutor`) for CPU-bound. Threads mainly for blocking IO you can't make async.
- Never block the event loop with sync IO or heavy CPU inside `async` code.

## Dependencies

- Prefer the standard library. Each third-party dependency is a liability — justify it against stdlib, and prefer a well-maintained, widely-used one over a clever niche one.
- Pin versions. Don't add a dependency for something you use once and could write in five lines.

## Logging & secrets

- `logging`, never `print`, in library/app code. Structured fields over string-concatenation.
- Never log secrets, tokens, or PII. Never hardcode credentials — read from env/secret store.

## Tests (pytest)

- Arrange–act–assert, one behavior per test, names that read as sentences (`test_rejects_expired_token`).
- Fixtures for setup, `@pytest.mark.parametrize` for cases. No branching/logic in a test body.
- Assert on observable behavior, not internals, so tests survive refactors. See `test` skill.

## Habit: name the alternatives

When more than one clean option exists, say so in a line before you commit — don't silently take the first that works. Common forks and the heuristic:

- **dataclass vs pydantic vs attrs** → dataclass internal, pydantic at validated boundaries, attrs only if already in the project.
- **sync vs async** → async only when IO concurrency is the actual need; it colors the whole call tree, so don't adopt it for a single call.
- **stdlib vs library** → stdlib unless the library removes real complexity (e.g. `httpx` over hand-rolled retries).
- **inheritance vs composition/Protocol** → composition and Protocols by default; inheritance only for genuine is-a with shared behavior.
