# 02-02 — Repository Created with README

◼ Beginner

This workflow applies when you create a repository on GitHub and select **"Initialize this repository with a README"**.

At first glance, this seems harmless. A README is a good thing — a professional repository should have one. Ticking the box feels like a helpful shortcut.

In practice, this single checkbox changes the structural relationship between your local and remote repositories in a way that needs to be understood — not avoided, but understood.

This document explains:

- Why the push fails in this situation
- What "diverging histories" actually means
- How to resolve it correctly
- What the professional standard is, and when initialising with a README is appropriate

---

## I. Core Concept — Why This Workflow Is Different

In 02-01, you created history locally first. The remote repository was empty when you connected to it, so there was no conflict — your local history became the remote history when you pushed.

In this workflow, history is created remotely first.

When you tick "Initialize this repository with a README", GitHub immediately:

- Creates a `README.md` file
- Records it as a commit
- Establishes the `main` branch at that commit

The remote repository is no longer empty.
It already contains a snapshot — one that your local machine does not have.

If you then create a project locally, run `git init`, and make your own first commit, you now have:

- A remote repository with one commit (the README)
- A local repository with one commit (your project)
- No shared history between them — no common ancestor commit

Git is designed to protect the integrity of history. When it detects two repositories with no shared ancestor and you attempt to push one into the other, it refuses. This is not a malfunction.

It is protection.

---

## II. What the Error Looks Like

After running the standard push sequence:

```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin <url>
git push -u origin main
```

Git responds with:

```
! [rejected] main -> main (fetch first)
error: failed to push some refs to 'https://github.com/...'
hint: Updates were rejected because the remote contains work that you do not have locally.
hint: Integrate the remote changes before pushing again.
```

Many students read this message and assume something is broken — their installation, their connection, their account settings. The message is actually precise and informative.

Git is saying: *"The remote has commits you do not have. I will not overwrite them. Bring those commits into your local repository first, then push."*

This is not an error.
It is a clear instruction.

---

## III. Understanding the Conflict — Mental Model

To resolve this correctly, visualise what exists on each side.

**Remote Repository (GitHub):**
```
Commit A — "Initial commit" — README.md added by GitHub
```

**Local Repository (your machine):**
```
Commit B — "Initial commit" — your project files
```

These two commits are independent. Neither knows the other exists. They have no shared parent — they are two separate starting points.

Git's history model is a linked chain: every commit points back to the commit before it. A merge is possible when two branches share a common ancestor somewhere in that chain — Git can trace back to the point where they diverged and reconcile the differences.

When there is no shared ancestor at all, Git calls this "unrelated histories." It cannot merge them automatically, because there is no reference point. Instead of guessing, it refuses — and waits for you to explicitly confirm that you understand what you are asking it to do.

---

## IV. The Correct Resolution — Pull Before Push

The solution is to bring the remote history down to your local machine first, merge it with your local history, and then push the unified result.

```bash
git pull origin main --allow-unrelated-histories
```

Let us unpack each component:

- `git pull` — fetches commits from the remote and merges them into your current branch
- `origin` — the name of the remote (configured in Step 6 of 02-01)
- `main` — the specific branch to pull from
- `--allow-unrelated-histories` — the explicit flag that tells Git: *"I understand these two histories have no shared ancestor. Merge them anyway."*

Without `--allow-unrelated-histories`, Git will refuse the merge entirely — because without the flag, unrelated histories are treated as a probable mistake. The flag is your confirmation that this is intentional.

After running this command, Git will:

I. Download the README commit from GitHub
II. Attempt to merge it with your local commit
III. If no file conflicts exist, create a **merge commit** that links both histories
IV. Your repository now has a unified history with both commits

If a text editor opens during this process (Git may prompt for a merge commit message), save and close it to confirm.

---

## V. After the Pull — Completing the Push

Once the pull and merge succeed, your local repository contains both commits — the GitHub README and your project work — with a merge commit connecting them.

Now push:

```bash
git push -u origin main
```

