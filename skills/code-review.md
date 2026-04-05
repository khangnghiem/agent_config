# Skill: Code Review

## Purpose

Perform a thorough, constructive code review of a diff or set of changed files.

## Instructions

When asked to review code, evaluate the changes along the following dimensions and provide actionable feedback:

### 1. Correctness
- Does the logic produce the expected result for all cases?
- Are edge cases and error paths handled?
- Are there any off-by-one errors, race conditions, or unhandled exceptions?

### 2. Readability
- Are names (variables, functions, classes) clear and descriptive?
- Is the code easy to follow without needing to trace many levels of indirection?
- Are comments present where needed and absent where the code speaks for itself?

### 3. Security
- Is user input validated and sanitised?
- Are there potential injection vulnerabilities (SQL, shell, etc.)?
- Are secrets or credentials accidentally included?

### 4. Performance
- Are there obvious algorithmic inefficiencies (e.g. O(n²) where O(n) is possible)?
- Are expensive operations (network, disk) avoided inside hot loops?

### 5. Tests
- Do tests accompany new or changed functionality?
- Do the tests actually exercise the changed code paths?

## Output Format

Group findings by severity:

- 🔴 **Must fix** – Bugs, security issues, or broken functionality.
- 🟡 **Should fix** – Readability, maintainability, or performance concerns.
- 🟢 **Nice to have** – Minor style or refactoring suggestions.

For each finding, include:
- The file and line number (if applicable).
- A clear description of the problem.
- A concrete suggestion or code snippet for the fix.
