# 07-01 — Decision Trees

---

## Purpose

Decision trees provide structured guidance when facing uncertainty in a Git workflow.

The instinct when something goes wrong with Git — particularly early in the learning curve — is to try things at random, or to ask for help without first attempting to diagnose the problem independently. Both responses are understandable. Neither builds the diagnostic reasoning that eventually makes Git feel manageable.

Decision trees interrupt that instinct with a question. The question has a small number of answers. Each answer leads to a specific action or the next question. The path from uncertainty to correct action is short and followable.

This document covers the four scenarios that produce the most confusion and the most avoidable errors:

- Repository initialisation versus cloning
- Push rejections
- Merge conflicts
- Submission verification

Use these trees when uncertain. Use the accompanying explanations to understand why each path leads where it does.

---

## I. Decision Tree — Init vs Clone

◼ Beginner

**Starting question:** Does a repository for this project already exist on GitHub or GitHub Classroom?

```
Does a repository already exist on GitHub / Classroom?
│
├── NO ──► git init
│          Then: git remote add origin <url>
│                git branch -M main
│                git push -u origin main
│
└── YES ──► git clone <url>
            Remote is already configured. Begin working.
```

**Follow-up — after init:** If you initialised locally and now need to connect to an existing remote, run `git remote add origin <url>`. The remote already exists; you are connecting your local repository to it. Do not run `git clone` as well — the repository is already on your machine.

**Follow-up — after clone:** The remote is configured automatically by `git clone`. Run `git remote -v` to verify it points to the correct repository before doing any other work.

**The rule that prevents most confusion:**

*Init creates. Clone copies. Never run both on the same project.*

Running `git init` inside a folder that was already created by `git clone` creates a nested `.git` directory — a repository inside a repository. This produces confusing behaviour and is difficult to untangle. If you suspect this has happened, run:

```bash
find . -name ".git" -type d
```

If more than one `.git` directory appears, the inner one must be deleted:

```bash
rm -rf path/to/inner/.git
```

Then verify that the remaining `.git` is at the correct project root before continuing.

---

## II. Decision Tree — Push Rejection

◆ Intermediate

**Starting question:** Did `git push` fail with an error message?

```
git push failed?
│
├── "error: src refspec main does not match any"
│   └── No commits exist yet.
│       Run: git add . && git commit -m "Initial commit"
│       Then: git push -u origin main
│
├── "fatal: No configured push destination"
│   or "fatal: 'origin' does not appear to be a git repository"
│   └── No remote configured.
│       Run: git remote add origin <url>
│       Then: git push -u origin main
│
├── "error: failed to push some refs"
│   or "Updates were rejected (non-fast-forward)"
│   └── Remote has commits your local repo does not have.
│       Run: git pull origin main
│       Resolve any conflicts.
│       Then: git push
│
├── "fatal: Authentication failed"
│   └── Credentials or remote URL are incorrect.
│       Run: git remote -v  ← confirm the URL
│       Check: HTTPS vs SSH format
│       Re-authenticate if needed, then push again.
│
└── "fatal: branch 'main' does not exist"
    └── Your default branch may be named 'master'.
        Run: git branch -M main
        Then: git push -u origin main
```

**Pre-push checklist** — run these before pushing when uncertain:

```bash
git status          # Confirm all changes are committed
git log --oneline   # Confirm commit history exists
git remote -v       # Confirm remote URL is correct
```

**The principle:**

Push rejections are not failures — they are diagnostic signals. The error message tells you exactly what is wrong. Read the first line of the error carefully. It contains the category of problem. The resolution follows directly from the category.

---

## III. Decision Tree — Merge Conflict

▲ Advanced

**Starting question:** Did Git report a conflict during a merge or pull?

```
Git reported a conflict?
│
├── YES
│   │
│   ├── Step 1: Identify conflicted files
│   │   Run: git status
│   │   Files marked "both modified" are conflicted.
│   │
│   ├── Step 2: Open each conflicted file
│   │   Look for conflict markers:
│   │
│   │   <<<<<<< HEAD
│   │   Your current content
│   │   =======
│   │   Incoming content (from the merge source)
│   │   >>>>>>> branch-name
│   │
│   ├── Step 3: Make the resolution decision
│   │   Three options:
│   │   (a) Keep your version — delete everything from ======= down
│   │   (b) Keep incoming version — delete everything from <<<<<<< to =======
│   │   (c) Combine both — manually edit to keep the correct content from each
│   │
│   ├── Step 4: Remove all conflict markers
│   │   No line beginning with <<<<<<<, =======, or >>>>>>> should remain.
│   │   Save the file.
│   │
│   └── Step 5: Stage and complete
│       git add <resolved-file>
│       git commit
│       (Git pre-fills a merge commit message — accept it or edit it)
│
└── NO ──► Merge completed successfully.
           Run: git log --oneline to confirm the merge commit.
```

