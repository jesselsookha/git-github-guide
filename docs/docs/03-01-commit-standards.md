# 03-01 — Commit Standards

◆ Intermediate

Committing is not saving.
It is recording.

The distinction matters more than it might initially seem. Saving a file preserves your current work on your local machine. Committing records a named, timestamped, authored snapshot of your project in a permanent history — one that can be reviewed, compared, recovered from, and evaluated by anyone who has access to the repository.

A commit is a permanent historical marker that contains:

- The complete state of all staged files at that moment
- Your configured name and email — establishing authorship
- An exact timestamp — establishing when the work was done
- A descriptive message — establishing what changed and why

In academic environments, commits are **evidence of development**. They demonstrate that work was done progressively, over time, by a specific person.

In professional environments, commits are **communication**. They tell the story of how a codebase evolved — a story that teammates, reviewers, and future maintainers will rely on to understand the work.

This document defines the standards for committing correctly — at both academic and professional levels.

---

## I. Core Principle — A Commit Is a Logical Unit of Work

A commit should represent one meaningful, self-contained change.

Not a week of accumulated edits.
Not a random collection of unrelated modifications.
Not a last-minute save before a deadline.

One logical unit.

What constitutes a logical unit depends on context, but the guiding question is always the same: *If someone reads this commit message without seeing the code, do they understand what changed and why?*

Good commits are:

- **Focused** — they address a single concern, feature, or fix
- **Intentional** — the developer made a deliberate choice to record this specific state
- **Descriptive** — the message communicates the nature of the change clearly
- **Chronological** — the sequence of commits tells a coherent story of development

Poor commits are:

- **Large and vague** — bundling hours of unrelated work with a message like "updates"
- **Misleading** — a message that does not accurately reflect what changed
- **Technically correct but semantically opaque** — the message is grammatically fine but provides no useful information

The difference between a good and poor commit history is not technical — it is a matter of discipline and communication.

---

## II. The Structure of a Good Commit Message

The minimum standard format for a commit message is a single, clear subject line of 50 characters or fewer:

```
Add login validation logic
Fix null reference in registration form
Implement sorting algorithm for student records
Update README with setup instructions
```

These messages are:
- Written in the **imperative mood** — as if completing the sentence "This commit will..."
- Specific enough that the change is identifiable without opening the diff
- Brief enough to display cleanly in `git log --oneline` and GitHub's commit list

Avoid:

```
update
changes
final
work
fix stuff
done
```

These messages communicate nothing. They do not tell a reviewer, a lecturer, or your future self what actually changed. They are entries in a history that cannot be read — which defeats the purpose of having a history at all.

A commit message must explain **what changed** — not simply that something changed.

---

## III. Extended Commit Messages — When More Context Is Needed

◆ Intermediate

For changes that require explanation beyond a single line, Git supports multi-line commit messages. The format is:

```
Short subject line (50 characters or fewer)

A longer explanation of what changed and why. This body section
is separated from the subject by a blank line. It can be as long
as necessary to provide context that the subject line cannot.

This is where you explain the reasoning behind the change — what
problem it solves, why this approach was chosen, or what edge cases
were considered.
```

When is an extended message appropriate?

- When a fix addresses a non-obvious bug and the reasoning behind the solution needs documenting
- When a refactor changes the structure of the code without changing its behaviour, and future readers need to understand why
- When a decision was made between competing approaches and the choice needs to be recorded

In academic contexts, this level of detail is not typically required for every commit. In professional environments, well-written commit bodies are a mark of seniority — they show that the developer is thinking not just about writing code, but about communicating decisions to the team.

---

## IV. Commit Message Types — Professional Convention

▲ Advanced

Many professional teams adopt the **Conventional Commits** specification — a lightweight standard for prefixing commit messages with a type label that clarifies intent. These prefixes improve readability, support automated changelog generation, and make the commit history scannable at a glance.

