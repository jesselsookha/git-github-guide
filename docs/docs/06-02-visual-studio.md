# 06-02 — Visual Studio

---

## I. IDE Context

◼ Beginner

**Visual Studio** (not to be confused with Visual Studio Code) is Microsoft's full enterprise IDE, designed primarily for .NET, C#, ASP.NET, and Windows application development. It is a significantly larger and more complex tool than VS Code — its Git integration is correspondingly deeper and more automated.

A key characteristic: Visual Studio may prompt "Would you like to create a Git repository?" when a new project is created. This automation is helpful, but students must understand what it is doing — `git init` at the solution root — rather than treating it as a mystery that produces a repository.

Git is integrated into Visual Studio, but it is not Visual Studio. The same structural rules apply.

---

## II. Under the Hood

Visual Studio executes standard Git commands against the `.git` directory, but abstracts more steps than VS Code. It introduces:

- The **Git Changes** panel — showing staged and unstaged changes
- The **Git Repository** window — showing branch history and commit graph
- An **integrated merge conflict editor** — a three-panel view for conflict resolution
- **Solution-level Git awareness** — Visual Studio understands that a `.sln` file and its associated projects may span multiple directories

Despite this additional complexity, the underlying commands are unchanged. Every operation in the Visual Studio Git interface has a direct CLI equivalent.

**The verification test:** open the terminal (View → Terminal, or use an external terminal navigated to the project root) and run:

```bash
git status
git log --oneline
git branch
```

The state reported by these commands is the authoritative state. The Git Changes panel and Git Repository window visualise the same information.

---

## III. Guided Workflow — New Project with Git

Scenario: you create a new C# console application in Visual Studio and want to version-control and publish it.

### Step 1 — Initialise Repository

- **UI Action:** New Project wizard → check "Place solution and project in same directory" → check "Add to Git" (or: Git → Init Repository after project creation)
- **CLI Equivalent:** `git init`
- **Effect:** Creates `.git` at the solution root

⚠ **Solution root is critical.** Visual Studio's project structure creates a solution file (`.sln`) and one or more project directories beneath it. The `.git` folder must be at the same level as the `.sln` file — the solution root — not inside a project subfolder. If Git is initialised in the wrong location, only part of the project is tracked.

---

### Step 2 — Stage Changes

- **UI Action:** Git Changes panel → select files to stage (click `+` next to individual files or "Stage All")
- **CLI Equivalent:** `git add <file>` or `git add .`
- **Effect:** Selected files move to "Staged Changes"

Visual Studio may offer "Commit All" — which stages and commits in one step. This is convenient but bypasses the staging step. Use "Stage All" then "Commit" when learning, to maintain awareness of what is being committed.

---

### Step 3 — Commit

- **UI Action:** Enter message → "Commit Staged"
- **CLI Equivalent:** `git commit -m "message"`
- **Effect:** Creates a snapshot in local history

---

### Step 4 — Push to GitHub

- **UI Action:** Git → Push, or "Push" button in Git Changes panel
- **CLI Equivalent:**
  ```bash
  git remote add origin <url>
  git push -u origin main
  ```
- **Effect:** Visual Studio may offer to create the remote repository through its GitHub integration. This automates `git remote add` — but the remote URL it configures must be the correct institutional or personal repository URL.

⚠ When working in GitHub Classroom: do not let Visual Studio create a new remote repository automatically. The Classroom repository already exists. Connect to it by copying its URL and configuring the remote manually, or by entering the URL when Visual Studio prompts for the remote.

---

## IV. Branching in Visual Studio

- **UI Action:** Branch dropdown (top of screen or Git menu) → "New Branch"
- **CLI Equivalent:** `git checkout -b <branch-name>`
- **Effect:** Creates branch pointer and moves HEAD

The **Git Repository** window provides a visual commit graph — showing branch points, merge commits, and the current HEAD position. This is a useful tool for understanding the repository structure, particularly when working in a team with multiple branches.

---

## V. Common Misconceptions

**"Git is part of Visual Studio."**
Git is a separate tool that Visual Studio integrates with. If Git is uninstalled or misconfigured, Visual Studio's Git features fail. The `.git` directory exists independently of the `.sln` file. Verifying state in the terminal confirms what is actually tracked.

**"The solution root and the repository root are always the same."**
They should be — but only if Git was initialised at the correct level. Students who initialise Git inside a project subfolder rather than at the solution root create a repository that does not track the entire project. Always verify: `git status` from the solution root should show all project files.

**"The graphical merge editor resolves conflicts automatically."**
The merge editor presents conflict choices visually — "Accept Current", "Accept Incoming", "Accept Both". These map to the three options available when resolving conflict markers manually. The editor does not resolve conflicts; it assists in making the resolution choice. Understanding what the markers mean ensures correct decisions even when the graphical tool is not available.

---

## VI. Professional Insight

▲ Advanced

Visual Studio is the standard IDE for enterprise .NET and C# development in professional environments. Its Git integration is designed for large-scale projects — solutions with many projects, complex branch structures, and team-level access control.

Its branch history visualisation and integrated conflict management are genuinely useful in complex merge scenarios. However, its high level of automation means that structural understanding of Git must be developed independently. Students who rely on Visual Studio's automation without understanding the underlying commands will encounter significant difficulty when:

- The automation fails and they must diagnose the issue from CLI output
- They work in a different IDE or a server environment with no GUI
- A force push or repository reset is performed by a teammate and they must understand what changed

Periodic CLI verification — `git status`, `git log --oneline`, `git branch` — is the practice that keeps structural understanding current regardless of what the IDE is doing automatically.

---

Proceed to: → 06-03 — Android Studio

---
