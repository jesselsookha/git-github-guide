# 04-02 — Pull Requests

❈ Collaboration

Pull Requests are the bridge between individual work and shared integration.

They are the moment in a collaborative workflow where a branch — developed in isolation, tested locally, committed carefully — becomes visible to the team and subject to review before it is allowed to enter `main`.

A Pull Request is not just a technical mechanism for merging code. It is a conversation. It is the point at which a contributor says: *"Here is what I built and why. I am ready for it to be reviewed."* And the point at which the team responds: *"Here is what we think. Here is what we would change. Here is our approval."*

Understanding Pull Requests as communication — not just code delivery — is what separates developers who collaborate well from those who simply push code.

---

## I. Core Concept — What Is a Pull Request?

◼ Beginner

A Pull Request is a **formal proposal to merge one branch into another** — almost always a feature branch into `main`.

It is created on GitHub (or equivalent platform) after a branch has been pushed. At the moment a PR is opened, nothing has been merged yet. The branch and `main` are still separate. The PR is the gateway between them — a space where the proposed changes can be inspected, discussed, and either approved or revised before integration.

A PR shows:

- **All commits** made on the branch — the complete development history leading to this proposal
- **A diff** — a line-by-line comparison of what changed between the branch and `main`
- **A title and description** — written by the contributor to explain the purpose and context of the change
- **A review thread** — where teammates can comment on specific lines, ask questions, or request changes

The key point for beginners: pushing a branch does not merge it. Pushing makes the branch available on GitHub. Opening a PR proposes the merge. The merge itself happens only after review and approval.

Think of a PR as saying:

*"I have completed this work. Here it is for inspection. Please review it before we add it to the shared project."*

---

## II. Practical Application — Creating a Pull Request

◆ Intermediate

After completing and pushing your branch:

I. Navigate to the repository on GitHub  
II. GitHub will typically display a banner: *"Your recently pushed branch — Compare & pull request."* Click it. If it does not appear, switch to your branch manually and click **Compare & pull request**.  
III. Review the base branch (`main`) and compare branch (your feature branch) — confirm these are correct  
IV. Write a **clear, specific title** that summarises the change:  

   - Good: *"Add about.html with team member profiles"*
   - Poor: *"my changes"*

V. Write a **description** that provides context:  

   - What was built or fixed
   - Any decisions that were made and why
   - Anything the reviewer should look at specifically
   - Whether any known issues or limitations remain

VI. Assign reviewers if the team has established who reviews what  
VII. Click **Create pull request**  

At this point, the PR is open. The branch is visible to every collaborator with repository access. It is not yet part of `main`. It waits for review.

---

## III. The PR Description — Why It Matters

◆ Intermediate

The PR description is the most underused part of the Pull Request workflow in academic settings — and one of the most valued in professional ones.

A PR without a description puts the entire burden of understanding on the reviewer. They must read every line of the diff, infer the intent, guess at the reasoning, and raise clarifying questions that could have been answered upfront. This wastes time and reduces the quality of review.

A well-written PR description does the following:

- **Summarises the change** in plain language — what the branch does at a functional level
- **Explains the reasoning** — why this approach was taken, what alternatives were considered
- **Flags anything specific** that the reviewer should pay attention to
- **Acknowledges known limitations** — work that is incomplete, edge cases not yet handled, technical debt introduced intentionally

A simple template that works at both academic and professional levels:

```
## What this PR does
A brief summary of the feature, fix, or change.

## Why
The reason this change was necessary or the problem it solves.

## Notes for reviewer
Anything specific the reviewer should look at, question, or be aware of.

## Known issues / limitations (if any)
Anything left outstanding, deferred, or known to be imperfect.
```

Writing a PR description is also a discipline for the contributor. Explaining your own code in plain language forces clarity of thought — and frequently reveals issues or gaps that were not obvious while writing the code.

---

## IV. Reviewing a Pull Request — Responsibilities and Etiquette

▲ Advanced

