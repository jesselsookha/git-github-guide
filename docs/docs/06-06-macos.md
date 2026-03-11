# 06-06 — macOS Git Workflow

---

## I. Context

◼ Beginner

macOS provides a Unix-based terminal environment natively through **Terminal.app** (in `/Applications/Utilities/`) and optionally through alternative shells such as iTerm2. Unlike Windows, where a separate Git Bash environment is typically needed for a Unix-compatible terminal, macOS users work directly in a native Unix shell where all standard Git commands operate exactly as they do on Linux.

This means macOS users have access to the same terminal environment used by the majority of professional developers and CI/CD systems worldwide. Git commands, shell scripting, SSH key management, and file permission operations are all available without additional tooling.

Universal principle: **Git commands are platform-independent.** A command that works in macOS Terminal works identically in a Linux terminal and in Git Bash on Windows. The platform changes; the commands do not.

---

## II. Installing and Verifying Git

Open Terminal and run:

```bash
git --version
```

If Git is not installed, macOS will offer to install the Xcode Command Line Tools — a package that includes Git, compilers, and other developer utilities. Follow the prompt and allow installation to complete.

Once installed:

```bash
git --version
# git version 2.x.x
```

If the version returned is unexpectedly old (2.24 or earlier), macOS's system-bundled Git may be taking precedence over a separately installed version. Install Git via Homebrew for the current version:

```bash
brew install git
```

Then verify that the correct version is being used:

```bash
which git
# /usr/local/bin/git  (Homebrew) or /opt/homebrew/bin/git (Apple Silicon)
```

---

## III. Guided Workflow — First Repository

Scenario: you want to initialise and publish a project from macOS Terminal.

### Step 1 — Navigate to Project Folder

```bash
cd path/to/project
```

Verify location:

```bash
pwd
```

The path shown must be the project root — the folder containing your source files.

---

### Step 2 — Initialise Repository

```bash
git init
```

Verify:

```bash
ls -a
```

You should see `.git` listed among the hidden files. This confirms Git is tracking the correct directory.

---

### Step 3 — Stage Changes

```bash
git add .
```

Verify:

```bash
git status
```

Files should appear under "Changes to be committed."

---

### Step 4 — Commit

```bash
git commit -m "Initial commit"
```

Verify:

```bash
git log --oneline
```

The first commit hash and message should be visible.

---

### Step 5 — Add Remote

```bash
git remote add origin https://github.com/yourusername/projectname.git
```

Verify:

```bash
git remote -v
```

Both fetch and push URLs should point to the correct repository.

---

### Step 6 — Rename Branch if Needed

```bash
git branch -M main
```

Only needed if Git defaulted to `master`. Modern Git versions default to `main`, but older installations may not.

---

### Step 7 — Push

```bash
git push -u origin main
```

Subsequent pushes:

```bash
git push
```

---

## IV. macOS-Specific Considerations

### SSH vs HTTPS

macOS developers frequently use SSH key authentication rather than HTTPS with a personal access token. SSH offers the advantage of not requiring credential re-entry after initial setup.

To use SSH, generate a key pair and register the public key with GitHub:

```bash
ssh-keygen -t ed25519 -C "your@email.com"
cat ~/.ssh/id_ed25519.pub
```

Copy the output and add it to GitHub under Settings → SSH and GPG keys.

Remote URLs using SSH have this format:
```
git@github.com:username/repository.git
```

Rather than:
```
https://github.com/username/repository.git
```

Both connect to the same repository. The difference is the authentication mechanism.

### File Permissions

macOS's Unix-based filesystem tracks file permissions as part of file metadata. In some configurations, Git may report file permission changes (e.g., `chmod`) as file modifications — showing files as "modified" even when their content has not changed.

If permission changes are being tracked and should not be:

```bash
git config core.fileMode false
```

This tells Git to ignore permission differences. Use with awareness — in some projects, file permissions are meaningful and should be tracked.

### Case Sensitivity

macOS's default filesystem (HFS+ and APFS in standard configuration) is **case-insensitive** — it treats `File.txt` and `file.txt` as the same file. Linux filesystems are case-sensitive by default.

This creates a class of cross-platform bug: a file renamed from `File.txt` to `file.txt` on macOS appears unchanged to the filesystem, so Git may not detect the rename. The repository on GitHub (hosted on Linux) does track the case change. This discrepancy can cause confusing behaviour when the repository is cloned on a Linux machine or run through a Linux CI pipeline.

To avoid this: use consistent, lowercase filenames. If a case rename is needed, use a two-step approach:

```bash
git mv File.txt temp.txt
git mv temp.txt file.txt
```

This forces Git to record the rename explicitly.

---

## V. Terminal as the Clearest Git View

▲ Advanced

macOS Terminal provides the most transparent view of Git's internal state — more than any IDE integration. Operations that IDEs abstract into buttons are fully visible in the terminal:

- HEAD position (`git log --oneline`, `git status`)
- Branch divergence (`git log --oneline --graph --all`)
- Merge state during a conflict (`git status`)
- Reflog inspection (`git reflog`)
- Reset and revert operations and their immediate consequences

Students who develop Git fluency in the macOS terminal develop strong repository intuition — not because macOS is special, but because the CLI removes all abstraction. Every operation's effect is immediately visible in the next `git status` or `git log` output.

This is particularly valuable for recovery operations (05-02) and advanced branching (04-01, 04-03), where understanding the exact current state of HEAD and the branch pointer is essential for choosing the correct next command.

---

## VI. Professional Insight

◆ Intermediate

macOS is the most common operating system in professional software development environments — particularly in web development, mobile development, and open-source contribution. Its Unix-based environment means that terminal workflows developed on macOS transfer directly to Linux servers, CI/CD runners, and containerised environments.

Git is not platform-bound. Whether on Windows, macOS, or Linux, the repository model is identical. The `.git` directory structure, commit graph, branch pointers, and remote configuration are the same everywhere. Only the shell environment and file system characteristics differ — and understanding those differences, as documented in this section, is the knowledge that prevents cross-platform surprises.

Professional developers on macOS typically use the terminal for advanced Git operations and an IDE or GitHub Desktop for routine commits and staging. The terminal is not an alternative to IDE integration — it is the foundation that makes IDE integration understandable and trustworthy.

---

Proceed to:

→ Part 7 — Reference
