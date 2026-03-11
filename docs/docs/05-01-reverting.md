# 05-01 — Reverting and Inspecting History

◆ Intermediate

Git is often described as a time machine for code.

The description is apt — but it undersells the precision involved. A time machine takes you somewhere and brings you back. Git's history model is more specific than that: every commit is a permanently recorded snapshot, every snapshot is addressable by its unique hash, and every transition between states is a deliberate act that either preserves the existing record or modifies it.

Understanding this distinction — between operations that preserve history and operations that rewrite it — is the difference between using Git's recovery capabilities confidently and using them fearfully. Once the model is clear, these commands become tools for control rather than sources of anxiety.

This document explains how to undo changes safely, how to inspect earlier states of a project, and what happens at a technical level when you do either.

---

## I. Core Concept — Revert vs Reset

◼ Beginner

Students encountering Git recovery for the first time often confuse `git revert` and `git reset`. They are not variations of the same command — they operate on fundamentally different principles and have entirely different consequences for shared repositories.

### `git revert` — Undo by Addition

`git revert` creates a **new commit** whose effect is the inverse of the commit you are targeting. The original commit remains in history, unchanged. A new commit is added that cancels its changes.

```
Before:  A → B → C   (C introduced a bug)
After:   A → B → C → C'  (C' undoes C's changes)
```

The history is preserved. Anyone who has already cloned or pulled the repository sees an accurate record of what happened: a change was made, then it was undone. The reasoning is visible. The timeline is intact.

This is why `git revert` is safe for collaboration — it adds to history rather than rewriting it. Other contributors are not affected.

### `git reset` — Undo by Removal

`git reset` moves the branch pointer backwards, discarding commits from the visible history. The commits do not disappear immediately — they remain in the reflog (covered in 05-02) — but they are no longer part of the branch's forward history.

```
Before:  A → B → C   (main points to C)
After:   A → B        (main now points to B; C is abandoned)
```

The commit C is no longer reachable from `main`. If this is a local-only change that has not been pushed, this is recoverable and sometimes appropriate. If C has already been pushed to a shared remote, `git reset` creates a divergence between your local history and the remote — which will require a force push to resolve, overwriting the remote's history.

**In shared repositories, `git reset` is dangerous.** It rewrites the history that other contributors have already received. Force-pushing a reset branch tells every contributor who has pulled from that branch that the history they have is wrong.

### The Rule

- For undoing changes in a shared repository: **use `git revert`**
- For discarding local, unpushed work during development: `git reset` has appropriate uses, but requires understanding what is being discarded
- When in doubt: **revert**

---

## II. Identifying the Commit to Revert

◆ Intermediate

Before reverting, locate the specific commit whose changes you want to undo. Every commit in Git has a unique identifier — a SHA-1 hash — that is its permanent address in the repository history.

To view the full commit history:

```bash
git log
```

Example output:

```
commit 3037ae6b2240457095def4bd5c149967bc24f9e5
Author: Jessel <jessel@example.com>
Date:   Wed Mar 4 18:00:00 2026

    Add login validation logic

commit b44d5f3a1c8f2e09d17b3a5c6e8f4d2a1b9c3e7f
Author: Jessel <jessel@example.com>
Date:   Tue Mar 3 14:30:00 2026

    Implement registration form
```

For a condensed view that is easier to scan:

```bash
git log --oneline
```

Example output:

```
3037ae6 Add login validation logic
b44d5f3 Implement registration form
c45f99d Add initial project structure
```

The shortened hash — the first seven characters — is sufficient for most operations. Git will match it to the full hash automatically.

When reading a log to find a commit to revert, read the messages. This is exactly why commit messages must describe what the change did: the moment you need to find and undo a specific change, the quality of your commit messages determines how quickly you can locate it. A history full of "update" and "fix" entries is extremely difficult to navigate under pressure.

---

## III. Reverting a Commit

◼ Beginner

```bash
git revert <commit-hash>
```

Example:

```bash
git revert 3037ae6
```

What happens:

I. Git calculates the inverse of the changes introduced by that commit
II. Git creates a new commit whose content is that inverse — staged automatically
III. A text editor opens for the commit message (pre-filled with "Revert '<original-message>'")
IV. Save and close the editor to complete the revert commit

Your working directory now reflects the project state as if that commit had never been made — but the history shows both the original commit and the revert commit. The record is complete and honest.

### If a conflict occurs during revert

Occasionally, changes made after the target commit are incompatible with reversing it. Git will pause and mark the conflicted sections:

```
<<<<<<< HEAD
Current state of the file
=======
State the revert is trying to restore
>>>>>>> parent of 3037ae6
```

Resolve the conflict as you would any merge conflict: edit the file, remove the markers, keep the correct content, then:

```bash
git add <conflicted-file>
git revert --continue
```

Or, to abandon the revert entirely:

```bash
git revert --abort
```

---

## IV. Understanding the Result

◆ Intermediate

After a successful revert, running `git log --oneline` will show something like:

