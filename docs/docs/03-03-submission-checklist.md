# 03-03 — Submission Checklist

❈ Collaboration

Before submitting any Git-based assignment, work through this checklist in full.

This document applies to:

- GitHub Classroom environments and institutional Git repositories
- Any academic submission where version control is part of the assessment
- Any structured workflow where the repository state is the deliverable

Readers outside an academic context: this checklist maps directly onto pre-release verification processes in professional environments. The guiding principle is the same in both contexts — **always verify before delivery.**

A submission is not the moment you press submit or push a final commit. A submission is the state your repository is in when the deadline arrives. Every item on this checklist exists because a student has submitted an assignment with that specific issue unresolved — and faced consequences that were entirely preventable.

Work through it every time.

---

## I. Repository Verification

◼ Beginner

The most basic and the most consequential check: confirm that you are working in the correct repository, pushing to the correct remote, and submitting the correct link.

A submission to the wrong repository — a personal account instead of the Classroom organisation, or a different assignment's repository — can result in a mark of zero through no fault of the code quality. The work exists. It is simply invisible to the person assessing it.

**Checklist:**

- [ ] You are working inside the correct repository folder
- [ ] The repository belongs to the correct organisation (if using GitHub Classroom)
- [ ] Your name or student number appears as a contributor in the commit history
- [ ] The repository is not empty — at minimum one meaningful commit exists

**Verification command:**

```bash
git remote -v
```

This shows the remote URL your commits are being sent to. Confirm that the URL contains the organisation name — not your personal GitHub username. If it points to a personal repository, the submission is in the wrong place.

Also verify directly in the browser: open GitHub, navigate to the organisation, find your repository, and confirm it exists and contains your work.

---

## II. Commit Verification

◆ Intermediate

Commits are the evidence of your work. They are what the lecturer sees, what automated systems track, and what academic integrity review examines. Verifying them before submission is not a formality — it is confirming that your development record is intact and accurate.

**Checklist:**

- [ ] All changes have been committed — no work exists only as unsaved files
- [ ] Commit messages are clear and descriptive — they explain what was done at each stage
- [ ] The commit history shows progressive development — not one large commit at the end
- [ ] Timestamps reflect actual development — not all clustered at a single point

**Verification commands:**

```bash
git status
```

If this returns:

```
nothing to commit, working tree clean
```

Your working directory and staging area are clear. All changes have been committed.

If modified or untracked files appear, stage and commit them before proceeding:

```bash
git add .
git commit -m "Final adjustments before submission"
```

```bash
git log --oneline
```

Review the commit history. Each entry should reflect a meaningful unit of work with a readable message. A history that reads:

```
a3f1c2e Add input validation to registration form
9d2b4a1 Implement sorting logic for student records
5c8e3f0 Set up initial project structure
```

is a history that tells a story. A history that reads:

```
f2a9c1b final
3b7d2e4 update
1c4a8f0 stuff
```

is not — and it will be assessed accordingly.

---

## III. Push Verification

◆ Intermediate

Local commits are not submissions. A commit exists in your local repository until it is pushed. If your machine fails, your internet connection drops, or you simply close the IDE without pushing, that work is not on GitHub — and therefore not submitted.

This is the single most common cause of lost submission marks. The work was done. It was committed. It was simply never pushed.

**Checklist:**

- [ ] Run `git push` and confirm it completes without errors
- [ ] Git responds with `Everything up-to-date` or a summary of pushed commits
- [ ] Open the repository in a browser and confirm the latest commit is visible
- [ ] Confirm the commit timestamp is before the deadline
- [ ] Confirm you are viewing the correct branch — `main` unless otherwise specified

**Do not rely on memory.** Always push immediately before the deadline, then open the repository in a browser and verify visually. The GitHub interface shows the most recent commit message and timestamp on the repository's main page — this is your confirmation.

If `git push` fails, do not ignore the error. Diagnose it immediately:

- `error: failed to push some refs` — run `git pull` first, resolve any conflicts, then push again
- `error: Authentication failed` — verify your credentials and remote URL
- No upstream branch — run `git push -u origin main`

Push failures at submission time are recoverable if diagnosed quickly. They become unrecoverable after the deadline.

---

## IV. README Verification

◼ Beginner

A repository submitted without a README — or with a placeholder README that was never updated — is incomplete, regardless of the quality of the code.

The README is the first document a lecturer opens when reviewing your submission. It sets the context for everything else they see. A clear, current README demonstrates that you understand your own project well enough to explain it to someone else.

**Checklist:**

- [ ] A `README.md` file exists at the root of the repository
- [ ] The README accurately describes the current state of the project — not an earlier version
- [ ] Setup and run instructions are present and correct — follow them yourself to verify
- [ ] Author information is included if required by your institution
- [ ] No placeholder text remains — all template sections have been completed
- [ ] The README is visible on the GitHub repository page (GitHub renders it automatically)

