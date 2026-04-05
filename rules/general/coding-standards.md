# General AI Agent Rules

Apply these rules in every project unless overridden by more specific rules.

## Code Quality

- Write clear, readable code with self-explanatory variable and function names.
- Prefer explicit over implicit behaviour.
- Keep functions short and focused on a single responsibility.
- Avoid deep nesting; extract helper functions when logic becomes complex.

## Comments & Documentation

- Only add comments when the *why* is not obvious from the code itself.
- Keep docstrings concise and accurate.
- Update existing comments when changing the code they describe.

## Error Handling

- Handle errors explicitly; never silently swallow exceptions.
- Provide meaningful error messages that help diagnose the problem.
- Validate inputs at the boundaries of the system.

## Testing

- Write tests alongside new functionality.
- Favour small, focused unit tests over large integration tests where possible.
- Tests should be deterministic and not depend on external state.

## Security

- Never commit secrets, credentials, or API keys.
- Sanitise all user-supplied input before use.
- Use the least-privilege principle when requesting permissions.

## Version Control

- Write short, imperative commit messages (e.g. `Add user login endpoint`).
- Make small, focused commits that address one concern at a time.
- Reference issue numbers in commit messages when applicable.
