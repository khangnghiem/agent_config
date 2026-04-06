# agent_config

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Workflows](https://img.shields.io/badge/workflows-9-brightgreen.svg)](.agents/workflows/)
[![Convention](https://img.shields.io/badge/convention-.agents%2F-purple.svg)](.agents/)

A curated collection of **AI agent workflows and templates** for use with coding assistants such as GitHub Copilot, Cursor, and Windsurf — built on the **Agent Playbook**.

> **How it works:** Drop the `.agents/` folder into any project. Your AI assistant reads the workflow files and responds to slash commands (e.g. `/build`, `/test`). No plugins or extensions required — just convention-based markdown that any agentic coding tool can follow.

## Repository Structure

```
agent_config/
├── .agents/
│   ├── AGENTS.md            # Manifest of all workflows
│   └── workflows/           # Hardened command files (one per slash command)
```

## What's Included

### Lifecycle Workflows

| Command | Purpose |
|---------|---------|
| `/research` | Gather facts from KIs, codebase, and web; produce ranked suggestions |
| `/spec` | Create technical specifications with ≥3 visual options |
| `/design` | Design UX/visual system with mockups and design artifacts |
| `/build` | Build with TDD (Red-Green-Refactor) and ODD (structured logging) |
| `/test` | E2E tests simulating real user behavior (e.g. Playwright) |
| `/deploy` | Prepare and execute releases (user-configured per project) |

### Support Workflows

| Command | Purpose |
|---------|---------|
| `/review` | Audit recent work, fix urgent issues, suggest improvements |
| `/advise` | Open-ended project analysis with prioritized suggestions |
| `/debug` | Systematic debugging using ODD (Observe → Reproduce → Fix) |

## Quick Start

### The 1-Liner Install

Run this in the root of your project to download and extract the `.agents` folder.

**macOS / Linux (Bash):**
```bash
curl -sL https://github.com/khangnghiem/agent_config/archive/refs/heads/main.tar.gz \
  | tar -xzk -C . --strip-components=1 agent_config-main/.agents
```

**Windows (PowerShell):**
```powershell
Invoke-WebRequest -Uri "https://github.com/khangnghiem/agent_config/archive/refs/heads/main.zip" -OutFile "main.zip"; Expand-Archive -Path "main.zip" -DestinationPath "."; Move-Item -Path "agent_config-main\.agents" -Destination "." -Force; Remove-Item -Recurse -Force "main.zip", "agent_config-main"
```

### Usage

1. **Drop in** — The `.agents/` folder is self-contained. No dependencies.
2. **Trigger workflows** — Type a slash command in your AI coding assistant (e.g. `/build`).
3. **Establish Rules** — Provide project-specific rules in your preferred format (e.g., a root `GEMINI.md`, `.cursorrules`, or `.windsurfrules`). The workflows will automatically enforce them.
4. **Customize** — Edit any workflow file to match your project's stack and conventions.

## Contributing

Contributions are welcome! Please:

- Use **Phase-driven architecture** for workflow files (`.agents/workflows/*.md`).
- Keep workflows under ~100 lines — concise and actionable.
- Test with at least one AI coding assistant before submitting.

## Philosophy

Read [docs/PHILOSOPHY.md](docs/PHILOSOPHY.md) to understand the principles behind ODD, TDD, Impact×Autonomy ranking, and the 6-step lifecycle.

## License

[MIT](LICENSE)
