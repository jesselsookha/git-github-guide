# How Git Works

◼ Beginner  
◆ Intermediate  

Most Git confusion does not come from commands.

It comes from not understanding the model.

A developer who has memorised the commands but not the model will follow steps correctly until something unexpected happens — and then be completely lost. A developer who understands the model may not remember the exact syntax, but they can reason about what a command should do, why an error occurred, and what the correct resolution looks like.

Once the model is clear, the commands become logical.

This section builds that model.

---

# I. Git Is a Snapshot System

Git does not store files the way traditional backup systems or cloud storage do.

A conventional backup copies your files and stores them. If you modify a file and back up again, you have two copies — the old version and the new one. But those copies exist as separate files, with no built-in relationship between them, no explanation of what changed, and no way to reconstruct the history of changes without comparing them manually.

Git works differently.

It stores *snapshots* of your project at specific moments in time. Each snapshot — called a commit — represents the complete state of your project at the moment you recorded it, along with:

- A full record of the project state — every tracked file at that point in time
- A timestamp — the exact date and time the commit was created
- An author — the name and email of the person who made the commit
- A message — a human-readable description of what changed and why
- A reference to the previous commit — creating a linked chain of history

The result is not a collection of edited files.
It is a structured, navigable timeline of project states.

Think of it as a sequence of photographs taken at meaningful intervals throughout the development of your project. Each photograph shows the complete picture. The sequence shows the story of how the project evolved.

This is why Git is so powerful for recovery. You are not looking for a "before" file to compare against an "after" file. You are navigating between known, complete project states.

---

# II. The Three Core Areas

Every Git repository has three distinct conceptual areas. Understanding what each one is — and what it is not — resolves a large proportion of beginner confusion.

### 1. Working Directory

The working directory is your actual project folder — the files you can see, open, and edit directly on your computer.

When you modify a file, that change happens in the working directory first. At this point, Git is aware that the file has changed (because it is tracking the project), but the change has not been recorded in any way. It is simply a modification in progress.

The working directory is where development happens.
It is not where history is stored.

---

### 2. Staging Area (Index)

The staging area is an intermediate preparation zone between the working directory and the repository.

When you are ready to record a change, you do not commit everything in your working directory automatically. Instead, you explicitly *select* which changes should be included in the next commit, and place them into the staging area.

This deliberate selection mechanism is one of Git's most important design features — and one that beginners frequently misunderstand or underuse.

Why does the staging area exist?

Imagine you have been working for two hours and have made changes to five different files. Some of those changes belong together logically — they are part of the same feature. Others are unrelated fixes. The staging area allows you to commit the related changes as one logical unit, and commit the unrelated changes separately. The result is a clean, readable history where each commit represents a coherent piece of work.

Without the staging area, every commit would bundle everything together — and the history would become a record of time spent rather than a record of logical progress.

You do not commit everything automatically.
You commit intentionally.

---

### 3. Repository (Local)

The local repository is Git's internal database — stored inside the hidden `.git` folder at the root of your project.

This is where committed history lives. Every commit you have ever made on this machine, for this project, is stored here. The repository contains:

- The full commit history — every snapshot you have recorded
- Branch information — which commits belong to which branches and where each branch currently points
- Configuration — remote connections, settings, and reference data

Once a change is committed, it is recorded permanently in the repository. It can be referenced, inspected, and recovered from at any point. This permanence is what makes Git a reliable history system rather than just a file tracker.

The repository is the source of truth for your project's history.

---

# III. The Flow of Change

Understanding the three areas individually is necessary. Understanding the directional flow between them is what makes Git usable.

The complete flow of a change, from editing to sharing, looks like this:

```
Working Directory
  → (git add)
Staging Area
  → (git commit)
Local Repository
  → (git push)
Remote Repository (GitHub)
```

And when retrieving changes from a shared remote:

```
Remote Repository (GitHub)
  → (git pull)
Local Repository
```

Each arrow represents a specific Git command. Each command moves the change one step further along the flow. Nothing moves automatically — every transition is explicit and under your control.

This directional model eliminates most confusion. When a student asks "why didn't my changes appear on GitHub?" the answer is almost always that a step in this flow was skipped. The change existed in the working directory but was never staged. Or it was staged but never committed. Or it was committed but never pushed. Each of those is a distinct, diagnosable situation — and each one has a specific resolution.

