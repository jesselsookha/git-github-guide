# 05-02 — Recovery

◆ Intermediate

Git is resilient.

This is not a marketing claim — it is a design property. Git's internal architecture makes it extremely difficult to permanently lose committed work. The mechanisms that prevent accidental loss are not optional features or safety modes: they are built into how the repository stores and references its history. Understanding them transforms Git recovery from a stressful emergency into a calm, procedural process.

The scenarios in this document — accidentally discarded commits, detached HEAD state, pushes that did not complete as expected — are all recoverable. In most cases, the work was never truly lost. It was simply no longer reachable through normal navigation. The tools described here restore that reachability.

---

## I. Core Concept — What Is HEAD?

◼ Beginner

To understand recovery in Git, you must first understand HEAD.

**HEAD** is a pointer — a reference that Git maintains to tell you and itself where you currently are in the repository history.

In normal operation:

- HEAD points to your current branch (e.g., `main`)
- When you commit, the branch advances — and HEAD moves with it
- HEAD always reflects the tip of whatever branch you are on

The `git status` command always shows where HEAD is:

```bash
git status
```

Example output in a normal state:

```
On branch main
Your branch is up to date with 'origin/main'.
nothing to commit, working tree clean
```

The first line — *"On branch main"* — tells you that HEAD is pointing to the `main` branch, which is pointing to its most recent commit.

HEAD is your position marker in the commit graph. Recovery, in most cases, is the act of moving HEAD — deliberately — to the position where your work can be found.

---

## II. Detached HEAD State — What It Is and Why It Happens

◆ Intermediate

Detached HEAD state occurs when HEAD points directly to a specific commit rather than to a branch.

This happens when:

- You check out a specific commit hash: `git checkout 3037ae6`
- You check out a tag: `git checkout v1.0`
- You arrive at an earlier commit via certain rebase or recovery operations

Git warns you immediately when this happens:

```
Note: switching to '3037ae6'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>
```

The critical implication: **any commits made in detached HEAD state are not attached to any branch.** They exist in the repository's object storage, but they are not reachable through any branch reference. If you navigate away from the detached commit without creating a branch, those commits become unreachable — and Git's garbage collection will eventually remove them.

`git status` in detached HEAD state:

```
HEAD detached at 3037ae6
nothing to commit, working tree clean
```

The phrase *"HEAD detached at 3037ae6"* is the signal. You are on a commit, not a branch.

### How to recover from detached HEAD safely

If you have made commits in detached HEAD state and want to keep them:

```bash
git checkout -b recovered-work
```

This creates a new branch at the current commit, attaching HEAD to it. Your commits now belong to this branch and are fully protected.

If you have not made any commits and simply want to return to your previous branch:

```bash
git checkout main
```

---

## III. Recovering Deleted Commits — The Reflog

▲ Advanced

The most powerful recovery tool in Git is one that most beginners have never heard of: **the reflog**.

The reflog — reference log — is a local record that Git maintains of every movement of HEAD. Every commit, every checkout, every branch switch, every reset — all of it is recorded in the reflog, independently of the commit history visible through `git log`.

Critically: **the reflog records movements even when commits are no longer reachable through any branch.** This is why commits that appear to have been "deleted" by a reset are almost always recoverable.

```bash
git reflog
```

Example output:

```
3037ae6 HEAD@{0}: commit: Add contact.html
b44d5f3 HEAD@{1}: commit: Add about.html
c45f99d HEAD@{2}: reset: moving to c45f99d
b44d5f3 HEAD@{3}: commit: Add about.html
```

Reading this output:

- `HEAD@{0}` — the most recent HEAD position
- `HEAD@{1}`, `HEAD@{2}` — progressively earlier positions
- Each line shows the commit hash, the operation that moved HEAD, and a description

If a `git reset --hard` discarded commits that you needed, those commits will appear in the reflog. Their hashes are still valid. You can reach them.

### Recovering a lost commit from reflog

I. Run `git reflog` and locate the hash of the commit you want to recover
II. Create a new branch at that commit:

```bash
git branch recovered-branch 3037ae6
```

Or check it out directly to inspect it first:

```bash
git checkout 3037ae6
```

Then, if it contains the work you need, create a branch:

```bash
git checkout -b recovered-branch
```

III. Merge the recovered branch back into `main` if appropriate:

```bash
git checkout main
git merge recovered-branch
```

The work is restored to the normal history.

### Reflog availability

The reflog is local — it exists only on your machine and is not pushed to GitHub. It is also not permanent: by default, Git retains reflog entries for 90 days. This is more than sufficient for recovering from most mistakes, but it means that work which was never committed at all — unsaved file changes, staged but uncommitted files — cannot be recovered through the reflog. **Commit regularly. Stage frequently. The reflog protects committed work; it cannot protect work that was never committed.**

---

## IV. Common Recovery Scenarios

◼ Beginner

### Scenario I — Accidentally Reset a Branch

You ran a reset command and a commit is no longer visible in `git log`:

```bash
git reset --hard HEAD~1
```

This moved the branch pointer back by one commit. The commit still exists in the reflog.

**Recovery:**

```bash
git reflog
```

Find the hash of the commit that was discarded. Then:

```bash
git branch recovered-work <hash>
git checkout main
git merge recovered-work
```

The commit is back in the history.

---

### Scenario II — Made Commits in Detached HEAD State

You checked out an earlier commit to inspect it, made some changes, committed them, and then switched back to `main` before creating a branch. The commits are no longer visible.

