---
name: commit
description: Write concise Git commit messages from staged or unstaged Git diffs. Use only when asked to draft, improve, or create a commit message.
---

# Git Commit Message Skill

Inspect the diff first and write a concise message that describes the intent
of the change.

## Inspect the diff

Check staged changes first:

```sh
git diff --staged
```

If nothing is staged, check unstaged changes:

```sh
git diff
```

Base the message on the actual diff, not just filenames. Focus on the
user-visible or developer-visible effect. If the diff contains unrelated
changes, suggest splitting it; otherwise write a message that honestly
covers the combined change.

## Write the message

Use the standard format:

```text
Imperative subject under 50 chars

Optional body wrapped at 72 chars. Explain what changed, why it changed,
and any important behavior, compatibility, testing, or follow-up context.
```

Rules:

- Use imperative mood: `Fix cache invalidation bug`
- Do not end the subject with a period
- Omit the body when the subject is sufficient
- Avoid merely listing changed files

## Verify

Ask the user if they are happy with the commit title and body.
If not, make the changes the user asked for and verify again.
Once verified, commit with the instructions below.

## Commit command

When committing from the shell, preserve newlines with a heredoc:

```sh
git commit -m "$(cat <<'EOF'
Subject line here

Body wrapped at 72 characters when useful.
EOF
)"
```
