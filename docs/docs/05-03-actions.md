# 05-03 — GitHub Actions

◆ Intermediate

GitHub Actions is a workflow automation system built directly into GitHub.

It allows you to define automated processes — called workflows — that run in response to events in your repository: a push to a branch, a Pull Request being opened, a release being published, or a schedule. Those workflows can compile your code, run your tests, package your application, deploy it to a server, or perform any sequence of commands that can be expressed in a script.

The key implication: every time you push code, something can happen automatically. The result of that push does not have to wait for a developer to manually check it. GitHub Actions makes the repository an active participant in the development process — not just a place where code is stored, but a system that responds to change.

Actions are not limited to mobile or web applications. They work for Java projects, C# and .NET projects, ASP.NET web applications, React Native apps, databases, and documentation systems including MkDocs. Any project that can be built or tested from a command line can be automated with Actions.

---

## I. Core Concept — What Actions Does and Why It Matters

◼ Beginner

GitHub Actions operates through **YAML workflow files** stored in a hidden directory at the root of your repository:

```
.github/workflows/build.yml
```

The file name is arbitrary — what matters is its location. Any `.yml` file in `.github/workflows/` is treated as a workflow definition by GitHub.

Every workflow file specifies three things:

- **Trigger (`on:`)** — the event that causes the workflow to run. Common triggers are `push` (code pushed to a branch), `pull_request` (a PR opened or updated), `schedule` (a time-based cron schedule), and `workflow_dispatch` (manual trigger from the GitHub interface).
- **Jobs** — independent units of work that run in parallel or in sequence. Each job runs in its own virtual machine.
- **Steps** — the individual commands or reusable actions that make up each job. Steps run in order within a job.

When a trigger fires, GitHub allocates a virtual machine (runner), checks out your repository onto it, executes every step in sequence, and reports the result — success or failure — back to the repository interface.

Think of it as a clean machine that knows nothing about your project, receives your code, follows your instructions exactly, and tells you whether the result was successful. This is exactly the standard you need: if it works on the runner, it works from a clean install. If it fails, there is a configuration or code issue that needs to be fixed before the project can be considered complete.

---

## II. Why Actions Matters for Students

◆ Intermediate

The value of Actions in an academic context is not primarily about automation for its own sake — it is about the feedback loop and the professional habit.

**Immediate, objective feedback.** When you push code, the workflow runs within seconds. If the build fails, you know immediately — not when a lecturer runs your project, not when a teammate clones the repository, but now. The error is in front of you while the code is fresh.

**Consistency.** The runner knows nothing about your machine, your IDE version, your local environment settings, or any configuration that exists only on your computer. If the workflow succeeds, the project builds in a clean environment. This is the same standard a professional deployment pipeline applies.

**Accountability.** Every workflow run is recorded in the repository's Actions tab with a full log. The history of which pushes passed and which failed is visible to everyone with repository access. This creates a transparent record of build health over time.

**Professional preparation.** CI/CD pipelines are standard practice in every serious software development environment. Understanding how to write and read a workflow file — even a simple one — is professional literacy. Knowing that a green checkmark means the build passed and a red cross means something broke is knowledge that transfers directly to every team and every tool.

---

## III. Anatomy of a Workflow File

◼ Beginner

A minimal workflow file has four sections. Here is a complete, annotated example for a Java project:

```yaml
name: Build Java Project         # Display name in the Actions tab

on:
  push:
    branches: [ "main" ]         # Trigger: run whenever code is pushed to main

jobs:
  build:                         # Job name (arbitrary)
    runs-on: ubuntu-latest       # Runner: a fresh Ubuntu virtual machine

    steps:
      - uses: actions/checkout@v3          # Step 1: check out the repository code
      
      - name: Set up JDK 17               # Step 2: install Java
        uses: actions/setup-java@v3
        with:
          java-version: '17'
          distribution: 'temurin'

      - name: Build with Maven            # Step 3: compile and package
        run: mvn --batch-mode package

      - name: Upload JAR artifact         # Step 4: save the compiled file
        uses: actions/upload-artifact@v3
        with:
          name: application-jar
          path: target/*.jar
```

Reading this file:

