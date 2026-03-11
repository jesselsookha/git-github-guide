# 04-04 — Security and Academic Integrity

❈ Collaboration

Collaboration in Git is not only technical — it is ethical.

Security ensures that repositories are protected from unauthorised access and accidental exposure. Academic integrity ensures that contributions are honest, attributable, and represent genuine individual work. Together, they form the foundation of responsible collaborative development.

Neither of these is a bureaucratic requirement imposed from outside. Both serve real purposes that protect real people: security protects your work from being seen by those who should not see it; integrity protects your reputation from claims that your history cannot defend against.

Understanding both — and building habits that honour both — is part of what it means to develop professionally.

---

## I. Core Concept — Why Security and Integrity Matter

◼ Beginner

A Git repository is not just a collection of files. It is a record — of what was built, when it was built, who built it, and how it evolved. That record has consequences in both academic and professional contexts.

**Security** matters because:

- Academic repositories may contain assessment material, partial solutions, or proprietary code that should not be visible to unauthorised parties
- A repository accidentally made public exposes your work to copying — which creates academic integrity risks for others as much as for yourself
- Credentials, API keys, and secrets committed to a repository are permanently exposed once pushed, regardless of whether they are later deleted

**Integrity** matters because:

- Commit history is used as evidence of genuine development — assessors use it to verify that work was done progressively, over time, by the named contributor
- In group projects, commit history establishes individual contribution — who built what, when, and with what level of engagement
- Manipulating, fabricating, or misrepresenting that history is an academic misconduct issue with the same seriousness as submitting plagiarised written work

The two are connected: a secure, well-maintained repository where all commits are genuine and attributable is simultaneously a protected asset and an honest record.

---

## II. Repository Security — Practical Controls

◆ Intermediate

### Visibility Settings

Every GitHub repository is either public or private. This is the most fundamental security decision.

**Private repositories** — visible only to the owner and explicitly invited collaborators. This is the correct setting for:

- GitHub Classroom assignments — the default and expected setting
- Any project that has not been deliberately prepared for public release
- Any repository containing assessment material, credentials, or proprietary code

**Public repositories** — visible to anyone on the internet, including unauthenticated visitors. Appropriate for:

- Finished portfolio projects that are deliberately being showcased
- Open-source contributions
- Projects that have been reviewed and cleared for public visibility

The distinction matters beyond privacy: a public academic repository can be found and copied by other students, creating an integrity problem for the person who published it as much as for those who copy from it.

**Check your visibility setting** before pushing for the first time. Once a commit has been pushed to a public repository, it is publicly visible — even if the repository is later made private, the content may already have been indexed or cached.

---

### Collaborator Permissions

When adding teammates to a repository, the access level granted determines what they can do:

- **Read access** — can view and clone, but cannot push
- **Write access** — can push branches and open Pull Requests, but cannot change repository settings
- **Admin access** — full control, including repository settings, access management, and deletion

For student group work:

- Repository owner typically holds Admin access (as the creator)
- Collaborators should have Write access — sufficient to contribute without the risk of accidental settings changes
- Lecturers and teaching assistants are typically granted access at the organisation level, not by individual student invitation

**Verify collaborator permissions** before the project begins. A collaborator with insufficient access cannot push. One with excess access can inadvertently alter settings or delete branches.

---

### What Must Never Be Committed

Security failures in Git repositories are often not the result of someone gaining unauthorised access — they are the result of sensitive information being committed and pushed by the developer themselves.

**Never commit:**

- Passwords or passphrases of any kind
- API keys, authentication tokens, or OAuth credentials
- Database connection strings containing usernames and passwords
- `.env` files containing configuration secrets
- SSH private keys or certificate files

The critical point: **deleting a committed secret in a subsequent commit does not remove it from the repository.** The original commit remains in history, permanently. Anyone with access to the repository — now or in the future — can view that commit and extract the credential.

If a secret is ever committed and pushed, the correct response is to revoke and regenerate the credential immediately — not to delete the file and hope no one noticed. The repository history cannot be safely cleaned without rewriting it, and rewriting shared history creates problems for every contributor.

The prevention is a `.gitignore` file that explicitly excludes secret files before they are ever tracked. Configuration secrets should be stored in environment variables or in files that are excluded from version control from the start.

---

### Confirming Repository Integrity

Before every push, verify that your commits are going to the correct repository:

```bash
git remote -v
```

For GitHub Classroom work: the URL must contain the classroom organisation name — not your personal GitHub username. If it points to the wrong place, the submission is being made in the wrong location.

---

## III. Academic Integrity in Git Workflows

◼ Beginner

In academic environments, commit history is not just a technical record — it is part of the assessment. Lecturers reviewing Git-based submissions can see:

- **Who contributed** — the name and email attached to every commit
- **When contributions were made** — the exact timestamp of every commit and push
- **How work progressed** — the sequence of changes from the first commit to the last
- **How much was done in each session** — the size and distribution of commits across the development period

This visibility is not punitive. It is protective. A well-maintained, genuine commit history is the strongest possible evidence that the work is yours, that it was done progressively, and that it reflects real understanding.

### What Constitutes Dishonest Practice

The following are academic integrity violations in Git-based workflows, regardless of whether they are explicitly named in any assessment rubric:

