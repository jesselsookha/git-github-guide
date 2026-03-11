# 06-01 — Visual Studio Code

---

## I. IDE Context

◼ Beginner

**Visual Studio Code** is a lightweight, extensible source code editor developed by Microsoft. It is one of the most widely used editors across all development disciplines — web, scripting, data science, and general-purpose development — precisely because it is fast, configurable, and honest about what it does.

Its Git integration is built in and requires no plugins. When VS Code detects a `.git` directory in the opened folder, it activates the Source Control panel and begins reading repository state directly from that directory.

**VS Code does not replace Git.** It provides a graphical interface for commands you already understand.

---

## II. Under the Hood

When VS Code detects a Git repository:

- It reads the `.git` folder continuously and reflects its state in the Source Control panel
- It displays modified, staged, and untracked files visually — separating "Changes" (unstaged) from "Staged Changes"
- Every Source Control action executes a Git CLI command against the `.git` directory

**The verification test:** open the integrated terminal (`Ctrl+`` ` or `View → Terminal`) and run:

```bash
git status
```

The terminal output and the Source Control panel will reflect identical state. This is not coincidence — they are reading from the same source.

---

## III. Guided Workflow — Creating and Publishing a Repository

Scenario: you start a new project folder in VS Code and want to publish it to GitHub.

### Step 1 — Initialise Repository

- **UI Action:** Source Control panel → "Initialize Repository"
- **CLI Equivalent:** `git init`
- **Effect:** Creates `.git` directory at the project root. VS Code immediately begins showing file changes in the Source Control panel.

⚠ Confirm the folder VS Code opened is the project root — not a parent folder. `git init` in the wrong location tracks the wrong files.

---

### Step 2 — Stage Changes

- **UI Action:** Source Control panel → click `+` next to each file, or `+` next to "Changes" to stage all
- **CLI Equivalent:** `git add <file>` or `git add .`
- **Effect:** Files move from "Changes" to "Staged Changes" in the panel

VS Code's clear visual separation between staged and unstaged files makes the staging area concept more intuitive than most IDEs. This is one of its strongest pedagogical properties — use it to reinforce understanding of what `git add` does, not to bypass that understanding.

---

### Step 3 — Commit

- **UI Action:** Enter message in the text field → click "Commit" (tick icon)
- **CLI Equivalent:** `git commit -m "message"`
- **Effect:** Creates a permanent snapshot of staged files in local history. Source Control panel clears.

A commit message entered in VS Code's input field is identical to a message passed with `-m` in the terminal. The same quality standards apply — write what changed, in imperative mood, specifically enough to be readable in `git log`.

---

### Step 4 — Publish to GitHub

- **UI Action:** "Publish Branch" button (appears after first commit if no remote is configured)
- **CLI Equivalent:**
  ```bash
  git remote add origin <url>
  git branch -M main
  git push -u origin main
  ```
- **Effect:** VS Code opens a GitHub authentication flow, creates the remote repository if it does not exist, connects the local repository, and pushes all commits.

"Publish Branch" is not a single action — it is a sequence of three commands. The automation is convenient. Understanding what it does matters when it fails or when the repository needs to be connected manually.

---

## IV. Branching in VS Code

- **UI Action:** Status bar (bottom-left, shows current branch name) → click → "Create new branch"
- **CLI Equivalent:** `git checkout -b <branch-name>`
- **Effect:** Creates a new branch pointer and moves HEAD to it. The status bar updates immediately to show the new branch name.

To switch between existing branches: click the branch name in the status bar → select a branch from the list. This is `git switch <branch-name>`.

---

## V. The Sync Button — What It Does

VS Code displays a "Sync Changes" button in the status bar after commits. This button performs two operations in sequence:

I. `git pull` — fetches remote commits and merges them locally
II. `git push` — uploads local commits to the remote

When synchronisation is routine — no conflicts, upstream is up to date — Sync is a convenient shortcut. When it fails, understanding that it is two operations is essential for diagnosing which part produced the error. A conflict reported after Sync is a `git pull` conflict, not a push failure.

---

## VI. Common Misconceptions

**"Sync = push."**
Sync is pull then push. Clicking Sync without understanding this can trigger an unexpected merge if the remote has new commits.

**"Files are staged automatically."**
They are not. Files in the "Changes" section are unstaged. They must be moved to "Staged Changes" before committing — unless "Commit All" is used deliberately.

**"Logging in to GitHub in VS Code configures the remote."**
GitHub authentication in VS Code handles credentials for push and pull — it does not configure `origin`. If "Publish Branch" was not used, the remote must be added manually via `git remote add origin <url>`.

---

## VII. Professional Insight

◆ Intermediate

VS Code is the recommended IDE for learning Git integration precisely because its transparency matches the CLI model. The separation of "Changes" and "Staged Changes" mirrors the working directory and staging area distinction. The integrated terminal allows immediate CLI verification of every UI action.

Professional developers use VS Code extensively for web development, scripting, and configuration work. Its extension ecosystem — GitLens, Git Graph, GitHub Pull Requests — adds visibility into history, blame annotations, and PR management without obscuring the underlying Git operations.

Developing dual fluency in VS Code — IDE controls alongside the terminal — builds the confidence and flexibility that professional environments require.

---

Proceed to: → 06-02 — Visual Studio

---
