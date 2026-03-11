# 07-02 — Cheat Sheet

---

## Purpose

This document is a fast reference for Git commands and workflows.

It is not a substitute for understanding. Every command listed here has a fuller explanation somewhere earlier in this guide — the workflow documents, the concept documents, the glossary. This cheat sheet is for the moment when you understand what you need to do and want the exact syntax without navigating back through the teaching material.

Use it alongside practice, not instead of it. A command you have run ten times with understanding is one you no longer need to look up. This reference exists for the others.

---

## I. Core Workflow — Sequential Reference

◼ Beginner

The fundamental development loop, in order:

```bash
# 1. Start — create or acquire a repository
git init                          # Create new repository in current folder
git clone <url>                   # Copy existing repository from remote

# 2. Configure identity (first time on a machine)
git config --global user.name "Your Name"
git config --global user.email "you@example.com"

# 3. Check current state
git status                        # What is staged, unstaged, untracked
git log --oneline                 # Compact commit history
git branch                        # List branches; * marks current branch

# 4. Make and record changes
git add <file>                    # Stage specific file
git add .                         # Stage all changed and new files
git commit -m "Descriptive message"   # Commit staged files

# 5. Connect to remote (first time, if using git init)
git remote add origin <url>       # Add remote named 'origin'
git branch -M main                # Rename branch to main if needed
git push -u origin main           # Push and set upstream tracking

# 6. Subsequent pushes and pulls
git push                          # Upload new local commits
git pull                          # Fetch remote commits and merge locally
git pull origin main              # Pull from specific remote branch

# 7. Branching
git checkout -b feature-name      # Create branch and switch to it
git switch <branch-name>          # Switch to existing branch
git branch                        # List all branches
git branch -d <branch-name>       # Delete branch (after merge)

# 8. Verify remote
git remote -v                     # Show remote URLs
```

---

## II. Essential Commands — Annotated Reference

◆ Intermediate

### Repository Setup

| Command | What it does |
|---|---|
| `git init` | Creates a new repository in the current folder. Creates the `.git` directory. Use when starting from scratch locally. |
| `git clone <url>` | Copies a remote repository to your local machine — full history included. Configures `origin` automatically. Use when joining an existing project. |
| `git remote add origin <url>` | Connects a local repository to a remote. Run after `git init` when the remote already exists. |
| `git remote -v` | Displays all configured remotes and their URLs. Run this to confirm you are pushing to the correct repository. |
| `git remote set-url origin <url>` | Updates the remote URL without removing and re-adding it. Use when the remote URL changes or was configured incorrectly. |

---

### Staging and Committing

| Command | What it does |
|---|---|
| `git status` | Shows the state of the working directory and staging area — modified, staged, untracked files. Run before every commit. |
| `git add <file>` | Stages a specific file for the next commit. |
| `git add .` | Stages all modified and new files in the current directory and below. |
| `git add -p` | Interactive staging — stages changes in hunks, allowing partial file staging. Useful for separating unrelated changes into separate commits. |
| `git diff` | Shows unstaged changes — differences between working directory and staging area. |
| `git diff --staged` | Shows staged changes — differences between staging area and last commit. |
| `git commit -m "message"` | Creates a commit with all staged changes. Message should describe what changed. |
| `git commit --amend` | Replaces the most recent commit with a new one. Use only before pushing — amending pushed commits requires force push. |

---

### History Inspection

| Command | What it does |
|---|---|
| `git log` | Full commit history — hash, author, date, message. |
| `git log --oneline` | Compact history — one line per commit. Most useful for navigation and copying hashes. |
| `git log --oneline --graph --all` | Visual commit graph across all branches. Shows branch points and merge commits. |
| `git show <hash>` | Shows full details of a specific commit — metadata and diff. |
| `git diff <hash1> <hash2>` | Compares two specific commits. |
| `git blame <file>` | Shows which commit last modified each line of a file — and who made that commit. |

---

### Undoing Changes

| Command | What it does |
|---|---|
| `git restore <file>` | Discards unstaged changes to a file — restores it to the staged or last committed state. Cannot be undone. |
| `git restore --staged <file>` | Removes a file from staging — unstages it without discarding changes. |
| `git revert <hash>` | Creates a new commit that undoes the changes from a specific commit. History preserved. Safe for shared repositories. |
| `git reset --soft HEAD~1` | Moves branch pointer back by one commit. Changes remain staged. Use to recommit differently. |
| `git reset --hard HEAD~1` | Moves branch pointer back by one commit. Changes are discarded. Use only on local, unpushed commits. |

---

### Branching and Merging

| Command | What it does |
|---|---|
| `git branch` | Lists all local branches. `*` marks the current branch. |
| `git branch <name>` | Creates a new branch at the current commit. Does not switch to it. |
| `git checkout -b <name>` | Creates a branch and switches to it in one command. |
| `git switch <name>` | Switches to an existing branch. Modern alternative to `git checkout <name>`. |
| `git merge <branch>` | Merges the specified branch into the current branch. |
| `git branch -d <name>` | Deletes a branch that has been fully merged. |
| `git branch --merged main` | Lists branches whose commits are all present in `main`. Safe to delete. |

---

### Remote Synchronisation