- **Bulk uploading at the last minute** — committing an entire project in one or two commits immediately before the deadline. This does not demonstrate development — it demonstrates that the Git record was constructed after the fact rather than during genuine work.
- **Claiming others' work** — copying code from a teammate's repository and committing it under your own name. Commit history does not prevent this, but it makes it detectable: if your commits appear after your teammate's identical commits, and you have no prior history for those sections of code, the pattern is visible.
- **Falsifying commit timestamps** — Git commit timestamps can be manipulated. Academic assessors are often aware of this and look for implausible patterns: commits that appear to predate the assignment being issued, timestamps that are too evenly spaced to reflect genuine working sessions, or histories that were clearly constructed in a single session but timestamped across weeks.
- **Rewriting history to hide evidence** — using `git rebase` or `git push --force` after submission to alter or remove commits. This is detectable if the lecturer has already reviewed or downloaded the history. It also raises significant integrity concerns about what was being hidden.
- **Deleting the repository and recreating it** with a cleaner history before submission. Same consequence: if the original state was observed, the discrepancy raises questions.

---

## IV. Honest Contribution in Group Projects

◆ Intermediate

In group assignments, Git provides something that no other assessment tool can: traceable individual contribution.

Every commit is attributed to the person who made it. Every branch is created by a specific account. Every Pull Request is opened, reviewed, and merged by named individuals. The group project's history is not just a record of what was built — it is a record of who built each part of it.

Honest contribution means:

- **Committing only work you genuinely did** — not pushing a teammate's code under your own credentials
- **Branch names that reflect your actual tasks** — not branches that inflate the appearance of contribution
- **Pull Requests that invite genuine review** — not PRs opened as a formality after the work has already been decided
- **Timesheets and contribution logs that match commit history** — inconsistencies between declared contributions and actual commits are observable

Dishonest practices in group work include:

- **Committing code you did not write** and attributing it to yourself through your account
- **Claiming credit for a teammate's commits** in reflections or contribution statements
- **Manipulating commit history** to make your contributions appear larger, more frequent, or differently timed than they were

Lecturers and teaching assistants who are familiar with Git can identify these patterns. The same patterns that make honest development legible also make dishonest development detectable.

**Integrity is not only about passing assessment.** It is about the professional identity you are building during your academic career. The habits formed now — honest attribution, genuine contribution, transparent process — are exactly the ones that colleagues, employers, and collaborators will rely on throughout a professional career.

---

## V. Professional Insight — Security in Industry

▲ Advanced

The security and integrity practices described in this document scale directly into professional development environments — where the consequences of failure are significantly higher.

**Access control at scale.** Professional organisations use role-based access management across hundreds of repositories and thousands of contributors. Branch protection rules prevent direct pushes to `main` at the platform level. Service accounts with limited, scoped permissions are used for automated systems. No individual has unrestricted access to everything.

**Secret management.** Professional teams use dedicated secrets management systems — AWS Secrets Manager, HashiCorp Vault, GitHub Encrypted Secrets — to store and inject credentials at runtime. Credentials never appear in code. The `.gitignore` and `.env.example` pattern is the minimum viable version of this principle.

**Audit logs.** Enterprise GitHub accounts maintain detailed audit logs of every action taken across the organisation: who pushed, who merged, who changed settings, who granted access. These logs are used in security reviews, incident investigations, and compliance audits. In this respect, the commit history is only part of the record — platform-level activity is tracked independently.

**Code signing.** In high-security environments, commits are cryptographically signed to verify that they genuinely came from the contributor they claim to come from. Unsigned commits in such environments may be automatically rejected.

**Continuous Integration as integrity enforcement.** CI pipelines run automated tests, security scans, and code quality checks on every PR. A PR that fails any of these checks cannot be merged. This is the technical equivalent of the academic integrity requirement — the system enforces a standard that individuals must meet before their work is accepted into the shared codebase.

The common thread across all of these practices is the same principle that applies in a student group project: **every contribution should be genuine, attributable, and able to withstand review.**

---

## VI. Common Pitfalls

◼ Beginner

These issues appear in student repositories regularly enough to name directly:

**Repository accidentally set to public** — check visibility before the first push. Changing to private after a public push does not undo what was made visible.

**Pushing to a personal repository instead of the classroom organisation** — always verify with `git remote -v`. The URL must contain the organisation name.

**Vague commit messages that obscure contribution** — "update" and "final" communicate nothing about what was done. They also make it impossible to trace individual contributions across a group project.

**Bulk commits before the deadline** — even genuine bulk commits raise integrity questions. Commit regularly throughout development, not only at the end.

**Credentials or sensitive files committed** — check `.gitignore` before the first `git add`. What is excluded before it is tracked is safe; what is committed once is permanently in history.

**Inconsistency between declared contributions and actual commits** — if your contribution statement says you built the login page but your commits show only one change to a stylesheet, the inconsistency is visible.

---

## Summary

Security and integrity are not constraints imposed on collaborative development.

They are the conditions under which collaborative development is trustworthy — for the people doing the work, for the people assessing it, and for the professional communities those people will eventually join.

Key principles:

- Keep repositories private unless there is a deliberate reason not to
- Verify collaborator permissions before the project begins
- Never commit secrets, credentials, or sensitive configuration
- Commit honestly and regularly — not in bulk at the deadline
- Use Pull Requests for transparent, reviewable integration
- Treat commit history as evidence — because it is

In academic contexts, these practices protect your work and your reputation.

In professional contexts, they are part of the trust that makes large-scale collaboration possible.

---

Proceed to:

→ Part 5 — Advanced Topics
