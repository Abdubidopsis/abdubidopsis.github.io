# Git Status, Commit, and Push Guide

This guide shows how to check whether your repository is up to date, and when you should commit or push.

## 1. Check sync with remote

Run:

```bash
git fetch
git status -sb
```

How to read the output:

- `## main...origin/main` -> local and remote are synced.
- `## main...origin/main [ahead 1]` -> local has commits not on remote. You need to push.
- `## main...origin/main [behind 2]` -> remote has commits not local. You need to pull/rebase.
- `## main...origin/main [ahead 1, behind 1]` -> both changed. Sync carefully (pull/rebase, resolve conflicts if needed).

## 2. Check if you need to commit

Run:

```bash
git status --short
```

If output has lines like these, you have local changes to commit:

- `M file` (modified)
- `A file` (added)
- `?? file` (untracked)

If no output appears, there are no local file changes.

## 3. Typical workflow

```bash
# Check state
git fetch
git status -sb
git status --short

# If files changed locally -> commit
git add .
git commit -m "Your message"

# If branch is ahead -> push
git push
```

## 4. Extra checks (very useful)

Local commits not on remote (means push needed):

```bash
git log --oneline origin/main..main
```

Remote commits not on local (means pull/rebase needed):

```bash
git log --oneline main..origin/main
```

## 5. Quick decision rules

- Files changed locally? -> Commit.
- Branch ahead of origin? -> Push.
- Branch behind origin? -> Pull/rebase before pushing.
