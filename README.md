# agent_config

A curated collection of **AI agent rules, skills, and templates** for use with coding assistants such as GitHub Copilot, Cursor, and Windsurf.

## Repository Structure

```
agent_config/
├── rules/                   # Behavioural rules and coding standards
│   ├── general/             # Language-agnostic rules
│   ├── languages/           # Language-specific rules (Python, TypeScript, …)
│   └── frameworks/          # Framework-specific rules (FastAPI, React, …)
├── skills/                  # Reusable agent skills (prompt instruction sets)
└── templates/               # Ready-to-use agent configuration templates
    ├── copilot/             # GitHub Copilot (.github/copilot-instructions.md)
    ├── cursor/              # Cursor (.cursorrules)
    └── windsurf/            # Windsurf (.windsurfrules)
```

## Quick Start

1. **Pick your assistant** – Browse `templates/` for the configuration file that matches your AI coding tool.
2. **Copy the template** – Place it in the location indicated at the top of the file (e.g. `.github/copilot-instructions.md`).
3. **Add rules** – Copy or reference the relevant files from `rules/` into the template.
4. **Add skills** – Copy or reference the relevant files from `skills/` to teach the agent specific tasks.
5. **Customise** – Replace every `TODO` placeholder with project-specific content.

## Contents

### Rules

| File | Description |
|------|-------------|
| `rules/general/coding-standards.md` | Universal coding standards (quality, comments, testing, security) |
| `rules/languages/python.md` | Python style, typing, and best-practice rules |
| `rules/languages/typescript.md` | TypeScript style, types, and React conventions |
| `rules/frameworks/fastapi.md` | FastAPI project structure, API design, and testing rules |

### Skills

| File | Description |
|------|-------------|
| `skills/write-unit-tests.md` | Generate comprehensive unit tests |
| `skills/code-review.md` | Perform structured, actionable code reviews |
| `skills/generate-api-docs.md` | Produce REST API documentation from source code |

### Templates

| File | Tool | Target path |
|------|------|-------------|
| `templates/copilot/copilot-instructions.md` | GitHub Copilot | `.github/copilot-instructions.md` |
| `templates/cursor/cursorrules.md` | Cursor | `.cursorrules` |
| `templates/windsurf/windsurfrules.md` | Windsurf | `.windsurfrules` |

## Contributing

Contributions are welcome! Please:

- Add new rules under the appropriate `rules/` subdirectory.
- Add new skills as self-contained Markdown files in `skills/`.
- Add new templates under `templates/<tool-name>/`.
- Keep files focused and well-documented.
