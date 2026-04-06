# Antigravity Global Rules (GEMINI.md)

This file contains the unified 3-tier rules for this repository, overriding any legacy agent personas or scattered rule files.

## Tier 1: Universal Rules

### Code Quality
- Write clear, readable code with self-explanatory variable and function names.
- Prefer explicit over implicit behaviour.
- Keep functions short and focused on a single responsibility.
- Avoid deep nesting; extract helper functions when logic becomes complex.

### Comments & Documentation
- Only add comments when the *why* is not obvious from the code itself.
- Keep docstrings concise and accurate.
- Update existing comments when changing the code they describe.

### Error Handling
- Handle errors explicitly; never silently swallow exceptions.
- Provide meaningful error messages that help diagnose the problem.
- Validate inputs at the boundaries of the system.

### Testing
- Write tests alongside new functionality.
- Favour small, focused unit tests over large integration tests where possible.
- Tests should be deterministic and not depend on external state.

### Security
- Never commit secrets, credentials, or API keys.
- Sanitise all user-supplied input before use.
- Use the least-privilege principle when requesting permissions.

### Version Control
- Write short, imperative commit messages (e.g. `Add user login endpoint`).
- Make small, focused commits that address one concern at a time.
- Reference issue numbers in commit messages when applicable.

---

## Tier 2: Stack Rules

### Python Stack
- **Style**: Follow [PEP 8](https://peps.python.org/pep-0008/) for formatting. Use [PEP 257](https://peps.python.org/pep-0257/) for docstrings. Use `ruff` for linting/formatting. Prefer f-strings.
- **Typing**: Add type hints to all public functions/methods. Use `from __future__ import annotations`. Avoid `Any`.
- **Imports**: Group standard library → third-party → local. No wildcard imports.
- **Patterns**: Prefer dataclasses/Pydantic over dicts. Use context managers. Use `pathlib.Path`. Raise specific exceptions.
- **Dependencies**: Pin in `requirements.txt` or `pyproject.toml`. Keep dev dependencies separate. Run security audits before release.

### TypeScript / Frontend Stack
- **Style**: Follow Google TS Style Guide. Use `eslint` + `prettier`. Single quotes for strings. Semicolons applied.
- **Types**: Explicit return types for exported functions. `interface` for shapes, `type` for unions/aliases. Never use `any` (use `unknown` instead). Strict mode enforced.
- **Imports**: Named exports preferred. Use path aliases.
- **Patterns**: `const` by default. Prefer `async/await`. Use `?.` and `??`. Avoid non-null assertions `!`.
- **React**: Function components with hooks over classes. Keep components small. Extract custom hooks.

### FastAPI Framework
- **Project Structure**: Organise into `api/`, `core/`, `models/`, `schemas/`, `services/`, and `tests/`.
- **API Design**: Version APIs (`/api/v1/`). Use Pydantic schemas. Specific HTTP statuses. Apply `summary`/`description` in decorators.
- **Dependencies**: Use FastAPI `Depends` for endpoints.
- **Error Handling**: Raise `HTTPException` with detail. Supply global exception handlers.
- **Configuration**: Load via Pydantic `BaseSettings`. Use environment variables or secret managers.
- **Testing**: Use `pytest` with `httpx.AsyncClient` + `pytest-asyncio`. Mock external services.

---

## Tier 3: Workflow Rules

- Reference the `workflows/` directory for standard operations (build, test, deploy).
- All AI interactions should default strictly to following this rule specification when writing or reviewing code.
