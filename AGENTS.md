# Python Backend & Data Kit

This kit configures a coding agent for Python services and data work: FastAPI or Django style backends, typed code, pytest suites, SQL and Postgres, and pandas or notebook analysis. It favours explicit types, small tested changes, and data that is checked before anyone relies on it.

## Working agreement

- Read the existing code and project configuration (`pyproject.toml`, `requirements*.txt`, `setup.cfg`) before changing anything. Follow the conventions already present.
- Make the smallest change that solves the problem. Keep unrelated cleanup out of the diff.
- Ask before destructive or hard-to-reverse steps: dropping or truncating tables, rewriting history, deleting data files, deploying, or pushing.
- Work inside the project's virtual environment. Do not install packages globally. Add dependencies to the project's dependency file and tell the user why.
- Keep secrets out of the repository. Read configuration from environment variables and list names only in an example env file.
- Report results honestly: say which commands you ran and what they printed, and what you could not run.

## Python conventions

- Target the Python version declared by the project. Use type hints on all public functions, methods and module-level constants.
- Run the project's type checker (mypy or pyright) and linter (ruff, flake8) if configured, and fix what you introduce. Do not add blanket `# type: ignore`; if one is needed, scope it and explain it.
- Prefer `pathlib`, `dataclasses` or Pydantic models, f-strings, context managers and `logging` over ad-hoc alternatives. Use `print` only in scripts meant to print.
- Raise specific exceptions. Do not catch bare `Exception` unless you log it and re-raise or return a controlled error. Never use bare `except:`.
- No mutable default arguments. No global mutable state in request paths.
- Keep functions short and side effects at the edges: pure functions for logic, thin I/O wrappers around them.

## Backend services

- Validate every request body, query parameter and path parameter with Pydantic models or framework validators. Return precise status codes (400 vs 404 vs 409 vs 422).
- Use dependency injection (FastAPI `Depends`, Django middleware or services) for database sessions, settings and the current user. Do not create connections inside handlers.
- Do not block the event loop in async handlers: use async drivers or run blocking work in a thread pool.
- Authenticate and authorise on every protected route; check ownership of the object, not only that the caller is signed in.
- Use parameterised queries or ORM expressions. Never build SQL by concatenating or formatting user input.
- Structured logging with request ids; never log passwords, tokens or full personal data.
- Version schema changes with the project's migration tool (Alembic, Django migrations). Never edit an applied migration.

## SQL and Postgres

- Name constraints and indexes. Use `timestamptz`, `numeric` for money, `text` over arbitrary `varchar(n)`, and foreign keys with deliberate `on delete` behaviour.
- Check query plans with `EXPLAIN (ANALYZE, BUFFERS)` on realistic data before adding indexes; add the index that the plan shows is missing, not one that merely looks plausible.
- For migrations on large tables, think about locks: add nullable columns first, backfill in batches, then add constraints (`not valid` then `validate`). Describe the rollback.
- Explore an unfamiliar schema (tables, columns, constraints, row counts) before writing queries against it.

## Data and notebooks

- Treat raw data as read-only. Write derived data to a separate location and record how it was produced.
- Set random seeds, pin library versions and avoid hidden state so results can be rerun top to bottom.
- Keep notebooks small: move reusable logic into importable modules with tests, and clear outputs before committing unless the output is the deliverable.
- In pandas, avoid chained assignment, prefer vectorised operations over row loops, and make dtypes explicit when reading files.
- Check data before using it: row counts, nulls, duplicates on the key, value ranges, referential integrity. Fail loudly when a check breaks.

## Testing

- Use pytest. One behaviour per test, descriptive names, arrange-act-assert.
- Use fixtures for setup; keep them close to where they are used. Prefer real objects and a throwaway test database over heavy mocking of your own code.
- Mock only external boundaries (HTTP APIs, clocks, queues).
- Test the failure paths: invalid input, missing rows, permission denied, timeouts.
- A bug fix includes a test that fails without it. Do not weaken or delete a failing test to get a green run.

## Before you finish

1. Run formatter, linter, type checker and the test suite with the project's commands.
2. Review the diff for debug prints, commented-out code, unrelated edits and new dependencies.
3. Summarise what changed, what you verified and what remains unverified.

## Skills in this kit

- fastapi-templates: use when starting or restructuring a FastAPI service.
- postgresql-table-design: use when designing or reviewing tables and indexes.
- postgres-database-migration: use when planning a migration against live data.
- sql-optimization-patterns: use when a query is slow.
- schema-exploration: use before querying an unfamiliar database.
- data-quality-frameworks: use when adding validation checks to a dataset or pipeline.
- debugging-strategies: use when chasing a bug or flaky test.
- security-and-hardening: use when handling input, auth, secrets and data access.
- observability-and-instrumentation: use when adding logs, metrics or traces.
- performance-optimization: use when a measured slowdown needs profiling.

## Commands

- `add-endpoint`: add a typed endpoint with schemas, tests and error handling.
- `explain-query`: analyse a query plan and suggest safe improvements.
- `data-check`: profile a dataset and propose validation checks.

## Sub-agents

- `python-reviewer`: reviews a Python diff for typing, error handling, security and test gaps.
- `sql-reviewer`: reviews SQL and migrations for correctness, locking and performance.

## Scoped rules

Agents that support scoped rules load these automatically. If yours does not, read the matching file before editing files it covers:

- `.agents/rules/python-typing.md` — always: Typing and style habits for every Python change.
- `.agents/rules/pytest-tests.md` — for `tests/**/*.py`, `**/test_*.py`, `**/*_test.py`: Applies when writing or editing tests.
- `.agents/rules/notebooks-sql.md` — for `**/*.ipynb`, `**/*.sql`: Applies to notebooks and SQL files: keep them reproducible and safe.