- The workflow runs on every push to `main`
- GitHub allocates a fresh Ubuntu machine
- The four steps install the required Java version, compile the project with Maven, and upload the resulting JAR file as a downloadable artifact
- If any step fails, the workflow stops and reports failure — the subsequent steps do not run

The `uses:` keyword references pre-built actions from the GitHub Actions marketplace. `actions/checkout` is the standard action that downloads your repository code onto the runner. `actions/setup-java` installs a specific Java version. `actions/upload-artifact` saves a file from the runner so it can be downloaded after the workflow completes.

The `run:` keyword executes a shell command directly — any command you could run in a terminal.

---

## IV. Android Project Workflow — Annotated Example

◆ Intermediate

Android projects are among the more complex build targets for Actions, because the Android SDK, Gradle, and signing configurations all need to be in place. An Actions workflow handles this automatically.

A typical Android build workflow:

```yaml
name: Android Build

on:
  push:
    branches: [ "release" ]       # Trigger on pushes to the release branch

env:
  date_today: ${{ github.run_number }}   # Use run number as a version identifier

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v3

      - name: Set up JDK 17
        uses: actions/setup-java@v3
        with:
          java-version: '17'
          distribution: 'temurin'

      - name: Grant execute permission for Gradlew
        run: chmod +x gradlew

      - name: Build APK (debug and release)
        run: ./gradlew assemble

      - name: Build App Bundle (AAB)
        run: ./gradlew app:bundleRelease

      - name: Upload APK Release
        uses: actions/upload-artifact@v3
        with:
          name: ${{ env.date_today }}-APK-release
          path: app/build/outputs/apk/release/

      - name: Upload AAB Release
        uses: actions/upload-artifact@v3
        with:
          name: ${{ env.date_today }}-AAB-release
          path: app/build/outputs/bundle/release/
```

What this workflow produces:

- On every push to the `release` branch, GitHub compiles the Android project entirely in the cloud
- Both a debug APK (for testing) and a release APK and AAB (for distribution) are generated
- The compiled files are uploaded as downloadable artifacts — accessible from the Actions tab without needing to build locally

This means a teammate without Android Studio configured can still install the latest build on a device by downloading the APK from GitHub. A lecturer can verify that the project builds without running it locally. The build history shows exactly which commits produced successful builds.

---

## V. Actions Across Project Types

▲ Advanced

The same workflow structure applies to any project type. What changes is which setup steps and build commands are used.

### Java Projects

```yaml
- uses: actions/setup-java@v3
  with:
    java-version: '17'
- run: mvn package          # Maven build
# or
- run: ./gradlew build      # Gradle build
```

Artifacts: JAR files uploaded from `target/` or `build/libs/`

---

### C# Console and Windows Forms

```yaml
- name: Set up .NET
  uses: actions/setup-dotnet@v3
  with:
    dotnet-version: '8.0.x'
- run: dotnet build
- run: dotnet test
- run: dotnet publish -c Release -o ./publish
```

Artifacts: published binaries from `./publish/`

---

### ASP.NET Web Applications

```yaml
- run: dotnet publish -c Release -o ./publish
- name: Deploy to Azure Web App
  uses: azure/webapps-deploy@v2
  with:
    app-name: your-app-name
    publish-profile: ${{ secrets.AZURE_PUBLISH_PROFILE }}
    package: ./publish
```

The `secrets.AZURE_PUBLISH_PROFILE` references a repository secret — a value stored securely in GitHub's settings and injected into the workflow at runtime, never visible in the workflow file itself. This is how credentials are handled safely in Actions.

---

### React Native

```yaml
- uses: actions/setup-node@v3
  with:
    node-version: '18'
- run: npm install
- run: npm test
- run: npm run build
```

For Android targets, the Android SDK setup steps from the Android example above are combined with the Node steps.

---

### Documentation — MkDocs

```yaml
- uses: actions/setup-python@v4
  with:
    python-version: '3.x'
- run: pip install mkdocs mkdocs-material
- run: mkdocs build
- name: Deploy to GitHub Pages
  uses: peaceiris/actions-gh-pages@v3
  with:
    github_token: ${{ secrets.GITHUB_TOKEN }}
    publish_dir: ./site
```

This is the workflow that publishes documentation — including this guide — automatically to GitHub Pages on every push to `main`. Every commit that modifies a Markdown file triggers a rebuild and a deployment. The live documentation is always current.

