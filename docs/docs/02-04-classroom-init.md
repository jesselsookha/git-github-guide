# 02-04 — GitHub Classroom: When You Initialised Instead of Cloning

❈ Collaboration

This document addresses a very specific and common scenario:

You accepted a GitHub Classroom assignment.
But instead of cloning the repository, you created your project locally and ran `git init`.

Now your work exists on your machine — but it is not connected to the Classroom repository in the way it needs to be.

Do not panic.

This can almost always be fixed. The approach depends on how far along your project is, and this document covers both paths clearly.

---

## I. Core Concept — What Went Wrong?

Let us restate the rule from 02-03:

**You initialise what you create.**
**You clone what already exists.**

In a GitHub Classroom workflow, the repository already exists before you touch anything. It was created the moment you accepted the assignment link. It belongs to the organisation. It has its own history — even if that history is minimal.

When you ran `git init`, you created a completely separate, independent repository on your machine. That local repository has no knowledge of the Classroom repository. It does not share its history. It was not cloned from it.

You now have:

- A **local repository** — created by you, on your machine, tracking your project files
- A **remote repository** — created by GitHub Classroom, living in the organisation, waiting to receive your work

These two repositories are unrelated. Git sees them as two completely independent histories.

This is the same structural situation described in 02-02, but with a more serious consequence: in 02-02, the conflict was a minor inconvenience you created yourself. Here, working in the wrong repository means your academic submission is going to the wrong place — or nowhere at all.

---

## II. How to Recognise This Situation

Several signs indicate this has occurred:

- You remember running `git init` after accepting the assignment
- Your lecturer has mentioned they cannot see your commits in the Classroom organisation
- Push fails with a rejection message even after you connected a remote
- Running `git remote -v` shows either nothing, or a URL that does not belong to the organisation

If `git remote -v` returns no output:

```
(no output)
```

You have never connected to the Classroom repository at all. Your local repository is entirely disconnected.

If `git remote -v` returns a URL and push still fails with:

```
error: failed to push some refs
hint: Updates were rejected because the remote contains work that you do not have locally.
```

You connected the remote, but the histories are diverging — your local commits and the remote's commits have different starting points.

Both situations are recoverable. The correct path depends on how much work you have done locally.

---

## III. Scenario A — Small Project, Early Stage

◼ Beginner

If your project is still small — few files, one or two commits, nothing you cannot re-create in a few minutes — the cleanest solution is to start fresh in the correct repository.

**Steps:**

I. **Back up your current project folder.** Copy it to a different location on your machine — a folder outside the current project directory. This ensures your work is safe before you delete anything.

II. **Delete the original project folder**, including its `.git` directory. You are removing the incorrectly initialised repository entirely.

III. **Return to GitHub Classroom.** Open the Classroom repository in your browser and copy its URL.

IV. **Clone the repository correctly:**

```bash
git clone <classroom-url>
```

V. **Open the cloned folder.** It will initially be empty or contain only the template files provided by the assignment.

VI. **Copy your work files into this cloned folder.** Move your project files from the backup into the correct repository folder.

VII. **Stage, commit, and push:**

```bash
git add .
git commit -m "Add initial project files"
git push
```

Your work is now inside the correct Classroom repository, with a clean history starting from the legitimate submission space.

This is the safest and cleanest approach for beginners. The minor cost is re-adding files; the benefit is a repository structure that is correct from the beginning.

---

## IV. Scenario B — Significant Work Already Done

◆ Intermediate

If you have been working for some time — multiple commits, substantial development, work you cannot reasonably recreate — you do not need to start over. The repositories can be connected and their histories merged.

### Step I — Add the Correct Remote

Inside your current project folder, add the Classroom repository as the remote:

```bash
git remote add origin <classroom-url>
```

If `origin` already exists but points to the wrong URL:

```bash
git remote remove origin
git remote add origin <classroom-url>
```

Verify:

```bash
git remote -v
```

Both fetch and push URLs should now show the Classroom organisation URL.

---

### Step II — Pull the Remote History

The Classroom repository has its own history — even if it only contains an initial commit or template files. Pull that history down and merge it with yours:

```bash
git pull origin main --allow-unrelated-histories
```

This is the same flag introduced in 02-02. It explicitly tells Git that the two histories have no shared ancestor and instructs it to merge them anyway.