**What the markers mean:**

- `<<<<<<< HEAD` — everything between this line and `=======` is your current branch's content
- `=======` — the dividing line between the two versions
- `>>>>>>> branch-name` — everything between `=======` and this line is the incoming content, from the branch being merged

Both sections represent valid work that existed on different lines of development. Git cannot determine which is correct — that decision requires human judgement about the project's intent. Make the decision, make the edit, remove the markers, commit.

**The principle:**

Conflicts are a normal consequence of parallel development. They are not errors — they are Git telling you that it found two different versions of the same content and needs you to decide which is correct. The process is always the same: find the markers, understand what each version contains, make the decision, clean the file, commit.

---

## IV. Decision Tree — Submission Verification

◼ Beginner

**Starting question:** Is the repository ready to be submitted?

```
Is the repository ready for submission?
│
├── Is this the correct repository?
│   Run: git remote -v
│   ─ URL contains classroom organisation name? ──► Continue
│   ─ URL points to personal account? ──► Wrong repo. Correct remote first.
│
├── Are all changes committed?
│   Run: git status
│   ─ "nothing to commit, working tree clean" ──► Continue
│   ─ Files listed as modified or untracked ──► Stage and commit them first
│
├── Is the latest commit pushed?
│   Run: git push
│   ─ "Everything up-to-date" ──► Continue
│   ─ Commits pushed ──► Continue
│   ─ Error ──► Resolve using Push Rejection tree (Section II above)
│
├── Is the commit visible on GitHub?
│   Open repository in browser. Confirm:
│   ─ Latest commit message is visible ──► Continue
│   ─ Commit timestamp is before the deadline ──► Continue
│   ─ Nothing visible / older commit shown ──► Push was not successful. Push again.
│
├── Is a README present?
│   ─ Yes, with current content ──► Continue
│   ─ No, or placeholder text remains ──► Update README before submitting
│
├── Does the project run?
│   Clone into a fresh folder. Open and run from there.
│   ─ Compiles and runs without errors ──► Continue
│   ─ Errors appear ──► Resolve before submitting
│
└── Final question:
    "If my lecturer opens this repository right now,
     does it fully and accurately represent my completed work?"
    ─ Yes ──► Submit.
    ─ Uncertain ──► Return to start of this tree.
```

---

## V. Professional Insight — Decision Trees in Industry

❈ Collaboration

Professional development teams encode the same diagnostic reasoning into runbooks, internal wikis, and onboarding documentation. The specific questions differ — "Should I branch or commit directly to trunk?", "What is the recovery procedure for a failed deployment?", "How do I roll back a production release?" — but the structure is identical: a starting question, a branching path of answers, a specific action at each terminal node.

Decision trees serve two purposes in professional environments. The first is immediate: they reduce the time between encountering a problem and acting correctly on it, particularly for less experienced team members under pressure. The second is longer-term: following a decision tree repeatedly internalises the diagnostic reasoning until the questions become intuitive and the tree is no longer needed.

Students who practice structured troubleshooting — reading error messages carefully, following diagnostic paths, understanding why each resolution works — are developing exactly the systematic thinking that professional debugging requires.

---

## Summary

Decision trees transform uncertainty into clarity by replacing guesswork with a sequence of answerable questions.

Four trees in this document:

- **Init vs Clone** — which starting command is correct, and what to do if both were used accidentally
- **Push Rejection** — what each push error means and the specific resolution for each
- **Merge Conflict** — the five-step resolution process and what the conflict markers represent
- **Submission Verification** — the complete pre-submission checklist in sequential question form

**The underlying principle for all four:**

Always interpret before acting. Git messages are diagnostic information, not punishment. Read them, understand what they are telling you, then act from that understanding.

---

Proceed to:

→ 07-02 — Cheat Sheet
