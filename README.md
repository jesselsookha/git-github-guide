# Git & GitHub Guide

**A structured, institutional-grade Git reference for students and educators.**

> Concept-first. CLI-grounded. Professionally aligned.

◼ Built for first-year students  
◆ Useful for intermediate developers  
▲ Valuable for advanced practitioners  
❈ Designed with team and group workflows in mind

---

## About This Guide

This guide was written from the front of a classroom.

As a lecturer in the practical programming space at Emeris, working with students across all year groups, a pattern became impossible to ignore: students were submitting broken repositories, overwriting each other's work in group projects, and treating Git as a filing system rather than a version control system. Existing tutorials — abundant as they are — were either too shallow to build real understanding, or too generic to address the specific pressures of assessed academic work.

This guide is the response to that pattern.

It addresses not just the commands, but the mental models behind them. It is structured to grow with a student across a full academic programme — from a first-year who has never opened a terminal, through the complexities of team collaboration, to a final-year developer preparing for professional practice. It is also written for lecturers who want a structured, dependable reference they can align their own teaching and submission standards to.

The live site is the primary format. It is free, complete, and publicly accessible.

→ **[Read the full guide](https://jesselsookha.github.io/git-github-guide/)**

---

## Why This Guide Exists

Most Git resources teach button locations. Click this, type that, push, done.

That approach produces students who can follow a workflow on a good day — and are completely lost the moment something goes wrong. They do not know what a staging area actually is. They do not understand why a push was rejected. They cannot recover a deleted branch. They do not know what their assessor can see in the commit history.

This guide takes a different position: **understanding before instruction**. Every command is preceded by an explanation of what it does and why it exists. Every IDE workflow is mapped back to its CLI equivalent — because a button that is understood is a button that can be replaced by a terminal, a different IDE, or a team with different tools.

The result is a guide that does not become obsolete when the interface changes.

---

## Who This Is For

| Audience | Best Starting Point |
|---|---|
| ◼ First-year students — encountering Git for the first time | Part 1 — Foundations |
| ◼ Students who can push but lack confidence or understanding | Part 2 — Guided Practice |
| ◆ Students preparing for assessed submissions | Part 3 — Professional Standards |
| ❈ Students working in group projects | Part 4 — Collaboration |
| ▲ Students who have made mistakes and need to recover | Part 5 — Advanced Topics |
| ◆ Students working across different IDEs | Part 6 — IDE Workflows |
| ▲ Any developer wanting structured reference | Part 7 — Reference |
| ❈ Lecturers designing Git workflows for their cohort | Parts 3, 4 & 7 |

---

## What the Guide Covers

```
◼  Part 1 — Foundations
      Why Git Matters · Welcome to Git · Installation · Configuration
      How Git Works · The Six Core Commands

◼  Part 2 — Guided Practice
      Empty Repository · Repository with README · GitHub Classroom Clone
      GitHub Classroom Init · Common Misconceptions · Assignment Lifecycle

◆  Part 3 — Professional Standards
      Commit Standards · README Guide · Submission Checklist

❈  Part 4 — Collaboration
      Branching · Pull Requests · Group Workflows
      Security & Academic Integrity

▲  Part 5 — Advanced Topics
      Reverting & Inspecting History · Recovery · GitHub Actions · Codespaces

◆  Part 6 — IDE Workflows
      IDE Philosophy · Visual Studio Code · Visual Studio · Android Studio
      NetBeans · GitHub Desktop · macOS Terminal

▲  Part 7 — Reference
      Decision Trees · Cheat Sheet · Glossary · Troubleshooting · Templates
```

---

## On Group Work and Team Collaboration

One of the most common points of failure in assessed group projects is not the code — it is the repository.

Branches overwritten. Commits made directly to `main`. A single contributor's name on 90% of the history. Merge conflicts nobody knows how to resolve. A repository that tells a story the group cannot explain.

❈ **Part 4** addresses team Git workflows directly and in depth — covering branching strategy, pull request discipline, the full mechanics of merge conflict resolution, and the academic integrity implications of commit history. **Part 6** extends this into the IDE environments students actually use: VS Code, Visual Studio, Android Studio, NetBeans, and GitHub Desktop — each with CLI equivalents mapped explicitly, so that the underlying Git model is never hidden behind a button.

The guide does not assume everyone in a team is working from the same IDE, or even the same operating system. It assumes everyone is working from the same Git.

---

## Core Principles

**◼ CLI-first.** Every IDE action is mapped to its CLI equivalent. Understanding the command means understanding any interface that runs it — now and in five years when the interface has changed.

**◆ Concept before tool.** Each section explains what Git is doing and why before showing how to do it. Commands without models produce students who cannot recover when something goes wrong.

**▲ Depth over simplification.** This guide does not reduce Git to five commands and a button. It builds understanding that scales — from a first assignment to a production codebase.

**❈ Academically honest.** Sections on academic integrity, commit timestamps, contribution visibility, and AI tool disclosure reflect the reality of assessed work. The guide is direct about what lecturers can see in a repository — because honesty serves students better than comfortable omission.

---

## Difficulty Level Key

| Symbol | Level | What It Means |
|---|---|---|
| ◼ | Beginner | Core concepts — no prior Git knowledge assumed |
| ◆ | Intermediate | Structured workflow — assumes basic familiarity |
| ▲ | Advanced | Deeper control, recovery, and automation |
| ❈ | Collaboration | Team practice, academic integrity, group workflow |

Sections are marked consistently throughout the guide. You can read linearly or navigate directly to the level relevant to your current work — the Learning Path section on the live site maps the full progression by year of study.

---

## The Live Site

This guide is published as a structured, searchable website using [MkDocs Material](https://squidfunk.github.io/mkdocs-material/) and hosted on GitHub Pages.

→ **[https://jesselsookha.github.io/git-github-guide/](https://jesselsookha.github.io/git-github-guide/)**

The site includes full-text search, a light and dark mode, mobile-friendly navigation, and a table of contents on every page. The repository contains the full source — all content files, the MkDocs configuration, and the GitHub Actions workflow that rebuilds and redeploys on every push.

---

## For Educators and Institutions

◆ This guide was developed from direct teaching experience and is structured as a curriculum resource — not a reference dump. It includes classroom activities, reflection questions, submission checklists, and templates designed for assessed academic work.

Lecturers and programme coordinators who want to align a cohort to a consistent Git workflow, provide a structured reference that complements their teaching, or explore institutional adoption are welcome to make contact.

❈ **Institutional licensing** — for programmes, departments, or institutions wanting to formally adopt this guide, integrate it into commercial training materials, or commission curriculum adaptation work, a separate licensing arrangement applies under the terms of the CC BY-NC-ND 4.0 licence included in this repository.

| Contact | Purpose |
|---|---|
| jsookha@emeris.ac.za | Institutional and departmental enquiries |
| jsookha@gmail.com | General, external, and consultancy enquiries |

---

## Run the Site Locally

```bash
pip install mkdocs-material
mkdocs serve
```

Open [http://127.0.0.1:8000](http://127.0.0.1:8000) — the site hot-reloads on every file save.

---

## Licence

© 2026 J. Sookha. All rights reserved.

Published under **Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International (CC BY-NC-ND 4.0)**.

Free to read and share with attribution. Not free to sell, adapt for redistribution, or include in commercial products without a separate written agreement.

Full licence terms: [LICENSE](./LICENSE)

---

*Written for students who want to understand Git — not just survive it.*
