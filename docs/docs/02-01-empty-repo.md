# 02-01 — Creating a Repository From an Empty Remote

◼ Beginner

---

## When Does This Workflow Apply?

Before typing a single command, understand when this workflow is correct.

Choosing the wrong workflow at the start creates problems that are frustrating to untangle — particularly for beginners who may not yet have the diagnostic vocabulary to understand what went wrong. Taking thirty seconds to identify the right workflow before touching the terminal prevents the majority of these situations.

This workflow applies when:

- You are creating a brand-new project that does not yet exist anywhere
- The repository does not yet exist on GitHub — or it exists but is completely empty
- You are working under your own personal GitHub account, not a GitHub Classroom organization

This is the correct workflow for:

- Personal projects you are starting from scratch
- Practice exercises and experiments
- Portfolio projects that you are initiating locally
- Any project where you are the origin of the work

This workflow begins **locally**.

The remote repository is the destination — not the starting point.

---

## The Big Picture — Mental Model First

Before running any commands, understand what the workflow will accomplish.

The sequence is:

```
Local Project Folder
  → Initialize Git (begin tracking)
  → Record first snapshot (initial commit)
  → Create remote repository on GitHub (empty)
  → Connect local to remote (add origin)
  → Push first snapshot (upload history)
```

In plain terms:

I. Tell Git to start tracking your project folder  
II. Record your first version in local history  
III. Create a destination repository on GitHub — with nothing in it  
IV. Link your local repository to that destination  
V. Upload your local history to GitHub  

At the end of this workflow, your project exists in two places: on your machine and on GitHub, with a shared, connected history between them.

There is no remote history yet.
You are establishing it.

---

## Step 1 — Locate Your Project Folder

This step depends on how your project was created.

### Scenario A — Your IDE Created the Project

Most students begin inside an IDE:

- A Java project created in NetBeans
- A C# or ASP.NET project created in Visual Studio
- An Android project created in Android Studio
- A web project or folder opened in VS Code

In every case, the important detail is the **project folder location**. You must know:

- Where the project is saved on your machine
- Which folder is the root of the project — the one that contains your source files and project configuration

Git must be initialised inside this root folder. If you initialise in the wrong location, Git begins tracking the wrong files — which creates a confusing and difficult-to-repair situation.

---

### Opening a Terminal in the Correct Folder — Windows

I. Open your project folder in Windows Explorer  
II. Click in the address bar at the top of the window  
III. Delete the current path displayed  
IV. Type `cmd` and press Enter  

The Command Prompt will open **directly inside that folder**. This is the correct and reliable way to ensure you are in the right location before running any Git commands.

---

### Opening a Terminal in the Correct Folder — macOS

I. Open your project folder in Finder  
II. Right-click on the folder (or Control-click)  
III. Select "New Terminal at Folder"  

If this option is not available, enable it via: System Preferences → Keyboard → Shortcuts → Services → "New Terminal at Folder."

---

### Navigating Manually via Terminal

If you are comfortable with the command line, you can navigate to your project folder directly:

```bash
cd path/to/your-project
```

To confirm your current location:

```bash
cd        # Windows — prints current path
pwd       # macOS — prints current path
```

For beginners who are still building terminal confidence, creating a new folder manually is also a valid approach:

```bash
mkdir my-project
cd my-project
```

The critical principle is this: **Git must be initialised in the correct folder.** Verify your location before proceeding.

---

## Step 2 — Initialise Git

With the terminal open inside your project folder, run:

```bash
git init
```

Git will respond with something similar to:

```
Initialized empty Git repository in C:/.../your-project/.git/
```

This message confirms that Git has created a hidden folder named `.git` inside your project directory. This folder is the repository — it stores everything Git needs to track your project:

- Your complete commit history
- All branch information
- All remote configuration
- All staging area data

You will not see this folder unless your system is configured to show hidden files and folders. That is completely normal — it is hidden by design to prevent accidental modification.

⚠ **Important:** If the `.git` folder is ever deleted, your entire commit history is lost and Git will no longer recognise the folder as a repository. Do not delete it.

`git init` does not upload anything to GitHub.
It does not create a remote repository.
It simply begins tracking your project locally.

---

## Step 3 — Stage Your Files

Now that Git is tracking the project, tell it what to include in the first snapshot.

```bash
git add .
```

- `git add` moves files from the working directory into the staging area
- The dot (`.`) means "everything in this folder and all subfolders"

The staging area is a preparation zone — a deliberate selection of changes that are ready to be committed. Your files are now staged, but they have not yet been permanently recorded.

Verify what has been staged:

```bash
git status
```

You should see your files listed under "Changes to be committed." Make a habit of running `git status` before every commit — it costs nothing and confirms exactly what will be recorded.

---

## Step 4 — Create the First Commit

```bash
git commit -m "Initial commit"
```

This command takes everything in the staging area and permanently records it as the first snapshot in your local repository history.

Every commit stores:

- The state of all staged files
- Your configured name and email (from `git config`)
- An exact timestamp
- The message you provided

For the first commit, `"Initial commit"` is widely accepted as a standard message. From this point forward, commit messages should describe the specific change being recorded — not just that something changed.

A commit is not saving. It is a **recorded version in history** — a point you can return to, compare against, and reference in recovery operations.

