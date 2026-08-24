---
name: review-code
description: Use when asked to do code review, review code
disable-model-invocation: true
---

# Code review

Start by inspecting the diff (staged changes by default). Systematically review
code changes for correctness, architecture, security, performance, maintainability,
and test quality. Distinguish blocking defects from optional suggestions. Do not
expose discovered secrets in the review output.

## Rules

**Categorization**

- `❌ bug:` — broken behavior, vulnerability, will cause incident
- `⚠️ risk:` — might work but fragile (race, missing null check, swallowed error)
- `📝 nit:` — style, naming, micro-optim. Non-blocking

**What not to do**

- Present hypothetical concerns as findings without a concrete failure scenario
- Repeat the same root cause across multiple findings
- Review unrelated pre-existing code unless the change exposes or worsens the issue
- Guess, assume or speculate. If unsure, state it clearly. **Don't invent problems**

**What to do**

- Show exact line numbers
- Show exact symbol/function/variable names in backticks
- Add clear problem description and concrete failure scenario
- Present suggested fix if obvious

## Output

List findings to user in order of severity. Number each finding sequentially using
its severity label, for example, `1. ❌ bug:`, `2. ⚠️ risk:`, and `3. 📝 nit:`.
Include clear explanation of where and why each issue occurs. If no issues are
found, tell the user that.
