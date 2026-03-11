# Core Git Commands

◼ Beginner  
◆ Intermediate  

This section introduces the essential Git commands that form the foundation of every workflow in this guide.

These commands must be understood conceptually, not memorised blindly. Memorising syntax without understanding purpose produces developers who can follow steps but cannot adapt when something unexpected occurs. For each command, this section explains not only what it does, but why it exists, when to use it, and what it actually changes in the repository model.

Every command here connects directly to the three-area model introduced in How Git Works. If a command's purpose is unclear, return to that section and re-read the model before continuing.

---

# I. Creating a Repository

### `git init`

```bash
git init
```

`git init` initialises a new Git repository in the current folder.

When you run this command, Git creates a hidden directory called `.git` inside your project folder. This directory is the repository — it contains the staging area, the commit history, the branch references, and all configuration data. Without it, Git has no awareness of your project. With it, Git begins tracking every change.

The output will confirm:

```
Initialized empty Git repository in /path/to/your-project/.git/
```

**Use this when:**
- Starting a brand-new project locally, before any remote repository exists

**Do NOT use this:**
- Inside a folder that was cloned from GitHub — cloned repositories are already initialised and contain a `.git` directory. Running `git init` inside a cloned repository creates a second, conflicting repository structure.

The `.git` directory is the repository. Treat it with care. If it is deleted, your commit history is gone and Git no longer tracks the project.

---

# II. Checking Status

### `git status`

```bash
git status
```

`git status` shows the current state of your working directory and staging area.

This is one of the most important commands in Git — not because it changes anything, but because it tells you exactly where you are at any moment. Before committing, before pushing, before pulling, running `git status` is the professional habit that prevents errors.

It displays:

- **Modified files** — files that have been changed in the working directory but not yet staged
- **Staged files** — files that have been added to the staging area and are ready to be committed
- **Untracked files** — files that Git has detected in the working directory but is not yet tracking
- **Current branch** — which branch you are currently on

Think of `git status` as your orientation command. Whenever you are unsure of your current state — what has been staged, what has been committed, what branch you are on — run `git status`. It costs nothing and reveals everything.

Use it frequently. Use it before every commit. Use it after every pull. Use it whenever Git behaves unexpectedly.

---

# III. Staging Changes

### `git add`

Stage a single file:

```bash
git add filename.ext
```

Stage all changes in the current directory:

```bash
git add .
```

`git add` moves changes from the working directory into the staging area. It is the act of selecting which changes should be included in your next commit.

The dot (`.`) in `git add .` means "everything in this folder and all subfolders." It is convenient, but it should be used deliberately. If you have changes to multiple unrelated files, staging everything together and committing them as one unit produces a confusing history. Staging files selectively — or in groups — produces a history where each commit represents a coherent piece of work.

A common professional practice is to use `git status` to see what has changed, then `git add` specific files or groups of files intentionally, rather than always using `git add .` without thinking.

Staging a file does not commit it. It places it in the staging area — waiting to be included in the next commit. You can stage files, un-stage them, modify them again, and re-stage them before ever committing.

---

# IV. Committing Changes

### `git commit`

```bash
git commit -m "Clear, structured message"
```

`git commit` takes everything in the staging area and records it as a permanent snapshot in the local repository. This is the act of creating a version — a point in history that can be referenced, inspected, compared, and returned to.

The `-m` flag specifies the commit message inline. The message is not optional. It is the human-readable record of what changed and why — the information that makes a commit useful to anyone who reads the history later, including your future self.

**Commit messages should be:**

- Specific — describing the exact change that was made
- Logical — reflecting a coherent unit of work, not an accumulation of unrelated changes
- Written in the present tense, imperative mood (the Git convention): "Add login validation" rather than "Added login validation" or "Adding login validation"

**Poor examples:**

```
"Update"
"Fix"
"Changes"
"wip"
```

These messages tell no story. Six months from now, or when a lecturer reviews the history, or when a colleague traces a bug — these commits are meaningless.

**Good examples:**

```
"Implement login validation logic"
"Fix null reference error in user profile screen"
"Add README with project overview and setup instructions"
"Refactor database connection to use environment variables"
```

Commit messages communicate intent. They are addressed to future readers — including yourself — who will need to understand not just what changed, but why.

A clean commit history built from clear messages is one of the most valuable things a developer can produce. It is a log of how the software was built.

---

# V. Viewing History

### `git log`

```bash
git log
```

`git log` displays the full commit history of the current branch, starting from the most recent commit.

For each commit, it shows:

- The **commit hash** — a unique identifier (SHA-1) for that specific commit
- The **author** — name and email
- The **date and time** the commit was created
- The **commit message**

The commit hash is important beyond identification. It is the reference used in recovery operations, `git revert`, `git reset`, and `git cherry-pick`. Knowing how to read `git log` and locate specific commits by their hashes is an essential skill for any intermediate Git user.

For a more compact view, useful when scanning long histories:

```bash
git log --oneline
```

This displays one line per commit, showing only the abbreviated hash and the message — much easier to scan quickly.

**Use `git log` to:**

- Review your own progress and verify that commits were recorded correctly
- Understand the sequence of changes when debugging a problem
- Identify the specific commit where a bug was introduced
- Prepare for recovery operations by locating the commit you want to reference

