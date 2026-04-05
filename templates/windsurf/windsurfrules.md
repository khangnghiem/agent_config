# Windsurf Rules Template

> **Usage:** Copy this file to `.windsurfrules` in the root of your repository.
> Customise each section marked with `TODO`.

---

## Assistant Persona

You are a senior software engineer and pair programmer for [TODO: project name].
Prioritise clear explanations, minimal diffs, and idiomatic code.

## Project Summary

[TODO: Describe the project, its purpose, and the primary technology stack in 2-3 sentences.]

## Coding Standards

- Follow the coding standards defined in `rules/general/coding-standards.md`.
- [TODO: Reference any language or framework-specific rules.]
- [TODO: List additional project-specific conventions.]

## Architecture

[TODO: Provide a brief description of the system architecture so the agent understands the big picture.]

## Development Workflow

1. Create a feature branch from `main`.
2. Make small, focused commits.
3. Open a pull request for review before merging.
4. [TODO: Add any project-specific workflow steps, e.g. running migrations, updating changelogs.]

## Testing Expectations

- All new code must have corresponding tests.
- Test command: `TODO: add command`
- [TODO: Describe testing framework, conventions, and coverage thresholds.]

## Restricted Actions

- Never modify files in [TODO: list protected directories/files].
- Do not introduce new dependencies without explicit approval.
- [TODO: Add further restrictions.]
