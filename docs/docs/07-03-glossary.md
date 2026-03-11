# 07-03 — Glossary

---

## Purpose

This glossary defines Git terminology with enough depth to be genuinely useful — not just as a lookup for definitions, but as a reference that explains what each term means, why it matters, and how it connects to the broader model.

Terminology is the foundation of fluency. A developer who can name what they are doing, and explain why, has understanding that survives tool changes and interface differences. A developer who knows only button locations does not.

Terms are grouped by function. Within each group, order moves from foundational to derived — start at the beginning of a section if a concept is unfamiliar.

---

## I. Starting a Repository

| Term | Definition |
|---|---|
| **Version Control** | A system that records changes to files over time — who changed what, when, and why. Version control allows you to retrieve any previous state of the project, compare versions, and collaborate without overwriting each other's work. Git is a distributed version control system: every contributor has a complete copy of the history, not just a connection to a central server. |
| **Git** | The version control system itself — a command-line tool that tracks changes in files, manages branches, and maintains a complete history of a project. Git runs locally on your machine. It does not require an internet connection to commit, branch, or inspect history. GitHub is not Git; it is a hosting service for Git repositories. |
| **Repository** | The complete record of a project managed by Git. A repository contains all project files, all committed history, all branches, and all configuration — stored in a hidden `.git` directory at the project root. Every contributor who clones a repository has a full, independent copy of this history. |
| **Remote Repository** | A version of the repository hosted on a server — typically GitHub, GitLab, or Bitbucket. The remote is the shared, authoritative copy that all contributors push to and pull from. It is not a "master" copy in a technical sense — every local clone is equally complete — but it serves as the coordination point for collaboration. |
| **`git init`** | Creates a new repository by adding a `.git` directory to the current folder. Everything Git needs to track the project — the object database, configuration, branch references — lives inside this directory. Running `git init` does not affect existing files; it simply begins tracking them. Use when starting a project from scratch that is not already on GitHub. |
| **`git clone <url>`** | Creates a local copy of an existing remote repository. The full history, all branches, and the remote configuration (`origin`) are all transferred. Use when joining a project that already exists — including GitHub Classroom assignments. After cloning, the remote is already configured and push/pull work immediately. |
| **Upstream** | The original repository from which you forked or cloned, or the remote branch that a local branch is configured to track. When `git push -u origin main` is run, the `-u` flag sets `origin/main` as the upstream for the local `main` branch — enabling plain `git push` and `git pull` without specifying the remote each time. |

---

## II. Working on Changes

| Term | Definition |
|---|---|
| **Working Directory** | The folder on your computer where the project files are located. This is where you edit code, add files, and make changes. The working directory reflects the current state of the project — which may be ahead of, behind, or identical to the last commit. |
| **Staging Area** | An intermediate space between the working directory and the commit history. Files must be explicitly moved into the staging area with `git add` before they can be committed. The staging area allows you to select which changes belong in the next commit — grouping related changes together and leaving unrelated work for a subsequent commit. This selectivity is the mechanism behind focused, logical commits. |
| **`git add <file>`** | Moves a specific file from the working directory into the staging area. The file's current content is captured at this moment — subsequent edits to the file are not automatically included in the staged version. Run `git add` again after further edits if you want them included. |
| **`git add .`** | Stages all modified and new files in the current directory and all subdirectories. Convenient, but requires awareness: this stages everything, including files that may not yet belong in this commit. Review `git status` before and after to confirm what is staged. |
| **`git status`** | Shows the current state of the working directory and staging area. Reports which files are modified but unstaged, which are staged and ready to commit, which are untracked, and which branch HEAD is on. Running `git status` before every commit is a discipline, not a formality. |
| **`.gitignore`** | A configuration file at the repository root that specifies files and patterns Git should not track. Common exclusions include build output, IDE configuration files, and credentials. Files excluded by `.gitignore` will not appear in `git status` as untracked and cannot be accidentally staged. A `.gitignore` should be committed to the repository so all contributors share the same exclusions. |
| **`git restore <file>`** | Discards unstaged changes to a file — reverts it to the state it was in at the last `git add` or, if not staged, the last commit. This operation cannot be undone. Use with care; unsaved work is permanently discarded. |
| **`git restore --staged <file>`** | Removes a file from the staging area without discarding its changes. The file returns to "modified but unstaged" status. Use when you accidentally staged a file that should not be in the next commit. |
| **`git rm <file>`** | Removes a file from both the working directory and Git's tracking. The deletion is staged automatically and will be committed on the next `git commit`. Use when a file should no longer exist in the project at all. |
| **`git mv <old> <new>`** | Renames or moves a tracked file, recording the rename in the staging area. Preferable to manually renaming a file, which Git may interpret as a deletion and a new untracked file rather than a rename. |

