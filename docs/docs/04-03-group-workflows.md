# 04-03 — Group Workflows

❈ Collaboration

Group projects require discipline in Git workflows.

Not technical ability alone — discipline. A team where every member is technically capable of using Git can still produce a broken, confused, unassessable repository if there is no agreed structure for how contributions are made, reviewed, and integrated.

Without a workflow, teams reliably encounter the same set of problems: code overwritten without warning, features that break each other, commits pushed to the wrong place, and a history that no longer reflects what actually happened or who actually did what. These are not Git problems. They are coordination problems — and they are solved by agreement, not by commands.

A workflow is the team's contract for how it uses Git. This document defines what that contract should look like at academic level, why it works, and how it connects to professional practice.

---

## I. Core Concept — What a Workflow Defines

◼ Beginner

A workflow is the **agreed process** for how a team uses Git together.

It answers the questions that, if left unanswered, become the source of every collaborative problem:

- How are branches created and named?
- Who is responsible for reviewing Pull Requests?
- When and how are merges performed?
- How are conflicts resolved, and by whom?
- What happens after a merge — does everyone update their local copy?

Without answers to these questions — agreed upon before work begins — each team member fills in the gaps with their own assumptions. Those assumptions rarely align. The result is not just technical errors but interpersonal friction: whose version is correct? Who broke the build? Why is this file different on my machine?

A workflow does not need to be long or complex. Even a simple, shared understanding — "create a branch, open a PR, the team lead merges" — prevents the majority of collaborative failures. The key is that it exists and that every member of the team has agreed to it.

---

## II. Why Teams Fail Without One

Before establishing the workflow, it is worth understanding precisely what happens in its absence.

**All members working on `main`** is the most common failure mode in student group projects. With no branching discipline, every contributor is pushing directly to the shared branch. The last push wins. Changes made by one person are silently overwritten by the next. By the time the overwriting is discovered — often at the point of submission — the history is fragmented and the work is difficult to recover.

**Unreviewed merges** happen when branches exist but there is no PR process. Branches are created, developed in isolation, and then merged directly into `main` without any teammate having seen the changes. Broken code enters the shared project. Conflicts that could have been discussed are instead discovered by whoever tries to run the project next.

**Unco-ordinated access** leads to confusion about repository ownership. Students push to personal repositories instead of the classroom organisation. Multiple repositories exist with partial versions of the project, and there is no clear authority over which version is current.

**Accumulated local work** — the scenario where a student works for days without pushing — means that when a push finally happens, it either conflicts dramatically with everyone else's progress or silently diverges from the agreed direction of the project.

Each of these failures has the same root cause: the team did not establish a workflow before starting.

---

## III. The Academic Group Workflow — Step by Step

❈ Collaboration

This is the standard collaborative workflow for academic group projects. It builds directly on the branching and Pull Request skills covered in 04-01 and 04-02.

### Step 1 — Repository Setup

A lecturer creates the GitHub Classroom assignment. Each group receives a private repository inside the classroom organisation. Before any development begins:

- The repository owner confirms that all group members have been added as collaborators with **Write** access
- All group members clone the repository — never initialise:

```bash
git clone <classroom-repository-url>
cd repository-name
```

- Everyone verifies their remote is correct:

```bash
git remote -v
```

If any group member's remote URL points to a personal account rather than the classroom organisation, it must be corrected before work begins.

---

### Step 2 — Task Assignment and Branching

Before the first line of code is written, the team assigns tasks and agrees on branch names.

Each member creates their branch from the current state of `main`:

```bash
git checkout main
git pull origin main
git checkout -b feature/homepage
```

The pull before creating the branch is important. It ensures the branch starts from the most current version of `main` — not from whatever state `main` was in when you last interacted with it.

Suggested branch names for the activity:

- `feature/homepage`
- `feature/about-page`
- `feature/contact-page`

---

### Step 3 — Development

Each member works independently on their branch. Within that branch, the standard development loop applies:

```bash
git add .
git commit -m "Add navigation structure to homepage"
git push origin feature/homepage
```

Commit regularly — after each meaningful unit of progress. Push at the end of every working session. Do not accumulate days of uncommitted work.

If a teammate merges their branch into `main` while you are still working, update your branch before continuing:

```bash
git checkout feature/homepage
git pull origin main
```

This merges the latest `main` into your branch, keeping you current and reducing the divergence you will eventually need to reconcile.

---

### Step 4 — Pull Requests

When a branch is ready for integration, the contributor opens a Pull Request. The PR should include:

- A clear title describing what the branch adds or fixes
- A description explaining what was done and any decisions made
- At least one requested reviewer — either the repository owner or a specific teammate

No branch should be merged without a PR. This is the rule — in academic projects and in professional ones.

---

### Step 5 — Review and Merge

The repository owner (or designated reviewer) reviews each PR. Teammates are encouraged to review each other's work as well. After approval:

- The repository owner merges the PR using **Merge Commit**
- The merged branch can be deleted from GitHub — it has served its purpose
- All team members update their local `main`:

```bash
git checkout main
git pull origin main
```

This step is not optional. A local `main` that does not include merged branches is out of date, and the next push from that machine will either conflict or overwrite merged work.

---

### Step 6 — Conflict Resolution

