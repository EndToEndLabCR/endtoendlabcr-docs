---
sidebar_position: 3
---

# Your First Contribution with Git & GitHub

This guide walks you through the practical steps of contributing to an EndToEndLabCR project — from cloning to your first merged pull request.

> **New to Git?** Start with the [Git & GitHub Basics](../tech-stack/git-and-github/git-basics.md) guide first, then come back here for the hands-on workflow.

---

## 1. Setup (do this once)

```bash
# Fork the repo on GitHub first (click "Fork" button)

# Clone your fork to your computer
git clone https://github.com/YOUR-USERNAME/repo-name.git
cd repo-name

# Connect to the original repo (upstream)
git remote add upstream https://github.com/EndToEndLabCR/repo-name.git

# Verify remotes
git remote -v
# You should see: origin (your fork) and upstream (original)
```

---

## 2. Daily Workflow (every contribution)

```bash
# 1. Make sure your main is up to date
git checkout main
git fetch upstream
git merge upstream/main
git push origin main

# 2. Create a new branch for your work
git checkout -b feature/what-youre-doing

# 3. Make your changes (edit files, add files, etc.)

# 4. Check what changed
git status
git diff

# 5. Stage your changes
git add <file>          # specific file
git add .               # all changed files

# 6. Commit your changes
git commit -m "type: description"

# 7. Push to your fork
git push -u origin feature/what-youre-doing

# 8. Open a PR on GitHub (see next section)
```

---

## 3. Commit Messages

We use **Conventional Commits** — a standard format that makes history readable.

### Format

```
type: description

optional body (explains why, not what)
```

### Types

| Type       | When to use                             | Example                         |
| ---------- | --------------------------------------- | ------------------------------- |
| `docs`     | Documentation changes                   | `docs: add git guide`           |
| `feat`     | New features                            | `feat: add user profile page`   |
| `fix`      | Bug fixes                               | `fix: correct typo in README`   |
| `refactor` | Code restructuring (no behavior change) | `refactor: simplify auth logic` |
| `chore`    | Maintenance tasks                       | `chore: update dependencies`    |
| `style`    | Formatting, whitespace                  | `style: fix indentation`        |

### Good vs Bad Commits

```
❌ Bad:  "update file"
✅ Good: "docs: add setup instructions for macOS"

❌ Bad:  "fix"
✅ Good: "fix: correct broken link in README"

❌ Bad:  "changes"
✅ Good: "feat: add user profile with name and avatar"
```

---

## 4. Pull Requests

### How to Create One

1. Push your branch to your fork: `git push -u origin your-branch`
2. Go to the **original repo** on GitHub
3. Click **"Compare & pull request"** (GitHub usually shows this prompt)
4. Or go to: `https://github.com/EndToEndLabCR/repo/compare/main...YOUR-USERNAME:your-branch`

### A Good PR Has

- **Clear title:** Follow the commit format (`type: description`)
- **Description:** What you changed and why
- **Screenshots** (if UI changed)
- **Linked issues** (if fixing a specific issue)

### PR Review Process

```
You open PR
    │
    ▼
Team reviews → Leave comments/suggestions
    │
    ▼
You address feedback → Push more commits
    │
    ▼
Reviewer approves → PR gets merged
    │
    ▼
Your branch is deleted (usually)
```

---

## 5. Cleanup (after your PR is merged)

```bash
# Switch back to main
git checkout main

# Delete your old branch
git branch -d feature/what-youre-doing

# Sync with upstream for next time
git fetch upstream
git merge upstream/main
```

---

## 6. Common Mistakes & How to Fix Them

### "I committed to main by accident"

```bash
# Don't panic. Create a branch from where you are
git checkout -b feature/my-accidental-work

# Reset main back to upstream
git checkout main
git reset --hard upstream/main
git push origin main --force
```

### "I forgot to add a file to my commit"

```bash
# Add the forgotten file
git add forgotten-file.md

# Amend the last commit
git commit --amend --no-edit
git push --force-with-lease
```

### "My branch is behind main"

```bash
# Fetch latest from upstream
git fetch upstream

# Merge into your branch
git merge upstream/main

# If there are conflicts, resolve them, then:
git add .
git commit -m "fix: resolve merge conflicts"
git push
```

### "I pushed to the wrong branch"

```bash
# Check which branches exist
git branch -a

# You can't easily "unpush" — but you can:
# 1. Create the correct branch from current state
git checkout -b correct-branch

# 2. Push it
git push origin correct-branch

# 3. Open PR from the correct branch
# 4. Delete the wrong branch on GitHub
git push origin --delete wrong-branch
```

---

---

## Related Guides

- [Git & GitHub Basics](../tech-stack/git-and-github/git-basics.md) — theory and concepts
- [Branch Naming Guidelines](../tech-stack/git-and-github/github/branch/naming-guidelines.md)
- [Commit Message Guidelines](../tech-stack/git-and-github/github/commits-guide.md)
- [Code Review Guidelines](../tech-stack/git-and-github/code-review-guidelines.md)
- [Branching Strategy](../tech-stack/git-and-github/branching-strategy.md)