```
f8c2a1d Revert "Add login validation logic"
3037ae6 Add login validation logic
b44d5f3 Implement registration form
c45f99d Add initial project structure
```

Both the original commit and the revert are visible. Anyone reading the history can see exactly what happened: a change was made, then it was deliberately undone. The revert commit can itself include a note in its body explaining why the change was reversed — which is the complete record a professional team needs for traceability.

This transparency is the reason `git revert` is the preferred tool in collaborative and academic contexts. There is no ambiguity, no altered timeline, no risk to other contributors. The history reflects reality.

---

## V. Inspecting an Earlier Version — Detached HEAD

▲ Advanced

Sometimes the goal is not to undo a commit but simply to look at what the project looked like at an earlier point. Perhaps you need to test whether a bug existed before a certain commit, or you want to review the state of the codebase at a specific milestone.

```bash
git checkout <commit-hash>
```

Example:

```bash
git checkout 3037ae6
```

What happens:

- Your working directory changes to reflect the exact state of the project at that commit
- You enter **detached HEAD state** — HEAD points directly to the commit rather than to a branch

Git will display a warning:

```
Note: switching to '3037ae6'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.
```

### What detached HEAD means

In normal operation, HEAD points to a branch — for example, `main`. When you commit, HEAD moves forward with the branch. Both HEAD and `main` advance together.

In detached HEAD state, HEAD points directly to a specific commit rather than to a branch. If you make new commits in this state, those commits are not attached to any branch. They exist in the repository but are not reachable through normal branch navigation. If you switch away from that commit without creating a branch, those commits become unreachable — and will eventually be garbage-collected by Git.

Detached HEAD is safe for **inspection** — reading files, running the project, testing behaviour. It is not safe for development unless you immediately create a branch:

```bash
git checkout -b review-from-3037ae6
```

This creates a new branch at the current detached commit, attaching HEAD to it. You can now commit safely — the commits belong to this branch and will not be lost.

---

## VI. Returning to the Current State

◼ Beginner

After inspecting an earlier commit or completing any detached HEAD work, return to your working branch:

```bash
git checkout main
```

This moves HEAD back to the tip of `main` — the most recent commit on the main branch. Your working directory is restored to the current project state.

If you created a branch during detached HEAD work and now want to merge it into `main`:

```bash
git checkout main
git merge review-from-3037ae6
```

---

## VII. Example Workflow — Multi-Part Assignment

◆ Intermediate

This scenario illustrates how history inspection serves a practical academic purpose — reviewing the state of a project at each stage without disturbing the current work.

Assume a three-part assignment committed separately:

```
c45f99d Add initial project structure     (Part 1)
b44d5f3 Implement core algorithm           (Part 2)
3037ae6 Add output formatting and tests    (Part 3)
```

To review the project at the end of Part 1 — perhaps to demonstrate Part 1 functionality independently, or to compare against a current bug:

```bash
git checkout c45f99d
```

The project is now in its Part 1 state. Test, examine, take notes.

To return to the current state:

```bash
git checkout main
```

To review Part 2:

```bash
git checkout b44d5f3
```

None of this affects the history or the current state of `main`. It is navigation, not modification.

---

## VIII. Professional Insight — Safe vs Unsafe Operations

▲ Advanced

Understanding which Git operations are safe in shared repositories and which are not is a mark of professional maturity. The distinction is simple in principle:

**Safe operations add to history without altering it:**
- `git revert` — adds a new commit that undoes previous changes
- `git checkout <hash>` — navigates to a previous state without modifying anything
- `git log`, `git diff`, `git show` — read-only inspection

**Unsafe operations in shared repositories rewrite existing history:**
- `git reset --hard` or `git reset --soft` — discards commits from the branch's visible history
- `git rebase` on pushed commits — rewrites commit hashes, invalidating what others have pulled
- `git push --force` — the delivery mechanism for rewritten history; forces the remote to accept a history that differs from what contributors already have

The test for whether an operation is safe: *have other people already received the commits I am about to modify?* If yes, those commits belong to the shared history. Modifying them requires force-pushing, which tells every contributor that the history they have is wrong — and forces them to resolve the divergence.

In professional environments, force-pushing to shared branches is either prohibited by branch protection rules or treated as a significant incident requiring team communication. In academic environments, it is a source of submission problems and integrity questions.

Use the safe tools. Reserve the powerful ones for local branches, and understand their consequences before applying them anywhere shared.

---

## Summary

Reverting is not deleting — it is **undoing with transparency**.
Inspecting history is not modifying — it is **navigating safely**.

Key principles:

- `git log --oneline` to identify commits quickly and clearly
- `git revert <hash>` to undo a commit safely, preserving history
- `git checkout <hash>` to inspect an earlier state without modifying anything
- Create a branch immediately if you plan to commit from a detached HEAD state
- `git checkout main` to return to the current working state
- Avoid `git reset` on pushed commits in any shared repository

These are not emergency commands. They are tools for informed control of a project's history — used routinely by developers who understand what they do, and used rarely by those who do not.

---

Proceed to:

→ 05-02 — Recovery