**Recovery:**

The commits are in the reflog. Run:

```bash
git reflog
```

Find the hashes of the commits made during detached HEAD state. Then:

```bash
git branch recovered-work <most-recent-detached-commit-hash>
git checkout main
git merge recovered-work
```

---

### Scenario III — Push Appeared to Succeed but Work Is Missing Online

You pushed, the terminal did not show an error, but the commits are not visible on GitHub.

**Diagnosis:**

```bash
git remote -v
```

Confirm the remote URL points to the correct repository — not a personal account, not the wrong organisation repository.

```bash
git log --oneline origin/main
```

This shows the commit history as GitHub sees it. Compare it to your local `git log --oneline`. If they differ, your local commits have not been pushed to the correct remote.

**Recovery:**

If the remote is correct but commits are missing, push again:

```bash
git push origin main
```

If the remote was wrong, correct it and push to the right destination:

```bash
git remote set-url origin <correct-url>
git push origin main
```

Then verify by opening the repository in a browser.

---

### Scenario IV — Accidentally Deleted a Branch

You deleted a branch and realised it contained uncommitted — or committed but unmerged — work.

**Recovery for committed work:**

Committed branches that are deleted still have their commits in the reflog. Run `git reflog` and find the most recent commit on the deleted branch. Then:

```bash
git checkout -b recovered-branch <hash>
```

**Prevention:**

Before deleting any branch, confirm it has been fully merged into its target:

```bash
git branch --merged main
```

This lists branches whose commits are all present in `main`. Branches not on this list still contain unmerged work.

---

## V. Reading Recovery Output

◆ Intermediate

When diagnosing a recovery situation, three commands provide the information needed to act:

**`git log --oneline`** — the visible commit history. Shows what is reachable from the current branch. If a commit is absent from this output, it may still be in the reflog.

**`git reflog`** — the complete movement history of HEAD. Shows everything that has happened locally, including positions that are no longer reachable through branches.

**`git status`** — the current state indicator. Most importantly: whether HEAD is on a branch or detached.

Reading these three outputs together gives a complete picture of where work is, where it was, and how to reach it.

---

## VI. Professional Insight — Recovery in Industry

▲ Advanced

Recovery skills matter in professional environments in proportion to the consequences of failure. A student who loses a local commit recovers and re-does a few hours of work. A professional team that loses commits from a production repository may face service outages, data inconsistencies, or broken releases.

The same tools apply — but the infrastructure around them is more robust:

**Protected branches** prevent accidental resets of `main` entirely. GitHub's branch protection rules can be configured to block any push that would rewrite history, making `git reset` on shared branches physically impossible without administrator intervention.

**Reflog and backup strategies** are documented and practiced. Teams often have runbooks — documented procedures for common recovery scenarios — so that a developer in crisis is not improvising under pressure.

**CI/CD pipelines** mean that even if local commits are lost, the build artifacts generated from those commits may still exist in the pipeline's artifact storage. Deployed code creates a secondary record of what existed.

**Code review history** on GitHub preserves the diff of every merged Pull Request, even if the branch was subsequently deleted. A developer who needs to recover the content of a deleted branch can often find it in the PR history.

The lesson for students: recovery is a skill, not an emergency. Learning it calmly, in a practice environment, builds the reflexes that will serve well when the stakes are higher.

---

## VII. Classroom Activity — Recovery Simulation

❈ Collaboration

**Objective:** Experience and recover from the most common Git recovery scenarios in a controlled, low-stakes environment.

**Setup:** Create a repository with at least four commits — enough history to navigate meaningfully.

**Steps:**

I. Run `git log --oneline` and record all commit hashes

II. Check out the first commit:
```bash
git checkout <first-commit-hash>
```

III. Observe the detached HEAD warning and run `git status` — read the output carefully

IV. Make a small change to any file and commit it:
```bash
git add .
git commit -m "Experimental change in detached HEAD"
```

V. Run `git status` again — observe that you are still in detached HEAD state

VI. Create a branch to preserve the work:
```bash
git checkout -b recovered-experiment
```

VII. Return to `main`:
```bash
git checkout main
```

VIII. Run `git reflog` — trace the sequence of HEAD movements that just occurred

IX. Simulate a reset:
```bash
git reset --hard HEAD~1
```

X. Run `git log --oneline` — observe the missing commit

XI. Use `git reflog` to find and restore it:
```bash
git branch restore-reset-commit <hash-from-reflog>
```

**Reflection:**

- What does HEAD represent, and why is its current position meaningful?
- What is the practical difference between `git log` and `git reflog`?
- In which situations would a committed commit be unrecoverable through reflog?

---

## Summary

Recovery is not panic — it is process.

In the vast majority of scenarios that feel catastrophic, the work is not lost. It is in the reflog, in a detached commit, or in a remote that was not checked. The tools to retrieve it are straightforward once the model is understood.

Key principles:

- HEAD is your position marker — always know where it is before acting
- `git status` shows whether HEAD is on a branch or detached
- `git reflog` shows every position HEAD has been — including apparently lost commits
- Create a branch immediately if you commit in detached HEAD state
- `git reset` on pushed commits is dangerous; use `git revert` instead
- Verify pushes in the browser — terminal confirmation is necessary but not always sufficient

Advanced Git commands build confidence when understood.
They transform mistakes into recoverable situations — and recoverable situations into learning.

---

Proceed to:

→ 05-03 — GitHub Actions
