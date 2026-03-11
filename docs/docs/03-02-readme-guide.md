# 03-02 — README Guide

◆ Intermediate

A repository without a README lacks context.

Code alone does not explain itself. A repository may contain perfectly written, functional code — and still be impenetrable to anyone who did not write it. The README is the document that provides the missing context: what this project is, why it exists, how to use it, and who is responsible for it.

In academic settings, a README demonstrates clarity of communication — the ability to explain technical work in plain language, which is a skill as important as the technical work itself.

In professional environments, a README is essential documentation. Open-source projects without READMEs attract no contributors. Internal tools without documentation create dependency on the original developer. Portfolio repositories without READMEs are invisible to employers who cannot quickly determine what a project does.

A README is not optional decoration.
It is structured explanation — and it should be treated as part of the deliverable.

---

## I. Core Purpose — What a README Must Answer

A README should answer five fundamental questions:

I. **What is this project?** — a clear, specific description of what it does
II. **What problem does it solve?** — the purpose or motivation behind the project
III. **How do I run it?** — step-by-step setup and execution instructions
IV. **What technologies are used?** — languages, frameworks, tools, and dependencies
V. **Who is responsible?** — authorship and contact information

If those five questions are unanswered, the repository is incomplete — regardless of how well the code is written.

Think of the README as the **front door** of your project. It is the first thing a visitor sees when they arrive at your repository. It sets expectations, provides orientation, and determines whether someone will engage with the project further or leave immediately.

A clear, professional README signals that the developer is thinking about their audience — not just about their own understanding of the code.

---

## II. Minimum Academic README Structure

◼ Beginner

Every academic repository must include a README that covers the following:

### Project Title

A clear, specific name that describes the project rather than the assignment. Avoid titles like *"Assignment 1"* or *"Project"* — these communicate nothing to anyone reading the repository independently.

Prefer:
- *"Sorting Algorithms in Java"*
- *"Student Registration Web Application"*
- *"Budget Tracker Android App"*

### Description

A short paragraph explaining what the project does and what learning objective or requirement it addresses. For example:

*"This project implements three sorting algorithms — bubble sort, selection sort, and merge sort — in Java, as part of the Data Structures and Algorithms module. It demonstrates comparative performance across randomly generated datasets."*

### Technologies Used

List the languages, frameworks, IDEs, and tools involved. This helps any reader — including yourself returning to the project months later — understand what is needed to run it.

Example:
- Java 17
- NetBeans IDE 20
- JUnit 5 (for testing)

### How to Run

Step-by-step instructions written for someone with no prior knowledge of the project. Do not assume familiarity with your specific setup.

Example:
```
1. Clone the repository using git clone <url>
2. Open the project in NetBeans via File → Open Project
3. Run Main.java using the green play button
4. Follow the console prompts to select a sorting algorithm
```

The test: could a classmate who has never seen your project follow these instructions and run it successfully? If not, add more detail.

### Author Information

Include your full name, student number (if required by your institution), and the course or subject. This establishes accountability and ensures your work is correctly attributed in academic records.

---

## III. Intermediate README Enhancements

◆ Intermediate

A foundational README covers the minimum. A stronger README demonstrates a deeper engagement with documentation as a discipline.

Consider adding:

- **Folder structure explanation** — a brief description of what each directory contains. This helps contributors and reviewers navigate the project without having to open every file.

  ```
  /src          — source code files
  /tests        — unit test files
  /docs         — additional documentation
  /screenshots  — interface screenshots
  ```

- **Screenshots or output examples** — a visual showing the running application or expected output. A single screenshot communicates more than several paragraphs for a UI-based project.

- **Example input/output** — for algorithmic or data-processing projects, showing a sample run helps readers verify they are using the project correctly.

- **Known limitations** — acknowledging what the project does not do, or what known issues exist, demonstrates intellectual honesty. It also prevents users from filing bug reports for expected behaviour.

- **Reflection notes** — particularly valuable in academic contexts. A brief section discussing challenges encountered and how they were resolved demonstrates problem-solving process — which is often part of what is being assessed.

Use Markdown formatting throughout. A well-formatted README with clear headings, code blocks, and bullet points is significantly easier to read than a wall of plain text — and the effort required is minimal once the syntax is understood.

---

## IV. Professional README Structure

▲ Advanced

Professional repositories — particularly those intended for open-source contribution, public use, or team collaboration — require a more comprehensive README structure.

Professional READMEs typically include:

- **Installation instructions** — how to set up the project on a local machine from scratch, including any system prerequisites
- **Environment setup** — required runtime versions (Node.js, Python, Java, .NET), environment variables, and configuration files
- **Configuration requirements** — how to configure API keys, database connections, or settings files (without including the actual secrets — use a `.env.example` template)
- **Licence information** — clarifying the terms under which the code can be used, modified, and distributed. A missing licence in a public repository means the code is technically under the author's full copyright and cannot legally be used by others.
- **Contribution guidelines** — explaining how to report issues, how to submit pull requests, the expected coding standards, and the review process
- **Version history or changelog** — documenting what changed between releases, which helps users understand whether to upgrade and what to expect
- **Contact information** — where to reach the maintainer for questions, support, or collaboration

Professional READMEs serve **contributors as much as users**. They are as much about how to participate in the project as they are about how to use it. An open-source project with a clear, welcoming README attracts contributions; one without creates barriers.

---

## V. The README as a Markdown Document

◆ Intermediate