If the merge completes without conflicts, Git creates a merge commit that links both histories. Your local commits and the Classroom repository's commits are now part of the same timeline.

If conflicts occur, resolve them as described in 02-02 — open the conflicted files, remove the conflict markers, choose or combine the content, then stage and commit.

---

### Step III — Push

Once the histories are unified:

```bash
git push -u origin main
```

Your work is now correctly connected to and visible inside the Classroom repository. From this point forward, your standard add → commit → push workflow applies normally.

---

## V. Why This Happens — Understanding the Structure

It is worth understanding structurally why `git init` creates this problem, not just that it does.

**The Classroom repository** was created by GitHub inside an organisation. It has at least one branch (`main`) and possibly an initial commit or template files. Its history has a defined starting point.

**Your locally initialised repository** was created on your machine by `git init`. It has a completely independent starting point — its own root commit with no connection to the Classroom repository.

These two repositories share no ancestor commit anywhere in their history chains.

Git's merge model requires a common ancestor to reconcile differences. Without one, it cannot determine how the two histories relate to each other. Rather than guess, it refuses to merge automatically.

That refusal is protection, not punishment.

`--allow-unrelated-histories` is the explicit override that says: *"I understand there is no shared ancestor. Merge these histories and create a new common point."*

---

## VI. A More Serious Mistake — Nested Repositories

▲ Advanced

There is a variation of this problem that is more difficult to diagnose.

Sometimes a student will:

I. Clone the Classroom repository correctly
II. Open their IDE and begin working
III. Accidentally run `git init` from inside the cloned project folder

This creates a repository *inside* a repository — a `.git` folder nested inside the existing `.git` structure of the cloned repository.

Symptoms:

- `git status` behaves unexpectedly or shows an empty staging area despite file changes
- Pushes fail for reasons that are not immediately obvious
- The commit history appears disconnected from the remote

**How to detect it:**

Navigate into subdirectories of your project and look for unexpected `.git` folders. A correctly cloned repository should only have one `.git` folder — at the root level.

On Windows, you may need to enable "Show hidden items" in Windows Explorer.

On macOS:
```bash
find . -name ".git" -type d
```

This lists all `.git` directories within the current folder. If more than one appears, a nested repository exists.

**How to fix it:**

Delete only the **inner** `.git` folder — the one that was created by `git init` inside the already-cloned repository. Do not delete the outer `.git` folder created by the original clone.

After deleting the inner folder:

```bash
git status
```

This should now behave correctly, reflecting the proper state of the original cloned repository.

---

## VII. Academic and Institutional Implications

❈ Collaboration

This is not purely a technical matter.

GitHub Classroom repositories track:

- Every commit, including its exact timestamp
- The contributor identity attached to each commit
- The full development history from first commit to submission

If you work in the wrong repository — whether a personal repository or a locally initialised one that was never properly connected — none of that tracking applies to the correct place.

The consequences:

- Your lecturer cannot verify your development process because the commits do not appear in the organisation
- Your commit history, even if it reflects genuine work, cannot be validated as belonging to the correct submission
- Academic integrity review becomes more complicated, not because you did something wrong, but because the evidence of your process is in the wrong location

Working in the correct repository protects you. It creates a verifiable record that your work was done, when it was done, and by whom. That record is the evidence that supports academic assessment — and the absence of it creates problems that are difficult to explain after a deadline.

---

## VIII. Prevention — The One Rule to Remember

Before typing a single Git command after accepting a Classroom assignment, ask one question:

**Did I create this repository myself?**

If yes → `git init`
If no → `git clone`

For every Classroom assignment, the answer is always **no** — the repository was created by GitHub when you accepted the link.

This single question, asked consistently, prevents every variation of the problem described in this document.

---

## IX. Summary

| Situation | Solution |
|---|---|
| ◼ Small project, early stage | Backup → Delete → Clone properly → Copy files back in |
| ◆ Significant work done | Add correct remote → Pull with `--allow-unrelated-histories` → Push |
| ▲ Nested repository detected | Find and delete inner `.git` only → Verify with `git status` |

The goal is not simply to make the push work.

The goal is to understand why it failed — so that you do not repeat the mistake, and so that the repository structure you submit reflects genuine, correctly tracked development.

Once you understand the rule — you clone what already exists — every Classroom workflow becomes straightforward.

---

Proceed to:

→ 02-05 — Common Misconceptions and Conflict Prevention
