---
name: Diagnose Bug
description: Perform root-cause analysis using an Observe -> Test -> Fix continuous loop (ODD + TDD).
---

# Skill: Diagnose Bug

## Instructions

When investigating a bug, a failing test, or unexpected system behavior, NEVER guess the fix and immediately overwrite code. Instead, follow this systematic, data-driven approach bridging Observability (ODD) and Testing (TDD).

### Phase 1: Observe (ODD)
1. **Analyze the error**: Look at the error message, stack trace, or failing test output.
2. **Evaluate Logs**: Ask yourself: "Do the current logs give me enough context to understand why this broke?"
   - Read `ERROR` level logs first for the failure point.
   - Read `DEBUG` or `INFO` logs backward to trace the lineage and state leading up to the error.
3. **Inject Temporary Telemetry**: If the existing logs are insufficient, **stop**. Your first code change should be to add temporary verbose logging around the suspected area. Rerun the process to capture the exact state failure.

### Phase 2: Reproduce (TDD)
1. **Write a Regression Test**: Once you understand the root cause from the logs, write a unit or integration test that reliably reproduces the bug (it must fail / show Red).
2. Never skip this step. The test prevents the bug from ever returning.

### Phase 3: Fix
1. **Implement the Fix**: Modify the core logic so the regression test turns Green.
2. **Clean up**: Remove massive temporary debug logs, but **leave behind** valuable, structured `WARN` or `ERROR` logs that would have helped you catch this faster.

## Output Format
When executing this skill, communicate your diagnostics clearly:

1. **Hypothesis**: What you think is wrong based on initial logs.
2. **Observation Step**: What logs you added or read to confirm the state.
3. **The Test**: The failing test case you wrote.
4. **The Fix**: The actual code change.

> [!TIP]
> The defining trait of this skill is discipline. We do not apply quick patches; we observe the system deeply, prove the failure with a test, and cure the root cause.
