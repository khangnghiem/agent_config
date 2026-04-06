# agent_config

A curated collection of **AI agent rules, skills, and templates** for use with coding assistants such as GitHub Copilot, Cursor, and Windsurf, strictly adhering to **Antigravity Agent Playbook** conventions.

## Repository Structure (`.agents`/ style)

```
agent_config/
├── .agents/                 # Drop-in folder containing the unified context
│   ├── AGENTS.md            # REFERENCE: Manifest of all workflows/skills
│   ├── rules/
│   │   └── GEMINI.md        # AUTHORITY: Consolidated 3-tier rules (Universal, Stack, Workflow)
│   ├── workflows/           # ACTIONS: Hardened command files (/build, /deploy, etc.)
│   └── skills/              # REFERENCE: Atomic specialized folders containing SKILL.md
└── templates/               # (Legacy/Pointers) Configuration stubs pointing to .agents/rules/GEMINI.md
```

## Quick Start

1. **Pick your assistant** – Browse `templates/` for the minimal configuration file that matches your AI coding tool.
2. **Copy the structure** – Map the `.agents/` directory into the root of your project.
3. **Absorb Rules** – Instead of sprawling `.cursorrules`, everything is centralized natively in `.agents/rules/GEMINI.md`.
4. **Trigger Workflows** – Use slash commands based on the action scripts in `.agents/workflows/` (e.g. `/build`).
5. **Utilise Skills** – Sub-agents will automatically refer to specialized `.agents/skills/<skill>/SKILL.md` folders when undertaking defined tasks.

## Contributing

Contributions are welcome! Please:

- Use **Phase-driven architecture** for Workflows (`.agents/workflows/*.md`).
- Ensure all skills are a directory containing `SKILL.md`.
- Keep the `.agents/rules/GEMINI.md` lean using the 3-Tier Rule System. 
