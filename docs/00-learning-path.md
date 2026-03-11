# Learning Path

This guide is designed to scale with you.

Git is not a one-semester tool.
It is a professional competency — one that develops progressively, in layers, over the full course of your studies and beyond.

The learning path below maps how your understanding should mature over time. Each stage introduces new depth without discarding what came before. Skills built in Year 1 are not replaced in Year 2. They become the foundation for what Year 2 requires.

If you are a working developer using this guide outside of an academic programme, read each stage as a level of maturity rather than a year of study. The progression is the same.

---

# Year 1 — ◼ Foundational Competence

Focus Areas:

I. Understanding what Git is and why it exists  
II. Working directory vs staging area vs committed history  
III. The relationship between local and remote repositories  
IV. The six core commands and what each one actually does  
V. A clean, consistent submission workflow  

Expected Outcome:

- You can create repositories — locally and on GitHub — and understand the difference between the two.
- You can connect a local repository to a remote and push work successfully.
- You can push without encountering conflict, because you understand what causes conflict in the first place.
- You understand when to pull before pushing, and why the order matters.
- You do not use `--force`, because you understand what it overwrites and why that matters.

What this stage is really about:

Year 1 is about building the correct mental model. The commands themselves are simple. What is difficult — and what this guide prioritises — is understanding the *structure* that those commands operate on. A student who understands the working directory, the staging area, and the commit history as three distinct and intentional spaces will make far fewer mistakes than one who has only memorised the commands.

Primary Sections:

- Foundations
- Guided Practice
- Professional Standards

---

# Year 2 — ◆ Structured Workflow

Focus Areas:

I. Branching — what a branch is, why it exists, and when to use one  
II. Merging — how branches are integrated and what merge commits represent  
III. Pull Requests — the formal mechanism for reviewing and accepting changes  
IV. Managing multiple features simultaneously without interfering with stable work  
V. Maintaining a clean, readable commit history that reflects structured development  

Expected Outcome:

- You work on branches confidently, creating them intentionally before beginning any new feature or fix.
- You merge deliberately — understanding what will happen before you execute the command.
- You can resolve basic merge conflicts without panic, because you understand what a conflict actually is.
- You collaborate on shared repositories without corrupting `main`.

What this stage is really about:

Year 2 is about discipline in a shared environment. A developer who understands branching and merging conceptually is not just more effective — they are safer to work with. The habits formed at this stage directly determine the quality of your collaboration in team projects, and they are the habits that professional environments will expect from day one.

Primary Sections:

- Collaboration
- Professional Standards
- IDE Workflows

---

# Year 3 — ❈ Academic Collaboration

Focus Areas:

I. Feature branch strategy — defining and agreeing on a branching model before work begins  
II. Pull request reviews — reading others' code critically and constructively before merging  
III. Merge discipline — understanding when to merge, who should merge, and how to document it  
IV. Conflict resolution — approaching diverging changes as a structured decision, not an emergency  
V. Repository hygiene — keeping commit history clean, branches named clearly, and `main` protected  

Expected Outcome:

- Your team has a documented workflow that everyone understands and follows consistently.
- `main` remains stable throughout the project, because no untested or unreviewed code is merged directly.
- Commits reflect structured development — small, logical, and clearly described.
- Merge conflicts, when they occur, are manageable and resolved through communication rather than force.

What this stage is really about:

Year 3 is where Git becomes a team instrument. The technical skills from Years 1 and 2 are assumed. The challenge now is coordination — aligning multiple contributors around shared conventions, shared history, and shared responsibility for the health of the codebase. This is the closest academic Git work comes to industry-grade collaboration, and the habits built here will transfer directly into professional environments.

Primary Sections:

- Group Workflows
- Security & Academic Integrity
- Advanced Recovery

---

# Final Year / Professional Preparation — ▲ Advanced Control

Focus Areas:

I. Reverting safely — undoing changes in a way that preserves history rather than erasing it  
II. Reset vs revert — understanding the difference between these two commands and when each is appropriate  
III. Recovering lost work — using Git's internal tools to retrieve commits that appear to be gone  
IV. GitHub Actions basics — understanding automated workflows and how they connect to repository events  
V. CI awareness — understanding what continuous integration means and why it depends on clean Git discipline  

Expected Outcome:

- You can recover from mistakes with confidence, because you understand that Git rarely destroys anything permanently.
- You understand history manipulation well enough to know when it is appropriate — and when it is not.
- You are aware of automation pipelines and understand how commit discipline directly affects them.
- Your Git history reflects the kind of structured, intentional development that professional environments expect.

What this stage is really about:

Final year is where control is fully internalised. The developer at this stage does not just use Git — they *think* in Git. They understand that a clean commit history is not an aesthetic preference but a functional requirement. They know that automation depends on structured branching, that recovery is possible because Git is non-destructive by design, and that the discipline built across previous years is what makes all of this reliable.

Primary Sections:

- Advanced
- Actions
- Reference

---

# Continuous Growth Model

Git proficiency develops in layers, not leaps:

Understanding → Discipline → Collaboration → Control

Each layer requires the previous one.

Understanding without discipline produces inconsistent work.
Discipline without collaboration produces habits that do not survive team environments.
Collaboration without control produces teams that cannot recover from mistakes.

If you skip layers, confusion increases — not just for you, but for everyone who works with your repositories.

If you follow the path, Git becomes predictable. Not easy in the sense of effortless, but predictable in the sense that you know exactly what is happening at every stage, and you know what to do when something goes wrong.

---

# The Professional Standard

By the end of your studies, you should be able to:

- Explain Git concepts clearly and accurately, without referencing tools or buttons
- Diagnose push and pull errors logically, by reasoning about repository state rather than trying commands at random
- Design a team workflow before coding begins, not as an afterthought when conflicts arise
- Maintain a clean, readable commit history that communicates your development process to anyone who reads it
- Recover from common repository mistakes with confidence, using the appropriate command for the situation

Git is not assessed only in assignments.

It is assessed implicitly in every interaction with a shared repository — in how you communicate through commit messages, in whether your branches are named clearly, in whether your `main` is stable, and in whether your history tells a coherent story of how the work was done.

That standard does not belong to academia alone.

It is the standard that professional teams hold each other to, every day.

---

Proceed to:

→ Part 1 — Foundations
