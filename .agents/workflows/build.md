---
description: Orchestrate the build phase using TDD and ODD.
---

// turbo-all

# /build

$ARGUMENTS

If `$ARGUMENTS` is provided, scope the build to that feature or component.
Otherwise, build everything defined in the approved spec.

> **Prerequisite**: `/spec` and `/design` must be completed and approved.
> **Paradigms**: Test-Driven Development (TDD) + Observability-Driven Development (ODD)
> **Next**: `/test`

## Phase 1: Test-First (TDD — Red)

1. Review the approved spec (`docs/REQUIREMENTS.md`) and design (`docs/DESIGN.md`).
2. Write **failing automated tests first**:

| Test Type | Scope | Example |
|-----------|-------|---------|
| **Unit** | Individual functions/methods | `test_calculate_risk_returns_score` |
| **Component** | UI components in isolation | `PatientCard.test.ts` (render, props, events) |
| **Integration** | Cross-layer interactions | `test_api_creates_patient_and_returns_201` |

3. Tests must cover:
   - All acceptance criteria from the spec.
   - Edge cases and error states from the design (empty, loading, overflow).
   - Boundary values, null inputs, and unauthorized access.
4. Run the test suite and confirm all new tests **fail** (Red state).
   - If tests pass without implementation, the tests are not targeting new logic — rewrite them.

## Phase 2: Implementation (TDD — Green)

5. Identify the core components needing integration.
6. Ensure `GEMINI.md` standard adherence (stack rules, typing, naming conventions).
7. Write the **minimal code** required to make all failing tests pass (Green state).
   - Do not add features or optimizations beyond what the tests require.

## Phase 3: Observability (ODD)

8. Apply observability at all service boundaries:

| Boundary | Logging Required |
|----------|-----------------|
| **Entry** | `INFO`: "Starting [operation] with [params]" |
| **Exit** | `INFO`: "Completed [operation] in [duration]ms" |
| **Error** | `ERROR`: Full context + stack trace, never silently swallowed |
| **External call** | Outbound API, DB, or file I/O with timing |

9. Inject `trace_id` / `correlation_id` for request-level tracing across layers.
10. Define monitoring metrics for key operations (rate, errors, duration — the RED method).
11. Write or update **regression tests** for any bugs encountered during development.

## Phase 4: Refactor & Compile

12. Refactor for readability, performance, and clean-code standards (SRP, DRY, KISS).
13. Re-run the **full** test suite to confirm zero regressions.
14. Run the project's standard build command (e.g. `npm run build`, `cargo build`, `uv run pytest`).

---

## Rules

| Rule | Description |
|------|-------------|
| **Test-first** | No implementation code before a failing test exists for it. |
| **Minimal green** | Write only enough code to pass — no gold-plating. |
| **Log at boundaries** | Never inside tight loops or low-level utilities. |
| **No silent catches** | Every `catch` block must log context before handling or re-throwing. |
| **Regression discipline** | Every bug fixed during build gets a permanent regression test. |
| **Context continuity** | If previous responses in this conversation contain recommendations or an approved plan, follow them as the primary directive. |
