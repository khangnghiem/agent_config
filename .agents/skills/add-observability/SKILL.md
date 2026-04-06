---
name: Add Observability
description: Inject structured logging, monitoring, and tracing into application code (Observability-Driven Development).
---

# Skill: Add Observability

## Instructions

When asked to "add observability" or inject telemetry into a component, your goal is to ensure the system is completely transparent in production. Treat logs and metrics as first-class citizens, not afterthoughts.

### 1. Structured Logging
- Always use structured logging (e.g., JSON format) rather than raw text strings.
- Pass contextual key-value pairs (e.g., `user_id`, `request_id`, `duration_ms`) instead of string interpolation.
- **Log Levels**:
  - `ERROR`: System is broken, intervention needed. Include stack traces.
  - `WARN`: Unexpected state but the system recovered.
  - `INFO`: Significant lifecycle events (startup, configuration loaded, key transactions).
  - `DEBUG`: Verbose tracing for development/troubleshooting (should be off in production).

### 2. Tracing and Correlation
- Ensure a unique `trace_id` or `correlation_id` is passed through all layers of a request (API gateway -> Controller -> Service -> DB).
- Every log message associated with that request must include this ID.

### 3. Boundary Placement
- Do NOT litter logs inside tight loops or low-level utility functions.
- DO place logs at major service boundaries:
  - Entrance: "Starting process X with parameters Y"
  - Exit: "Completed process X in Z ms"
  - Catch blocks: Catch and log the exact failure context before re-throwing or handling.

### 4. System Metrics (RED / USE)
- Consider how the feature will be monitored on a dashboard:
  - **Rate**: Request/event volume per second.
  - **Errors**: Number of failed requests.
  - **Duration/Latency**: How long the operation took.
- Where appropriate, outline what backend metrics (CPU, Memory) might need correlated monitoring for this feature (especially for AI or data-heavy workloads).

## Anti-Patterns to Avoid
- Logging PII (Passwords, raw healthcare data, exact addresses).
- Empty catch blocks (`try { ... } catch (e) { console.error(e); }`) losing trace context.
- Meaningless logs like "Here 1" or "Done".
