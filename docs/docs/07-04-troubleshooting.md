# 07-04 — Troubleshooting

---

## Purpose

Troubleshooting is the practice of diagnosing a problem before acting on it.

The instinct when Git produces an error is to try something — anything — to make it stop. That instinct produces the second, third, and fourth errors. Every Git error message contains diagnostic information. Reading it carefully and understanding what it means is the step that separates a two-minute resolution from a twenty-minute escalation.

This document provides structured diagnostic tools for the problems that appear most frequently:

- Init versus clone confusion
- Push rejections
- Merge conflicts
- An extended error message reference covering the errors students encounter most often

Use the appropriate section when a problem arises. Follow the diagnostic path. Understand why the resolution works, not just that it does.

---

## I. Init vs Clone Confusion

**Symptom:** You are unsure which command to use to start working on a project, or something went wrong at the beginning of the workflow.

**Diagnostic path:**

```
Does a repository for this project already exist on GitHub or Classroom?
│
├── YES → Use git clone <url>
│         The repository comes to you. Remote is already configured.
│
└── NO → Use git init
          Then connect: git remote add origin <url>
```

**Common mistake:** running `git init` inside a folder that was created by `git clone`.

Cloning creates a folder that already contains a `.git` directory. Running `git init` inside that folder creates a second, inner `.git` directory. Git now behaves unpredictably — sometimes reading from one directory, sometimes from the other.

**Detection:**

```bash
find . -name ".git" -type d
```

If two `.git` directories appear, the inner one must be removed:

```bash
rm -rf path/to/inner/.git
```

Verify only one `.git` remains, at the project root, before continuing.

**Other common mistake:** running `git clone` after having already set up the project locally with `git init`.

If this has happened and both a local `git init` repository and a cloned repository exist in different folders, the solution is to identify which one contains your actual work, discard the other, and proceed with the correct one. The `git log --oneline` output of each will help identify which has your commits.

---

## II. Push Rejections

**Symptom:** `git push` fails with an error message.

**Before diagnosing — run this checklist first:**

```bash
git status          # Are there uncommitted changes? Push only works on commits.
git log --oneline   # Does a commit history exist? First push requires at least one commit.
git remote -v       # Does origin point to the correct repository URL?
```

If any of these reveal the problem, resolve it before continuing to the error-specific diagnostics below.

---

### Error: "src refspec main does not match any"

**Meaning:** The branch `main` does not exist yet. This happens when `git push -u origin main` is attempted before any commits have been made.

**Resolution:**

```bash
git add .
git commit -m "Initial commit"
git push -u origin main
```

A branch only exists after it has at least one commit. The branch is created by the first commit.

---

### Error: "fatal: 'origin' does not appear to be a git repository" or "No configured push destination"

**Meaning:** No remote named `origin` is configured. This happens after `git init` when `git remote add` was not run.

**Resolution:**

```bash
git remote add origin <url>
git push -u origin main
```

Verify the remote was added:

```bash
git remote -v
```

---

### Error: "error: failed to push some refs" or "Updates were rejected (non-fast-forward)"

**Meaning:** The remote has commits that your local repository does not. Pushing would overwrite those commits on the remote, which Git refuses to do without explicit instruction.

This happens when:
- A teammate has pushed since you last pulled
- You initialised the remote with a README or `.gitignore` that you have not pulled
- Another device pushed commits you have not received

**Resolution:**

```bash
git pull origin main
```

If the pull produces a merge conflict, resolve it (see Section III), then:

```bash
git push
```

The history now includes both the remote commits and your local commits — the push is accepted.

---

### Error: "fatal: Authentication failed"

**Meaning:** GitHub rejected your credentials. This can mean:
- Your password is wrong (GitHub no longer accepts account passwords for Git operations — a Personal Access Token is required for HTTPS)
- Your PAT has expired
- The remote URL is incorrect — pointing to a repository you do not have write access to
- SSH keys are not configured correctly

**Resolution:**

```bash
git remote -v
```

Confirm the URL. If it is correct, regenerate your Personal Access Token on GitHub (Settings → Developer Settings → Personal Access Tokens) and use it as the password when prompted.

For SSH: verify the key is registered on GitHub (Settings → SSH and GPG Keys) and test the connection:

```bash
ssh -T git@github.com
```

A successful response: `Hi username! You've successfully authenticated...`

---

### Error: "fatal: branch 'main' does not exist"

**Meaning:** Git was initialised with a default branch named `master`, but you are trying to push to `main`.

**Resolution:**

```bash
git branch -M main
git push -u origin main
```

The `-M` flag renames the current branch forcefully. After this, the branch is named `main` and the push proceeds normally.

---

## III. Merge Conflicts

**Symptom:** Git reports a conflict during `git merge`, `git pull`, or `git rebase`.

Git is telling you that two branches modified the same lines of the same file in ways it cannot automatically reconcile. This is not an error — it is Git correctly identifying that a human decision is required.

**Five-step resolution process:**

**Step 1 — Identify all conflicted files:**

```bash
git status
```

Files marked `both modified` are conflicted. Every one of them must be resolved before the merge can be completed.

---

**Step 2 — Open each conflicted file.**

Git has inserted conflict markers directly into the file content. A conflicted section looks like this:

```
<<<<<<< HEAD
Content from your current branch
=======
Content from the branch being merged
>>>>>>> branch-name
```