---

## III. Recording and Managing History

| Term | Definition |
|---|---|
| **Commit** | A permanent, addressable snapshot of the staged files at the moment the commit is created. Each commit contains the project state, the author's name and email, an exact timestamp, the hash of the parent commit, and a descriptive message. Commits are immutable — once created, their content and hash cannot change. The chain of commits forms the project's complete history. |
| **Commit Hash** | The unique identifier for a commit — a 40-character SHA-1 string generated from the commit's content, metadata, and parent hash. Even a single character difference in any of these inputs produces a completely different hash. The first seven characters are usually sufficient to reference a commit unambiguously in a repository. |
| **Commit Message** | The descriptive text attached to a commit explaining what changed. Convention: written in imperative mood ("Add feature" not "Added feature"), 50 characters or fewer for the subject line, with an optional body section separated by a blank line for extended explanation. Commit messages are the primary tool for understanding a repository's history without reading every diff. |
| **`git commit -m "message"`** | Creates a commit from all currently staged files with the provided message as the subject line. If the message requires more than a subject line, run `git commit` without the `-m` flag to open the configured text editor for a full multi-line message. |
| **`git log`** | Displays the commit history of the current branch, from newest to oldest. Each entry shows the full hash, author, date, and message. `git log --oneline` shows one line per commit — hash abbreviated to seven characters and message subject. `git log --oneline --graph --all` adds a visual representation of the branch structure. |
| **`git diff`** | Shows line-by-line differences between two states. Without arguments: differences between working directory and staging area (unstaged changes). With `--staged`: differences between staging area and last commit (what will be committed). With two hashes: differences between any two commits. |
| **`git show <hash>`** | Displays the full metadata and diff of a specific commit. Use when you need to understand exactly what a single commit changed. |
| **Tag** | A named reference to a specific commit — typically used to mark releases (e.g., `v1.0`, `v2.3.1`). Unlike branches, tags do not move as new commits are made. Annotated tags (created with `git tag -a`) include a message and are recommended for release marking. |
| **`git revert <hash>`** | Creates a new commit that applies the inverse of the specified commit's changes. The original commit remains in history; a new "revert" commit is added after it. The project state returns to what it was before the reverted commit, but the history is preserved intact. Safe for shared repositories. |
| **`git reset`** | Moves the branch pointer to a previous commit, with varying effects on staged and working files depending on the mode. `--soft`: moves pointer, keeps changes staged. `--mixed` (default): moves pointer, unstages changes but keeps them in working directory. `--hard`: moves pointer and discards all changes. Reset rewrites the branch's visible history — do not use on commits that have been pushed to a shared remote. |
| **`git reflog`** | Shows every movement of HEAD — commits, checkouts, resets, rebases — including positions no longer reachable through any branch. The reflog is the recovery tool of last resort: commits that appear to have been lost through a reset are almost always findable here. Retained locally for 90 days by default. |
| **`git bisect`** | Performs a binary search through the commit history to locate the specific commit that introduced a bug or regression. You mark a known good commit and a known bad commit; Git checks out the midpoint for you to test; you mark it good or bad; Git narrows the search until the introducing commit is found. |

---

## IV. Branching and Merging

