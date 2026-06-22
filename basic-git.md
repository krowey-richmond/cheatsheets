# 🚀 Basic Git & GitHub Cheatsheet

> A practical Git command reference for daily development workflow.

---

# 🧠 Core Concept

Git has 3 areas:

- **Working Directory** → your files
- **Staging Area** → prepared changes
- **Repository** → saved commits (history)

GitHub = remote copy of your repository.

---

# ⚙️ Setup

### Set identity

```bash
git config --global user.name "Your Name"
git config --global user.email "you@email.com"
```

### Set default branch to main

```bash
git config --global init.defaultBranch main
```

### Check config

```bash
git config --list
git config --show-origin --list
```

---

# 📁 Start a Project

### Initialize repository

```bash
git init
```

### Clone repository

```bash
git clone <repo_url>
```

---

# ✏️ Basic Workflow (MOST IMPORTANT)

```bash
git status
git add .
git commit -m "message"
git push
```

### Shortcut commit (tracked files only)

```bash
git commit -am "message"
```

---

# 📦 File Commands

### Create files (Git Bash / Linux)

```bash
touch index.html
touch styles.css app.js
```

### Windows alternative

```bash
echo "" > file.txt
```

---

# 📤 Staging & Undo

### Stage file

```bash
git add <file>
git add .
```

### Unstage file

```bash
git restore --staged <file>
```

### Discard changes

```bash
git restore <file>
```

### Hard reset (danger)

```bash
git reset --hard
```

---

# 🌿 Branching

### View branches

```bash
git branch
```

### Create branch

```bash
git branch feature-name
```

### Create + switch

```bash
git checkout -b feature-name
```

Modern:

```bash
git switch -c feature-name
```

### Switch branch

```bash
git checkout main
git switch main
```

### Merge branch

```bash
git checkout main
git merge feature-name
```

### Create branch from correct sources

```bash
git branch new-branch-name source-branch
```

---

# 🌐 GitHub Remote

### Add remote

```bash
git remote add origin <url>
```

### Push to GitHub

```bash
git push -u origin main
```

### Check remote

```bash
git remote -v
```

### Delete remote branch

```bash
git push origin --delete master
```

---

# 🔄 Sync

### Pull updates

```bash
git pull
```

### Fetch only

```bash
git fetch
```

---

# 📜 History & Debug

### View commits

```bash
git log
```

### Compact graph view

```bash
git log --oneline --graph --decorate --all
```

### Show changes

```bash
git diff
git diff --staged
```

### Show commit details

```bash
git show <commit_id>
```

---

# 🧹 Fixing Mistakes

```bash
git restore file
git restore --staged file
git reset
git reset --hard
```

---

# 🧠 Git Mental Model

- `add` → select changes
- `commit` → save snapshot
- `push` → upload to GitHub
- `pull` → download updates
- `branch` → parallel timeline

---

# 🚀 Recommended Workflow

```bash
git checkout -b feature
# work
git add .
git commit -m "feature done"
git checkout main
git merge feature
git push
```

---

# ⚠️ Ignore for now

- submodules
- worktrees
- cherry-pick
- reflog
- advanced log filters

---

# 🎯 Goal

Learn workflow first.
Commands come naturally later.
