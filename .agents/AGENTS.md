# Global Agents Manifest (.agents)

This is the manifest of all AI agent workflows for this project.

## Development Lifecycle

```
/research → /spec → /design → /build → /test → /deploy
 (Facts)    (SDD)   (UX)    (TDD+ODD)  (E2E)   (Ops)
```

## Workflows (Actionable Commands)

Workflows are hardened command files used to orchestrate complex development cycles.

### Lifecycle Workflows
- `/spec`: Create technical specifications. Present ≥3 visual options, recommend one, and produce a requirements document.
- `/design`: Design the UX/visual system. Present ≥3 design directions with mockups, and produce architecture + design artifacts.
- `/build`: Build with TDD (Red-Green-Refactor) and ODD (structured logging). Unit/component/integration tests are written here.
- `/test`: Build and run E2E tests simulating real user behavior (e.g., Playwright bots). Observability-grade logging with drill-down and alerting.
- `/deploy`: Prepare and execute releases. User-configured per project (TODO template).

### Support Workflows
- `/research`: Research a topic — gather facts from KIs, codebase, and web, then produce ranked suggestions (Impact × Autonomy).
- `/review`: Review work just done — audit, fix urgent issues, suggest strategic improvements.
- `/advise`: Open-ended project analysis with prioritized suggestions (Impact × Autonomy).
- `/debug`: Systematic debugging using ODD (Observe → Reproduce → Fix) methodology.
- `/learn`: Document repeated mistakes made by AI Agents and prevent recursion.
