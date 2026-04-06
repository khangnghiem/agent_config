---
description: Structured suggestions with analysis, tradeoffs, and priorities
---

// turbo-all

# /advise - Smart Suggestions

$ARGUMENTS

If `$ARGUMENTS` is provided, narrow all analysis to that scope (e.g., `/advise testing`, `/advise performance`).
Otherwise, analyze the entire project for open-ended improvement discovery.

## 1. Understand the Context

Before suggesting anything, orient yourself:

- Read root-level files (`README.md`, docs, config) to understand the project.
- Read any files directly related to `$ARGUMENTS`.
- Check relevant **Knowledge Items** for past decisions, rejected approaches, and established patterns.
- Scan recent git history and open TODOs/FIXMEs — don't suggest what's already done or in progress.

### Internal Analysis (not shown to user)

Answer these before generating suggestions:

- What is the project's **current bottleneck**?
- What single change would **10× progress**?
- What's the **riskiest assumption** that hasn't been validated?
- What is the user **not asking about** that they should be?

Use these answers to filter and rank — don't just pattern-match TODOs.

## 2. Categorize & Format Suggestions

**Categories:** 🎯 Quick Win | ✨ Enhancement | 🚀 New Idea | 🔧 Refactor | ⚠️ Risk | 🛠️ Tooling

Use this format for each suggestion:

> ### [Emoji] [Title]
>
> **Impact:** 🔴 Low / 🟡 Medium / 🟢 High
> **Autonomy:** 🤖 Full / 🧑‍💻 Guided / 🔄 Interactive
>
> [2-3 sentence description of what and why]
>
> **Tradeoffs:** ✅ Pro: [benefit] | ⚠️ Con: [risk or cost]
>
> **Depends on:** _(optional)_ #N or [prerequisite]

## 3. Prioritize

- Rank by **Impact × Autonomy** — high-impact items the agent can execute fully go first.
- ⚠️ Risks get priority regardless.
- 🎯 Quick Wins with high impact go next.
- Cap at **5 suggestions max**. Expand all with detail cards.

## 4. Visualize

Generate visuals for any suggestion rated **🟡+ Impact** that changes system structure or user-facing layout.

- **UI / layout**: Use the `generate_image` tool to generate a mockup image. Keep the image intuitive.
- **Architecture / workflow**: Generate an architecture diagram or flowchart.

Attach directly below the relevant suggestion card. Skip for pure config or text-only changes.

## 5. Present and Wait

Start with a summary table for quick comparison:

| #   | Suggestion | Category | Impact   | Autonomy |
| --- | ---------- | -------- | -------- | -------- |
| 1   | [Title]    | 🎯/✨/🚀 | 🔴/🟡/🟢 | 🤖/🧑‍💻/🔄 |

Then list the full detail cards below the table, with visuals where applicable.

Close with your recommendation:

> **💡 My recommendation:** **#N, #N** — [1-sentence reason tied to the bottleneck from Step 1].

---

## Rules & Anti-Patterns

| Rule              | Description                                    |
| ----------------- | ---------------------------------------------- |
| **Context first** | Never suggest without reading relevant context |

| **No auto-implement** | Present and wait for user's pick |
| **Be specific** | Reference actual files, lines, or topics — no generic advice |
| **State dependencies** | If suggestions conflict or depend on each other, say so |
