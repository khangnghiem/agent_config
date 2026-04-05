# FastAPI Rules

Rules specific to projects using the FastAPI framework.

## Project Structure

```
app/
├── main.py          # Application entry point
├── api/
│   └── v1/          # Versioned routers
├── core/
│   ├── config.py    # Settings (Pydantic BaseSettings)
│   └── security.py  # Auth helpers
├── models/          # ORM / database models
├── schemas/         # Pydantic request/response schemas
├── services/        # Business logic
└── tests/
```

## API Design

- Version all public APIs under `/api/v1/`, `/api/v2/`, etc.
- Use Pydantic schemas for all request bodies and response models.
- Return appropriate HTTP status codes (201 for creation, 204 for deletion, etc.).
- Provide `summary` and `description` in every route decorator for auto-generated docs.

## Dependency Injection

- Use FastAPI's `Depends` for shared resources (database sessions, current user, etc.).
- Keep dependency functions small and testable.

## Error Handling

- Raise `HTTPException` with a descriptive `detail` message.
- Use a global exception handler for unexpected errors to avoid leaking stack traces.

## Configuration

- Load settings via a Pydantic `BaseSettings` class; never hardcode values.
- Store secrets in environment variables or a secrets manager; never in source code.

## Testing

- Use `pytest` with `httpx.AsyncClient` / `TestClient` for route tests.
- Use `pytest-asyncio` for async tests.
- Mock external dependencies (databases, third-party APIs) in unit tests.
