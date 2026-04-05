# TypeScript Rules

Rules specific to TypeScript projects.

## Style

- Follow the [Google TypeScript Style Guide](https://google.github.io/styleguide/tsguide.html) unless overridden here.
- Use `eslint` + `prettier` for linting and formatting.
- Use single quotes for strings unless the string contains single quotes.
- End every statement with a semicolon.

## Types

- Always declare explicit return types for exported functions.
- Prefer `interface` for object shapes that may be extended; use `type` for unions, intersections, and aliases.
- Avoid `any`; use `unknown` when the type is genuinely unknown and narrow it before use.
- Enable `strict` mode in `tsconfig.json`.

## Imports

- Use named exports; avoid default exports except for React components.
- Use path aliases (configured in `tsconfig.json`) instead of deep relative paths.

## Patterns

- Use `const` by default; only use `let` when reassignment is required.
- Prefer `async/await` over raw Promises for async code.
- Use optional chaining (`?.`) and nullish coalescing (`??`) over manual null checks.
- Avoid non-null assertion (`!`) unless the value is guaranteed to be defined.

## React (when applicable)

- Prefer function components with hooks over class components.
- Keep components small and composable.
- Extract complex logic into custom hooks.
