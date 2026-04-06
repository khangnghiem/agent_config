---
description: Document repeated mistakes made by AI Agents and prevent recursion.
---

// turbo-all

# /learn - Self-Correction & Metacognition

$ARGUMENTS

If `$ARGUMENTS` is provided, scope the learning to that topic.
Otherwise, use the last major bug or interaction deviation in the current context.

Be concise. Do not guess.

## Phase 1: Mining the Trajectory

Analyze the current conversation or the specific mistake just resolved:
1. What was the **intended** action?
2. What action was **actually** performed (the hallucination or error)?
3. What contextual rule or constraint was missing that allowed this mistake?

## Phase 2: Formulate the Constraint

Synthesize the learning into a single, generic operational constraint.
- **Good:** "Always use `replace_file_content` instead of `sed` in bash for multi-line YAML edits."
- **Bad:** "I need to fix the spaces in `ci.yml` line 42."

Format the constraint as:
> **CONSTRAINT:** Do NOT [anti-pattern], ALWAYS [correct pattern] when working on [context].

## Phase 3: Codify the Learning

Append the new constraint to the project's permanent memory (e.g., `GEMINI.md`, `.cursorrules`, or the relevant project instruction document). 
Update the relevant section of that document directly with your editing tools.

Do exactly what is formulated in Phase 2. Present the final rule that was successfully saved to the user.