README files on GitHub are written in **Markdown** — a lightweight text formatting language designed to be readable as plain text while rendering as formatted content in the browser.

Markdown's simplicity is its strength. It requires no special tools, works in any text editor, and produces clean, professional output when rendered. Understanding the core syntax allows you to structure your README clearly and efficiently.

Why does the format matter? Because an unformatted README — a wall of plain text with no headings, no code blocks, and no visual structure — is difficult to read. Formatting is not cosmetic. It is a service to your reader.

Key Markdown syntax:

**Headers** create navigable sections:
```
# Project Title
## Installation
### Step 1
```

**Bullet lists** organise information clearly:
```
- Item one
- Item two
- Item three
```

**Numbered lists** for sequential steps:
```
1. Clone the repository
2. Install dependencies
3. Run the project
```

**Code blocks** display commands and code samples without ambiguity:
````
```bash
git clone https://github.com/username/project.git
cd project
```
````

**Links** connect to external resources:
```
[GitHub Repository](https://github.com/username/project)
```

**Images** display screenshots directly in the README:
```
![App screenshot](screenshots/main-screen.png)
```

**Bold and italic** for emphasis — used sparingly:
```
**Important:** Read the setup instructions before running.
*Note: This feature is experimental.*
```

**Tables** for structured information:
```
| Command | Description |
|---------|-------------|
| `git status` | Show working tree state |
| `git log` | Show commit history |
```

Writing in Markdown forces you to think about the structure of your documentation before you write it — where sections begin and end, what belongs in a list versus a paragraph, and what requires a code block. This discipline produces better documentation and better-organised thinking.

---

## VI. Markdown Tooling

◼ Beginner

Markdown can be written in any plain text editor — Notepad, TextEdit, or directly in the GitHub web editor. However, using a Markdown editor with a live preview significantly reduces the trial-and-error of writing and formatting simultaneously.

**VS Code** includes Markdown preview built in. Open any `.md` file and press `Ctrl+Shift+V` (Windows) or `Cmd+Shift+V` (macOS) to preview the rendered output alongside the source.

For a dedicated Markdown writing and preview experience, **Andika** is a browser-based Markdown editor developed by [Jessel Sookha](https://www.github.com/jesselsookha) and available at [jesselsookha.github.io/andika](https://jesselsookha.github.io/andika). It allows you to write, format, and preview Markdown before committing to GitHub — particularly useful for students who are still developing familiarity with the syntax.

GitHub's own web editor renders a live preview when editing `.md` files directly in the browser interface.

---

## VII. Professional Conventions — Badges and Status Indicators

▲ Advanced

Professional and open-source repositories frequently include **badges** in the README header — small dynamic icons that communicate the current status of the project at a glance.

Common badges include:

- **Build status** — whether the CI pipeline is currently passing or failing
- **Test coverage** — the percentage of code covered by automated tests
- **Latest release version** — the current published version
- **Licence type** — what licence governs the project
- **Code quality** — ratings from static analysis tools

Badges are generated by external services (GitHub Actions, Codecov, Shields.io) and embedded as image links in the README. They provide instant visibility into the project's health without requiring anyone to open the codebase.

For students, badges are not required — but understanding what they represent is important context for reading professional repositories. A repository where the build badge shows red is a warning sign. A repository with high test coverage and a green build is a signal of maintained, production-quality code.

---

## VIII. README Evolution — A Living Document

◆ Intermediate

A README is not written once and forgotten. It should evolve in parallel with the project.

A healthy README lifecycle looks like this:

- **At project creation** — basic title, description, and initial run instructions. Even a minimal README is better than none.
- **During development** — add screenshots as the interface takes shape, update the folder structure as the project grows, add known limitations as they are discovered.
- **At submission or release** — ensure all instructions are current, author information is complete, and the README accurately reflects the final state of the project.

A README that was written at the beginning and never updated is a README that no longer accurately describes the project. Outdated instructions, references to files that no longer exist, and missing documentation for features that were added later all signal neglect.

**A stale README is worse than a sparse one** — because it actively misleads the reader.

Updating the README as the project changes is a mark of discipline and professionalism. It takes minutes per session and pays dividends every time someone reads the repository.

---

## IX. Common README Mistakes

These mistakes are consistently observed in student repositories — and are consistently penalised, both academically and in professional review:

- **Leaving a default template unchanged** — a README with placeholder text still visible (`[Your project name here]`) communicates that the developer did not treat documentation as part of their work
- **Writing only one sentence** — a description of three words does not explain a project. Expand enough for a reader to understand the purpose and scope.
- **Copy-pasting the assignment brief** — this tells the reader what was required, not what was built. Write in your own words, describing what you actually created.
- **Omitting run instructions** — the most common and most damaging omission. If the project cannot be run from the README alone, the README is incomplete.
- **Forgetting to update after changes** — instructions that refer to files, menus, or features that no longer exist mislead rather than guide.

A README must evolve with the project. It is part of your codebase — not an afterthought written in the final five minutes before submission.

---

## Summary

A README transforms code into a communicable project.

Without it, a repository is a collection of files.
With it, a repository is a presented, explained, accessible piece of work.

If someone clones your repository — a classmate, a lecturer, a potential employer, a future version of yourself — the README is their starting point. It should answer every question they are likely to have before they even open a file.

Treat it as both an **academic requirement** and a **professional portfolio piece**.

A well-written README signals something that the code alone cannot: that the developer understands not just how to build software, but how to communicate about it.

---

Proceed to:

→ 03-03 — Submission Checklist