| Term | Definition |
|---|---|
| **Branch** | A named pointer to a specific commit that advances automatically as new commits are made on it. Branches enable parallel development — work on one branch does not affect any other. The `main` branch is the default shared line of development. Feature branches are created from it, developed independently, and merged back when the work is complete. |
| **HEAD** | The pointer that marks your current position in the repository history. In normal operation, HEAD points to the current branch, which points to its most recent commit. When you switch branches, HEAD moves. When you commit, the branch advances and HEAD moves with it. In detached HEAD state, HEAD points directly to a commit rather than a branch. |
| **Detached HEAD State** | A state in which HEAD points to a specific commit rather than to a branch. Occurs when you run `git checkout <hash>` or `git checkout <tag>`. Work done in detached HEAD state is not attached to any branch — new commits will be lost if you navigate away without first creating a branch. Safe for inspection; requires branch creation before committing. |
| **`git checkout -b <n>`** | Creates a new branch and switches to it in one command. The new branch starts at the current commit. This is the standard command for beginning work on a new feature or fix. |
| **`git switch <n>`** | Switches to an existing branch. Moves HEAD to point to the named branch and updates the working directory to reflect that branch's state. Modern alternative to `git checkout <n>` for branch switching specifically. |
| **Merge** | The operation that integrates the history of one branch into another. A merge commit is created that has two parent commits — the tips of both branches. If the changes do not overlap, the merge is automatic. If both branches modified the same lines, a conflict occurs and must be resolved manually. |
| **Merge Conflict** | A situation where Git cannot automatically integrate two branches because both have modified the same lines of the same file in incompatible ways. Git marks the conflicting sections with `<<<<<<<`, `=======`, and `>>>>>>>` markers and pauses the merge until the developer resolves the conflict manually, stages the resolved file, and commits. |
| **`git merge <branch>`** | Merges the specified branch into the current branch. If the current branch can be updated by simply moving its pointer forward (a fast-forward), no merge commit is created. If the branches have diverged, a merge commit is created. |
| **Rebase** | An alternative to merging that replays the commits from one branch on top of another, creating a linear history without a merge commit. Produces a cleaner, more readable history at the cost of rewriting commit hashes. Do not rebase commits that have been pushed to a shared remote — the rewritten hashes will conflict with what others have already pulled. |
| **`git stash`** | Saves uncommitted changes (both staged and unstaged) to a temporary stack and reverts the working directory to the last commit. Use when you need to switch branches but are not ready to commit current work. Restore with `git stash pop`. |

---

## V. Collaboration and Synchronisation

| Term | Definition |
|---|---|
| **`git push`** | Uploads local commits to the configured remote branch. After the first push with `-u` (which sets the upstream tracking), subsequent pushes require only `git push` without additional arguments. Push does not happen automatically — it is always an explicit action. |
| **`git push -u origin main`** | Pushes the local `main` branch to the `origin` remote and sets it as the upstream tracking branch. After running this once, `git push` and `git pull` will use these settings by default. |
| **`git pull`** | Fetches commits from the remote and merges them into the current local branch. Equivalent to running `git fetch` followed by `git merge`. If the remote has commits that conflict with local changes, a merge conflict will result and must be resolved before the pull completes. |
| **`git fetch`** | Downloads commits, branches, and tags from the remote without merging them into the local branch. Allows inspection of what is on the remote before deciding to integrate. Use `git log origin/main` after fetching to review incoming commits. |
| **Fork** | A copy of another user's repository created under your own GitHub account. Forking is used in open-source contribution: you fork the original project, make changes in your fork, and submit a Pull Request to propose those changes back to the original. Your fork is independent — changes in your fork do not affect the original unless your PR is accepted. |
| **Pull Request (PR)** | A proposal, created on GitHub, to merge one branch into another — typically a feature branch into `main`. A PR shows all commits on the branch, a diff of all changes, and a discussion thread where reviewers can comment, approve, or request changes. The merge itself happens only after review and approval. Pull Requests are the primary mechanism for code review and controlled integration in collaborative development. |
| **`git remote`** | Manages connections to remote repositories. `git remote -v` shows all configured remotes. `git remote add <name> <url>` adds a new remote. `git remote set-url <name> <url>` updates an existing remote's URL. The default remote name is `origin` by convention. |
| **GitHub** | A cloud-based hosting platform for Git repositories. Provides the repository web interface, Pull Requests, Issues, GitHub Actions, Codespaces, and GitHub Classroom. GitHub is not Git — it is a service built on top of Git. Other equivalent hosting platforms include GitLab and Bitbucket. |

