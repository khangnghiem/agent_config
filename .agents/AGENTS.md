# Antigravity Global Agents Manifest (.agent)

This is the manifest of all AI agent workflows and skills for this project.

## Development Lifecycle

```
/research → /spec → /design → /build → /test → /deploy
 (Facts)    (SDD)   (UX)    (TDD+ODD)  (E2E)   (Ops)
```

## Workflows (Actionable Commands)

Workflows are hardened command files used to orchestrate complex development cycles.

### Lifecycle Workflows
- `/spec`: Create technical specifications. Present ≥3 visual options, recommend one, update `docs/REQUIREMENTS.md`.
- `/design`: Design the UX/visual system. Present ≥3 design directions with mockups, update `docs/ARCHITECTURE.md`, `docs/DESIGN.md`, `docs/USER_JOURNEY.md`.
- `/build`: Build with TDD (Red-Green-Refactor) and ODD (structured logging). Unit/component/integration tests are written here.
- `/test`: Build and run E2E tests simulating real user behavior (e.g., Playwright bots). Observability-grade logging with drill-down and alerting.
- `/deploy`: Prepare and execute releases. User-configured per project (TODO template).

### Support Workflows
- `/research`: Research a topic — gather facts from KIs, codebase, and web, then produce ranked suggestions (Impact × Autonomy).
- `/review`: Review work just done — audit, fix urgent issues, suggest strategic improvements.
- `/advise`: Open-ended project analysis with prioritized suggestions (Impact × Autonomy).
- `/debug`: Systematic debugging using ODD (Observe → Reproduce → Fix) methodology.

## Skills (Knowledge & Instructions)

Skills provide deep expertise in specific domains and paradigms.

- `write-spec`: Author structured technical specifications from vague requirements (SDD).
- `write-unit-tests`: Generate comprehensive unit tests (TDD).
- `add-observability`: Inject structured logging, monitoring, and tracing (ODD).
- `diagnose-bug`: Perform root-cause analysis using an Observe -> Test -> Fix continuous loop (ODD + TDD).
- `code-review`: Perform a thorough, constructive code review.
- `generate-api-docs`: Produce clear, accurate REST API documentation.