This time, the push succeeds.

Why? Because your local repository now includes the remote's history. There is no longer any divergence. Git can verify that your local commits build on top of the remote commits, and the push proceeds normally.

---

## VI. What If There Is a Merge Conflict?

In most beginner cases, the pull resolves cleanly because the remote only contains a README.md and your local project likely does not. There is no overlap to conflict.

However, if both the remote and your local project contain a README.md with different content, Git will pause and mark the file as conflicted.

You will see conflict markers inside the file:

```
<<<<<<< HEAD
Your local README content
=======
The README content from GitHub
>>>>>>> origin/main
```

To resolve:

I. Open the conflicted file in your editor
II. Decide which content to keep — yours, the remote version, or a combination of both
III. Delete the conflict markers entirely (`<<<<<<<`, `=======`, `>>>>>>>`)
IV. Save the file
V. Stage the resolved file and commit:

```bash
git add README.md
git commit -m "Resolve merge conflict in README"
git push -u origin main
```

Conflict resolution is not an emergency procedure. It is a normal part of working with Git in any environment where more than one source of change exists. The process is always the same: read the markers, make a decision, remove the markers, stage and commit.

---

## VII. Professional Insight — When Should You Initialise with README?

▲ Advanced

From a workflow perspective, the question of whether to initialise with a README depends on where your development is starting from.

**If you are developing locally first:**
Do not initialise with README on GitHub. Start with an empty repository as described in 02-01. Add the README locally as part of your first or second commit, and push it as part of your normal workflow. This avoids diverging histories entirely.

**If you are starting from GitHub first:**
Initialising with a README is entirely appropriate. In this scenario, clone the repository immediately after creation, and begin your project inside the cloned folder. The README commit is already in your local history from the moment you clone — no divergence, no conflict.

The pattern by skill level:

◼ **Beginner projects** — Initialise locally first. Keep the remote empty. Avoids the diverging history situation entirely.

◆ **Intermediate projects** — Understand the pull-before-push resolution. Be comfortable with `--allow-unrelated-histories` as a tool, not a workaround.

▲ **Advanced** — Manage diverging histories confidently. Understand when to allow unrelated histories, when to rebase instead of merge, and when the cleanest path is to delete and recreate the remote.

---

## VIII. Common Mistakes in This Workflow

### Mistake I — Force Pushing

When push fails, some students search online and find:

```bash
git push --force
```

Force push does resolve the rejection — but by overwriting the remote history entirely. The README commit that GitHub created is deleted. Any work that existed on the remote is erased.

In a solo beginner project this may seem harmless. In any collaborative environment, force pushing over others' commits is destructive and disrespectful.

**The institutional rule is clear:**
Do not use `--force` to resolve push rejections. Use `git pull` to bring histories together properly.

---

### Mistake II — Deleting and Recreating the Repository Repeatedly

This works — deleting the remote and recreating it without the README removes the divergence. But it teaches nothing and should only be used if the repository contains no meaningful content and the intent is simply to reset cleanly.

If you find yourself deleting and recreating repositories regularly, it is a signal that the underlying concept of diverging histories needs to be understood — not navigated around.

---

### Mistake III — Pulling Without Specifying the Branch

```bash
git pull
```

Without specifying `origin main`, this command may fail or produce unexpected results, particularly if upstream tracking has not yet been configured. During initial setup with unrelated histories, explicit is always better:

```bash
git pull origin main --allow-unrelated-histories
```

Clarity of intent produces clarity of result.

---

## IX. Summary — Decision Logic

Use this reference to choose the correct path:

| Situation | Action |
|---|---|
| Remote repository is empty | Follow 02-01 directly |
| Remote has a README commit | Pull with `--allow-unrelated-histories`, then push |
| Conflict occurs during pull | Resolve manually, stage, commit, then push |

The single rule:

**Before pushing, your local repository must contain all commits that the remote already has.**

If it does not, pull first.

---

Proceed to:

→ 02-03 — GitHub Classroom: Cloning Your Assignment Repository
