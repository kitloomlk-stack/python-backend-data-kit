# Python typing and style

- Annotate parameters and return values of every public function and method. Use modern syntax supported by the project's Python version (`list[str]`, `X | None`).
- Run the configured type checker and linter after edits and fix the errors you introduced.
- No bare `# type: ignore`; scope it to an error code and add a short reason.
- Prefer Pydantic models or dataclasses over loose dictionaries for structured data crossing function boundaries.
- Do not use mutable default arguments; use `None` plus a default inside the function, or `field(default_factory=...)`.
- Catch specific exceptions. Never write a bare `except:`; log and re-raise when you catch `Exception`.
- Use `logging` with a module-level logger, not `print`, in library and service code.
- Use `pathlib.Path` for paths and context managers for files, connections and locks.
- Import at module top in the order the formatter expects; avoid wildcard imports.