---

## VI. Reading Workflow Results

◆ Intermediate

After a workflow runs, its result appears in multiple places:

**On the repository's main page:** a small coloured dot next to the most recent commit. Green means the last workflow passed. Red means it failed. Yellow means it is currently running.

**In the Actions tab:** a full list of all workflow runs, sorted by date. Each run shows which branch triggered it, whether it passed or failed, and how long it took.

**Inside a workflow run:** clicking on any run shows the individual jobs and steps. Each step's output is logged — every command that was run, every line it printed, and the exit code. When a build fails, the log shows exactly which step failed and what the error was.

Learning to read these logs is a practical debugging skill. A compilation error in a Maven build produces the same error message in an Actions log as it does in a local terminal. A test failure shows the same stack trace. The environment is different; the errors are identical.

A workflow that passes is a signal that the project builds cleanly from the repository, in a clean environment, exactly as a new contributor or a deployment system would experience it.

A workflow that fails is a signal to fix the problem — before it becomes someone else's problem when they clone the repository or before it blocks a deployment.

---

## VII. Professional Insight — CI/CD Pipelines

▲ Advanced

GitHub Actions is an implementation of **Continuous Integration** and optionally **Continuous Deployment** — two practices that are foundational to professional software development.

**Continuous Integration (CI)** is the practice of automatically building and testing every change as soon as it is pushed. The goal is to discover integration problems immediately, while the change is fresh and the developer who made it is available to fix it. CI prevents the scenario where a team works for weeks, merges everything at once, and discovers that the pieces do not fit together.

**Continuous Deployment (CD)** extends CI by automatically deploying successfully built and tested code to a production or staging environment. When the CI pipeline passes, the deployment happens without manual intervention. This enables teams to ship changes multiple times per day with confidence.

Together, CI/CD pipelines enforce a discipline that makes large-scale software development safe and fast:

- No code reaches production without passing automated tests
- Build failures are discovered in minutes, not days
- Deployment is a routine, automated operation — not a stressful manual procedure
- The history of builds provides an audit trail of what was deployed and when

Academic projects rarely need full CD — there may be no production environment to deploy to. But understanding CI — writing a workflow, reading its output, treating a failed build as a thing to be fixed before moving on — builds the foundational habits that professional environments rely on.

---

## VIII. Classroom Activity — Actions in Practice

❈ Collaboration

**Objective:** Write a workflow file for an existing project, trigger it, read the output, and understand what it means.

**Steps:**

I. Create a repository with a simple project — Java, C#, or a React app

II. Create the workflow directory:
```bash
mkdir -p .github/workflows
```

III. Create a workflow file (`.github/workflows/build.yml`) using the appropriate template from Section V

IV. Commit and push:
```bash
git add .github/
git commit -m "Add CI workflow for build automation"
git push
```

V. Open the repository on GitHub and navigate to the **Actions** tab

VI. Observe the workflow run in real time — watch the steps execute in sequence

VII. If the build passes: download the artifact (JAR, EXE, or APK) and verify it runs

VIII. Intentionally introduce a compile error, push again, and observe the failure in the log

IX. Fix the error, push, and watch the workflow pass

**Reflection:**

- What information does the Actions log provide that `git log` does not?
- How would this workflow change your confidence in the state of the repository?
- What would need to be added to the workflow to also run automated tests?

---

## Summary

GitHub Actions transforms a repository from a place where code is stored into a system that responds to change.

Every push can trigger a build. Every Pull Request can be verified before it is merged. Every release can be packaged and deployed automatically. The result is visible to everyone, recorded permanently, and independent of any individual machine or configuration.

Key principles:

- Workflow files live in `.github/workflows/` and are written in YAML
- Triggers define when a workflow runs; jobs and steps define what it does
- Runners are clean virtual machines — if the build passes there, it passes everywhere
- Green checkmark: build passed. Red cross: something needs to be fixed.
- Logs provide line-by-line detail of every step — read them, do not ignore them
- Actions is the entry point to CI/CD — a professional practice that starts here

Actions transforms GitHub from a version control host into a **collaboration and automation platform**.

---

Proceed to:

→ 05-04 — Codespaces
