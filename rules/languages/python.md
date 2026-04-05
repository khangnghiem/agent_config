# Python Rules

Rules specific to Python projects.

## Style

- Follow [PEP 8](https://peps.python.org/pep-0008/) for formatting.
- Use [PEP 257](https://peps.python.org/pep-0257/) conventions for docstrings.
- Use `ruff` for linting and formatting; configuration lives in `pyproject.toml`.
- Prefer f-strings over `.format()` or `%`-formatting.

## Typing

- Add type hints to all public functions and methods.
- Use `from __future__ import annotations` at the top of every module for forward-compatible annotations.
- Avoid `Any` unless genuinely necessary; prefer `Union`, `Optional`, or `TypeVar`.

## Imports

- Group imports: standard library → third-party → local, separated by blank lines.
- Never use wildcard imports (`from module import *`).
- Import only what is used.

## Patterns

- Prefer dataclasses or Pydantic models over plain dictionaries for structured data.
- Use context managers (`with` statements) for resource management.
- Use `pathlib.Path` instead of `os.path` for filesystem operations.
- Raise specific exceptions; avoid bare `except` clauses.

## Dependencies

- Pin dependencies in `requirements.txt` or `pyproject.toml`.
- Keep development dependencies separate from runtime dependencies.
- Run `pip-audit` or `safety` before shipping a new release.
