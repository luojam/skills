---
name: commit
description: Use when asked to commit or create a commit
disable-model-invocation: true
---

# Git commit message skill

## Inspect

Run `git diff --staged`. If nothing is staged, stop and tell the user.
Gather relevant repo context as needed, including untracked files.

## Message

Base the message on the diff and known context. State what the change
accomplishes in a short, specific, imperative subject. Default to
subject only. Add a body only when omitting it would lose essential
context, such as a non-obvious reason or constraint. Do not add a body
merely to restate the subject or narrate the diff.

Do not invent intent or benefits. Ask the user when missing context
prevents an accurate description of the change.

Suggest splitting unrelated changes; if kept together, cover each
distinct change.

## Format

```text
Imperative subject

Optional body wrapped at 72 chars. Max 1 paragraph if possible.
```

### Rules:

- Use imperative mood: `Fix cache invalidation bug`
- Do not end the subject with a period
- Aim for 50 char or shorter subject with 72 char hard cap

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