A README that describes features you removed, refers to files that no longer exist, or still says `[Your name here]` is worse than a minimal README — because it actively misleads the reader.

---

## V. Functional Verification

◆ Intermediate

This step is often skipped because it feels obvious. It should never be skipped.

A project that worked yesterday may not work today. A file that was working in one folder may have a broken reference when cloned into a fresh location. A dependency that was available in your development environment may not be listed anywhere for someone else to install.

**Checklist:**

- [ ] Open the project in the IDE from the cloned repository — not from a local shortcut or cached version
- [ ] The project compiles or builds without errors
- [ ] The application runs and produces expected behaviour
- [ ] No missing files, broken references, or absent dependencies exist
- [ ] Any assets referenced in the README (screenshots, example files) are present in the repository

**The critical test:** clone your own repository into a fresh folder on your machine and run it from there. If it works, the submission is complete. If it does not, there is a configuration or file dependency that needs to be addressed before submission.

This is not paranoia — it is the same verification step that professional development teams perform before every release. The difference between "it works on my machine" and "it works from a clean clone" is the difference between a submittable project and one that will fail assessment.

---

## VI. Institutional Additions

▲ Advanced

Individual institutions, programmes, or assignments may require steps beyond this checklist. Always read the specific assessment instructions carefully — submission requirements vary.

Common institutional additions include:

- **LMS submission** — submitting the repository URL through a learning management system such as Moodle, Blackboard, or Canvas, in addition to or instead of the GitHub submission
- **Commit hash inclusion** — some assessors require you to include the hash of your final commit in the submission form, creating a verifiable record of exactly which commit was submitted
- **Submission tags** — tagging the final commit with a specific label (e.g., `git tag submission-v1`) to mark the official submission point explicitly in the history
- **Branch naming** — some assignments require work to be submitted on a specific branch name, not `main`
- **Repository naming conventions** — specific formats for the repository name that allow automated processing or roster matching

**Failure to follow institutional submission rules can result in penalties — even if the code is correct and the work is complete.**

Read the instructions. Follow them exactly. If anything is unclear, ask before the deadline — not after.

---

## VII. Academic Integrity

Commit history is part of academic assessment. This is not a secondary consideration — at many institutions it is assessed directly, and at all institutions it is visible to the assessor.

Healthy repositories demonstrate:

- **Gradual progress** — commits distributed across the full development period, not clustered at the end
- **Logical development sequence** — commits build on each other in a way that reflects genuine incremental development
- **Realistic timestamps** — working sessions distributed across days or weeks, consistent with the assignment duration

Repositories that raise integrity concerns show:

- A single large commit containing the entire project, created immediately before the deadline
- Commits with timestamps that contradict the claimed development timeline
- History that appears altered — commits that were rebased or amended to change timestamps or messages after work was completed

Git is a protection as much as an assessment tool. A well-maintained commit history is evidence on your behalf — evidence of when you started, how you progressed, and that the work is genuinely yours. Use it as such.

Last-minute bulk uploads do not represent healthy development. More importantly, they cannot prove anything about the process — which is exactly what commit history is there to establish.

---

## VIII. Final Confirmation

Before the deadline passes, ask yourself one question:

> **If my lecturer opens this repository right now, does it fully and accurately represent my completed work?**

If the answer is *yes* — you are done.

If the answer is *uncertain* — verify immediately. Check the repository in the browser. Confirm the latest commit. Confirm the correct remote. Confirm the README is current. Run the project one more time.

Double-checking is not optional.
It is the final step of professional discipline.

The developers who do not lose work to avoidable submission errors are not the ones who trust their memory. They are the ones who verify.

---

## Summary Checklist — Quick Reference

Use this condensed version as a final pass before every submission:

| Check | Command | Confirm |
|---|---|---|
| Correct repository | `git remote -v` | URL shows organisation, not personal account |
| All changes committed | `git status` | "nothing to commit, working tree clean" |
| History is clean | `git log --oneline` | Multiple commits with clear messages |
| Work is pushed | `git push` | No errors; confirms up-to-date |
| Visible on GitHub | Open browser | Latest commit shown with correct timestamp |
| README is present | Open GitHub page | Readme renders; no placeholders |
| Project runs | Clone to fresh folder | Compiles and executes without errors |
| Institutional steps | Assignment brief | LMS submission, tags, naming — as required |

A repository is not just code.

It is a reflection of your process, your discipline, and your professionalism. Every check on this list is an opportunity to ensure that what you submit accurately represents the work you did.

---

Proceed to:

→ Part 4 — Collaboration