| Command | What it does |
|---|---|
| `git push` | Uploads all new local commits to the configured upstream remote branch. |
| `git push -u origin main` | Pushes and sets the upstream tracking. Required on first push from a new local branch. |
| `git push origin <branch>` | Pushes a specific branch to the remote. |
| `git pull` | Fetches remote commits and merges them into the current branch. |
| `git pull origin main` | Fetches and merges from a specific remote branch. |
| `git fetch` | Downloads remote commits without merging. Allows inspection before integration. |

---

## III. Advanced Commands

▲ Advanced

### History Navigation

| Command | What it does |
|---|---|
| `git checkout <hash>` | Moves to a specific commit in detached HEAD state. Safe for inspection; create a branch before committing. |
| `git reflog` | Shows all HEAD movements — including commits no longer reachable through branches. Essential for recovery. |
| `git bisect start` | Begins a binary search through history to locate the commit that introduced a bug. |

---

### Rewriting History (Local Only)

| Command | What it does |
|---|---|
| `git rebase <branch>` | Reapplies the current branch's commits on top of another branch, creating a linear history. Do not rebase pushed commits. |
| `git rebase -i HEAD~<n>` | Interactive rebase — reorder, edit, squash, or drop the last `n` commits. Use before pushing to clean up a messy working branch. |
| `git commit --amend` | Replaces the most recent commit. Local only — amending pushed commits requires force push and disrupts collaborators. |

---

### Stashing

| Command | What it does |
|---|---|
| `git stash` | Saves uncommitted changes (staged and unstaged) and reverts the working directory to the last commit. Useful when switching branches mid-work. |
| `git stash list` | Shows all stashed changesets. |
| `git stash pop` | Applies the most recent stash and removes it from the stash list. |
| `git stash apply <stash@{n}>` | Applies a specific stash without removing it from the list. |

---

### Selective Integration

| Command | What it does |
|---|---|
| `git cherry-pick <hash>` | Applies the changes from a specific commit onto the current branch. Useful for applying a fix from one branch to another without a full merge. |

---

### Inspection and Search

| Command | What it does |
|---|---|
| `git grep <pattern>` | Searches all tracked files for lines matching a pattern. Faster than filesystem search for code-specific patterns. |
| `git shortlog -sn` | Summarises commit count by author. Useful for contribution visibility. |
| `git tag <name>` | Creates a lightweight tag at the current commit. Used to mark releases. |
| `git tag -a <name> -m "message"` | Creates an annotated tag with a message — the preferred format for releases. |

---

## IV. Extended Command Reference — by Category

The following is organised by Git's own functional groupings. Commands are listed with brief descriptions; fuller explanations are in the glossary (07-03) and throughout the guide.

### Start a working area
- `clone` — Clone a repository into a new directory
- `init` — Create an empty Git repository or reinitialise an existing one

### Work on the current change
- `add` — Add file contents to the index (staging area)
- `mv` — Move or rename a tracked file — Git records the rename rather than treating it as a delete and add
- `restore` — Discard changes in the working directory or unstage files
- `rm` — Remove files from the working tree and from Git tracking

### Examine history and state
- `bisect` — Binary search through history to find which commit introduced a bug
- `diff` — Show differences between commits, or between working directory and staging area
- `grep` — Search tracked files for a pattern
- `log` — Show commit history with metadata
- `show` — Show details of a specific commit, tag, or object
- `status` — Show the current state of the working directory and staging area

### Grow, mark, and tweak history
- `branch` — List, create, or delete branches
- `commit` — Record staged changes as a new commit
- `merge` — Join two or more branches together
- `rebase` — Reapply commits on top of another base commit
- `reset` — Move HEAD and optionally the staging area and working directory to a previous state
- `switch` — Switch branches (modern alternative to `checkout` for branch operations)
- `tag` — Create, list, or delete tags at specific commits

### Collaborate
- `fetch` — Download objects and references from a remote without merging
- `pull` — Fetch from a remote and merge into the current branch
- `push` — Upload local commits to a remote repository

---

## V. Professional Insight — Cheat Sheets in Practice

❈ Collaboration

Every experienced developer uses reference material. The belief that professional competence means having every command memorised is incorrect — and counterproductive. The goal is not memorisation; it is understanding combined with efficient access to syntax.

Professional teams maintain internal cheat sheets and workflow documentation for exactly this reason: to reduce friction for infrequently used but important commands, and to ensure consistency in how common workflows are performed across the team. Onboarding documentation typically includes command references. Team wikis often contain workflow guides specific to the codebase and branching model.

Using a cheat sheet responsibly means knowing *what* you need to do before looking up *how* to do it. The cheat sheet provides syntax; the understanding of when and why comes from practice and the fuller explanations in this guide.

---

## Summary

This cheat sheet covers:

- The complete core workflow in sequential order
- Essential commands annotated with their purpose and appropriate use
- Advanced commands for history navigation, rewriting, stashing, and selective integration
- The extended command reference organised by Git's own functional categories

**The principle for using it well:**

A cheat sheet reinforces fluency. It is the support structure you use while understanding builds — and the reference you reach for quickly when confidence is established and you simply need the exact flag or argument. Use it with that distinction in mind.

---

Proceed to:

→ 07-03 — Glossary