---

# IV. Local vs Remote

The distinction between local and remote is fundamental to understanding Git's collaborative model.

**Local Repository:**
- Exists on your machine, in the `.git` folder inside your project
- Works offline — you can commit, branch, and review history without an internet connection
- Contains your full project history — every commit you have ever made on this machine

**Remote Repository (e.g., GitHub):**
- Exists on a server, hosted by a platform like GitHub, GitLab, or Bitbucket
- Enables collaboration — multiple contributors can push to and pull from the same shared history
- Stores the shared version of the project — the authoritative record that all contributors synchronise with

Git does not automatically synchronise these two.

You are always in control of when synchronisation occurs. This is a deliberate design choice. Git is a *distributed* version control system — meaning every contributor holds a full, independent copy of the repository. There is no single "master copy" that everyone edits directly. Instead, each developer works locally and then explicitly chooses to share their changes by pushing, and explicitly chooses to receive others' changes by pulling.

This design is what makes Git resilient. If the remote server goes down, every contributor still has a complete copy of the history. Work can continue locally and be synchronised later.

---

# V. What `git pull` Really Means

`git pull` is one of the most commonly misunderstood commands in Git, and the misunderstanding has real consequences.

Many beginners treat `git pull` as "download my files from GitHub." This mental model is incorrect, and it leads to errors that are difficult to explain without understanding what `pull` actually does.

`git pull` is not a download command.

It is the combination of two separate operations:

```
git fetch    — retrieve commits from the remote repository
git merge    — merge those commits into your current local branch
```

When you run `git pull`, Git first fetches any commits from the remote that you do not have locally. Then it attempts to merge those commits into your current branch. The result is a merged local branch that contains both your work and the work from the remote.

This is why conflicts can occur during a pull.

If someone else modified the same lines of code that you modified since your last synchronisation, Git cannot automatically determine which version is correct. Both sets of changes are legitimate — they just happen to overlap. Git pauses and asks you to resolve the conflict manually before the merge can be completed.

This is not an error. It is Git doing its job correctly.

Understanding `pull` as `fetch + merge` also explains why the order of operations matters: you should generally pull before pushing in a shared repository, to ensure that your local history is current before you try to add to the remote history.

---

# VI. Why Merge Conflicts Happen

Merge conflicts are the most feared event for Git beginners. They are also among the most misunderstood.

A conflict is not a sign that something has gone wrong.
It is a sign that two sets of work have diverged and now need to be reconciled.

Conflicts happen when:

- Two contributors modify the same lines of the same file on different branches or at different times
- Two branches change the same file structure in incompatible ways

Git cannot resolve these situations automatically, because doing so would require guessing intent — and Git does not guess. It stops, marks the conflicting sections clearly inside the affected files, and waits for a human decision.

The conflict markers look like this:

```
<<<<<<< HEAD
Your version of the code
=======
The incoming version of the code
>>>>>>> branch-name
```

Everything between `<<<<<<< HEAD` and `=======` is your version. Everything between `=======` and `>>>>>>> branch-name` is the incoming version. Your job is to decide: keep yours, keep theirs, or write a combination that incorporates both.

Conflicts are decision points — not errors, not failures, not signs that something is broken.

Experienced developers encounter conflicts regularly and resolve them calmly, because they understand what is happening. Beginners who have not been taught this model sometimes panic and make things worse by attempting to force-push their way out of the situation. Understanding conflicts removes that impulse.

---

# VII. The Mental Model — Putting It Together

If you understand:

- The **working directory** — where you make changes
- The **staging area** — where you select what to record
- The **local repository** — where committed history is stored
- The **remote repository** — where shared history lives
- The **directed flow of changes** — add → commit → push, pull → merge

Then every Git command becomes predictable. You will always know which area a command affects, why it behaves the way it does, and what the expected outcome should be.

Without this model, Git feels arbitrary — commands that sometimes work and sometimes produce confusing errors, with no apparent logic connecting them.

With this model, Git becomes a structured, logical system. The commands are not a list of things to memorise. They are a vocabulary for describing operations on a model you understand.

Understanding the model is more important than memorising commands.

Commands can be looked up. Understanding cannot be Googled in the middle of a crisis.

---

Proceed to:

→ Core Git Commands
