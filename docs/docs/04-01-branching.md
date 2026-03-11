# 04-01 — Branching

❈ Collaboration

Branching is the foundation of collaborative Git workflows.

It is the mechanism that allows multiple contributors to work independently on the same project — in parallel, without interfering with each other — while still maintaining a single, coherent shared history that can be reviewed, integrated, and released.

Without branching, collaborative development is a coordination problem. Two people editing the same file at the same time overwrite each other's work. Two features being built simultaneously become entangled in each other's unfinished changes. Every push to a shared repository is a risk to whatever was there before.

Branching solves all of this — not by keeping people apart, but by giving each contributor their own protected workspace inside the shared repository, with a structured process for bringing that work back together when it is ready.

---

## I. Core Concept — What Is a Branch?

◼ Beginner

A branch is a **parallel line of development** inside the repository.

When you create a branch, you are not copying the project into a separate folder. You are creating a new pointer in Git's history — a new path of commits that diverges from an existing point in the timeline. Work you do on that branch does not affect any other branch. Changes on `main` do not affect your branch. The two lines evolve independently until a deliberate merge brings them together.

The `main` branch is the default — the stable, shared line of development that represents the agreed-upon state of the project. It is the branch that lecturers review, that teams deploy from, and that pull requests target.

Feature branches are the working spaces. They are created from `main` at a specific point, developed in isolation, and merged back into `main` once the work is complete and reviewed.

Why branches matter in collaborative work:

- They prevent one contributor from overwriting another's work — each person's changes are isolated until deliberately integrated
- They allow multiple features to be developed simultaneously without becoming entangled
- They provide a safe space for experimentation — work that might not work out can be discarded without affecting the stable codebase
- They create a review checkpoint — changes must pass through a merge process before entering `main`, which is the point at which they can be evaluated

To create a new branch and switch to it immediately:

```bash
git checkout -b feature-login
```

This creates a branch called `feature-login` and moves you into it in one command. From this point, any commits you make belong to `feature-login` and do not appear on `main` until explicitly merged.

To see all existing branches and confirm which one you are on:

```bash
git branch
```

The branch marked with `*` is your current branch.

---

## II. Practical Application — Branching in Group Work

◆ Intermediate

In a collaborative project, each contributor works on their own branch, and changes are integrated into the shared codebase through a structured review process. This is the model used by professional development teams and the one this guide uses throughout the Collaboration section.

The complete collaborative cycle:

I. **Clone the shared repository** — every contributor starts from the same point  
II. **Create a branch for your assigned task** — give it a clear, descriptive name  
III. **Develop locally** — edit files, test changes, work at your own pace  
IV. **Commit regularly with clear messages** — each commit should describe a logical unit of progress  
V. **Push your branch to GitHub** — making it visible to teammates and available for review  
VI. **Open a Pull Request** — formally proposing that your branch be merged into `main`  
VII. **Review and respond to feedback** — address comments, make adjustments, re-push  
VIII. **After approval, merge** — the branch is integrated into `main`  
IX. **Pull the updated `main` locally** — every contributor synchronises after a merge  

```bash
git pull origin main
```

This cycle — branch, develop, commit, push, review, merge, pull — is the heartbeat of structured collaborative development. It applies equally to a three-person student group and a hundred-person engineering team.

---

## III. Naming Conventions and Conflict Prevention

▲ Advanced

Branch names are not just labels — they are communication. In a collaborative project, the branch list on GitHub is visible to every contributor, and each name tells teammates something about what is being worked on and by whom.

### Naming Conventions

Use descriptive, lowercase names that make the branch's purpose immediately clear:

- `feature/about-page` — a new feature being added
- `fix/login-validation-error` — a bug fix
- `docs/update-readme` — documentation changes
- `refactor/simplify-database-connection` — structural improvement without behaviour change

The prefix before the `/` categorises the work — the same categories used in Conventional Commits. Vague names like `branch1`, `test`, or `johns-branch` provide no information to teammates and make the branch list unreadable in any project with more than two contributors.

The convention is worth establishing before work begins, not after the first confusion.

### Conflict Prevention

The most effective approach to merge conflicts is not resolving them well — it is not creating them unnecessarily.

- **Pull the latest `main` before creating any branch** — start from the most current state of the project, minimising the divergence your branch will eventually need to reconcile
- **Communicate about overlapping files** — if two people are working in the same file or feature area, coordinate before starting rather than discovering the conflict at merge time
- **Make small, focused commits** — large commits that touch many files in many areas dramatically increase the surface area for conflicts; small focused commits reduce it
- **Merge and close branches promptly** — a branch that has been sitting for two weeks accumulates more divergence from `main` with every passing day; integrate completed work quickly
- **Never work directly on `main`** — direct commits to `main` bypass the review process and create exactly the scenario that branching is designed to prevent

