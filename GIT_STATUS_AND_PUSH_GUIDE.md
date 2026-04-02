# Git Status, Commit, Push, and Sync Guide (Beginner-Friendly)

This guide is for first-time users and daily users. It explains:

- how to check if your local repo is up to date,
- when to commit,
- when to push,
- how to bring online (GitHub) changes into your local computer,
- and what to do if conflicts happen.

## 1. One-time setup (first time only)

Set your name and email once on your computer:

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

Check that it is set:

```bash
git config --global --list
```

## 2. Clone a repo (first time for a project)

```bash
git clone https://github.com/OWNER/REPO.git
cd REPO
```

If the repo already exists on your machine, just enter it:

```bash
cd /path/to/repo
```

## 3. Check current state quickly

```bash
git fetch
git status -sb
git status --short
```

How to read `git status -sb`:

- `## main...origin/main` -> local and remote are synced.
- `## main...origin/main [ahead 1]` -> local has commits not on remote. Push is needed.
- `## main...origin/main [behind 2]` -> remote has commits not local. Pull/rebase is needed.
- `## main...origin/main [ahead 1, behind 1]` -> both changed. Pull/rebase, then push.

How to read `git status --short`:

- `M file` -> modified file.
- `A file` -> staged new file.
- `?? file` -> untracked new file.
- no output -> no local file changes.

## 4. When do you need to commit?

Commit when you changed files locally and want to save a checkpoint in git.

```bash
git add .
git commit -m "Clear message about what changed"
```

You do not need to commit if no files changed.

## 5. When do you need to push?

Push when local branch is ahead of remote (you have local commits not on GitHub).

```bash
git push
```

## 6. If someone changed files online (GitHub), update local

Recommended safe flow:

```bash
git fetch
git pull --rebase
```

Why `--rebase`: cleaner history with fewer merge commits.

## 7. If you have local edits and need to pull first

Option A (if changes are ready): commit first, then pull.

```bash
git add .
git commit -m "WIP before pulling"
git pull --rebase
```

Option B (if changes are not ready): stash, pull, then restore.

```bash
git stash
git pull --rebase
git stash pop
```

## 8. Conflict handling (quick)

If git reports conflicts during rebase/pull:

1. Open files and resolve conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`).
2. Stage resolved files.
3. Continue rebase.

```bash
git add .
git rebase --continue
```

If needed, cancel rebase:

```bash
git rebase --abort
```

## 9. Daily workflow template

```bash
# Start
git fetch
git status -sb

# Bring latest remote updates first if behind
git pull --rebase

# Work on files...

# Save your work
git add .
git commit -m "Describe change"

# Publish
git push
```

## 10. Useful checks

Local commits not on remote:

```bash
git log --oneline origin/main..main
```

Remote commits not on local:

```bash
git log --oneline main..origin/main
```

## 11. Quick decision rules

- Files changed locally? -> Commit.
- Branch ahead of origin? -> Push.
- Branch behind origin? -> Pull/rebase before pushing.
- Ahead and behind? -> Pull/rebase, resolve conflicts, then push.
