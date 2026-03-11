# 07-05 — Templates

---

## Purpose

Templates provide ready-to-use structures for academic submissions and professional practice.

A template is not a substitute for thought — it is a scaffold that ensures nothing is forgotten. The value of a template is not that it writes your README or your commit messages for you; it is that it answers the question "what should be in here?" so that effort can go into the content rather than the structure.

Every template in this document has a "Why" annotation explaining the purpose of each section. Read the annotations. A template understood is a template used correctly. A template copied blindly produces submissions that look complete but communicate nothing.

---

## I. Academic README Template

Copy this structure as the starting point for every academic project README. Replace every placeholder with content specific to the project.

```markdown
# [Project Title — specific, not "Assignment 1"]

- **Developer**: [Full Name]
- **Student Number**: [Your Student Number]
- **Group**: [Group Name or Number, if applicable]
- **Course**: [Course Name]
- **Subject**: [Subject/Module Name]

## Links
- **GitHub Repository**: [Full URL to repository]
- **Demo Video**: [YouTube or other video link, if required]
```

**Why this section:** Establishes authorship and provides direct access to the repository and demonstration. This is the first thing a lecturer sees. It must be complete, accurate, and specific. A title that says "Assignment 1" tells a reviewer nothing about what the project does.

---

## II. Project Overview Template

```markdown
## Project Overview

[App/Project Title] is a [type of application — mobile app, web application, 
console application, etc.] developed as part of [assignment name or number] 
in the [Subject Name] subject.

The application was built using [primary language/framework] and [IDE/tooling].

The primary purpose of this project is to [describe what the application does 
in one to two sentences]. 

This project was developed to meet the following requirements:
- [Requirement 1 — e.g., "Implement a functional mobile application"]
- [Requirement 2 — e.g., "Use GitHub for version control with regular commits"]
- [Requirement 3 — e.g., "Automate builds using GitHub Actions"]
```

**Why this section:** Provides context for anyone reading the repository — including future employers — without requiring them to read the assignment brief. The overview should describe what was built, not what was required. It communicates both competence (what was done) and clarity (ability to explain it).

---

## III. Purpose and Features Template

```markdown
## Purpose and Features

### Purpose
[Describe the primary goal of the application in two to three sentences. 
What problem does it solve? What does a user experience when they use it?]

### Key Features
- **[Feature 1]**: [Brief description of what this feature does]
- **[Feature 2]**: [Brief description of what this feature does]
- **[Feature 3]**: [Brief description of what this feature does]
- **[Feature 4 — optional]**: [Brief description]

[Optional closing sentence describing the overall user value of the feature set.]
```

**Why this section:** Breaks the application into assessable, named features. A lecturer reviewing your submission can check each feature against the requirements. For portfolio purposes, employers can scan a feature list to understand scope and complexity quickly. Features should be specific and real — not aspirational or placeholder.

---

## IV. Design Considerations Template

```markdown
## Design Considerations

The following design principles guided development decisions:

1. **User Experience (UX)**: [Describe how the interface was designed for 
   intuitive use — navigation structure, layout choices, or interaction patterns.]

2. **Responsiveness / Compatibility**: [Describe how the application handles 
   different screen sizes, devices, or environments.]

3. **Simplicity**: [Describe any deliberate choices to reduce complexity — 
   what was left out and why.]

4. **Performance**: [Describe any optimisation decisions — loading speed, 
   memory usage, battery consumption, or data efficiency.]

5. **[Additional consideration if relevant]**: [Description]
```

**Why this section:** Demonstrates that development involved deliberate thinking about how the application would be experienced, not just whether it would compile. Design considerations are a mark of professional awareness. Even simple academic projects benefit from this reflection — and the act of writing it often reveals decisions that should have been made differently.

---

## V. GitHub and Version Control Template

```markdown
## GitHub and Version Control

This project was managed using Git for version control, with the repository 
hosted on GitHub [Classroom / personal account].

### Commit Discipline
All code changes were committed in logical units with descriptive messages 
throughout the development period. The commit history reflects the 
progressive development of the project.

### GitHub Actions
Automated workflows were configured in `.github/workflows/` to:
- [Describe workflow 1 — e.g., "Compile and build the project on every push to main"]
- [Describe workflow 2 — e.g., "Run unit tests and report results"]
- [Describe workflow 3 — e.g., "Generate and upload APK/AAB build artifacts"]

Workflow results are visible in the Actions tab of the repository.
```

**Why this section:** Demonstrates adoption of professional version control practices beyond simply storing files on GitHub. Describing commit discipline and Actions workflows shows that Git was used as a development tool, not just a submission mechanism. This section is particularly relevant for assessments where the process is evaluated alongside the product.

---

## VI. Screenshots and Demo Template

```markdown
## Screenshots

### [Screen or Feature Name]
![Screenshot description](screenshots/screen-name.png)
*Caption: [Describe what this screenshot demonstrates — which feature, 
which state, or what the user is experiencing.]*

### [Screen or Feature Name]
![Screenshot description](screenshots/screen-name-2.png)
*Caption: [Description]*

## Video Demo
A demonstration of the application's core functionality is available at:
[Video URL]
```

**Why this section:** Visual evidence of functionality that cannot be conveyed by code alone. Screenshots and video demonstrate that the application runs, looks as intended, and behaves as described. For assessors who do not compile and run the project themselves, screenshots are the primary evidence of a working implementation. Store screenshot files in a `/screenshots` directory in the repository and commit them — they must be present for the markdown image links to render.

