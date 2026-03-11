# 06-03 — Android Studio

---

## I. IDE Context

◼ Beginner

**Android Studio** is the official IDE for Android application development, built on JetBrains' IntelliJ IDEA platform. Its primary focus is the **Gradle build system**, the Android emulator, device management, and project structure management. Git integration is present but secondary — it exists under the **VCS (Version Control System)** menu and is not foregrounded the way it is in VS Code or GitHub Desktop.

This is important context: in Android Studio, Git is something you must explicitly activate and deliberately manage. The IDE will not remind you to commit. It will not warn you that you have uncommitted changes before closing. The responsibility for maintaining a healthy Git workflow is entirely the developer's.

---

## II. Under the Hood

When Git is initialised or detected in an Android Studio project:

- File status is shown with **colour coding** in the project tree: green for new untracked files, blue for modified tracked files
- The **Commit panel** (accessible via the left-side toolbar or `Git → Commit`) shows staged and unstaged changes
- The **Git menu** provides access to branches, remotes, log, and push/pull operations
- The **Terminal tab** (bottom toolbar) provides direct CLI access

**The verification test:** open the Terminal tab and run:

```bash
git status
```

The colour indicators and commit panel reflect the same state. The terminal is authoritative.

---

## III. Guided Workflow — New Android Project

Scenario: you create a new Android project in Android Studio and want to version-control and publish it.

### Step 1 — Initialise Git Repository

- **UI Action:** VCS → Enable Version Control Integration → select "Git"
- **CLI Equivalent:** `git init`
- **Effect:** Creates `.git` directory at the project root

⚠ **Project root vs `app/` directory.** Android Studio's project structure has a top-level project folder containing a Gradle wrapper, settings files, and an `app/` subdirectory that contains the actual application code. The `.git` folder must be at the **project root** — the top level — not inside `app/`. Git initialised inside `app/` tracks only the application code, missing Gradle configuration, manifests, and resource files.

Verify:
```bash
ls -a    # macOS/Linux
dir /a   # Windows
```

You should see `.git` at the same level as `build.gradle`, `gradlew`, and the `app/` directory.

---

### Step 2 — Configure .gitignore

Before the first commit, configure `.gitignore` to exclude Gradle build artifacts:

```
# Gradle
.gradle/
build/
app/build/

# IDE
.idea/
*.iml

# Android
local.properties
```

Android projects generate substantial build output with every compilation. Without a `.gitignore`, these files will be staged and committed — creating a repository that grows rapidly with binary files that cannot be meaningfully diffed and should not be part of the version history.

Android Studio may offer to create a `.gitignore` automatically. Accept it — then review and extend it if necessary.

---

### Step 3 — Stage Changes

- **UI Action:** Commit panel → select files with checkboxes
- **CLI Equivalent:** `git add <file>` or `git add .`
- **Effect:** Checked files are staged for commit

Checkboxes in the commit panel represent the staging operation. Each checked file is the equivalent of running `git add <file>` for that file.

---

### Step 4 — Commit

- **UI Action:** Enter message → "Commit"
- **CLI Equivalent:** `git commit -m "message"`
- **Effect:** Creates snapshot in local history

**Important:** "Commit" in Android Studio commits locally only. The button does not push to GitHub. The remote repository is unaffected until you explicitly push.

There is also a "Commit and Push" button — which performs `git commit` then `git push` in sequence. This is convenient for a mature workflow where you are confident in what you are committing. Use "Commit" alone when learning, to maintain the habit of verifying before pushing.

---

### Step 5 — Add Remote and Push

- **UI Action:** Git → Manage Remotes → "+" to add remote URL → then Git → Push
- **CLI Equivalent:**
  ```bash
  git remote add origin <url>
  git push -u origin main
  ```
- **Effect:** Connects local repository to GitHub and uploads commits

---

## IV. Branching in Android Studio

- **UI Action:** Branch indicator (bottom-right of the window, shows current branch name) → "New Branch"
- **CLI Equivalent:** `git checkout -b <branch-name>`
- **Effect:** Creates branch pointer and moves HEAD. The indicator updates to show the new branch name.

To switch branches: click the branch indicator → select the branch. This is `git switch <branch-name>`.

---

## V. Common Misconceptions

**"The `.git` folder should be inside `app/`."**
No. It must be at the project root. A `.git` directory inside `app/` tracks only application code. Gradle configuration, project-level settings, and the gradlew wrapper are outside it and untracked.

**"Gradle build files should be committed."**
Gradle-generated build artifacts — the `build/` and `.gradle/` directories — should not be committed. They are generated output, not source. The `build.gradle` and `settings.gradle` files (source configuration) should be committed. The distinction is: source files that define the build go in; generated files that result from the build stay out.

**"Commit and Push is two separate operations done together."**
Yes — that is precisely what it is. "Commit and Push" is `git commit` followed immediately by `git push`. Understanding this separation matters when the push fails (the commit succeeded; the push did not) or when you want to commit without pushing (on a slow connection, or before reviewing the diff one more time).

---

## VI. Professional Insight

◆ Intermediate

Android Studio is the industry-standard IDE for Android development. Its Gradle build system, device management, and emulator integration are unmatched for mobile work. Its Git integration is functional and sufficient for most workflows.

The caution for professional Android development is the same as for academic projects: Gradle environments generate significant build output, and `.gitignore` hygiene is essential. A repository that has committed build artifacts early in its history will carry that weight permanently — and the only way to remove it is a history rewrite that affects every contributor.

The discipline of reviewing what is staged before committing is more important in Android Studio than in most other IDEs — precisely because Android projects have more files that should not be committed.

---

Proceed to: → 06-04 — NetBeans

---
