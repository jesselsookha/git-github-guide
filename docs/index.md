# Git & GitHub Guide (2026 Edition)

Welcome.

This guide is a structured, institutional-grade reference designed to develop real Git competency — not button familiarity.

It does not simplify Git by hiding how it works.
It builds understanding by explaining why it works the way it does.

It is written for:

- First-year students encountering Git for the first time
- Intermediate students working in teams
- Senior students building production-level projects
- Lecturers aligning workflow and submission standards
- Developers at any stage who want a structured, concept-first reference

If you are not a student — if you are a developer, a career-changer, or someone returning to Git after a period away — this guide is still for you. The concepts are universal. The discipline is transferable. The structure scales.

---

## ◼ If You Are New to Git

Start here:

I. **Learning Path**
II. Part 1 — Foundations  
III. Part 2 — Guided Practice  
IV. Part 3 — Professional Standards  

Do not skip the Foundations section.

Git is not difficult — but misunderstanding early concepts creates confusion that compounds over time. Many developers who struggle with Git are not struggling with Git at all. They are struggling with a mental model that was never properly established.

The Foundations section exists to build that model correctly, from the beginning.

---

## ◆ If You Already Use Git

You may proceed directly to:

- Branching
- Pull Requests
- Group Workflows
- Reverting & Recovery
- GitHub Actions

However, before collaborating on assessed or production work, take the time to verify that your understanding of `pull`, merging, and commit discipline aligns with this guide. Many intermediate users have gaps they are not aware of — particularly around diverging histories, staging intent, and the difference between `reset` and `revert`.

If confusion arises at any point, return to Foundations.

Most Git problems are conceptual, not technical.

---

## ❈ If You Are Working in a Team

Read carefully:

- Branching
- Pull Requests
- Group Workflows
- Security & Academic Integrity

Team repositories do not fail because Git is difficult.
They fail because of inconsistent workflow — different assumptions, undocumented conventions, and decisions made without shared agreement.

This guide provides a structured collaboration model for both academic group projects and professional team environments. The principles are the same in both contexts. Only the stakes differ.

---

# What This Guide Is — And What It Is Not

This guide is:

- Concept-first
- CLI-grounded
- Tool-agnostic
- Academically structured
- Professionally aligned

This guide is not:

- A shortcut to pushing assignments
- A GitHub Desktop manual
- A collection of random commands
- A simplified "just click here" tutorial

You are expected to understand what Git is doing — not just which button to press.

The distinction matters. Buttons change. Interfaces change. Platforms change. The underlying model of how Git tracks, stages, commits, and synchronises history does not change. That model is what this guide teaches.

---

# How This Guide Is Structured

The content is layered intentionally.

◼ **Beginner sections** establish core mental models.
◆ **Intermediate sections** develop structured workflow.
▲ **Advanced sections** deepen control and recovery.
❈ **Collaboration sections** formalise academic and professional team practices.

Each section builds on the one before it. You may read linearly or reference specific sections as needed — but the Foundations are not optional, regardless of experience level. They establish the vocabulary and mental model that every later section depends on.

---

# The Core Principle

> A Git repository is not cloud storage.
> It is a version-controlled history of your work.

This distinction is not subtle. It changes everything about how you use Git.

Cloud storage stores files. Git stores *history* — a structured, navigable record of every meaningful change you have chosen to record. That history has authors, timestamps, messages, and relationships. It can be inspected, compared, branched, merged, and recovered from.

When you understand this properly:

- `clone` makes sense — you are replicating a history, not downloading a folder
- `init` makes sense — you are beginning a history, not creating a backup
- `pull` makes sense — you are merging remote history into your local one
- `push` makes sense — you are uploading your local history to a shared remote
- branches make sense — they are independent lines of history that can later be reconciled
- merge conflicts stop being frightening — they are moments where two histories diverge and require a human decision

Everything else becomes implementation detail.

---

# Before You Continue

Ask yourself:

- Do I understand what a repository actually is?
- Do I understand the difference between local and remote?
- Do I know when I should pull — and when I should not?
- Do I understand why `--force` is dangerous?

If the answer to any of these is uncertain, begin at **Part 1 — Foundations**.

There is no shortcut that bypasses this understanding.
There is only the choice between learning it now — or being confused by it later.

---

Proceed to:

→ **Learning Path**