---

## VII. Challenges and Learnings Template

```markdown
## Challenges and Learnings

### Challenge 1: [Name the challenge specifically]
**What happened:** [Describe the problem that was encountered.]
**How it was resolved:** [Describe the solution and what was learned from it.]

### Challenge 2: [Name the challenge]
**What happened:** [Description]
**How it was resolved:** [Description]

### Summary
From these challenges, the key lessons learned were: [summarise the most 
important technical or process insights that will carry into future projects.]
```

**Why this section:** Demonstrates problem-solving process and intellectual honesty. Every non-trivial project involves challenges — documentation of those challenges and their resolutions shows that the developer can reflect on their own work and extract transferable learning. This is one of the most valuable sections for both academic assessment and professional portfolio building.

---

## VIII. Future Enhancements Template

```markdown
## Future Enhancements

Given additional time or scope, the following improvements would be considered:

1. **[Enhancement 1]**: [Describe what it would add and why it would improve the project]
2. **[Enhancement 2]**: [Description]
3. **[Enhancement 3]**: [Description]
```

**Why this section:** Demonstrates forward-thinking and honest scope awareness. Enhancements should be genuine — features that would meaningfully improve the application, not padding. This section also signals professional maturity: the ability to ship a complete version of something while being clear about its current limitations and the direction of future development.

---

## IX. References Template

```markdown
## References

1. [Author or Organisation]. *[Title of source]*. [Year]. [URL or publication details]
2. [Documentation or official resource — e.g., Android Developer Documentation]
3. [Tutorial, course material, or textbook used]
4. [Any other resource consulted]
```

**Why this section:** Acknowledges the sources that informed the work and maintains academic integrity. References are not only for code copied verbatim — they include documentation consulted for API usage, tutorials that demonstrated an approach, and any other resource that shaped how the project was built. Incomplete or missing references are an academic integrity concern regardless of whether copying occurred.

---

## X. Disclosure of AI Tool Usage Template

```markdown
## Disclosure of AI Tool Usage

In the development of this project, AI tools were used to assist with 
specific tasks as described below.

### Tools Used
- [Tool name — e.g., GitHub Copilot, ChatGPT, Claude]

### Sections Where AI Assistance Was Used
- [Describe the section, feature, or task — e.g., "Brainstorming initial 
  feature list", "Reviewing grammar in the README", "Generating boilerplate 
  code for the database connection class"]

### Purpose and Extent of Use
[Describe what the AI tool produced and how it was used — e.g., "Suggestions 
were reviewed, edited, and integrated where appropriate. All final code was 
understood and verified before inclusion."]

### Dates of Use
[Insert dates or date range]

### Evidence
[Links to AI chat logs, screenshots, or other evidence if required by the 
institution]
```

**Why this section:** Transparency about AI tool use is an academic integrity requirement at most institutions — and increasingly a professional expectation as well. This section is not a confession; it is a record. The act of documenting AI usage encourages reflection on the extent and nature of that usage, which supports genuine learning. Institutions differ in their specific requirements; ensure this section meets the requirements of your assessment.

---

## XI. Commit Message Templates

Copy these as starting points for commit messages following Conventional Commits style:

```
feat: Add [feature name]
Example: feat: Add user authentication flow

fix: Resolve [issue description]
Example: fix: Resolve null pointer exception on profile screen

docs: Update [document name] with [description of change]
Example: docs: Update README with installation instructions

refactor: Simplify [component or function name]
Example: refactor: Simplify database connection logic

test: Add [test type] for [feature or component]
Example: test: Add unit tests for login validation

chore: Update [dependency or configuration]
Example: chore: Update Gradle wrapper to version 8.0

style: Fix [formatting issue]
Example: style: Fix inconsistent indentation in MainActivity

perf: Optimise [component or operation]
Example: perf: Optimise image loading in RecyclerView adapter
```

**Why these templates:** Consistent commit message format makes repository history readable and searchable. The `type: description` convention signals the category of change at a glance, supports automated changelog generation, and demonstrates professional development discipline. Adapt the type prefix to the nature of the change; keep the description specific enough to be meaningful without reading the diff.

---

## XII. Submission Structure Template

```markdown
# Submission Structure

This repository contains:

1. **README.md** — Project overview, features, design considerations, 
   version control documentation, and all required sections.
2. **Source Code** — Organised in [language/framework] project structure 
   under [folder path].
3. **Screenshots** — Stored in `/screenshots/` — referenced in README.
4. **`.github/workflows/`** — GitHub Actions workflow configuration.
5. **References** — Included at the end of README.md.
6. **Disclosure of AI Usage** — Included in README.md.
```

**Why this section:** Provides a manifest of the submission so a reviewer can verify completeness without having to explore the repository structure independently. A clear submission structure communicates that the developer organised their work deliberately — not just committed files until the deadline.

---

## Summary

Templates provide structure so that effort goes into content.

This document contains templates for:

- Academic README (header, overview, features, design, version control, screenshots)
- Challenges and learnings
- Future enhancements
- References
- Disclosure of AI tool usage
- Commit messages in Conventional Commits format
- Submission structure manifest

**The principle behind all of them:**

Consistency builds credibility. Submissions that are consistently structured, honestly documented, and clearly written demonstrate both academic discipline and the professional habit of producing work that communicates rather than merely exists.

A README that is rushed, incomplete, or placeholder-filled tells the reader as much about the developer's standards as the code does. These templates make it straightforward to produce the other kind.