| Type | Purpose | Example |
|---|---|---|
| `feat:` | New feature | `feat: add user login functionality` |
| `fix:` | Bug fix | `fix: correct calculation error in payment module` |
| `chore:` | Maintenance tasks | `chore: update project dependencies` |
| `refactor:` | Code restructuring without behaviour change | `refactor: simplify authentication logic` |
| `docs:` | Documentation changes | `docs: update README with installation steps` |
| `style:` | Formatting, whitespace, or style fixes | `style: fix indentation in main activity class` |
| `test:` | Adding or updating tests | `test: add unit tests for login validation` |
| `perf:` | Performance improvements | `perf: optimise search query for large datasets` |
| `ci:` | Continuous integration configuration | `ci: fix broken build pipeline configuration` |
| `build:` | Build system or dependency changes | `build: update Gradle build script` |
| `revert:` | Reverting a previous commit | `revert: undo feat: add experimental payment gateway` |

Why does this convention matter?

Because at scale — in a team working on a large codebase — scanning hundreds of commits is only possible if they are categorised. A developer tracing a regression needs to quickly identify `fix:` commits. A release manager generating a changelog needs to identify `feat:` commits. Automated tools that produce version numbers and release notes depend on these prefixes to function correctly.

Students are not required to adopt Conventional Commits for academic work. But being aware of the convention — and beginning to apply it — develops habits that professional environments will recognise and value immediately.

---

## V. Good Practices for Commit Messages

◆ Intermediate

These practices apply at all levels — from first-year academic projects to production codebases:

- **Be clear and concise** — the message should be understandable to someone reading the history without the surrounding context
- **Use the imperative mood** — write "Add feature" rather than "Added feature" or "Adding feature." The convention is borrowed from the way Git itself writes automated messages: "Merge branch...", "Revert commit..."
- **Keep the subject line to 50 characters or fewer** — this ensures it displays correctly in `git log --oneline`, GitHub's commit list, and most Git tooling
- **Capitalise the first word** — treat it like a sentence beginning, without a trailing full stop
- **Do not use the subject line to explain why** — the *why* belongs in the body; the subject should describe *what*
- **Add a body when the change needs explanation** — separate it from the subject with a blank line, and write in full sentences

These are not arbitrary style rules. Each one exists because Git histories are read by people — under pressure, when something has gone wrong, or when understanding the past is necessary to make a good decision about the future.

---

## VI. Institutional Standard for Academic Projects

◼ Beginner

For beginner-level academic assignments, the expectation is clear and achievable:

Use plain, specific messages that describe what was done at each stage:

```
Add initial project structure
Implement Question 1 logic
Fix calculation error in Task 2
Add input validation to registration form
Refactor main method for clarity
Final submission adjustments
```

Commit at these moments:

- After completing each logical task or requirement
- At the end of every working session — even if the work feels incomplete
- Before closing your IDE — make it a closing habit

**Minimum expectation:** Multiple commits distributed across the development period.

A single large commit created minutes before the deadline does not represent healthy development. It cannot demonstrate process. It cannot show when work was started, how problems were approached, or where thinking evolved. Even if the final code is correct, a single-commit history raises questions that a well-distributed history answers naturally.

---

## VII. Frequency and Discipline

◆ Intermediate

Professional development consistently favours **small, frequent commits** over infrequent large ones. This is not merely a stylistic preference — it has practical consequences.

**Why small, frequent commits matter:**

- **Easier debugging** — when something breaks, `git bisect` and `git log` are only useful if commits are small enough to isolate the change that introduced the problem. A commit containing fifty changed files tells you almost nothing about where a bug entered.
- **Clearer change history** — reviewers can read a history of focused commits and understand the progression of work. A history of massive commits requires opening every diff to understand anything.
- **Better collaboration** — small commits reduce the surface area of merge conflicts. When each commit addresses one concern, conflicts are localised and easier to resolve.
- **Easier recovery** — reverting a small, focused commit is safe and precise. Reverting a large commit that bundled ten unrelated changes creates risk of removing valid work alongside the problematic change.

In academic contexts, frequent commits also demonstrate:

- Progressive development — the work happened over time, not all at once
- Independent work — a pattern of commits across multiple sessions is consistent with genuine development
- Structured problem-solving — the order of commits reflects a logical approach to the assignment

