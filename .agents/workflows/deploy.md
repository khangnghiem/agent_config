---
description: Prepare and execute releases (user-configured per project).
---

// turbo-all

# /deploy

$ARGUMENTS

`$ARGUMENTS` must be one of: `local`, `dev`, `staging`, `prod`.
If omitted, default to `local`.

> **Prerequisite**: `/test` must be completed.
> **Paradigm**: Observability-Driven Development (ODD) — logging and monitoring verification is mandatory.

## Phase 1: Resolve Environment

Parse `$ARGUMENTS` and set the active environment:

| Argument | Environment | Risk Level | Rollback Required |
|----------|-------------|------------|-------------------|
| `local`  | Local / Docker Compose | 🟢 Low | No |
| `dev`    | Development / Preview | 🟡 Medium | Recommended |
| `staging` | Staging / Pre-production | 🟠 High | **Yes** |
| `prod`   | Production | 🔴 Critical | **Mandatory** |

## Phase 2: Pre-Deploy Gates

1. Verify all tests pass:

| Test Tier | Source | `local` | `dev` | `staging` | `prod` |
|-----------|--------|---------|-------|-----------|--------|
| Unit / Component | `/build` | ✅ | ✅ | ✅ | ✅ |
| Integration | `/build` | ⚪ | ✅ | ✅ | ✅ |
| E2E (user simulation) | `/test` | ⚪ | ⚪ | ✅ | ✅ |

2. Audit security and architecture against `GEMINI.md` standards.
3. **`staging` / `prod` only**: Verify observability readiness:
   - [ ] Structured logging at all service boundaries.
   - [ ] Monitoring endpoints / dashboards accessible.
   - [ ] Alerting rules configured for critical error thresholds.
   - [ ] Health check endpoint returns valid status.

## Phase 3: Environment Configuration (USER TODO)

> Fill in per project. These values persist across deployments.

### `local`

| Setting | Value (fill in) | Examples |
|---------|-----------------|----------|
| **Deploy command** | `___` | `docker compose up -d`, `npm run dev`, `cargo run` |
| **Env file** | `___` | `.env.local`, `.env.development` |

### `dev`

| Setting | Value (fill in) | Examples |
|---------|-----------------|----------|
| **Target** | `___` | Preview URL, feature branch deploy, dev cluster |
| **Deploy command** | `___` | `vercel --env preview`, `fly deploy --app myapp-dev` |
| **Env file / secrets** | `___` | `.env.dev`, Vault path, GitHub Secrets |
| **Rollback procedure** | `___` | Redeploy previous commit, revert PR |
| **Propagation delay** | `___` | Seconds to wait before smoke test (e.g., 30s) |

### `staging`

| Setting | Value (fill in) | Examples |
|---------|-----------------|----------|
| **Target** | `___` | Staging URL, pre-prod cluster, QA environment |
| **Deploy command** | `___` | `fly deploy --app myapp-staging`, `kubectl apply -f staging/` |
| **Env file / secrets** | `___` | `.env.staging`, Vault path, GitHub Secrets |
| **Rollback procedure** | `___` | Redeploy previous tag, revert migration, blue-green switch |
| **Propagation delay** | `___` | Seconds to wait before smoke test (e.g., 45s) |

### `prod`

| Setting | Value (fill in) | Examples |
|---------|-----------------|----------|
| **Target** | `___` | Cloudflare Pages, AWS ECS, Vercel Production |
| **Deploy command** | `___` | `wrangler pages deploy`, `docker compose -f prod.yml up -d`, `vercel --prod` |
| **Env file / secrets** | `___` | `.env.production`, Vault path, GitHub Secrets |
| **Rollback procedure** | `___` | `git revert` + redeploy, blue-green switch, previous Docker tag |
| **Propagation delay** | `___` | Seconds to wait before smoke test (e.g., 60s for CDN, 30s for PaaS) |

## Phase 4: Execute Deployment

4. Run the deploy command for the active environment.
5. Wait for the configured propagation delay before verification (`dev`, `staging`, and `prod` only).

## Phase 5: Post-Deploy Verification

Verification depth scales with environment risk:

### `local`

6. Confirm the service starts without errors.
7. Spot-check the primary user journey manually or via `browser_subagent`.

### `dev`

6. Health check endpoint returns 200.
7. Primary user journey works end-to-end (`browser_subagent`).
8. No new `ERROR` level log entries in the first 2 minutes.

### `staging`

6. Health check endpoint returns 200.
7. **Full** E2E suite from `/test` passes against the staging URL.
8. No new `ERROR` level log entries in the first 5 minutes.
9. Confirm monitoring dashboards show healthy baseline.

### `prod`

6. Health check endpoint returns 200.
7. Primary user journey works end-to-end (`browser_subagent`).
8. No new `ERROR` level log entries in the first 5 minutes.
9. Confirm monitoring dashboards show **healthy baseline**:
   - [ ] Error rate at or below pre-deploy levels.
   - [ ] Latency within expected percentiles.
   - [ ] Resource usage (CPU, memory) stable.

## Phase 6: Failure Protocol

10. If any verification check fails:
    - **`local`**: Fix and re-run.
    - **`dev`**: Rollback recommended; fix and redeploy.
    - **`staging` / `prod`**: Execute the rollback procedure immediately.
    - Use the `diagnose-bug` skill to investigate.
    - Re-enter `/build` → `/test` → `/deploy` cycle.

---

## Rules

| Rule | Description |
|------|-------------|
| **Environment required** | Always resolve to `local`, `dev`, `staging`, or `prod` — no ambiguous deploys. |
| **Never skip tests** | Deployment must not proceed if required test tiers are failing (unless `/skip` emergency). |
| **Observe after deploy** | Post-deploy monitoring is not optional — depth scales with environment risk. |
| **Rollback-ready** | `staging` and `prod` must have a documented rollback procedure before execution. |
| **Propagation-aware** | Always wait for CDN/registry propagation before running smoke tests. |
| **Staging = prod rehearsal** | Staging runs the full E2E suite — it is the final gate before production. |
| **Prod = max ceremony** | Production deploys require full observability audit, all test tiers, and extended monitoring. |
