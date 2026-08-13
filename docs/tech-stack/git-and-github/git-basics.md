# Git & GitHub Basics

A beginner-friendly introduction to Git and GitHub — the foundation for contributing to EndToEndLabCR projects.

---

## What is Git?

**Git is a version control system** — it tracks changes to your files over time so you can:

- Go back to any previous version
- See who changed what and when
- Work on different features at the same time without breaking things

Think of it like a **save point system** in a video game. Every time you make a meaningful change, you "save" (commit) your progress. If something goes wrong, you can load a previous save.

### Key Concepts

| Term                  | What it means                                      | Analogy             |
| --------------------- | -------------------------------------------------- | ------------------- |
| **Repository (repo)** | A folder with all your project files + Git history | A project folder    |
| **Commit**            | A saved snapshot of your changes                   | A save point        |
| **Branch**            | A parallel version of your code                    | A parallel universe |
| **Main/Master**       | The default, stable branch                         | The "real world"    |

---

## What is GitHub?

**GitHub is a website that hosts Git repositories** so multiple people can work together.

Without GitHub, Git only lives on your computer. GitHub puts it online so others can:

- See your code
- Suggest changes
- Review your work before it goes live

### GitHub-Specific Concepts

| Term                  | What it means                                            |
| --------------------- | -------------------------------------------------------- |
| **Fork**              | Your personal copy of someone else's repo                |
| **Clone**             | Downloading a repo to your computer                      |
| **Pull Request (PR)** | A request to merge your changes into someone else's repo |
| **Merge**             | Combining your changes into the main codebase            |
| **Upstream**          | The original repo you forked from                        |
| **Origin**            | Your fork (your copy on GitHub)                          |

---

## How It All Fits Together

```
                    ┌────────────────────────┐
                    │   GitHub (the cloud)   │
                    │                        │
  ┌─────────────┐   │   ┌─────────────────┐  │   ┌──────────────────┐
  │  Upstream   │   │   │   Your Fork     │  │   │  Other People's  │
  │ (original)  │◄──┼──►│   (origin)      │◄─┼─► │  Forks           │
  └─────────────┘   │   └─────────────────┘  │   └──────────────────┘
                    │            ▲           │
                    └────────────┼───────────┘
                                 │ git push / git pull
                                 ▼
                    ┌─────────────────────────┐
                    │  Your Computer (local)  │
                    │                         │
                    │  ┌───────────────────┐  │
                    │  │  Your Files + Git │  │
                    │  └───────────────────┘  │
                    └─────────────────────────┘
```

**The contribution flow:**

1. You **fork** the upstream repo → creates your copy on GitHub
2. You **clone** your fork → downloads it to your computer
3. You **branch** off main → creates a safe space to work
4. You **edit** files → make your changes
5. You **commit** → saves your changes
6. You **push** → sends changes to your fork on GitHub
7. You open a **PR** → asks the upstream repo to accept your changes
8. Your PR gets **merged** → your changes become part of the main project

## Quick Reference Card

Print this or keep it open while you work:

```
┌──────────────────────────────────────────────────────────────┐
│                    GIT QUICK REFERENCE                       │
├──────────────────────────────────────────────────────────────┤
│  git status              → See what changed                  │
│  git diff                → See the actual changes            │
│  git add <file>          → Stage a file                      │
│  git commit -m "msg"     → Save changes                      │
│  git push                → Send to GitHub                    │
│  git pull                → Get latest changes                │
│  git checkout -b <name>  → Create + switch to new branch     │
│  git checkout main       → Switch to main branch             │
│  git branch -d <name>    → Delete a branch                   │
│  git log --oneline       → See commit history                │
│  git remote -v           → See connected repos               │
├──────────────────────────────────────────────────────────────┤
│  Before every new task:                                      │
│    git checkout main && git pull upstream main               │
├──────────────────────────────────────────────────────────────┤
│  Commit format: type: description                            │
│  Types: docs | feat | fix | refactor | chore | style         │
└──────────────────────────────────────────────────────────────┘
```

---

## Next Steps

Ready to start contributing? Follow our practical guides:

- [Your First Contribution Guide](../../guides-and-tutorials/git-github-guide.md) — commands, PRs, and common mistakes
- [Branch Naming Guidelines](./github/branch/naming-guidelines.md)
- [Commit Message Guidelines](./github/commits-guide.md)
- [Code Review Guidelines](./code-review-guidelines.md)
