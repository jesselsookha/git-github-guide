# 02-05 — Common Misconceptions and Conflict Prevention

◼ Beginner

By this point in the guide, you have worked through multiple workflows:

- Initialising locally and pushing to an empty remote
- Resolving diverging histories caused by a remote README
- Cloning Classroom repositories correctly
- Repairing an incorrectly initialised project

Most Git problems at beginner level do not come from technical complexity.

They come from misunderstanding the origin of a repository — who created it, where it lives, and what relationship exists between the local and remote copies.

This document consolidates the most common conceptual mistakes, explains why they happen, and provides a clear prevention model. Understanding these patterns removes the need to memorise fixes — because you will be able to identify the situation before it becomes a problem.

---

## I. The Most Important Question in Git

Before typing any command, ask:

**Who created this repository?**

This single question determines which workflow applies.

- If you created it → `git init`
- If it was created for you → `git clone`

Confusion begins almost every time a student skips this question and proceeds on assumption.

The assumption is usually: *"I need to get started, so I'll just run `git init`."* That assumption is correct in exactly one situation — when you are creating something from scratch that did not previously exist anywhere. In every other situation, it creates the problems documented throughout this section.

Asking the question costs five seconds.
The problems caused by skipping it can cost hours.

---

## II. Misconception 1 — "GitHub and Git Are the Same Thing"

This is the most foundational misconception in Git education, and it underlies many of the errors that follow from it.

**Git** is a version control system. It is software installed on your local machine. It tracks the history of changes in your project files. It manages branches, staging, commits, and merges. It works entirely offline. It has no knowledge of any remote platform unless you explicitly configure one.

**GitHub** is a hosting platform. It is a website — a service — that stores remote Git repositories on servers and provides a web interface for interacting with them. GitHub also adds its own collaboration tools: pull requests, issues, project boards, Actions workflows, and access management. But underneath all of those features, GitHub is simply storing Git repositories.

You can use Git without GitHub — local repositories, offline development, and even collaboration over direct network connections are all possible without GitHub being involved at all.

You cannot use GitHub meaningfully without Git — because everything GitHub does with your code depends on Git being the underlying version control system managing that code.

Understanding this separation explains behaviour that otherwise seems confusing:

- `git init` does not create anything on GitHub — it only initialises Git locally
- `git clone` copies the repository structure from GitHub to your machine
- `git push` is required because local and remote are separate — nothing synchronises automatically

---

## III. Misconception 2 — "Initialising on GitHub Is Always Helpful"

GitHub's repository creation form offers a helpful-looking checkbox: *"Initialize this repository with a README."*

It is understandable to tick this. A README is good practice. GitHub is encouraging you to start with documentation. What could go wrong?

What goes wrong is covered in full in 02-02. In summary: ticking that checkbox causes GitHub to create a commit before your local project has any commits. If you then initialise locally and create your own first commit, you have two repositories with different histories and no shared ancestor. Push fails.

The checkbox is not wrong — it is context-dependent.

- If you are starting from GitHub first and will clone immediately → tick it freely
- If you are developing locally first → leave it unticked, every time

Prevention is simple: when in doubt, create an empty remote. You can always add a README in your first local commit and push it as part of your normal workflow.

---

## IV. Misconception 3 — "If Push Fails, Something Is Broken"

When Git produces:

```
error: failed to push some refs
hint: Updates were rejected because the remote contains work that you do not have locally.
```

The natural reaction, especially for beginners, is to assume:

- Git is broken
- The installation is corrupt
- The GitHub repository has an error
- Everything needs to be deleted and started over

None of these are true.

This error message is Git working exactly as designed. It is telling you something precise and actionable: *the remote contains commits that your local repository does not have.* Before you can add to the remote history, you need to bring your local repository up to date with what is already there.

The solution is not to force the push.
The solution is to pull first.

```bash
git pull origin main
```

Then resolve any conflicts if they arise. Then push.

This pattern — pull, resolve, push — is the professional response to push rejection. Recognising the error message as information rather than failure is the first step to responding to it correctly.

---

## V. Misconception 4 — "Force Push Fixes Everything"

This misconception is particularly dangerous because it works — in the immediate sense. Running:

```bash
git push --force
```

after a push rejection does push your commits. The error goes away. The repository updates.

What is not visible is what was destroyed in the process.

Force push does not resolve diverging histories. It *erases* the remote history and replaces it with your local history. Any commits that existed on the remote but not on your machine are permanently deleted from the remote.

In a solo project where the only remote commit was a GitHub-generated README, this may seem inconsequential. But the habit of reaching for `--force` when push fails is one of the most damaging habits a developer can develop. In any collaborative context — shared repository, team project, Classroom group assignment — force pushing over commits that other people created destroys their work without warning.

**Force push is not a repair tool. It is a history rewrite tool.**

There are legitimate, advanced uses for force push — but they require a clear understanding of what will be overwritten and explicit consent from everyone who shares that repository. As a beginner response to a push rejection, it is never appropriate.

The institutional rule is simple and unambiguous: if push is rejected, pull. Not force.

---

## VI. Misconception 5 — "Download ZIP Is the Same as Clone"

GitHub presents a "Download ZIP" option on every repository page. It is prominently placed and easy to use. Many beginners use it because it feels familiar — it is just downloading files, like any other download.

The difference between ZIP and clone is not subtle. It is the difference between having a Git repository and not having one.

**Download ZIP:**
- Downloads the current state of the files only
- Contains no `.git` directory
- Contains no commit history
- Has no remote connection
- Cannot be used to push changes back to GitHub

**Clone:**
- Downloads the complete repository, including full commit history
- Creates a `.git` directory, establishing a fully functional local repository
- Automatically configures `origin` as the remote
- Enables push, pull, branch, and all other Git operations