---

## VI. Advanced Operations

| Term | Definition |
|---|---|
| **`git cherry-pick <hash>`** | Applies the changes introduced by a specific commit onto the current branch, creating a new commit with the same changes but a different hash. Use when you need a specific fix from another branch without merging the entire branch. |
| **`git grep <pattern>`** | Searches all tracked files for lines matching a pattern. Respects `.gitignore`. Useful for finding where a function, variable, or string is used across the project without leaving the terminal. |
| **`git blame <file>`** | Annotates each line of a file with the commit hash, author, and date of the last change to that line. Use to understand when and why specific lines of code were written or modified. |
| **`git archive`** | Creates a compressed archive (`.zip` or `.tar`) of the repository at a specific commit or tag. Use for distributing a snapshot of the project without the full Git history. |
| **`git submodule`** | Allows one Git repository to be embedded inside another as a tracked dependency. The outer repository stores a reference to a specific commit in the inner repository, rather than copying its files. Used in projects with shared libraries or dependencies that are themselves version-controlled. |
| **`git worktree`** | Allows multiple working directories to be attached to a single repository. Each worktree can be on a different branch simultaneously. Use when you need to work on two branches at the same time without stashing or committing incomplete work. |
| **`git shortlog -sn`** | Summarises the commit history by author — showing the number of commits per contributor. Useful for reviewing contribution distribution in a group project. |
| **`git tag -a <n> -m "message"`** | Creates an annotated tag at the current commit with a name and message. Annotated tags are stored as full Git objects with their own metadata and are the recommended format for release marking. `git push origin --tags` pushes all tags to the remote. |

---

## VII. Core Concepts — Extended

| Term | Definition |
|---|---|
| **Distributed Version Control** | Unlike centralised systems (where history lives on a single server), distributed version control gives every contributor a complete copy of the repository — including the full history. This means Git operations (commit, branch, log, diff) work without network access. It also means there is no single point of failure; any clone can reconstruct the full history. |
| **The Three Areas** | Git manages three distinct areas: the **working directory** (where files are edited), the **staging area** (where changes are prepared for commit), and the **commit history** (the permanent record). Most Git problems arise from confusion about which area a given operation affects. Every command in Git acts on one or more of these three areas. |
| **Fast-Forward Merge** | A merge where the current branch has no commits that are not already in the branch being merged. Rather than creating a merge commit, Git simply moves the current branch pointer forward to the tip of the other branch. The result is a linear history — as if the development had happened on one branch all along. |
| **Non-Fast-Forward** | A state in which the remote branch has commits that the local branch does not, making a simple fast-forward push impossible. Git rejects the push to prevent you from overwriting commits on the remote that you have not yet received. The resolution is to pull first (receiving the remote commits), resolve any conflicts, and then push the combined history. |
| **Protected Branch** | A branch configured on GitHub (or equivalent) to prevent direct pushes, require Pull Request approval before merging, or require passing CI checks before integration. Protected branches enforce collaboration and review discipline at the platform level rather than relying on individual compliance. |

---

## Summary

This glossary is organised to support understanding, not just lookup.

Sections move from foundational concepts to derived operations — repository setup, working on changes, recording history, branching, collaboration, and advanced operations. Reading a section in order builds the model; jumping to a specific term provides the definition.

Terminology is the foundation of fluency. Developers who can name and explain what they are doing can communicate with teammates, read documentation, understand error messages, and adapt to new tools — because the concepts those tools implement are the ones described here.

---

Proceed to:

→ 07-04 — Troubleshooting