---

## Step 5 — Create an Empty Repository on GitHub

Now move to GitHub to create the remote destination.

I. Log into your GitHub account
II. Click the **+** icon in the top-right corner
III. Click **New repository**
IV. Configure the following:

- **Repository name:** Use lowercase letters, hyphens instead of spaces (e.g., `my-project`, not `My Project`)
- **Visibility:** Public (visible to anyone — suitable for portfolio work) or Private (visible only to you and those you invite)
- **Do NOT tick "Initialize this repository with a README"**
- **Do NOT add a .gitignore**
- **Do NOT add a licence**

### Why must the repository be empty?

Because you have already created history locally. If GitHub creates a README file, it simultaneously creates a commit — and now the remote has a commit that your local repository does not. This is called diverging histories, and it causes the first push to fail with a rejection error.

This is one of the most common beginner mistakes. The fix exists (covered in 02-02), but it is entirely preventable by leaving the repository empty at creation.

V. Click **Create repository**

GitHub will display a setup page with instructions. This page confirms that the repository was created and is empty — exactly as required.

---

## Step 6 — Connect Your Local Repository to GitHub

On the GitHub setup page, locate the repository URL.

Click **Code** → Select **HTTPS** → Copy the URL.

It will look like:

```
https://github.com/yourusername/projectname.git
```

Note that:
- It ends in `.git`
- This is not the same as the browser URL for the repository page
- This is the URL Git uses for push and pull operations

Now, back in your terminal:

```bash
git remote add origin https://github.com/yourusername/projectname.git
```

This command registers a remote connection named `origin` that points to your GitHub repository. "Origin" is the universally accepted naming convention for the primary remote. Once this is configured, every push and pull operation can reference it by this name.

Verify the connection was configured correctly:

```bash
git remote -v
```

You should see two lines — one for fetch and one for push — both pointing to the same URL. If the URL is incorrect, update it:

```bash
git remote set-url origin https://github.com/yourusername/projectname.git
```

---

## Step 7 — First Push

Upload your local history to GitHub:

```bash
git branch -M main
git push -u origin main
```

### What `git branch -M main` does

This renames the current branch to `main`. Modern Git defaults to `main` as the primary branch name, and GitHub expects it. Older installations may have defaulted to `master`. Running this command ensures consistency regardless of your Git version.

### What `git push -u origin main` does

This command does three things simultaneously:

I. **Uploads your commits** — transfers all committed history to the GitHub repository
II. **Creates the remote branch** — establishes `main` on GitHub if it does not yet exist
III. **Sets upstream tracking** — the `-u` flag links your local `main` branch to `origin/main`, so that all future pushes and pulls from this branch know where to go automatically

After this first push, all subsequent pushes from this branch require only:

```bash
git push
```

The upstream is already configured. Git knows where to send the commits.

---

## The Ongoing Development Loop

After the initial setup is complete, your daily workflow simplifies to three commands:

```bash
git add .
git commit -m "Describe what you completed"
git push
```

You do **not** need to repeat:
- `git remote add origin ...`
- `git branch -M main`
- `git push -u origin main`

Those are first-time setup commands. Running them again on an existing repository will produce errors — particularly `git remote add`, which will tell you that `origin` already exists.

The development loop should become a habit — run it after every meaningful unit of progress, at the end of every working session, and always before closing your IDE.

If the work is not pushed, it is not on GitHub.
If it is not on GitHub, it has not been submitted.

---

## Common Mistakes in This Workflow

### Mistake I — Initialising the README on GitHub

**What happens:**
GitHub creates a commit when the README is added. Your local repository has a different first commit. The two histories have no shared ancestor. When you attempt to push, Git rejects it.

**Error message:**
```
error: failed to push some refs to 'https://github.com/...'
hint: Updates were rejected because the remote contains work that you do not have locally.
```

**Fix:**
If the repository was just created and contains nothing important, delete it on GitHub and recreate it without the README.

Alternatively, pull and merge the histories — this is covered fully in 02-02.

---

### Mistake II — Running Commands in the Wrong Folder

**What happens:**
Git is initialised in a parent folder, the Desktop, or the wrong project directory. Git begins tracking files you did not intend.

**Fix:**
Run `git status` to see which files are being tracked. If the output lists unexpected files or the wrong path, delete the `.git` folder that was created incorrectly and reinitialise in the correct location.

---

### Mistake III — Forgetting Your Current Location

Students sometimes open a terminal, do not check their current directory, and initialise Git in an unintended location — including the Desktop, which then attempts to track every file on the desktop surface.

Always verify your location before running `git init`:

```bash
cd        # Windows
pwd       # macOS
```

Or observe the path displayed in the terminal prompt. If the path shown is not your project folder, navigate there before proceeding.

---

## Institutional Standard for This Workflow

When starting your own project:

- Initialise locally — do not create any history on GitHub first
- Create the GitHub repository empty — no README, no .gitignore, no licence
- Use `-u` on the first push to set upstream tracking
- All subsequent work follows: add → commit → push
- Never use `--force` — it overwrites remote history and is not a recovery tool

This is professional practice. These habits are the same ones used by developers in every industry context where Git is the version control system of record.

---

Proceed to:

→ 02-02 — Repository Created with README
