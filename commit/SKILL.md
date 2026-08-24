---
name: commit
description: Use when asked to commit or create a commit message
disable-model-invocation: true
---

# Git commit message skill

## Inspect

Run `git diff --staged`. If nothing is staged, fall back to `git diff`.

## Message

Base the message on the actual diff, not just filenames. If it contains
unrelated changes, suggest splitting it; otherwise write a message that
honestly covers the combined change.

## Format

```text
Imperative subject

Optional body wrapped at 72 chars. Max 1 paragraph if possible.
```

### Rules:

- Use imperative mood: `Fix cache invalidation bug`
- Do not end the subject with a period
- Aim for 50 char subject with 72 char hard cap
- Prefer using only the subject. Add body only when title can't accurately describe what was done.

## Verify

Write the complete proposed message to `.git/COMMIT_EDITMSG`, using a
heredoc so that hard newlines are preserved:

```sh
cat >.git/COMMIT_EDITMSG <<'EOF'
Subject line here

Body wrapped with hard newlines at or before column 72.
EOF
```

Mechanically reject lines longer than 72 characters:

```sh
awk 'length($0) > 72 {
  printf "Line %d is %d characters\n", NR, length($0)
  invalid = 1
}
END { exit invalid }' .git/COMMIT_EDITMSG
```

Do not present or commit the message unless this command succeeds.

## Validate

Show the verified title and body to the user and ask if they are happy
with it. If not, make requested changes and repeat verification before
presenting it again.

## Commit

Once validated, commit directly from the file:

```sh
git commit -F .git/COMMIT_EDITMSG
```
