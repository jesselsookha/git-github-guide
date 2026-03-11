# 06-04 — NetBeans

---

## I. IDE Context

◼ Beginner

**NetBeans** is a long-standing open-source IDE maintained by the Apache Software Foundation, used primarily for Java development and also supporting PHP and C/C++. It is a mature, stable tool with a structured and relatively transparent Git integration — accessible through the **Team** menu.

NetBeans is well-suited to learning Git in an IDE context because its workflow is explicit: operations are named clearly, the commit window separates staging from committing in a visible way, and the interface does not automate as aggressively as enterprise IDEs.

---

## II. Under the Hood

When a project is under Git version control in NetBeans:

- File status is shown with **colour indicators** in the project tree: green for added files, blue for modified files
- The **commit window** (Team → Commit) presents files with checkboxes representing the staging area
- Branch operations update Git references through Team → Branch/Tag menus

**The verification test:** open a terminal in the project directory and run:

```bash
git status
```

The colour indicators and commit window reflect the same state. NetBeans is executing Git commands in the background — the terminal confirms this.

---

## III. Guided Workflow — New Java Project

Scenario: you create a new Java project in NetBeans and want to version-control and publish it.

### Step 1 — Initialise Repository

- **UI Action:** Team → Initialize Git Repository
- **CLI Equivalent:** `git init`
- **Effect:** Creates `.git` folder in the project directory

⚠ The initialisation dialog in NetBeans may offer to specify the repository root. Confirm that it matches the project root — the folder that contains your Java source files and NetBeans project configuration. Initialising in a parent folder tracks more files than intended.

---

### Step 2 — Stage Changes

- **UI Action:** Team → Commit → select files in the commit dialog
- **CLI Equivalent:** `git add <file>` or `git add .`
- **Effect:** Checked files are moved into the staging area

NetBeans' commit window combines staging and commit preparation in one dialog. Checking a file in the dialog is equivalent to running `git add` for that file. Unchecked files remain unstaged and will not be included in the commit.

This single-window approach is practical but requires attention: it is easy to proceed with the default file selection without reviewing whether all checked files should be in this commit.

---

### Step 3 — Commit

- **UI Action:** Enter message in the commit dialog → "Commit"
- **CLI Equivalent:** `git commit -m "message"`
- **Effect:** Creates a snapshot in local history

---

### Step 4 — Add Remote

- **UI Action:** Team → Remote → Add Remote
- **CLI Equivalent:** `git remote add origin <url>`
- **Effect:** Configures the remote repository connection

NetBeans will prompt for the remote URL. Use the HTTPS URL from GitHub (ending in `.git`). Once configured, verify:

```bash
git remote -v
```

---

### Step 5 — Push

- **UI Action:** Team → Remote → Push
- **CLI Equivalent:** `git push -u origin main`
- **Effect:** Uploads commits to the remote repository

Subsequent pushes: Team → Remote → Push (same action, but without the `-u` upstream configuration on the second and subsequent pushes).

---

## IV. Branching in NetBeans

- **UI Action:** Team → Branch/Tag → Create Branch
- **CLI Equivalent:** `git branch <n>` followed by `git switch <n>`
- **Effect:** Creates a branch pointer and updates HEAD

To switch between existing branches: Team → Branch/Tag → Switch To Branch. The branch history visualisation in NetBeans (Team → Show Changes) helps students understand how commits diverge on different branches.

---

## V. Common Misconceptions

**"Selecting files in the commit window is different from staging."**
It is not — selecting a file in NetBeans' commit window is the staging operation. Ticking a checkbox is `git add <file>`. The single window combines what the CLI separates into two commands, but the operation is identical.

**"Push will work without configuring a remote."**
It will not. NetBeans' push operation requires a remote to be configured first. If the remote was not added via Team → Remote → Add Remote, the push fails with a remote-not-found error. This is a common first-push problem in NetBeans.

**"When NetBeans prompts to pull before pushing, I can ignore it."**
When NetBeans reports that the remote is ahead — meaning the remote has commits your local repository does not — it will prompt to pull before pushing. This prompt must be understood, not dismissed. The remote is ahead because either a teammate pushed, or an initialisation action on GitHub created a commit. Pull, resolve any conflicts, then push.

---

## VI. Professional Insight

◆ Intermediate

NetBeans is used in professional Java development, particularly in enterprise and educational contexts. Its Git interface is less automated than Android Studio or Visual Studio, which makes it a useful learning environment — the operations are named and sequenced in a way that maps clearly to the underlying commands.

Professional developers using NetBeans for Java should maintain the same habits that apply in any IDE: verify remote configuration before pushing, check the branch indicator before committing to a shared repository, and periodically confirm state in the terminal to ensure the IDE's display matches the repository reality.

---

Proceed to: → 06-05 — GitHub Desktop

---
