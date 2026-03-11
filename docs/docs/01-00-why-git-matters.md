# Why Git Matters

◼ Beginner  
◆ Intermediate  
▲ Advanced  

Git is not simply a submission tool.

It is not a backup mechanism.
It is not a cloud storage solution.
It is not a requirement imposed by lecturers.

Git is a version control system designed to manage change.

Understanding this distinction changes everything. When Git is treated as a submission tool, it is used poorly — one commit at the end, no meaningful history, no real understanding of what happened between start and finish. When Git is understood as a system for managing change, it becomes something entirely different: a record of how thinking evolved, how problems were solved, and how a project grew from nothing into something complete.

---

# I. The Problem Git Solves

Before version control systems became standard practice, developers managed projects like this:

- Copy project folder → "Project_Final"
- Copy again → "Project_Final_Final"
- Copy again → "Project_Final_Real"
- Accidentally overwrite something important
- Lose previous work permanently

This is not an exaggeration. It was — and in many environments still is — the default approach for anyone who has not been taught structured version control. The folder names become longer and more desperate. The actual sequence of changes becomes impossible to reconstruct. If something broke two weeks ago and nobody noticed until today, there is no reliable way to find out what changed or when.

This approach does not scale.
It does not support collaboration.
It does not preserve history.
It does not explain *why* changes were made.

Git solves this problem by replacing folder duplication with structured, navigable history:

- Tracking changes — every modification is recorded, not just the final state
- Recording history — the full sequence of development is preserved and inspectable
- Allowing safe experimentation — changes can be made on branches without touching stable work
- Supporting collaboration — multiple contributors can work simultaneously without overwriting each other
- Enabling recovery — previous states are always accessible, because nothing is truly deleted

Git replaces guesswork with a verifiable record.

---

# II. Git in Modern Computing

Git is the dominant version control system used across virtually every area of modern software development:

- Software development
- Web development
- Mobile application development
- DevOps pipelines
- Research codebases
- Open-source communities

Platforms like GitHub, GitLab, and Bitbucket are built entirely around Git. They are not alternatives to Git — they are hosting services for Git repositories, with collaboration tools layered on top. Understanding this distinction matters: the platform is not the version control system. Git is.

It is worth noting how completely Git has displaced earlier systems. Version control tools like SVN (Subversion) and CVS (Concurrent Versions System) were widely used before Git's rise. Git's distributed model — where every contributor holds a full copy of the repository and its history — proved more flexible, more resilient, and more suitable for modern collaborative development than centralised predecessors.

Understanding Git is not optional in modern computing environments.

It is foundational — in the same way that understanding functions is foundational to programming, or understanding HTTP is foundational to web development. It is infrastructure-level knowledge that underpins almost everything else.

---

# III. Academic Relevance

In an academic setting, Git provides something that no file submission system can replicate:

- Evidence of progress — when work was done, not just that it was done
- Transparent development history — how the project evolved across the full assignment period
- Fair assessment opportunities — the process of development becomes visible, not just the outcome
- Collaboration control — in group work, individual contributions are traceable
- Structured submission — the repository itself becomes the deliverable, not just a compressed archive

A single "Final submission" commit tells a lecturer nothing about your process.

It cannot answer: when did you start? Did you work steadily or in a last-minute rush? Did you refactor your approach when something was not working? Did you fix bugs thoughtfully or abandon broken code? Did you write the code yourself?

A structured commit history answers all of these questions:

- When you began
- How you progressed across sessions
- Where you refactored and why
- When bugs were identified and fixed
- How features evolved from initial attempts to completed implementations

Git reveals thinking patterns — and thinking patterns are what academic assessment is ultimately trying to evaluate.

---

# IV. Professional Relevance

Employers in the technology industry increasingly review candidates' public repositories as part of evaluation. A GitHub profile is not just a portfolio — it is evidence of how you work, not just what you can produce.

Employers and technical interviewers review:

- Public repositories and their structure
- Commit history — frequency, quality, and discipline of messages
- README quality — whether documentation is present and professional
- Contribution patterns — solo work vs. collaborative participation

A repository with clear commits, logical structure, and professional documentation communicates discipline. It shows that the developer thinks in logical increments, communicates their intent, and understands that code is read and maintained by others.

A repository with one massive commit, no README, and a random file structure communicates inexperience. It suggests that Git was used as a filing cabinet rather than a development instrument.

The comparison is not harsh — it is the lens that professional environments actually apply.

Git is part of your professional identity. That identity begins forming while you are still a student, and the habits you build now are exactly the ones that transfer into the workplace.

---

# V. Git Is About Thinking in Versions

At its core, Git teaches you to think differently about your own work.

Instead of asking:

*"How do I save this?"*

You begin asking:

*"What logical change did I just complete — and is it worth recording?"*

This shift in thinking produces real, measurable improvements in development practice:

- Smaller commits — because you think in logical units rather than saving everything at once
- Cleaner code — because committing thoughtfully encourages you to finish a thing before moving to the next
- Structured experimentation — because branches allow you to try something without risking the stable version
- Safer collaboration — because your work is isolated until you choose to share it, and merged only when it is ready

This mindset is not unique to Git. It reflects professional software development practice more broadly. Git simply enforces it — or rather, rewards it. Developers who think in versions produce better work, clearer histories, and safer collaborations than those who do not.

---

# VI. The Core Mindset

You are not learning Git to pass an assignment.

You are learning Git to:

- Manage change safely, in a way that can always be reviewed and recovered
- Work with others effectively, without overwriting or obstructing their contributions
- Recover from mistakes confidently, knowing that Git's design protects history
- Build software professionally, with habits that will serve you for the entire duration of your career

When Git is understood properly:

- `clone` makes sense — you are replicating an existing history onto your machine
- `init` makes sense — you are beginning a new history in a folder that had none
- `pull` makes sense — you are bringing remote changes into your local timeline
- `push` makes sense — you are uploading your local timeline to the shared remote
- branches make sense — they are independent development paths that can be rejoined
- merge conflicts become manageable — they are moments where two timelines diverged and must be reconciled by a person

Git matters because change is constant in software development.

Features are added. Bugs are found. Requirements evolve. Teams grow. Code is revisited months after it was written by someone who was not the original author.

Git is how all of that is managed — not perfectly, but predictably. And predictability, in software development, is worth more than most people realise until they have lost work, corrupted a shared repository, or shipped a bug that could have been traced and caught if history had been maintained properly.

---

Proceed to:

→ Welcome to the Guide
