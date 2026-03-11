# Installing Git

◼ Beginner

Git must be installed correctly before any meaningful work can begin.

This statement is worth taking seriously. Git is not installed on most systems by default, and an incomplete or incorrectly configured installation creates problems that are difficult to diagnose — because the errors that follow do not always make it obvious that installation is the root cause.

Improper installation leads to:

- Command failures — Git commands are not recognised in the terminal
- Authentication issues — Git cannot communicate with GitHub
- Environment confusion — IDEs detect Git inconsistently or not at all
- Incorrect version usage — older system-bundled versions may behave differently from current Git

This section ensures your Git environment is stable, correctly installed, and accessible to all tools that depend on it.

---

# I. Installing Git on Windows

I. Visit the official Git website:
   `https://git-scm.com`

II. Click **Download for Windows**

III. Run the installer

### Recommended Installer Settings

The Git for Windows installer presents a series of configuration screens. For most beginners, the default settings are acceptable — but several options deserve deliberate attention.

Ensure the following are selected:

- ✔ **"Git from the command line and also from 3rd-party software"**
  This adds Git to your system PATH, making it available in Command Prompt, PowerShell, and within IDEs. Without this, Git only works inside Git Bash.

- ✔ **Default branch name: `main`**
  Modern Git and GitHub use `main` as the default branch name. Older installations may default to `master`. Aligning these from the start prevents naming conflicts when connecting to GitHub repositories.

- ✔ **Use bundled OpenSSH**
  Ensures consistent SSH handling. Unless you have a specific reason to use an external SSH client, leave this at default.

- ✔ **Checkout Windows-style, commit Unix-style line endings**
  Windows and Unix systems handle line endings differently. This setting ensures your files display correctly on Windows while remaining compatible with collaborators on macOS or Linux.

If unsure about any other options — leave them at their defaults.

---

# II. Installing Git on macOS

### Option A — Official Installer

I. Visit `https://git-scm.com`
II. Download the macOS installer
III. Run the installer and follow the prompts

macOS may prompt for a security confirmation on first run, as the installer is from an external developer. This is expected — proceed through the system prompt.

### Option B — Homebrew (Recommended for Developers)

Homebrew is a package manager for macOS that simplifies installation and updates of developer tools. If Homebrew is already installed, Git can be installed with a single command:

```bash
brew install git
```

The advantage of this approach is that updates are straightforward:

```bash
brew upgrade git
```

Homebrew-installed Git typically stays more current than the version bundled with macOS's developer tools. For developers who plan to work seriously with Git, Homebrew is the preferred route.

### Option C — Xcode Command Line Tools

macOS ships with a version of Git bundled inside the Xcode Command Line Tools. Running any Git command in Terminal for the first time may prompt you to install these tools. While functional, this version is often older. It is preferable to install Git directly via the official installer or Homebrew.

---

# III. Verifying Installation

After installation, open a terminal:

- **Windows:** Command Prompt or PowerShell
- **macOS:** Terminal

Run:

```bash
git --version
```

You should see output similar to:

```
git version 2.x.x
```

The specific version number is less important than confirming that Git is accessible. If this command runs without error, the installation is functional.

If the command is not recognised:

- Close and reopen the terminal — new PATH entries require a fresh session
- Restart the computer — some installers require a full restart to take effect
- Reinstall Git, ensuring the PATH option is selected during setup

---

# IV. Confirming Git Is Available in PATH

The PATH is a system-level list of directories that the operating system searches when you type a command. For Git to work from any terminal window — and for IDEs to find it automatically — Git's executable must be in the PATH.

On Windows, open Command Prompt and run:

```bash
where git
```

On macOS, open Terminal and run:

```bash
which git
```

Both commands return the file path to the Git executable. If a path is returned, Git is available globally. If nothing is returned, Git is not in the PATH — and this must be corrected before proceeding.

---

# V. Common Installation Issues

### Git not recognised after installation

Symptom: Running `git --version` returns "command not found" or "'git' is not recognised."

Cause: Git's directory was not added to the system PATH during installation.

Fix:
- Reinstall Git on Windows, ensuring the option "Git from the command line and also from 3rd-party software" is selected
- On macOS, reinstall via Homebrew or the official installer
- After reinstalling, open a new terminal window and test again

---

### Permission issues on macOS

Symptom: The installer cannot complete, or Git commands fail with permission errors.

Cause: macOS security restrictions may block unsigned or externally sourced installers, or Terminal may not have been granted necessary permissions.

Fix:
- Install via Homebrew, which handles permissions more gracefully than direct installers
- Ensure Terminal has Full Disk Access in macOS System Preferences → Security & Privacy → Privacy

---

### Git version appears very old

Symptom: `git --version` returns a version significantly older than the current release (e.g., 2.x vs current 2.40+).

Cause: On macOS, the system may be using the Xcode-bundled Git rather than the one you installed.

Fix:
- On macOS, run `which git` to confirm which executable is being used
- If it points to `/usr/bin/git`, the system version is taking priority
- Install via Homebrew and follow Homebrew's instructions to set the correct PATH priority

---

# VI. Why Installation Matters

It may seem like a minor preliminary step, but Git's installation has consequences that extend across every workflow in this guide.

Git must be accessible globally because:

- IDEs depend on it — Visual Studio Code, Android Studio, Visual Studio, and NetBeans all locate Git through the system PATH. If Git is absent or misconfigured, these tools cannot execute version control operations.
- The CLI depends on it — every command in this guide is executed through a terminal. If Git is not in the PATH, none of those commands will work.
- Automation tools depend on it — GitHub Actions, CI/CD pipelines, and build scripts that invoke Git rely on it being available in the execution environment.
- Your collaborators depend on it — if your local Git installation is broken, you cannot push, pull, or sync reliably. That affects not just your work, but any shared repository you contribute to.

If Git is unstable at installation level, every workflow becomes unreliable — and the errors that follow can be extremely difficult to trace back to their source.

Installation is foundational. It is worth doing once, correctly.

---

Proceed to:

→ Configuring Git Identity
