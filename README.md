# 🚀 Learn Git & GitHub

A **friendly, copy-paste-ready guide** for absolute beginners who want to confidently use Git and GitHub.  
This guide teaches you what Git is, how to use it, and why each step matters — all with simple examples.

> 🧠 **Who is this for?**  
> Students, new developers, or anyone who’s ever asked:  
> _“How do I push my code to GitHub?”_

---

## 🧭 Table of Contents

1. [What is Git & GitHub?](#-what-is-git--github)
2. [Install & Setup](#️-install--setup)
3. [Create or Clone a Repo](#-create-or-clone-a-repo)
4. [Track Changes & Commits](#-track-changes--commits)
5. [Branching](#-branching)
6. [Merging](#-merging)
7. [Fix Merge Conflicts](#-fix-merge-conflicts)
8. [Undo & Recover](#-undo--recover)
9. [Remotes & GitHub](#-remotes--github)
10. [Pull Requests](#-pull-requests)
11. [.gitignore Basics](#-gitignore-basics)
12. [Everyday Workflow](#-everyday-workflow)
13. [Troubleshooting](#-troubleshooting)
14. [Cheat Sheet](#-cheat-sheet)
15. [Glossary](#-glossary)
16. [Practice Exercises](#-practice-exercises)
17. [Contributing](#-contributing)
18. [License](#-license)

---

## 💡 What is Git & GitHub?

| Term       | Meaning                                                                             |
| ---------- | ----------------------------------------------------------------------------------- |
| **Git**    | A version control system that tracks changes in your code over time.                |
| **GitHub** | A website that hosts your Git repositories online so you can share and collaborate. |

**Think of it like this:**  
🧍 _You_ = developer  
🗃️ _Git_ = your local history tracker  
☁️ _GitHub_ = the cloud backup + collaboration space

---

## ⚙️ Install & Setup

Make sure Git is installed:

```bash
git --version
```

If you see a version number, you’re good!  
If not, [download Git](https://git-scm.com/downloads).

**Optional (for GitHub lovers):**

```bash
gh --version  # GitHub CLI
```

### 🪪 Configure your identity

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

### 🧩 Recommended setup

```bash
git config --global init.defaultBranch main
git config --global pull.rebase false
git config --global core.editor "code --wait"  # VS Code users
```

Verify your settings:

```bash
git config --list --show-origin
```

---

## 🆕 Create or Clone a Repo

**Start a new project folder:**

```bash
git init
git branch -M main
```

Create a first file:

```bash
echo "# My First Git Project" > README.md
git add README.md
git commit -m "docs: add README"
```

**Clone an existing GitHub repo:**

```bash
git clone https://github.com/<username>/<repo>.git
cd <repo>
```

> 💬 **Tip:** “Init” means _initialize a Git history_. “Clone” means _copy someone else’s repo from GitHub._

---

## 📝 Track Changes & Commits

Check what’s changed:

```bash
git status
```

Stage and commit:

```bash
git add <file>   # pick specific file
git add .        # add everything (use carefully)
git commit -m "feat: add first version"
```

View history:

```bash
git log --oneline --graph --decorate --all
```

**Good commit messages:**

- ✅ `feat: add contact form`
- ✅ `fix: correct typo in header`
- ✅ `docs: explain setup steps`

> 🧠 **Why commit?**  
> It’s like saving a checkpoint of your project.

---

## 🌿 Branching

Branches let you experiment without breaking your main code.

```bash
git branch              # show branches
git switch -c feature/ui
# work...
git switch main
```

> 💬 “Branching” = working on a copy of your project history.

---

## 🔀 Merging

Merge your feature branch into main:

```bash
git switch main
git merge feature/ui
```

Keep a clear merge commit:

```bash
git merge --no-ff feature/ui -m "Merge feature/ui"
```

> 💡 Beginners should stick with **merge**, not **rebase**, until comfortable.

---

## ⚡ Fix Merge Conflicts

When Git can’t merge automatically, it marks conflicts like this:

```text
<<<<<<< HEAD
Your current change
=======
Their incoming change
>>>>>>> feature/ui
```

To fix:

1. Keep the correct version.
2. Delete `<<<<<<<`, `=======`, `>>>>>>>`.
3. Add and continue:
   ```bash
   git add <file>
   git merge --continue
   ```

> In VS Code: use the blue “Accept Current / Incoming / Both” buttons.

---

## 🧯 Undo & Recover

| Task                | Command                                     |
| ------------------- | ------------------------------------------- |
| Unstage a file      | `git restore --staged <file>`               |
| Discard local edits | `git restore <file>`                        |
| Edit last commit    | `git commit --amend`                        |
| Revert a bad commit | `git revert <commit>`                       |
| Reset to old commit | `git reset --hard <commit>` ⚠️ irreversible |

View differences:

```bash
git diff          # unstaged
git diff --staged # staged
```

---

## 🌐 Remotes & GitHub

Connect your local repo to GitHub:

```bash
git remote add origin https://github.com/<username>/<repo>.git
git push -u origin main
```

Later, push updates:

```bash
git push
git pull
```

**Sync branches:**

```bash
git push -u origin feature/ui
```

---

## 💬 Pull Requests (PRs)

A **Pull Request** = asking to merge your branch into another (e.g., main).

### Steps

1. Push your branch:
   ```bash
   git push -u origin feature/ui
   ```
2. On GitHub, click **“Compare & pull request”**.
3. Add a title & description.
4. Review, discuss, and merge.
5. Pull updates locally:
   ```bash
   git switch main
   git pull
   ```

> ✅ **Squash & merge** = keeps history clean  
> 🧩 **Merge commit** = keeps all commits

---

## 🚫 .gitignore Basics

Ignore junk files you don’t want in Git.

Example:

```
# Node
node_modules/
dist/
.env

# Python
__pycache__/
*.pyc

# OS/Editor
.DS_Store
.vscode/
Thumbs.db
```

Apply after creating:

```bash
git rm -r --cached .
git add .
git commit -m "chore: apply .gitignore"
```

> 🧠 Never upload `.env` or API keys — they are **secrets**.

---

## 🔄 Everyday Workflow (Simple Flow)

```bash
git switch main
git pull
git switch -c feature/my-task

# Work on code
git add .
git commit -m "feat: add login button"

git push -u origin feature/my-task
# open PR on GitHub
```

After merge:

```bash
git switch main
git pull
git branch -d feature/my-task
git push origin --delete feature/my-task
```

---

## 🧩 Troubleshooting

| Problem                              | Fix                                                    |
| ------------------------------------ | ------------------------------------------------------ |
| **Detached HEAD**                    | `git switch -c temp && git switch main`                |
| **Push rejected (non-fast-forward)** | `git pull` → resolve → `git push`                      |
| **Merge conflict**                   | open file, fix, `git add` + `git merge --continue`     |
| **Undo merge in progress**           | `git merge --abort`                                    |
| **Committed secret**                 | rotate secret, remove file, rewrite history (advanced) |

---

## 📘 Cheat Sheet

```bash
# Init & clone
git init
git clone <url>

# Inspect
git status
git log --oneline --graph
git diff

# Commit
git add .
git commit -m "message"
git commit --amend

# Branch
git switch -c <branch>
git merge <branch>

# Remote
git push -u origin <branch>
git pull

# Undo
git restore <file>
git reset --hard <commit>
git revert <commit>
```

---

## 🧠 Glossary (Plain English)

| Term                  | Meaning                                  |
| --------------------- | ---------------------------------------- |
| **Repo**              | Your project folder with Git tracking.   |
| **Commit**            | A saved version of your code.            |
| **Branch**            | A separate line of work.                 |
| **Merge**             | Combine branches.                        |
| **Rebase**            | Rebuild your branch history.             |
| **Remote**            | Online copy of your repo (e.g., GitHub). |
| **PR (Pull Request)** | Propose and review code before merging.  |

---

## 🧪 Practice Exercises

1. **Create your first repo**
   - Run `git init`, add a README, make your first commit.
2. **Branch & merge**
   - Make a new branch, edit a file, merge back.
3. **Conflict practice**
   - Create the same file in two branches, merge, and resolve conflict.
4. **Push to GitHub**
   - Create a remote, push, and make a pull request.

---

## 🤝 Contributing

Want to improve this guide?

- Use clear branch names: `feature/<topic>` or `fix/<topic>`
- Keep examples simple for beginners
- Follow the [Conventional Commits](https://www.conventionalcommits.org/) format:
  - `feat:`, `fix:`, `docs:`, `chore:`, etc.

---

## 📜 License

MIT License © 2025 [Karan Bastola](https://github.com/karanbastola)

---

⭐ **If this helped you, star the repo and share it with a friend learning Git!**
