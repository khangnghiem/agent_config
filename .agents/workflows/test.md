---
description: Build and run end-to-end tests simulating real user behavior.
---

// turbo-all

# /test

$ARGUMENTS

`$ARGUMENTS` can be:
- An **environment**: `local`, `dev`, `staging`, `prod` — scopes test execution to that target.
- A **journey name** — scopes testing to that specific scenario.
- Omitted — runs all journeys against `local` by default.

> [!IMPORTANT]
> This workflow is **NOT** for unit tests, component tests, or integration tests — those are built during `/build` (TDD phase).
> This is for **real user simulation**: E2E tests that exercise the full system as a human would.

> **Prerequisite**: `/build` must be completed.
> **Input**: `docs/USER_JOURNEY.md`
> **Next**: `/deploy`

## Phase 1: Resolve Environment

Parse `$ARGUMENTS` and set the active target:

| Argument | Target | Base URL | Purpose |
|----------|--------|----------|---------|
| `local` (default) | Local dev server | `localhost:*` | Fast iteration during development |
| `dev` | Development / Preview | Configured dev URL | Validate feature branch deploys |
| `staging` | Staging / Pre-prod | Configured staging URL | Full regression before production |
| `prod` | Production | Configured prod URL | Post-deploy smoke verification |

Test depth scales with environment:

| Test Category | `local` | `dev` | `staging` | `prod` |
|---------------|---------|-------|-----------|--------|
| **Happy path** | ✅ | ✅ | ✅ | ✅ |
| **Failure path** | ✅ | ✅ | ✅ | ⚪ Smoke only |
| **Edge case** | ✅ | ⚪ | ✅ | ⚪ Skip |
| **Performance thresholds** | ⚪ | ⚪ | ✅ | ✅ |

## Phase 2: Test Platform Setup

1. Identify or build the E2E testing platform for the project:

| Product Type | Platform | Agent Pattern |
|-------------|----------|---------------|
| **Browser app** | Playwright | Bot agent: navigate, click, type, assert DOM and visual state |
| **API service** | HTTP client (httpx, supertest) | Replay agent: real user request sequences with auth flows |
| **CLI tool** | Shell script | Command agent: exercises commands exactly as a user would |
| **Mobile app** | Detox / Maestro | Touch agent: tap, swipe, scroll, assert screen content |

2. The test agent must simulate realistic user journeys defined in `docs/USER_JOURNEY.md`.
3. Test infrastructure **is code** — it must be version-controlled, reviewed, and maintained like production code.

## Phase 3: Test Scenario Design

4. Map each user journey from `docs/USER_JOURNEY.md` to a concrete test scenario.
5. Cover categories according to the depth table in Phase 1:

| Category | Examples |
|----------|---------|
| **Happy path** | User completes the full journey successfully |
| **Failure path** | Network timeout, invalid input, expired session, 403 forbidden |
| **Edge case** | Concurrent users, large datasets, slow connections, empty states |

6. If fixing a bug, use the `diagnose-bug` skill to write a regression E2E test first.

## Phase 4: Observability-Grade Logging

7. Every test step must emit a structured log with a `trace_id` linking the full journey:

| Log Level | Purpose | Example |
|-----------|---------|--------|
| `INFO` | Journey milestones | "User completed checkout in 3.2s" |
| `DEBUG` | Step-level detail | "POST /api/cart returned 200 in 45ms" |
| `WARN` | Threshold breaches | "Step 'add to cart' took 2.1s (threshold: 1s)" |
| `ERROR` | Assertion failures | "Expected 'Success' banner, got error modal" |

8. Log aggregate metrics after each run for flakiness tracking:
   - Success/failure rates per journey, step-level latency (p50/p95), and flaky test count.

## Phase 5: Execution & Reporting

9. Set the base URL for the resolved environment.
10. Execute the E2E test runner against the target.
11. Report results with structured output:

| Metric | Format |
|--------|--------|
| **Environment** | Which target was tested (local/dev/staging/prod) |
| **Per-journey** | Pass/Fail + duration + screenshot on failure |
| **Aggregate** | Total pass rate, mean duration, flaky test count |
| **Logs** | Full trace log with `trace_id` for failed journeys |

---

## Rules

| Rule | Description |
|------|-------------|
| **Not unit tests** | This workflow tests *user behavior*, not code paths. |
| **Environment-aware** | Always resolve the target environment — test depth scales accordingly. |
| **Traceable** | Every step must emit a structured, filterable log. |
| **Deterministic** | Flaky tests are bugs — track and fix them, don't retry-and-ignore. |
| **Screenshot on fail** | Every failed assertion must capture visual state for debugging. |
| **Infra is code** | Test platform setup is committed, reviewed, and versioned. |
| **Staging = full regression** | Staging runs the complete test matrix — it gates production deploys. |
| **Prod = smoke only** | Production tests verify health, not explore edge cases. |
