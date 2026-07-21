---
name: review-code
description: Review code changes systematically for correctness, architecture,
    security, performance, maintainability, and test quality.
disable-model-invocation: true
---

# Code review

Start by inspecting the diff (staged changes by default). Systematically review
code changes for correctness, architecture, security, performance, maintainability,
and test quality. Distinguish blocking defects from optional suggestions. Do not
expose discovered secrets in the review output.

## Rules

**Severity:**

- `❌ bug:` — broken behavior, vulnerability, will cause incident
- `⚠️ risk:` — might work but fragile (race, missing null check, swallowed error)
- `📝 nit:` — style, naming, micro-optim. Non-blocking
- `❓ q:` — genuine question if uncertain or unknown

**Drop:**

- Presenting hypothetical concerns as findings without a concrete failure scenario
- Repeating the same root cause across multiple findings
- Reviewing unrelated pre-existing code unless the change exposes or worsens the issue
- Guessing, assuming or speculating. If unsure, state it clearly and ask. **Don't invent problems**

**Keep:**

- Exact line numbers
- Exact symbol/function/variable names in backticks
- Concrete fix or clear description
- The _why_ if the fix isn't obvious from the problem statement

## Output

List findings to user in order of severity. Include clear explanation of where and
why each issue occurs. If no issues found, tell the user that. Don't manufacture
nits or hypotheticals just to seem thorough.
