# 02-03 — GitHub Classroom: Cloning Your Assignment Repository

❈ Collaboration

This workflow applies when:

- A lecturer creates an assignment using GitHub Classroom
- You receive an invitation link
- You accept the assignment
- A private repository is automatically created for you inside the organisation

This is not your personal repository.
This is an institutional repository.

That distinction is not administrative detail — it changes everything about how you should interact with it. Understanding what GitHub Classroom actually creates, and why cloning is the only correct starting action, is the foundation of every successful Classroom workflow.

---

## I. Core Concept — What GitHub Classroom Actually Does

When a lecturer creates an assignment in GitHub Classroom, a specific and deliberate structure is established behind the scenes.

I. The assignment is attached to a GitHub **organisation account** — not a personal account
II. A template repository may or may not be provided, depending on the assignment design
III. An invitation link is generated and shared with students
IV. Each student who accepts the link triggers an automatic action: GitHub creates a **private repository** under the organisation, linked to that student's GitHub account

By the time you click the invitation link and accept the assignment, the repository already exists. It was created by GitHub. You did not create it, and you do not own it in the way you would own a personal repository.

What this means structurally:

- The repository has an owner: the organisation
- You have **write access** — you can push commits to it
- Your lecturer has **administrative access** — they can view all commits, timestamps, and contributor activity
- The repository is **private** — only you and the lecturer can see it

That repository is the official submission space for this assignment.

You do not create it.
You do not initialise it.
You do not decide its structure.

**You clone it.**

---

## II. What "Clone" Actually Means

The word "clone" is sometimes treated casually — as if it just means "download." It is worth understanding precisely.

`git clone` means:

*"Create a complete local copy of an existing remote repository, including its full history, all branches, and all configuration — and connect my local copy to the remote automatically."*

When you clone, Git:

- Downloads every file in the repository
- Downloads the complete commit history
- Creates a `.git` directory in the local folder, establishing it as a fully functional Git repository
- Automatically configures `origin` to point back to the URL you cloned from

You are not starting Git.
Git is already started — on the remote.

Cloning is the act of replicating that existing repository to your machine, fully connected and ready to use.

This is fundamentally different from `git init`, which *begins* a new history in a folder that had none.

The distinction in one line:

- `git init` — starts history
- `git clone` — copies existing history

That distinction must be clear before proceeding with any Classroom workflow.

---

## III. The Standard Classroom Workflow — With Template Files

Most assignments include starter code or a template structure. When a template is provided, the repository already contains:

- Project files and folder structure
- Possibly initial commits reflecting the template state
- A README or instructions file

The correct workflow is:

### I. Accept the Assignment Link

- Click the invitation link provided by your lecturer
- Accept the assignment on GitHub
- Wait for GitHub to confirm that your repository has been created

You will see a message similar to: *"Your assignment repository has been created."* A link to the repository will be provided.

---

### II. Copy the Repository URL

Navigate to your newly created repository.

Click **Code** → Select **HTTPS** → Copy the URL.

The URL will end in `.git` and will be under the organisation's name, not your personal account. For example:

```
https://github.com/organisation-name/assignment-yourname.git
```

---

### III. Clone the Repository

Open a terminal in the directory where you keep your projects, and run:

```bash
git clone https://github.com/organisation-name/assignment-yourname.git
```

Git will:

- Create a new folder with the repository name
- Download all files and commit history
- Create the `.git` directory inside it
- Configure `origin` automatically

**Do not run `git init`.** Clone has already initialised Git inside the repository folder. Running `git init` afterwards creates a second, conflicting repository structure — which is covered in detail in 02-04.

---

### IV. Open the Project in Your IDE

Once cloned, open the project using your IDE:

- **NetBeans** → File → Open Project → navigate to cloned folder
- **Visual Studio** → File → Open → Solution → select the `.sln` file
- **Android Studio** → File → Open → navigate to cloned folder
- **VS Code** → File → Open Folder → select cloned folder

The project is now ready for development. The remote is already configured. You can begin working immediately.

---

## IV. What If the Repository Is Empty?

This is a common source of confusion.