When a conflict occurs during a merge or a pull, the team responds together — not individually.

The process:

I. Identify the conflicted file(s) — Git will mark them in `git status`
II. Open the conflicted file — locate the conflict markers
III. **Discuss with the teammate whose work is in conflict** — do not resolve unilaterally
IV. Edit the file to reflect the correct combined content
V. Remove all conflict markers
VI. Stage, commit, and push:

```bash
git add conflicted-file.html
git commit -m "Resolve merge conflict between homepage and about page"
git push origin feature/homepage
```

The PR will update automatically and can now be merged.

Conflict resolution is a collaborative act, not a technical one. The technical steps are straightforward. The important part is the conversation about which content is correct.

---

## IV. Review Responsibilities

▲ Advanced

The question of who reviews Pull Requests must be settled before the project begins.

### Academic Model

The repository owner — or a designated team lead — reviews and merges all PRs. This ensures consistency and creates a single point of accountability. The lecturer can audit the review history to confirm that integration was deliberate and reviewed.

For a group of three, a reasonable structure is: the repository owner reviews all PRs from collaborators; collaborators are encouraged but not required to also review each other's work.

### Professional Model

Professional teams typically require a minimum of one or two approvals before a branch can be merged. Reviewers are often assigned based on file ownership — the developer most familiar with the code being changed is the most qualified to review it.

At scale, review responsibilities are defined by team agreements and sometimes enforced by branch protection rules: `main` cannot be merged into without approval from a designated list of reviewers.

### Open Source Model

In open-source projects, any contributor can leave a review. Maintainers hold final merge authority. The review thread is public — transparent to the entire community.

What all three models share: review is not self-service. You do not review your own PR and merge it. The separation between contributor and reviewer is what makes the process meaningful.

---

## V. Common Pitfalls in Group Work

◼ Beginner

These failure patterns are observed in student group projects consistently enough that naming them directly is useful. Each one is preventable — not by skill, but by discipline.

**Everyone works directly on `main`.**
*Prevention:* Create a branch before making any change. Agree on this rule before work begins.

**PRs are merged without review.**
*Prevention:* Establish a rule that no PR is merged without at least one comment from a reviewer who is not the contributor. Even "looks good" is an improvement over no review at all.

**Students push incomplete, broken code.**
*Prevention:* Test locally before pushing. A push should represent a working state — or, if incomplete, a clearly labelled work-in-progress commit.

**Local commits are never pushed.**
*Prevention:* Push at the end of every working session. The remote repository is the submission. Local commits are not.

**Confusion about repository ownership.**
*Prevention:* Run `git remote -v` before every first push in a new session. The URL must contain the classroom organisation name.

**Teammates do not pull after merges.**
*Prevention:* Make pulling after a merge a team rule. After every PR is merged, the team lead notifies the group. Every member runs `git pull origin main` before continuing.

---

## VI. Professional Workflow Models

▲ Advanced

The feature branching model used in this guide is the foundation of professional collaborative development. Understanding how it scales into formal workflow strategies prepares students to enter environments with more complex requirements.

### Feature Branching

One branch per feature or task. Branches are created from `main`, developed independently, and merged back via Pull Request. This is the model used throughout this guide. It is appropriate for student projects and for most small-to-medium professional teams.

### Git Flow

Designed for projects with planned releases. Introduces a permanent `develop` branch as the integration point between feature branches and `main`. The full structure:

- `main` — stable, released code only
- `develop` — integration branch; where features are merged
- `feature/*` — individual features, branched from `develop`
- `release/*` — release preparation branches, branched from `develop`
- `hotfix/*` — urgent production fixes, branched from `main`

Git Flow adds rigour at the cost of overhead. It is well-suited to projects with defined release cycles but unnecessary for continuous deployment or small teams.

### Trunk-Based Development

All developers work on very short-lived branches (or directly on `main`) and integrate multiple times per day. The constraint that makes this safe is a comprehensive automated testing infrastructure: every push triggers a CI pipeline that verifies the build. Without that pipeline, trunk-based development is fragile. With it, it enables faster iteration than any branched workflow.

### What They Share

All three models are variations on the same principle: **isolate work until it is ready, then integrate through a defined process.** The scope of isolation and the formality of the integration process differ. The principle does not.

Recognising this principle makes it possible to read and adapt to any collaborative workflow — whether it is described in a team README, enforced by branch protection rules, or handed down in a developer onboarding document.

---

## Summary

A group workflow is not a constraint on how individuals work. It is the agreement that makes individual work composable into a shared project.

Without it, collaboration is coordination by collision — whoever pushes last wins, and the history reflects luck more than intention.

With it, collaboration is structured and assessable. Each contribution is visible. Each review is documented. Each merge is intentional. The history tells the story of how the project was built together.

Key principles:

- Agree on the workflow before writing the first line of code
- Branch before editing — always, every task, every member
- Open a PR before merging — no exceptions
- Decide who reviews and merges — and enforce it as a team rule
- Pull after every merge — every contributor, without exception
- Confirm repository URL before every push — `git remote -v`

In academic contexts, a well-executed group workflow demonstrates teamwork, discipline, and professional readiness.

In professional contexts, it is the infrastructure on which everything else depends.

---

Proceed to:

→ 04-04 — Security and Academic Integrity