---

# VI. Connecting to a Remote Repository

### `git remote add origin`

```bash
git remote add origin https://github.com/username/repository.git
```

This command links your local repository to a remote repository — typically hosted on GitHub.

Breaking it down:

- `git remote` — manages the set of tracked remote repositories
- `add` — adds a new remote entry
- `origin` — the conventional name for the primary remote. "Origin" is not a Git keyword — it is a naming convention so widely used that it has become the default. You could name it anything, but deviating from convention creates confusion.
- The URL — the HTTPS or SSH address of the remote repository

This command is run once per repository. Once a remote is configured, it persists in the repository's `.git/config` file. All future push and pull operations reference it by name.

To verify the remote was configured correctly:

```bash
git remote -v
```

This lists all configured remotes with their fetch and push URLs. If the URL is incorrect, it can be updated:

```bash
git remote set-url origin https://github.com/username/correct-repository.git
```

---

# VII. Pushing Changes

### `git push`

```bash
git push
```

`git push` uploads your local commits to the remote repository, making them available to collaborators and visible on GitHub.

The first push to a new remote requires an additional flag:

```bash
git push -u origin main
```

Breaking this down:

- `-u` (or `--set-upstream`) — links your local `main` branch to the `origin/main` branch on the remote. This upstream relationship means that after the first push, you can run plain `git push` without specifying the remote and branch every time.
- `origin` — the name of the remote
- `main` — the branch you are pushing

After the upstream is set with `-u`, all future pushes from this branch require only:

```bash
git push
```

**Important:** `git push` only uploads commits — changes that have been staged and committed. Unsaved file changes and staged-but-not-committed changes are not pushed. If your changes are not appearing on GitHub, the most common cause is that the push was never run, or that changes were never committed before pushing.

---

# VIII. Pulling Changes

### `git pull`

```bash
git pull
```

`git pull` fetches commits from the remote repository and merges them into your current local branch. As covered in How Git Works, this is a combined `git fetch` + `git merge` operation.

**Use `git pull`:**

- Before starting new work in a shared repository — to ensure you are working from the latest version
- Before pushing, if you are unsure whether the remote has changed since your last synchronisation — to avoid push rejections caused by diverging histories

In a solo project with no collaborators, pulling is less critical — but it is still good practice, particularly if you work across multiple devices.

In a collaborative project, pulling regularly is essential. The longer you go without pulling, the more likely your local history is to diverge from the remote, and the more complex the eventual merge will be.

---

# IX. Cloning a Repository

### `git clone`

```bash
git clone https://github.com/username/repository.git
```

`git clone` creates a local copy of a remote repository — complete with the full commit history, all branches, and the remote connection pre-configured.

When you clone a repository, Git:

- Downloads the complete repository history
- Creates a fully initialised `.git` directory
- Configures `origin` as the remote, pointing to the URL you cloned from

**Use `git clone` when:**

- Working on an existing GitHub repository
- Accepting a GitHub Classroom assignment
- Contributing to an open-source project
- Setting up your development environment for a shared project on a new machine

**Never run `git init` inside a cloned repository.** A cloned repository is already initialised. Running `git init` inside it creates a nested `.git` directory — a repository inside a repository — which produces confusing behaviour and breaks the expected workflow.

The fundamental rule: **you clone what already exists. You initialise what you are creating from scratch.**

---

# X. The Essential Beginner Workflow

Understanding which workflow applies to your situation prevents the majority of beginner Git errors.

### Workflow A — New Project, Starting Locally

Use when you are creating a project from scratch and it does not yet exist on GitHub:

```bash
git init
git add .
git commit -m "Initial commit"
git remote add origin <url>
git push -u origin main
```

I. `git init` — begins tracking the project locally
II. `git add .` — stages all current files
III. `git commit -m "Initial commit"` — records the first snapshot
IV. `git remote add origin <url>` — connects to the GitHub repository (which should be empty — do not initialise it with a README)
V. `git push -u origin main` — uploads history and sets upstream tracking

---

### Workflow B — Existing Remote Repository

Use when a repository already exists on GitHub — whether created by you, by a lecturer, or via GitHub Classroom:

```bash
git clone <url>
# make changes
git add .
git commit -m "Descriptive message"
git pull   # if collaborating or if remote may have changed
git push
```

I. `git clone <url>` — replicates the full repository to your machine
II. Make your changes in the working directory
III. `git add .` — stage the changes
IV. `git commit -m "..."` — record the snapshot
V. `git pull` — retrieve any remote changes before pushing (prevents rejection)
VI. `git push` — upload your commits

---

### The Ongoing Development Loop

After initial setup, most of your working time will follow this simple rhythm:

```bash
git add .
git commit -m "Describe what you completed"
git push
```

Repeat this loop regularly — after every meaningful unit of work, at the end of every working session, and always before closing your development environment.

If it is not pushed, it has not been submitted. If it has not been committed, it is not in the history. If it is not in the history, it does not exist from the perspective of anyone else reviewing your repository.

---

These commands are foundational.

Every workflow, every collaboration model, every recovery technique in this guide builds upon them. Understanding each one — not just its syntax, but its purpose and its place in the model — is the foundation of everything that follows.

---

Proceed to:

→ Part 2 — Guided Practice
