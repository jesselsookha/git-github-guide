# 05-04 — Codespaces

◆ Intermediate

GitHub Codespaces is a cloud-based development environment — a complete, preconfigured workspace that lives in the browser or connects to your local VS Code installation, without requiring anything to be installed on your machine.

The practical significance of this is larger than it might initially appear. In a student cohort, a substantial portion of setup time — across every project, every semester — is spent dealing with environment inconsistencies: one student has the wrong Java version, another's IDE cannot find the Gradle wrapper, a third's machine produces build errors that do not appear on anyone else's. Codespaces eliminates this category of problem entirely. The environment is defined by the repository, not by the individual machine.

In professional contexts, Codespaces is used for onboarding, contribution to open-source projects, and polyglot development where different team members work in different technology stacks. The same principle applies: consistent, reproducible environments that are independent of local configuration.

---

## I. Core Concept — What a Codespace Is

◼ Beginner

A **Codespace** is a virtual machine hosted by GitHub that contains:

- Your repository's complete code — checked out automatically at the branch you select
- A preconfigured development environment — Linux-based, with VS Code as the editor, extensions, and the development tools appropriate for your project
- A full terminal — running on the virtual machine, giving access to any command-line operation
- Persistent storage for the duration of the Codespace — changes you make are saved until you stop or delete it

Think of it as VS Code running on a computer in the cloud, already connected to your repository. You open a browser, navigate to your repository, start a Codespace, and arrive at a functioning development environment — no installation required.

When you push commits from inside a Codespace, they are pushed directly to GitHub using your credentials. The Codespace is already authenticated — no separate credential setup is needed.

When the Codespace is stopped, uncommitted changes are preserved. When it is deleted, any unsaved or uncommitted work is lost. The rule is the same as always: **commit and push regularly.** The Codespace is not the repository — the repository is.

---

## II. Why Codespaces Is Useful

◆ Intermediate

### Consistency — Every Developer in the Same Environment

The most common source of "works on my machine" problems is environmental difference. Two developers using the same codebase but different JDK versions, different operating systems, or different dependency versions will sometimes produce different build results. In a student group where each member set up their IDE independently, these differences accumulate.

A Codespace environment is defined by a configuration file in the repository (`.devcontainer/devcontainer.json`) — or by GitHub's defaults for the detected project type. Every person who opens the repository in Codespaces gets an identical environment. This eliminates the environmental variable entirely.

### No Local Setup Delays

Setting up a development environment for a new project — installing the right SDK, configuring the IDE, resolving dependency conflicts — can consume hours, particularly for students new to a technology stack. Codespaces bypasses this entirely. Open the Codespace, and the environment is ready.

This is especially useful for:
- Students who need to start work on a new project type quickly
- Collaborators who want to contribute to a project without permanently modifying their local machine
- Anyone accessing their work from a device that is not their primary development machine

### Portability

Because Codespaces runs in the browser, it is accessible from any device with an internet connection. A student can continue work from a university lab machine, a tablet, or any computer without needing to set up Git, an IDE, or any dependencies.

### Direct Integration with GitHub Actions

Pushing commits from a Codespace triggers any configured GitHub Actions workflows immediately. The combination — edit in Codespace, push, watch the CI pipeline run, read the results — is a complete development feedback loop without a local IDE involved at any stage.

---

## III. Starting a Codespace

◼ Beginner

I. Navigate to your repository on GitHub
II. Click the **Code** button (the same button used to copy the clone URL)
III. Select the **Codespaces** tab
IV. Click **Create codespace on main** (or on whichever branch you want to start from)
V. GitHub allocates a virtual machine, checks out the repository, and opens VS Code in the browser

The first time a Codespace is created for a repository, it may take a minute to initialise — the virtual machine needs to be provisioned and the environment set up. Subsequent uses of the same Codespace are faster because the environment is already configured.

Inside the Codespace:

- The editor interface is VS Code — the same keyboard shortcuts, settings, and extension behaviour apply
- The terminal at the bottom is a full Linux shell — `git`, language runtimes, and build tools are available
- Files edited in the Codespace are tracked by Git exactly as they would be locally
- Committing and pushing works identically to local development:

```bash
git add .
git commit -m "Update from Codespace"
git push
```

---

## IV. Codespaces and GitHub Actions — The Complete Cloud Loop

◆ Intermediate

Codespaces and GitHub Actions are complementary tools that together create a complete cloud-based development and build pipeline.

The workflow:

I. Developer opens repository in Codespaces — no local setup required  
II. Code is edited and committed inside the Codespace  
III. Commit is pushed to GitHub  
IV. GitHub Actions workflow triggers automatically  
V. The workflow compiles, tests, and packages the project on a separate runner  
VI. Results are visible in the Actions tab; artifacts are downloadable  

Nothing in this chain requires a local machine beyond a browser. A student without a capable local machine — or a machine configured for a specific technology stack — can participate fully in the development process.