In academic group projects, these practices demonstrate professional discipline and make the collaborative workflow assessable — each contribution is traceable, reviewable, and attributable.

---

## IV. Classroom Activity — Branching Simulation

❈ Collaboration

This activity simulates a real-world collaborative Git workflow. Students practice creating branches, committing work, pushing to a shared repository, and integrating contributions through Pull Requests — in a structured, low-risk environment where mistakes are recoverable and instructive.

### Objective

- Create and manage a shared repository using role-based access
- Clone the repository and create individual feature branches
- Push changes and open Pull Requests for review
- Experience and resolve a merge conflict (optional extension)
- Log contributions accurately in a timesheet

### Group Setup

Form groups of three. Assign the following roles:

- **Repository Owner** — creates the repository, manages access, reviews and merges Pull Requests
- **Collaborator A and B** — contribute features via branches, review each other's Pull Requests

### Repository Owner Instructions

I. Create a new repository named `Git-Practice-TeamName` on GitHub  
II. Initialise with a README so the repository is not empty  
III. Go to Settings → Collaborators → Add collaborators by GitHub username  
IV. Grant **Write** access — this allows collaborators to push branches but not to modify repository settings  

### Collaborator Instructions

I. Accept the GitHub collaboration invitation (check your email or GitHub notifications)

II. Clone the repository:
```bash
git clone https://github.com/owner-username/Git-Practice-TeamName.git
cd Git-Practice-TeamName
```

III. Create your assigned branch:
```bash
git checkout -b feature-aboutPage
```

IV. Create your assigned file (`index.html`, `about.html`, or `contact.html`) and add initial content

V. Stage, commit, and push:
```bash
git add .
git commit -m "Add about.html with team member details"
git push origin feature-aboutPage
```

VI. Open a Pull Request on GitHub (covered in detail in 04-02)

VII. Review at least one teammate's Pull Request — leave a comment, approve, or request changes

VIII. After all PRs are merged, pull the updated `main`:
```bash
git pull origin main
```

### Optional — Merge Conflict Demonstration

Two students intentionally edit the same line in the same file on different branches. When one branch is merged first, the second PR will show a conflict. The team must:

- Identify which lines conflict
- Discuss and agree on the correct resolution
- Edit the file to remove conflict markers and keep the correct content
- Commit the resolution and complete the merge

This teaches the most important truth about merge conflicts: they are resolved through communication and human judgement, not through Git commands alone.

### Timesheet Logging

Each student records their contributions:

| Date | Branch | Commit Message | Task Type |
|---|---|---|---|
| 05/03/2026 | feature-aboutPage | Add about.html with team details | Feature |

This reinforces accountability. In professional environments, equivalent records are generated automatically from commit history — which is another reason why commit messages must be clear and accurate.

---

## V. Professional Insight — Branching Strategies Beyond the Classroom

▲ Advanced

The feature branching model practised in this activity — one branch per task, merged via Pull Request — is the foundation upon which larger professional strategies are built.

As teams and codebases grow, the same principles apply but with greater structure:

### Feature Branching
Every new feature, however small, lives in its own branch. Nothing is developed directly on `main`. This is the model used in this guide and the appropriate model for most student projects.

### Git Flow
A formal branching model designed for projects with scheduled releases. It uses a permanent `develop` branch as the integration point, `feature/*` branches for new work, `release/*` branches for release preparation, and `hotfix/*` branches for urgent production fixes. `main` is reserved exclusively for stable, released code.

Git Flow adds discipline at the cost of complexity. It is well-suited to teams with defined release cycles, but excessive for small projects with continuous deployment.

### Trunk-Based Development
Developers work in very short-lived branches — or directly on `main` (the "trunk") — and integrate multiple times per day. This model requires a mature automated testing infrastructure: CI pipelines that run the full test suite on every push, and deployment automation that allows rapid releases. Without that infrastructure, trunk-based development is fragile. With it, it is extremely fast.

Understanding that these models exist — and that they are all variations on the same core principle of *isolate, develop, review, integrate* — prepares students to read and adapt to any collaborative workflow they encounter in a professional setting.

---

## Summary

Branching is not a Git technicality. It is the behaviour of a disciplined collaborator.

It separates work, prevents interference, enables parallel development, and creates the structured review checkpoint that keeps shared codebases stable.

In academic contexts, branching demonstrates that you understand collaborative development — not just that you can push code.

In professional contexts, it scales into release strategies, CI/CD pipelines, and code review cultures that entire engineering organisations depend on.

The habits start here:

- Name branches clearly and descriptively
- Commit frequently within your branch
- Communicate with teammates about areas of overlap
- Never commit directly to `main`
- Pull after every merge

Branching is not just technical.
It is collaborative behaviour — practised deliberately.

---

Proceed to:

→ 04-02 — Pull Requests
