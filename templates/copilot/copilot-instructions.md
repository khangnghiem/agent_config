# GitHub Copilot Instructions Template

> **Usage:** Copy this file to `.github/copilot-instructions.md` in your repository.
> Customise each section marked with `TODO`.

---

## Project Overview

<!-- TODO: Replace with a 2-3 sentence description of your project. -->
This is a [TODO: type of project] built with [TODO: main technology stack].
Its primary purpose is [TODO: describe the core functionality].

## Coding Standards

- Follow the conventions in `rules/general/coding-standards.md`.
- <!-- TODO: Add any project-specific standards here. -->

## Language & Framework Rules

- <!-- TODO: Reference the relevant language rule file, e.g. rules/languages/python.md -->
- <!-- TODO: Reference the relevant framework rule file, e.g. rules/frameworks/fastapi.md -->

## Project Structure

<!-- TODO: Briefly describe the top-level directories and their purpose. -->
```
src/          # Application source code
tests/        # Automated tests
docs/         # Documentation
```

## Testing

- Run tests with: `TODO: add test command`
- Test files live in: `TODO: add test directory`
- <!-- TODO: Describe any specific testing conventions or required coverage thresholds. -->

## Key Conventions

<!-- TODO: List 3-5 project-specific conventions that Copilot should always respect. -->
1. 
2. 
3. 

## Do Not

<!-- TODO: List things Copilot should never do in this project. -->
- Do not commit directly to `main` or `master`.
- Do not add dependencies without updating the dependency lock file.
- <!-- TODO: Add further restrictions. -->