There may be multiple conflicted sections within a single file.

---

**Step 3 — Make the resolution decision for each conflict.**

Three options:

- **Keep your version:** Delete from `=======` down to and including `>>>>>>>`. Delete the `<<<<<<< HEAD` line.
- **Keep the incoming version:** Delete from `<<<<<<< HEAD` down to and including `=======`. Delete the `>>>>>>> branch-name` line.
- **Combine both:** Edit the content between the markers to reflect the correct combined result. Remove all three marker lines.

There is no fourth option. Git cannot make this decision. The correct content depends on the intent of both changes — which only the developers who wrote them can determine. In a team setting, discuss with the person whose branch produced the conflict before resolving.

---

**Step 4 — Remove all conflict markers.**

After editing, no line beginning with `<<<<<<<`, `=======`, or `>>>>>>>` should remain anywhere in the file. Leaving a marker in place will cause a syntax error or a commit that contains literal conflict marker text — which is always wrong.

Save the file.

---

**Step 5 — Stage and commit:**

```bash
git add <resolved-file>
git commit
```

If multiple files were conflicted, run `git add` for each one before committing. Git pre-fills the commit message for a merge commit — accept it or edit it as appropriate.

After committing:

```bash
git log --oneline
```

The merge commit should appear at the top of the history with two parent references.

---

## IV. Common Error Messages — Reference Table

| Error Message | Meaning | Resolution |
|---|---|---|
| `fatal: not a git repository (or any of the parent directories)` | The current folder is not inside a Git repository. | Navigate to the correct project folder with `cd`, or run `git init` if starting a new repository. |
| `fatal: remote origin already exists` | `git remote add origin` was run when `origin` is already configured. | Update instead of adding: `git remote set-url origin <url>` |
| `error: failed to push some refs` | Remote has commits not present locally. | Run `git pull`, resolve any conflicts, then push. |
| `hint: Updates were rejected because the tip of your current branch is behind` | Same as above — non-fast-forward rejection. | `git pull origin main`, resolve, push. |
| `fatal: refusing to merge unrelated histories` | Local and remote repositories have no common ancestor — they were initialised independently. | `git pull --allow-unrelated-histories`, resolve the resulting merge, push. |
| `HEAD detached at <hash>` | You checked out a commit directly rather than a branch. | If you have uncommitted changes to keep: `git checkout -b new-branch`. To return to main: `git checkout main`. |
| `fatal: Authentication failed` | GitHub rejected your credentials. | Check that you are using a Personal Access Token (not your account password) for HTTPS, or verify SSH key configuration. |
| `fatal: 'origin' does not appear to be a git repository` | No remote named `origin` is configured. | `git remote add origin <url>` |
| `fatal: branch 'main' does not exist` | Default branch is named something other than `main`. | `git branch -M main` then `git push -u origin main`. |
| `error: Your local changes to the following files would be overwritten by merge` | Unstaged local changes conflict with incoming changes. | Stage and commit your changes first, or stash them: `git stash`, then pull, then `git stash pop`. |
| `CONFLICT (content): Merge conflict in <file>` | Automatic merge failed due to conflicting changes. | Open the file, resolve conflict markers manually, stage, and commit. |
| `nothing to commit, working tree clean` | Not an error — all changes are committed. | The working directory is clean. Proceed with push or other operations. |

---

## V. Diagnostic Discipline — A General Approach

When something goes wrong with Git that is not covered by the scenarios above, the following process reliably narrows the problem:

**I. Read the full error message.** Git's error messages are specific. The first line names the error type. The subsequent lines describe the context. Do not dismiss the message as technical noise — it is the primary diagnostic tool.

**II. Establish current state:**

```bash
git status
git log --oneline
git remote -v
git branch
```

These four commands together establish: what is staged and unstaged, what the commit history looks like, what remote is configured, and which branch HEAD is on. Most problems are visible in this output.

**III. Identify which of the three areas is involved.** Is the problem in the working directory (uncommitted changes), the staging area (staged but not committed), or the remote (push/pull failures)? The area involved points to the category of resolution.

**IV. Act on understanding, not on guessing.** If the cause is not clear, do not run commands hoping one will work. Look up the error message in this document or in the decision trees (07-01). Run the command that addresses the identified cause.

---

## VI. Professional Insight

In professional teams, troubleshooting Git is systematic rather than reactive. Teams document common errors and their resolutions in internal wikis. Onboarding processes include diagnostic runbooks. CI/CD pipeline logs provide the same category of error information that Git CLI output does — and are read with the same diagnostic approach.

The difference between a developer who resolves Git problems quickly and one who does not is rarely technical knowledge. It is the habit of reading error messages carefully, establishing current state before acting, and understanding why a resolution works rather than repeating it by memory.

That habit, practised in academic projects where the consequences of errors are recoverable, transfers directly to professional environments where they may not be.

---

## Summary

Troubleshooting requires diagnostic discipline — reading before acting, understanding before repeating.

This document provides:

- Init vs clone diagnostic path and correction
- Push rejection diagnostics for every common error type
- The five-step merge conflict resolution process with full explanation of conflict markers
- A reference table of the most common error messages, their meanings, and their resolutions
- A general diagnostic approach for problems not explicitly covered

**The principle for all of it:**

Git messages are diagnostic information, not punishment. Read them. Understand them. Act from that understanding.

---

Proceed to:

→ 07-05 — Templates
