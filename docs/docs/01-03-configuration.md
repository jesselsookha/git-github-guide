# Configuring Git Identity

◼ Beginner

Before your first commit, Git must know who you are.

This is not a formality. Git records authorship information in every commit — permanently. Your name and email are embedded into the history of every repository you contribute to. This information travels with your commits when you push to GitHub, when a lecturer reviews your submission, and when a future employer inspects your public repositories.

It is part of your development history, and it should be configured correctly from the beginning.

---

# I. Why Identity Matters

Every commit Git records contains the following information:

- Author name
- Author email
- Timestamp — the exact date and time the commit was created
- Commit message — the description you provide

This information is permanently stored in the repository history. It cannot be edited without rewriting history — which is a disruptive and, in shared repositories, a damaging operation.

The consequences of incorrect configuration are real:

- **Anonymous commits** — if no name is configured, commits may appear without an author, making attribution impossible
- **Incorrect attribution** — if a name or email does not match the account, commits will not link to the correct GitHub profile
- **Confusion in group projects** — when contributors cannot be clearly identified, collaborative work becomes harder to assess and harder to manage
- **Broken GitHub profile linking** — GitHub links commits to profiles by matching the commit email to a registered account. If the email does not match, the commit appears as an unlinked contribution — invisible to your contribution graph and to any reviewer looking at your profile

In an academic context, this matters for honest assessment. In a professional context, it matters for traceability, code ownership, and accountability.

Configure your identity once. Configure it correctly.

---

# II. Setting Your Name

Open a terminal and run:

```bash
git config --global user.name "Your Full Name"
```

Use your real, full name.

Avoid:

- Nicknames or handles
- Student numbers
- Abbreviations or initials

Your commit history is part of your professional identity. The name attached to your commits is the name that appears in GitHub's commit log, in pull request reviews, in contribution histories, and in any repository that is ever reviewed by someone other than yourself. Treat it accordingly.

The `--global` flag means this setting applies to all repositories on your machine. You only need to set it once.

---

# III. Setting Your Email

```bash
git config --global user.email "your-email@example.com"
```

The email address used here must match the email registered to your GitHub account.

This is the mechanism GitHub uses to associate commits with profiles. When you push commits whose author email matches your GitHub account, those commits appear on your profile's contribution graph, link correctly in pull request histories, and display your profile when inspectors hover over your name in the commit log.

If the emails do not match:

- Commits will appear as contributions from an unrecognised author
- Your contribution graph on GitHub will not reflect the work
- Reviewers, lecturers, and potential employers will see commits that cannot be traced to your profile

If you have multiple email addresses — one for GitHub, one for institutional use — use whichever matches your GitHub account. The GitHub account is the source of truth for how commits are attributed online.

---

# IV. Personal Email vs Student Email

This is a practical question worth addressing directly.

Use the email that is connected to your GitHub account — whichever that may be.

However, there is a longer-term consideration: student email addresses are typically deactivated after graduation. If you use your student email for your GitHub account and your Git configuration, and then lose access to that address, you may face challenges recovering or maintaining that account.

If you intend to maintain your GitHub account and your repositories beyond your studies — which is strongly recommended — consider creating or transitioning to a personal email address as your primary GitHub account email while you are still a student.

This avoids a situation where your commit history and professional portfolio become inaccessible because of an expired institutional email.

Consistency matters more than which domain the email belongs to. What matters is that your Git configuration, your GitHub account, and your long-term access to both are all aligned.

---

# V. Verifying Configuration

After setting your name and email, verify that both are stored correctly.

Run:

```bash
git config --list
```

This outputs all current Git configuration values. Look for:

```
user.name=Your Full Name
user.email=your-email@example.com
```

If these values are missing or incorrect, re-run the configuration commands in Sections II and III with the correct values. The new values will overwrite the old ones.

You can also verify individual values directly:

```bash
git config user.name
git config user.email
```

Each command returns just that one value — useful for quick checks without parsing the full list.

---

# VI. Local vs Global Configuration

Git operates with a hierarchy of configuration levels:

**Global configuration** applies to all repositories on your machine. This is what the `--global` flag sets. It is stored in a file called `.gitconfig` in your home directory.

**Local configuration** applies only to a single repository. It is stored inside that repository's `.git/config` file and overrides global settings for that repository only.

To set a local identity override inside a specific repository:

```bash
git config user.name "Different Name"
git config user.email "different-email@example.com"
```

Run these commands without `--global`, inside the repository folder.

This is useful in professional situations where you contribute to work repositories under a different name or corporate email, while maintaining a personal identity for personal projects. For example, a developer might have their personal email set globally, and override it with their work email inside client repositories.

Most students will use global configuration only. But understanding the distinction prepares you for multi-account workflows that are common in professional environments.

---

# VII. Why This Step Must Not Be Skipped

Misconfigured identity is one of the most common and least obvious sources of problems in student projects.

The consequences accumulate:

- Broken contribution tracking means a shared project cannot reliably show who did what
- Confusion in collaborative repositories can lead to disputes about authorship that are genuinely difficult to resolve after the fact
- Incorrect academic attribution means your work may not be visible under your name when a lecturer reviews the repository
- An unlinked GitHub profile means the commits you make as a student — which should be building a professional portfolio — are invisible to anyone who looks at your account

Git tracks authorship strictly and permanently.

Configure it correctly once, verify it immediately, and you will never encounter these problems.

---

Proceed to:

→ How Git Works