Opening a PR is the contributor's responsibility. Reviewing one is the team's.

Review is not optional in a collaborative workflow. A PR that sits unreviewed is blocked work — the contributor cannot merge, cannot clean up the branch, and cannot move on. In professional environments, unreviewed PRs are a team performance issue, not an individual one.

### What a reviewer looks for

- **Correctness** — does the code do what the PR description says it does?
- **Clarity** — is the code readable? Are variable names, structure, and logic understandable?
- **Completeness** — are there obvious edge cases that are not handled? Missing files, missing documentation?
- **Consistency** — does the approach match the patterns and conventions established elsewhere in the project?
- **Conflicts** — does the diff reveal anything that would conflict with work in progress on other branches?

### How to leave a review on GitHub

GitHub's PR interface allows reviewers to:

- **Comment on specific lines** — click the `+` icon next to any line in the diff to add a line-level comment
- **Suggest changes** — GitHub's "suggestion" feature allows reviewers to propose specific edits that the contributor can accept with one click
- **Approve** — indicate that the PR is ready to merge
- **Request changes** — indicate that revisions are required before the PR can be merged

### Review etiquette

- **Be specific** — "This function could use a comment explaining the logic" is more useful than "needs improvement"
- **Be constructive** — frame observations as questions or suggestions, not judgements
- **Be timely** — review promptly; blocked PRs create blocked teammates
- **Separate the code from the person** — review the work, not the writer

In academic group projects, giving and receiving code review is itself an assessed skill. Treat it accordingly.

---

## V. Merging Pull Requests

◆ Intermediate

Once a PR is approved, it can be merged. GitHub offers three merge strategies, each with different implications for the commit history:

### Merge Commit (Recommended for Academic Projects)

```
Creates a new "merge commit" that joins the branch history into main
```

This preserves the complete history of the branch — every commit, in order, with a merge commit at the point of integration. The history accurately reflects how the project was built and by whom.

This is the correct choice for academic projects. Every commit in the branch is part of the development record.

### Squash and Merge

```
Combines all commits from the branch into a single commit on main
```

Useful when a branch contains many small, messy work-in-progress commits that are not meaningful individually. The entire branch's changes appear as one clean commit on `main`. The original branch history is not preserved in `main`.

This is common in professional teams where branch history is considered internal scaffolding rather than public record.

### Rebase and Merge

```
Replays the branch's commits directly onto main, without a merge commit
```

Produces the cleanest linear history — the branch's commits appear as if they had been made directly on `main`. This is the hardest to understand and the most likely to produce complications if the branch has diverged significantly.

**In academic contexts:** use Merge Commit. The preserved history is evidence of your development process, and that evidence is part of what is assessed.

After any merge, every collaborator must update their local copy:

```bash
git pull origin main
```

This is not optional. A local copy of `main` that does not include merged branches is out of date, and the next push from that machine will produce a rejection or conflict.

---

## VI. Common Confusions Clarified

◼ Beginner

**"Do I need a PR if I am the only contributor?"**

Technically no — with write access, you can push directly to `main`. But opening PRs even in solo projects builds the habit, creates a documented record of changes, and prepares you for every collaborative context where PRs are non-negotiable. Many developers use PRs on solo projects as a personal review practice — a moment to read their own code one more time before it enters the permanent record.

**"Does pushing automatically merge?"**

No. Pushing uploads your branch to GitHub and makes it visible. A PR is required to propose the merge. Approval is required to proceed. The merge itself is a deliberate action — never automatic.

**"Can anyone merge a PR?"**

Only contributors with write access can merge. In a student group, the team should agree in advance on who has merge authority — typically the repository owner or a designated lead. Uncoordinated merging leads to the same branch being merged twice, or a conflicted branch being merged without resolution.

**"Why not commit directly to `main`?"**

Because direct commits bypass every safeguard that branching and Pull Requests provide. There is no review step. There is no opportunity for teammates to see what is changing before it changes. There is no discussion. A direct commit to `main` is an unilateral change to the shared project — which is exactly the collaborative anti-pattern that the entire branching model is designed to prevent.

