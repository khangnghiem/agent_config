# Philosophy

This document explains the principles behind the Agent Playbook — the _why_ behind every workflow in this repository.

## Core Belief

**AI coding assistants are only as good as their instructions.** Without structured workflows, agents produce inconsistent, hard-to-verify output. With them, agents become reliable collaborators that follow engineering discipline.

## The 6-Step Lifecycle

Every feature moves through a deliberate sequence:

```
/research → /spec → /design → /build → /test → /deploy
```

Each step has a clear input, output, and verification gate. Skipping steps is allowed — but never by accident. This linearity prevents the "jump straight to code" anti-pattern that causes rework.

## Observability-Driven Development (ODD)

Traditional development treats logging and monitoring as afterthoughts. ODD makes them **first-class citizens**:

- **Structured logging** is written _during_ `/build`, not bolted on later.
- **Drill-down alerting** is configured _during_ `/test`, not after production incidents.
- Logs are the **supervisor** — they tell you what the code _actually did_, not what you _think_ it did.

When an agent builds code with ODD, every function emits traceable events. Debugging becomes log querying, not guesswork.

## Test-Driven Development (TDD)

The `/build` workflow enforces Red-Green-Refactor:

1. **Red** — Write a failing test that defines the expected behavior.
2. **Green** — Write the minimum code to pass the test.
3. **Refactor** — Clean up while keeping tests green.

This isn't dogma — it's a forcing function. It ensures agents write _verifiable_ code, not just _plausible_ code.

## Impact × Autonomy Ranking

Every suggestion, whether from `/advise`, `/review`, or `/research`, is ranked on two axes:

- **Impact** — How much does this improve the project? (🔴 Low → 🟢 High)
- **Autonomy** — Can the agent do this alone, or does it need human decisions? (🤖 Full → 🧑‍💻 Guided → 🔄 Interactive)

The product of these two values determines priority. High-impact, fully-autonomous improvements ship first. This prevents agents from spending time on low-value work or blocking on decisions they can't make.

## Convention Over Configuration

The `.agents/` folder is a convention, not a framework:

- **No runtime dependencies.** It's just markdown files.
- **No lock-in.** Works with any AI coding assistant that reads project files.
- **No magic.** Every workflow is a readable, editable document.

You don't install anything. You drop in a folder and start typing slash commands.

## Design Constraints for Workflows

When writing or modifying workflows, follow these principles:

1. **Under ~100 lines.** If a workflow is longer, it's doing too much.
2. **Phase-driven.** Clear numbered steps with distinct inputs and outputs.
3. **Tool-driven output.** Use `generate_image` for visuals, not ASCII art. Use tables for structured data, not prose.
4. **Verification gates.** Every workflow should end with a way to confirm the work is correct.
5. **No filler.** Reference files and lines directly. Skip preamble.