A ZIP download is a snapshot of files.
A clone is a replication of the living repository.

They are not interchangeable. If you download ZIP and then try to work with the files as if they were a cloned repository, you will be unable to push — because there is no Git repository and no remote connection. The only correct approach in a Classroom context is always to clone.

---

# Conflict Prevention Model

◆ Intermediate

Most beginner Git problems follow the same underlying pattern. Rather than memorising individual fixes, understanding the pattern lets you prevent the problem before it occurs — or diagnose it quickly when it does.

### The Three-Stage Prevention Model

Every time you begin a Git operation, apply these three checks in sequence.

---

## Stage I — Identify Repository Origin

Ask: *Did I create this repository, or does it already exist somewhere?*

- If you created it → `git init` is correct
- If it exists on GitHub or in a Classroom organisation → `git clone` is correct

If the answer is genuinely unclear, stop. Open a browser, check GitHub, check the Classroom organisation, and find the repository before running any commands. Running `git init` when the repository already exists is the root cause of the majority of problems documented in this section.

---

## Stage II — Verify Remote Connection

Before pushing, confirm that your local repository is connected to the correct remote:

```bash
git remote -v
```

**If no output appears:** You are not connected to any remote. Add the correct one:

```bash
git remote add origin <url>
```

**If an incorrect URL appears:** Remove the incorrect remote and add the correct one:

```bash
git remote remove origin
git remote add origin <correct-url>
```

**If the correct URL appears:** You are connected. Proceed to Stage III.

This command alone — run habitually before every push — prevents a significant number of submission errors. It takes three seconds and provides absolute confirmation of where your commits will go.

---

## Stage III — Sync Before Push

Before pushing, ask: *Could the remote contain commits that I do not have locally?*

This is true whenever:

- Someone else has pushed to the shared repository since your last pull
- GitHub created a commit (e.g., from a README, Actions workflow, or Classroom template)
- You are working across multiple machines and pushed from one without pulling to the other

If there is any possibility the remote is ahead of your local copy, pull first:

```bash
git pull origin main
```

Resolve any conflicts. Then push.

**Push should never be the first instinct. Synchronisation should.**

The professional habit is: pull → work → commit → pull again → push. Pulling before pushing is a small cost with a large benefit: it prevents rejection errors, reduces conflict accumulation, and ensures the history you push is built on the most current foundation.

---

# Advanced Insight — Why Conflicts Exist

▲ Advanced

Understanding *why* conflicts happen — not just how to fix them — removes the anxiety that makes them feel dangerous.

Git is a **distributed** version control system. This is a deliberate architectural choice with important consequences.

In a centralised version control system, there is one authoritative server that everyone interacts with directly. Every change goes to the server immediately. Conflicts are prevented because only one person can edit a file at a time, or changes are locked until the previous version is checked in.

Git works differently. Every clone is a complete, independent, fully functional repository. When you clone a repository, you do not get a connection to a central copy — you get a full copy. You can work entirely offline. Your commits are recorded locally. The remote does not know you have made changes until you choose to push.

This means multiple people — or multiple machines — can work on the same file at the same time, producing different versions. When those versions are eventually reconciled (through push, pull, or merge), Git must determine how to combine them.

When the changes do not overlap — one person edited lines 1–20, another edited lines 50–70 — Git can merge them automatically without any input.

When the changes do overlap — two people edited the same lines in different ways — Git cannot determine which version is correct, because there is no objective answer. This is not a flaw. It is a design principle that preserves human agency over important decisions.

Conflicts are the moments where Git defers to you — and rightly so.

Understanding Git as distributed removes the fear that conflicts represent failure. They represent the natural consequence of independent development, and they are resolved by the same kind of judgment that created them: human decision-making.

---

# Classroom-Specific Pitfalls

❈ Collaboration

The following errors are observed specifically in GitHub Classroom environments and are worth naming directly.

**Initialising instead of cloning** — the primary error covered in 02-04. Always clone Classroom repositories.

**Pushing to a personal repository** — working in a personal GitHub repository rather than the Classroom organisation repository. The lecturer cannot see work that is not in the correct organisational space.

**Submitting ZIP files** — uploading a compressed archive to a submission portal instead of pushing commits to the repository. ZIP files do not contain Git history and are not an acceptable substitute in any Git-based submission workflow.

**Working offline without pushing before the deadline** — committing locally throughout the assignment period but never pushing. At the deadline, the remote repository is empty. Locally committed work that was never pushed is, from the perspective of the submission system, non-existent.

**Prevention strategy for all of these:**

After every working session, without exception:

```bash
git add .
git commit -m "Describe what you completed"
git push
```

If it is not pushed, it is not submitted.

This is not a strict rule imposed for academic reasons alone. It mirrors professional practice: work that is only on your machine is work that is at risk. A hard drive fails, a laptop is stolen, a file is accidentally deleted. The remote repository is the safe copy. Push regularly.

---

# Summary — The Discipline of Git

Git rewards discipline. The mistakes documented in this section are almost never the result of Git behaving incorrectly. They are the result of steps being skipped, questions not being asked, and assumptions not being verified.

Discipline means:

- Knowing where the repository came from before touching any commands
- Knowing which folder you are in before running `git init`
- Checking remote configuration before pushing
- Pulling before pushing in any shared context
- Never using `--force` to resolve a push rejection

Most Git problems are not technical. They are logical.

When something goes wrong, slow down. Ask: *What is the structure of this repository? Where did it come from? What does the remote contain that I might not have locally?*

Answering those questions leads to the correct resolution — almost every time.

---

Proceed to:

→ 02-06 — Assignment Lifecycle
