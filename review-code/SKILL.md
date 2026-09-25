---
name: review-code
description: Use when asked to do code review or to review code
disable-model-invocation: true
---

# Code review

Inspect the requested scope; default to the staged diff. If empty or
unavailable, say so and stop. Systematically review code changes for
correctness, security, and performance. Verify potential findings
against relevant surrounding code, callers, and tests. Do not modify
files.

## Rules

- Report only issues introduced, exposed, or worsened by the changes
- Each finding must be supported by code evidence, have a concrete
  trigger and clearly explained real failure scenario or impact
- Do not report speculative findings
- Report each root cause only once

## Output

Number findings sequentially in order of severity. Each should include:

- Severity (Critical/High/Medium/Low) and short descriptive title
- Short description of real scenario where the issue would happen
- Clear, concise explanation of where and why the issue occurs. Include
  `path:line` and relevant `symbols`

If no issues are found, say so. Briefly mention any gaps or uncertainty.
