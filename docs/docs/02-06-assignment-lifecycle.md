# 02-06 — Assignment Lifecycle

❈ Collaboration

This document explains the full lifecycle of a Git-based academic assignment — from the moment it is created to the moment it is submitted and archived.

It applies to:

- GitHub Classroom environments
- Institutional GitHub organisations
- Any academic submission that uses a Git repository as the submission medium
- Any structured educational workflow that evaluates development process as well as outcome

Where organisation-specific procedures differ from the universal principles described here, they will be noted clearly. Readers outside an academic context will find that this lifecycle maps directly onto the feature development lifecycle in professional environments — with the roles and terminology changed, but the structure identical.

---

## I. Core Concept — Git as a Development Record, Not Just Submission

An assignment repository is not a storage folder that happens to be on GitHub.

It is a **development timeline**. Every commit is a moment in that timeline — a record of what was done, when it was done, and by whom. The repository, viewed as a whole, tells the story of how the project was built.

It is:

- A development timeline that shows the progression of work from start to finish
- A record of authorship that demonstrates individual contribution in group work
- A structured audit trail that supports academic integrity review when needed
- A portfolio item that, for assessed work, represents not just what you built but how you built it

Submission is not the final push.

Submission is the final state of a **continuous history**. The commits leading up to that final push are the submission — the push simply ensures they are visible.

If there is no commit history, there is no visible development process. A repository with one commit made the night before the deadline tells a very different story than a repository with twenty commits spread across three weeks of development. Both might contain identical final code. The histories are not equivalent, and they will not be assessed equivalently.

---

## II. Phase 1 — Assignment Creation (Lecturer Perspective)

❈ Collaboration

Understanding this phase helps students understand the structure they are working within — and why certain rules exist.

In a GitHub Classroom model:

I. The lecturer creates an assignment inside the Classroom interface
II. The assignment is linked to a GitHub organisation account
III. An optional template repository may be attached — providing starter files, folder structure, or instructions
IV. An invitation link is generated
V. Students accept the link individually
VI. GitHub automatically creates a **private repository** for each student inside the organisation

Structural points worth understanding:

- **Repository ownership** belongs to the organisation — not to the student's personal GitHub account
- The **student has write access** — they can push commits, create branches, and modify files
- The **lecturer has administrative access** — they can view all commits, timestamps, contributor activity, and the full history at any time
- **Repository visibility is private** — only the student and the lecturer (and any teaching assistants with access) can see it

This structure is not arbitrary. It ensures academic integrity by keeping submissions within an auditable, access-controlled space. It prevents sharing between students. It allows automated tracking of submission timestamps. And it mirrors real-world organisational structures, where repositories are owned by the company or team rather than by individuals.

For readers outside this academic context:

Identical structures exist in professional environments. Enterprise GitHub organisations, GitLab groups, Azure DevOps projects, and Bitbucket workspaces all use the same model: repositories belong to the organisation, individuals have role-based access, and activity is tracked centrally. The lifecycle logic is the same — only the terminology changes.

---

## III. Phase 2 — Assignment Acceptance

◼ Beginner

The student's responsibilities at this stage are minimal but critical:

I. Accept the assignment invitation link — do this as soon as it is provided. Delay occasionally causes issues with repository creation timing.
II. Wait for confirmation that your repository has been created. GitHub displays a confirmation message and a link to your repository.
III. Copy the repository URL — use the HTTPS URL ending in `.git`, found under Code → HTTPS.
IV. **Clone the repository** — never initialise.

```bash
git clone <assignment-url>
```

At this stage, the repository already exists. Your only role is to replicate it correctly to your machine.

Refer to 02-03 for the full cloning workflow and 02-04 if you have already initialised by mistake.

---

## IV. Phase 3 — Development Cycle

This is the longest phase and the one where the most errors occur — not because Git is difficult, but because consistency breaks down over time.

Development should follow a consistent, repeatable rhythm. The specific rhythm:

```bash
git add .
git commit -m "Clear, descriptive message"
git push
```

This loop should occur:

- After completing a meaningful unit of work — a feature, a fix, a section of functionality
- At the end of every working session, regardless of whether the work feels "complete enough to commit"
- Before closing your IDE — make it a closing ritual

**Why commit even when the work feels incomplete?**

Because an uncommitted, unpushed change is invisible to everyone else and at risk on your machine. Partial progress committed to a repository is recoverable, reviewable, and protected. Partial progress that exists only as unsaved file changes is none of those things.

Professional teams commit small, logical units of work frequently — not to produce a perfect history, but to produce a *safe* and *traceable* one. The habit starts here.

**Institutional recommendation:** Push at minimum once per working session, even if the session felt unproductive. A commit that says "In progress — partial implementation of login screen" is more valuable than nothing.

---

## V. Phase 4 — Mid-Assignment Verification

◆ Intermediate

At any point during the assignment period, you should be able to verify:

I. **Your commits are visible on GitHub** — open the repository in a browser and confirm that recent commits appear under the commit history
II. **You are on the correct branch** — unless instructed otherwise, you should be working on `main`
III. **No unexpected conflicts exist** — `git status` should return clean or show only intended unstaged changes

Use these commands to confirm:

```bash
git status          # Check current state
git log --oneline   # Review recent commit history
git remote -v       # Confirm remote URL is the Classroom repository
```

If your work is not visible on GitHub after pushing, one of three things happened:

- The push failed silently — check the terminal output for errors
- You pushed to a different branch — check which branch is shown on GitHub
- You are connected to the wrong remote — run `git remote -v` and verify the URL

Mid-assignment verification is not paranoia. It is the same discipline a professional developer applies when working on a shared codebase — the assurance that what you believe is synchronized is actually synchronized.

---

## VI. Phase 5 — Pre-Submission Discipline

