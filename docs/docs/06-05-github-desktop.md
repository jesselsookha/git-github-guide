# 06-05 — GitHub Desktop

---

## I. IDE Context

◼ Beginner

**GitHub Desktop** is a graphical Git client developed and maintained by GitHub. Its purpose is specifically to lower the barrier to entry for Git — making staging visible, reducing terminal intimidation, and providing a smooth authentication path to GitHub.

It is worth being precise about what GitHub Desktop is and is not: it is a **Git client**, not Git itself. It executes standard Git commands against your local repository. The repository it manages is identical to any repository managed by VS Code, a terminal, or any other tool.

GitHub Desktop is an excellent starting point for beginners — particularly for making the staging concept visible. It is not sufficient for advanced operations such as rebasing, recovery through reflog, or complex conflict resolution.

---

## II. Under the Hood

Every action in GitHub Desktop — staging, committing, pushing, branching — executes a standard Git command locally against the `.git` directory.

**The verification test:** open the repository folder in a terminal and run:

```bash
git status
git log --oneline
git branch
```

The state matches exactly what GitHub Desktop displays. This is the proof that GitHub Desktop is a visualisation layer — the same underlying system, through a different interface.

---

## III. Guided Workflow — Create and Publish a Repository

Scenario: you want to create a new repository and publish it to GitHub using GitHub Desktop.

### Step 1 — Create Local Repository

- **UI Action:** File → New Repository → enter name and local path → "Create Repository"
- **CLI Equivalent:** `git init`
- **Effect:** Creates a new folder with a `.git` directory inside it

GitHub Desktop may offer to add a README, `.gitignore`, or licence at creation. If working toward a GitHub Classroom submission, leave all three unchecked — the Classroom repository structure takes precedence.

---

### Step 2 — Stage Changes

- **UI Action:** Left panel → check files to include
- **CLI Equivalent:** `git add <file>`
- **Effect:** Checked files are staged

This is GitHub Desktop's strongest pedagogical feature: staging is explicitly visualised as a checkbox action. Each checked file is staged. Each unchecked file is not. The left panel is a direct, visible representation of the staging area.

---

### Step 3 — Commit

- **UI Action:** Enter summary (and optional description) → "Commit to main"
- **CLI Equivalent:** `git commit -m "summary"`
- **Effect:** Creates a snapshot in local history. The left panel clears.

The summary field maps to the commit message subject. The optional description field maps to the commit message body — the extended explanation after the blank line. Both correspond directly to the multi-line commit message format described in 03-01.

---

### Step 4 — Publish Repository

- **UI Action:** "Publish Repository" button (top bar)
- **CLI Equivalent:**
  ```bash
  git remote add origin <url>
  git push -u origin main
  ```
- **Effect:** GitHub Desktop creates the remote repository on GitHub (if not already existing) under your account, configures `origin`, and pushes all commits

⚠ **For GitHub Classroom:** do not use "Publish Repository." The Classroom repository already exists. Instead, use "Add Existing Repository" to add the folder you cloned, or clone the Classroom repository through GitHub Desktop using File → Clone Repository.

---

### Step 5 — Push Subsequent Changes

- **UI Action:** "Push origin" button (top bar)
- **CLI Equivalent:** `git push`
- **Effect:** Uploads new commits to the remote repository

---

## IV. Branching in GitHub Desktop

- **UI Action:** "Current Branch" dropdown → "New Branch"
- **CLI Equivalent:** `git checkout -b <branch-name>`
- **Effect:** Creates a branch pointer and moves HEAD. The "Current Branch" indicator updates.

To switch branches: click "Current Branch" → select from the list. Merges are performed through Branch → Merge into Current Branch, which maps to `git merge <branch-name>`.

---

## V. Common Misconceptions

**"GitHub Desktop is Git."**
GitHub Desktop is a client that executes Git commands. Removing GitHub Desktop from your machine does not remove the Git repositories it was managing — they are `.git` directories on your filesystem. Git itself is installed separately.

**"GitHub Desktop handles everything automatically."**
GitHub Desktop does not auto-stage, auto-commit, or auto-push. Every action requires deliberate input. What it does is make those actions visually accessible — the checkboxes, buttons, and input fields are front-ends for commands that the user must still choose to execute.

**"Logging in to GitHub in GitHub Desktop means my repository is connected."**
Authentication handles credentials for push and pull. It does not configure the remote. A repository must still be published or manually connected to a remote URL before pushes will succeed.

---

## VI. Professional Insight

◆ Intermediate

GitHub Desktop is appropriate for:

- Early-stage learners building confidence with the staging and commit cycle
- Simple, personal workflows where the full power of the CLI is not needed
- Demonstrating the staging concept visually in teaching contexts

It is not sufficient for:

- Rebasing or squashing commits
- Recovery through reflog
- Complex merge operations
- Any operation not exposed in its interface

Professional developers may use GitHub Desktop for simple day-to-day operations, but maintain CLI fluency for anything beyond the basics. The limitation is not a criticism of the tool — GitHub Desktop does exactly what it is designed to do. The limitation is that professional Git usage regularly requires capabilities it does not expose.

---

Proceed to: → 06-06 — macOS Terminal

---