---

## VII. Classroom Activity — Pull Request Simulation

❈ Collaboration

Building directly on the branching activity in 04-01, this activity focuses on the PR workflow — creating, reviewing, and merging Pull Requests as a structured team process.

### Objective

- Create Pull Requests for individually developed branches
- Practice reviewing a teammate's changes in the GitHub interface
- Experience the feedback loop between contributor and reviewer
- Complete a structured merge into `main`

### Roles

- **Repository Owner** — reviews all PRs, merges approved work, manages branch protection if configured
- **Collaborators** — create PRs, review each other's work, respond to review comments

### Steps

I. Each collaborator pushes their feature branch (from 04-01 activity)  
II. Each collaborator opens a PR with a clear title and description  
III. Each collaborator reviews at least one teammate's PR — leaves at least one substantive comment  
IV. Repository owner performs final review and merges approved PRs  
V. All collaborators pull the updated `main`:  

```bash
git pull origin main
```

### Optional Extension — Conflict Resolution

If two students edit the same file on different branches and one is merged first, the second PR will show a conflict. The activity:

I. GitHub marks the PR as "conflicted — cannot be merged automatically"  
II. The contributor pulls `main` into their branch:  

```bash
git pull origin main
```

III. Git marks the conflicted sections in the affected file  
IV. The contributor and reviewer discuss which version to keep  
V. The contributor edits the file, removes conflict markers, saves, stages, and commits:  

```bash
git add conflicted-file.html
git commit -m "Resolve merge conflict in contact page"
git push origin feature-contactPage
```

VI. The PR updates automatically — it can now be merged  

This extension is worth running at least once in a controlled environment. The first time a student encounters a merge conflict under deadline pressure is not the right time to learn how to resolve it.

---

## VIII. Professional Insight — Review Models in Industry

▲ Advanced

The PR workflow practised in academic group projects reflects the foundation of how professional software teams manage code quality and shared responsibility.

In production environments, this process is significantly more formalised:

**Code Owners** — specific files or directories are assigned to designated reviewers. A change to the authentication module may require approval from a security-focused team member, regardless of who opened the PR.

**Mandatory review counts** — many teams require a minimum of two approvals before a PR can be merged. This distributes review responsibility and reduces the risk of errors being overlooked.

**Protected branch rules** — `main` (and often `develop`) is configured so that direct pushes are blocked entirely. The only way to add code to `main` is through an approved PR. GitHub enforces this at the platform level.

**Continuous Integration** — every PR triggers an automated pipeline: the test suite runs, code coverage is checked, static analysis tools scan for security vulnerabilities, and the build is verified. A PR cannot be merged until all checks pass. This means code review and automated verification happen simultaneously — humans review for intent and design; machines review for correctness and safety.

**Draft Pull Requests** — professional teams often open PRs while work is still in progress, using GitHub's "Draft PR" feature. This signals that the work is not ready for review, but makes it visible early — allowing teammates to track progress, comment on direction, and identify potential conflicts before they accumulate.

Every one of these practices exists because, at scale, code quality cannot depend on any single person's attention or memory. The PR process is the mechanism by which teams maintain shared standards across thousands of changes, made by dozens of contributors, in parallel.

---

## Summary

Pull Requests are not administrative overhead.
They are the collaborative checkpoint — the moment when individual work becomes team work.

Key principles:

- Open a PR before merging — always, even in solo projects
- Write a clear title and a useful description — explain the *what* and the *why*
- Review others' PRs promptly and specifically — blocked PRs block teammates
- Use Merge Commit for academic projects — preserve the full development history
- Pull `main` after every merge — every contributor, every time

In academic contexts, Pull Requests demonstrate structured, transparent collaboration — and they are part of what is assessed.

In professional contexts, they are the primary mechanism by which teams maintain code quality, share knowledge, and build shared ownership of a codebase.

---

Proceed to:

→ 04-03 — Group Workflows