This phase is critical and frequently underestimated.

Before the deadline, work through the following sequence:

**I. Check for uncommitted changes:**

```bash
git status
```

If any modified files appear under "Changes not staged for commit," those changes are not yet in your history. Stage and commit them:

```bash
git add .
git commit -m "Final updates before submission"
```

**II. Push everything:**

```bash
git push
```

Do not assume a previous push covered everything. Run it explicitly before the deadline.

**III. Confirm on GitHub — in a browser:**

- Open your repository on GitHub
- Confirm that the latest commit is visible and has a timestamp before the deadline
- Confirm you are looking at the correct branch (`main` unless otherwise specified)
- Confirm the commit message reflects your final state

**IV. If your institution requires LMS submission:**

Follow the LMS instructions. Submit the repository URL, not a ZIP file. Ensure the URL points to the correct Classroom repository and not a personal one.

**The professional equivalent of this phase** is the pre-release checklist before deploying to production. In professional environments, deadlines are replaced by:

- Release freeze dates
- Pull request merge deadlines
- Production deployment windows

The principle remains identical: the remote repository reflects the official state of the work. Verify that it is current before the deadline passes.

---

## VII. Phase 6 — After Submission

❈ Collaboration

After the submission deadline, the following rules apply:

- **Do not rewrite history** — do not use `git rebase` to reorganise commits
- **Do not delete commits** — removing commits from history after submission misrepresents the development timeline
- **Do not force push** — this overwrites the history that was submitted and assessed

Your institution may implement:

- Repository locking at the deadline — preventing further pushes automatically
- Marking based on commit history and timestamps
- Review of the development timeline as part of the assessment criteria

Whether or not your institution explicitly enforces these rules, Git's commit timestamps are part of the permanent record. They are visible to anyone with access to the repository. They reflect when work was done, when it was pushed, and in what order.

This protects both the student and the lecturer. The student has evidence of when they worked. The lecturer has an auditable record to assess against. Neither party should want that record altered after the fact.

---

## VIII. Common Lifecycle Failures

### Failure I — Working Without Pushing

A student works consistently throughout the assignment period — commits regularly, builds the project properly — but never pushes. At the deadline, the remote repository is empty or shows only an initial commit.

Git does not synchronise automatically. Local commits do not appear on GitHub until they are pushed. Local work, no matter how thorough, is not submission.

The fix is simple and preventable: push at the end of every working session.

---

### Failure II — The Last-Minute Massive Commit

One commit. Made minutes before the deadline. The entire project — weeks of work — bundled into a single snapshot.

This raises academic integrity questions that are difficult to resolve favourably, even when the student genuinely did the work.

Healthy development history shows gradual progress: early structural commits, incremental feature additions, bug fixes, README updates, refactoring. That pattern is recognisable and credible.

A single commit containing an entire project is not. Even if entirely legitimate, it cannot demonstrate process — and process is part of what is being assessed.

---

### Failure III — Working in the Wrong Repository

A student works diligently, commits regularly, pushes consistently — but to a personal repository instead of the Classroom organisation repository. The lecturer sees an empty submission space.

Always confirm the remote before beginning any assignment:

```bash
git remote -v
```

The URL must contain the organisation name, not your personal GitHub username.

---

### Failure IV — Rewriting History Before Submission

Using `git rebase` or `git push --force` to clean up, reorganise, or alter commit history before submission.

Even with good intentions — wanting to present a clean history — history rewriting after the fact misrepresents the development timeline. Commit timestamps that appear too evenly spaced, suspiciously clean commit messages, or a history that looks significantly different from what was visible during the assignment period all raise concerns.

For academic contexts: leave the history as it is. An imperfect but genuine history is more valuable than a polished but altered one.

---

## IX. Professional Insight — Why This Lifecycle Matters

▲ Advanced

The academic assignment lifecycle and the professional feature development lifecycle are structurally identical. The terms simply change:

| Academic | Professional |
|---|---|
| Assignment | Feature or task |
| Lecturer | Team lead or product owner |
| Deadline | Release date or sprint end |
| Submission | Merge to `main` branch |
| Repository in organisation | Repository in company account |

The full lifecycle in professional terms:

**Create → Clone → Develop → Commit → Push → Verify → Review → Merge → Archive**

Understanding this now — while the stakes are academic — builds the habits and mental models that professional environments will assume you already have.

Teams do not teach new developers how to commit consistently, how to verify before pushing, or how to maintain a readable history. They expect those habits to already be in place. The assignment lifecycle is where they form.

---

## X. Universal vs Institutional Rules

For clarity across different reading contexts:

**Universal Git principles** — apply regardless of institution, platform, or employer:

- Clone existing repositories; initialise only when creating new ones
- Commit frequently; push regularly; never lose local-only work
- Never force push in a shared repository context
- The remote repository is the official record — verify it reflects your actual state

**Institution-specific practices** — may vary by course, year, or programme:

- Repository naming conventions
- Branch naming policies
- Whether LMS submission is required alongside GitHub
- Whether tags are required for final submission commits
- How commit history is weighted in assessment

When reading this guide outside its originating institution: apply the universal principles first. Adapt the institutional procedures to your context.

---

## XI. Lifecycle Summary Model

The full assignment lifecycle in sequence:

```
Creation → Acceptance → Clone → Develop → Commit → Push → Verify → Submit → Archive
```

At every stage, ask one question:

**Is my local repository synchronised with the remote?**

If yes — you are safe to proceed.
If unsure — run `git status`, `git log`, and `git remote -v` before proceeding.

Synchronisation is not a technical checkbox. It is the ongoing discipline that makes Git meaningful as a submission system, a collaboration tool, and a professional record of your work.

---

Proceed to:

→ Part 3 — Professional Standards