For Android development specifically: Codespaces provides the Java and Gradle environment for writing and committing code. GitHub Actions provides the Android SDK environment for compiling the APK. The compilation happens on a GitHub-hosted runner configured for Android builds — which is substantially easier to configure through Actions than locally.

---

## V. Codespaces Across Technologies

▲ Advanced

Codespaces is not language-specific. GitHub detects the project type from the repository contents and configures the environment accordingly. For more precise control, a `.devcontainer/devcontainer.json` file can specify the exact environment:

```json
{
  "name": "Java Project",
  "image": "mcr.microsoft.com/devcontainers/java:17",
  "extensions": [
    "vscjava.vscode-java-pack"
  ]
}
```

This file tells Codespaces to use a pre-built container image with Java 17 and to install the VS Code Java extension pack when the Codespace is created. The result is a consistent, project-specific environment for every contributor.

Technology-specific notes:

- **Java** — JDK, Maven, and Gradle are available by default in Java Codespaces. NetBeans is not available (it is a desktop application), but VS Code with the Java extension pack provides equivalent functionality for most tasks.
- **C# / .NET** — .NET SDK is preconfigured. Console applications, class libraries, and ASP.NET projects can be built and run from the terminal.
- **React Native** — Node.js and npm are available. JavaScript and TypeScript projects run in the Codespace. Mobile device emulation is not available in the cloud environment; APK/IPA compilation is handled by Actions.
- **MkDocs** — Python and pip are available. MkDocs can be installed, documentation built, and the live preview server run inside the Codespace (`mkdocs serve`), accessible through a forwarded port.

**Port forwarding** is a Codespaces feature that makes locally-running services accessible in the browser. When a server process starts inside the Codespace (a web application, a documentation preview, a development server), Codespaces creates a temporary URL that forwards browser traffic to that port. This is how web applications and MkDocs previews are accessed from a Codespace without deploying them.

---

## VI. Limitations and Honest Context

◆ Intermediate

Codespaces is a powerful tool, but it is not the right tool for every situation.

**Free tier limits.** GitHub provides a monthly free allocation of Codespace hours and storage for personal accounts. Once exhausted, Codespaces incurs cost. Students should be aware of their usage, particularly if keeping Codespaces running for long periods without active use.

**Not a replacement for local development skills.** Codespaces removes the need for local setup — it does not remove the need to understand what is being set up. A student who relies exclusively on Codespaces without understanding how Git, their SDK, and their build system interact will encounter difficulties the moment they need to work in a local environment — in an exam, on a machine without internet access, or in a professional environment that does not use Codespaces.

**Internet dependency.** Codespaces requires a stable internet connection. Local development does not. In environments where connectivity is unreliable, local development remains the more resilient option.

**Performance variation.** Cloud-hosted virtual machines may be slower than a capable local machine for compute-intensive tasks. Large builds or database operations may take longer in Codespaces than locally.

The recommended approach: use Codespaces to reduce friction, particularly for setup and consistency. Develop local environment skills in parallel so that both options are available.

---

## VII. Classroom Activity — Codespaces in Practice

❈ Collaboration

**Objective:** Experience the complete cloud development loop — from opening a Codespace through pushing code and observing an Actions workflow run.

**Steps:**

I. Lecturer creates a GitHub Classroom assignment with a starter repository that includes a basic GitHub Actions workflow

II. Each student opens their repository in Codespaces rather than cloning locally

III. Students edit their assigned files using the browser-based VS Code interface

IV. Students commit and push from the Codespace terminal:
```bash
git add .
git commit -m "Add implementation in Codespace"
git push
```

V. Students navigate to the Actions tab and observe the workflow triggered by their push

VI. Students download the compiled artifact (JAR, HTML output, or documentation site) from the Actions run

VII. Students attempt to run the downloaded artifact to verify it works

**Reflection:**

- What problems that would have occurred in local setup were avoided by using Codespaces?
- What would happen to uncommitted work in a Codespace if the Codespace were deleted?
- How does the combination of Codespaces and Actions change the role of the developer's local machine?

---

## Summary

GitHub Codespaces removes the local environment from the development equation — providing a consistent, preconfigured, cloud-hosted workspace that is always ready, always connected to GitHub, and always independent of individual machine configuration.

Key principles:

- A Codespace is VS Code in the cloud — fully functional, fully connected to your repository
- Consistency: every contributor gets the same environment, regardless of their local machine
- Commit and push from Codespaces exactly as you would locally — the commands are identical
- Codespaces + Actions = a complete cloud CI/CD loop with no local dependencies
- The devcontainer configuration file enables precise, reproducible environment definitions
- Codespaces complements local development skill — it does not replace the need for it

Together with GitHub Actions, Codespaces transforms GitHub from a code repository into a **complete development and automation platform** — accessible from a browser, reproducible by any contributor, and independent of any single machine.

---

Proceed to:

→ Part 6 — IDE Workflows