If your repository shows only one commit at the moment of submission, it does not reflect a healthy workflow. Even if the final product is excellent, the history undermines the evidence of how it was produced.

---

## VIII. What Should Not Be Committed

Certain categories of files should never be committed to a repository — not because they cannot be, but because doing so creates security risks, repository bloat, and collaboration problems.

**Never commit:**

- **Compiled binaries** — `.exe`, `.class`, `.jar`, `.apk`, `.dll` files are generated from source code and should be reproducible from it. Committing them bloats the repository and creates noise in diffs.
- **Build output folders** — `bin/`, `obj/`, `build/`, `dist/` directories change with every compilation and have no place in version history.
- **IDE-specific configuration files** — `.idea/`, `.vs/`, `.vscode/` (unless the team has agreed to share VS Code settings), `.DS_Store` on macOS. These are machine-specific and pollute other developers' environments when committed.
- **Secrets and credentials** — API keys, passwords, connection strings, `.env` files containing private configuration. Once committed to a public or semi-public repository, these credentials must be considered compromised. This is not recoverable by simply deleting the file in a subsequent commit — the credential remains visible in the history.
- **Large media files** — videos, high-resolution images, and other large binary files are poorly suited to Git's diff model and inflate repository size significantly.

The tool for managing this is the `.gitignore` file — a configuration file at the root of the repository that tells Git which files and patterns to exclude from tracking entirely. Every project should have one, tailored to the technologies in use. GitHub provides template `.gitignore` files for most common languages and frameworks.

---

## IX. Amending vs Rewriting History

▲ Advanced

Git provides commands that allow previously recorded commits to be modified:

```bash
git commit --amend    # Modify the most recent commit
git rebase -i         # Interactively reorder, edit, or squash multiple commits
```

These are powerful tools — and they must be used with an understanding of their consequences.

**`git commit --amend`** replaces the most recent commit with a new one. The original commit is discarded. This is useful for correcting a typo in a commit message or adding a file that was accidentally omitted from the last commit — *provided that commit has not yet been pushed.*

Once a commit has been pushed to a shared remote, amending it changes its hash. Anyone who has already pulled that commit now has a version of history that conflicts with yours. Pushing an amended commit requires `--force`, which overwrites the remote's history — and causes problems for every contributor who has built on top of it.

**`git rebase -i`** allows you to reorganise, edit, combine (squash), or delete commits from a branch's history. In a professional context, this is used to clean up a messy working branch before merging into `main` — presenting a polished series of commits rather than a rough development trail.

Guidelines:

- **Before pushing** — amending and rebasing are safe. No one else has seen those commits yet.
- **After pushing to a shared branch** — do not rewrite. The cost to collaborators is not worth the benefit of a cleaner history.
- **In academic contexts** — do not rewrite history after any point where the work has been seen or assessed. Timestamps and sequence are part of the academic record.
- **As a rule of thumb** — if others have pulled your commits, those commits are part of the shared history and should not be changed.

The right moment for history cleanup is before integration, not after.

---

## X. Commit Quality as Professional Identity

A well-maintained commit history communicates things about a developer that no CV can:

- **Discipline** — the developer commits regularly, not sporadically
- **Technical maturity** — commit messages describe changes at the right level of abstraction
- **Clarity of thought** — logical units of work reflect organised thinking
- **Respect for collaborators** — clear messages acknowledge that others will read this history

Your Git history is part of your professional footprint. It is visible in every public repository, reviewable in every assessment, and inspectable in every technical interview that involves a portfolio review.

Even in academic projects — especially in academic projects — treat it as such. The habits that form during study are the habits that follow you into every professional environment you enter.

---

## Summary

A commit is not a backup.
It is a documented decision.

Every commit you make is a statement: *"This is a meaningful point in the development of this project, and here is what changed and why."*

Commit:

- **Clearly** — with messages that a stranger could read and understand
- **Frequently** — after each logical unit of work, not at the end of a week
- **Logically** — staging related changes together, not everything at once
- **Responsibly** — without force-pushing over shared history or rewriting the record

Professional standards begin at student level.
The history you build today is the portfolio you present tomorrow.

---

Proceed to:

→ 03-02 — README Guide
