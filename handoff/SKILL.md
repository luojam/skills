---
name: handoff
description: Compact the current conversation into a handoff document for another agent to pick up.
disable-model-invocation: true
---

Write a handoff document summarising the current conversation so a fresh agent can continue the work.

Do not duplicate content already captured in other relevant artifacts (specs, plans, ADRs, issues, commits, diffs). Reference them by path or URL instead.

Redact any sensitive information, such as API keys, passwords, or personally identifiable information.