Sometimes a lecturer creates an assignment with no starter files — no template, no initial content, just an empty repository. Students then ask: *"If there is nothing in it, why do I still have to clone?"*

The answer is structural, not about file content.

Even when a Classroom repository contains no files, it still contains:

- A branch (`main`) established by GitHub
- Repository configuration tied to the organisation
- Access permissions linking your account to the lecturer's account
- Institutional ownership — the repository belongs to the organisation, not to you

If you clone this empty repository, you are working inside the correct submission space from the very first commit. Every commit you make, every push you perform, goes directly into the repository your lecturer is tracking.

If instead you:

- Create your own folder
- Run `git init`
- Create your own repository
- Try to connect it later

You are working in a disconnected personal repository. Your commits are not visible to your lecturer. Your work is not inside the assessment system. Even if you eventually connect the repositories with `--allow-unrelated-histories`, the history tells a fragmented story — which matters in assessment contexts where development process is evaluated.

**Even an empty Classroom repository must be cloned.**

---

## V. The Correct Workflow After Cloning

Once the repository is cloned and the project is open in your IDE, your workflow is simple:

```bash
git add .
git commit -m "Describe what you completed"
git push
```

You do not need to:

- Add a remote (`git remote add`) — clone configured it automatically
- Rename the branch — it is already set to `main`
- Set upstream tracking — the first push may require `-u`, but after that, plain `git push` works

Verify the remote configuration at any time:

```bash
git remote -v
```

You will see `origin` pointing to the organisation repository URL — confirming that your commits are going to the correct place.

---

## VI. Common Mistakes in Classroom Workflows

### Mistake I — Running `git init` After Cloning

This is the most damaging Classroom error. When `git init` is run inside a cloned repository, it creates a new `.git` folder inside a directory that already has one — or worse, overwrites the existing one entirely.

The result is a repository structure that is disconnected from the remote, with commits that no longer belong to the correct history.

The rule: **If you cloned, do not initialise.**

---

### Mistake II — Downloading ZIP Instead of Cloning

GitHub provides a "Download ZIP" option on every repository page. This downloads the current file contents — but nothing else. No `.git` folder. No commit history. No remote connection.

If you download a ZIP:

- Git is not active in that folder
- You cannot push
- You have no connection to the submission repository
- Any work done in the ZIP folder is invisible to your lecturer unless manually re-added through the correct workflow

ZIP is a file transfer.
Clone is repository replication.

They are not interchangeable, and in an academic submission context, ZIP is never the correct approach.

---

### Mistake III — Pushing to a Personal Repository

Some students:

- Create their own repository on GitHub
- Push their work there
- Submit that personal repository link

This bypasses the Classroom system entirely. The submission is not inside the organisation. The lecturer may not have access. The automated tracking that GitHub Classroom provides does not apply.

Always confirm that you are pushing to the organisation repository by running:

```bash
git remote -v
```

The URL should contain the organisation name — not your personal GitHub username.

---

## VII. Professional Insight — Why Clone Is the Correct Model

▲ Advanced

In professional development environments, the same principle applies unconditionally: you never initialise a repository that already exists remotely. You clone it.

When you join a company and are given access to a codebase, you clone the repository. When you contribute to an open-source project, you fork it (which creates your own remote copy) and then clone your fork. When you set up a new machine, you clone your repositories from GitHub.

Initialising would create a disconnected local repository with no shared history — which is exactly the problem described throughout 02-02 and 02-04. Professional environments have no tolerance for this, because it risks breaking the shared history that teams depend on.

GitHub Classroom mirrors this real-world model deliberately. The assignment repository belongs to the organisation. Your role is to work within it, contribute to it, and submit through it — not to create a parallel structure.

The goal is not only submission.
It is to practise collaborative development correctly, with the same discipline that professional workflows require.

---

## VIII. Summary — Decision Logic

| Repository origin | Correct action |
|---|---|
| You created it yourself | See 02-01 or 02-02 |
| GitHub Classroom created it | Clone — always |
| Classroom repo is empty | Still clone — always |

The rule does not change based on content:

**You initialise what you create.**
**You clone what already exists.**

---

Proceed to:

→ 02-04 — GitHub Classroom: When You Initialised Instead of Cloning
