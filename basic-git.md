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

**Use:**

- Set the name that appears on your commits.
- Set the email linked to your commits and GitHub account.

### Set default branch to main

```bash
git config --global init.defaultBranch main
```

**Use:**

- Make all new repositories start with `main` instead of `master`.

### Check config

```bash
git config --list
```

```bash
git config --show-origin --list
```

**Use:**

- See your current Git settings.
- See where each Git setting comes from for debugging.

---

# 📁 Start a Project

### Initialize a repository

```bash
git init
```

**Use:**

- Turn the current folder into a Git repository.

### Clone a repository

```bash
git clone <repo_url>
```

**Use:**

- Download an existing repository from GitHub.

---

# ✏️ Basic Workflow (MOST IMPORTANT)

```bash
git status                  # Check status
git add .                   # Stage all changes
git add <file>              # Stage one file
git commit -m "message"     # Commit staged files
git push                    # Push changes
git pull                    # Pull changes
```

**Use:**

- See changed, staged, and untracked files.
- Prepare all changed files for the next commit.
- Save staged changes as a snapshot in history.
- Upload your local commits to GitHub.
- Download and merge the latest changes from GitHub.

### Shortcut commit (tracked files only)

```bash
git commit -am "message"
```

**Uses:**

- Quickly commit changes to existing tracked files.

---

# 📦 File Commands

### Create files (Git Bash / Linux)

```bash
touch index.html
touch styles.css app.js
```

**Use:**

- Create new empty files from the terminal.

### Windows alternative

```bash
echo "" > file.txt
```

**Use:**

- Create an empty file in PowerShell or Command Prompt.

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

**Use:**

- Remove a file from staging without losing changes.

### Discard changes

```bash
git restore <file>
```

**Use:**

- Throw away changes and restore the last committed version.

### Unstage everything

```bash
git reset
```

**Use:**

- Remove all files from staging while keeping changes.

### Hard reset (danger)

```bash
git reset --hard
```

**Use:**

- Completely discard all uncommitted changes and return to the last commit.

---

# 🌿 Branching

### View local branches

```bash
git branch
```

**Use:**

- See all local branches and your current branch.

### Create branch

```bash
git branch feature-name
```

**Use:**

- Start a new line of development.

### Create a branch from another branch

```bash
git branch new-branch source-branch
```

**Use:**

- Create a branch starting from a specific branch.

### Create + switch

```bash
git checkout -b feature-name
```

**Use:**

- Create a branch and immediately move to it.

**Modern:**

```bash
git switch -c feature-name
```

**Use:**

- Create a branch and switch to it using modern Git.

### Switch branch

```bash
git checkout main
git switch main
```

**Use:**

- Move to another branch to continue work there.

### Merge branch

```bash
git checkout main
git merge feature-name
```

**Use:**

- Bring another branch's commits into the main branch.

### Delete local branch

```bash
git switch main
git branch -d local-branch
```

**Use:**

- Remove a local branch that is no longer needed.

### Force delete a local branch

```bash
git branch -D branch-name
```

**Use:**

- Delete a local branch even if it has unmerged commits.

---

# 🌐 GitHub Remote

### Add remote repo

```bash
git remote add origin <url>
```

**Use:**

- Connect your local project to a GitHub repository.

### Check remote

```bash
git remote -v
```

**Use:**

- See the names and URLs of connected repositories.

### Push to GitHub

```bash
git push -u origin main
```

**Use:**

- Push the main branch for the first time and remember its remote.

### Push branch to Github

```bash
git push --set-upstream origin branch-name
```

or

```bash
git push -u origin branch-name
```

**Use:**

- Upload a new branch to GitHub and track it.

### Delete remote branch

```bash
git push origin --delete master
```

**Use:**

- Remove a branch from GitHub.

---

# 🔄 Sync

### Pull updates

```bash
git pull
```

**Use:**

- Download and merge the latest remote changes.

### Fetch only

```bash
git fetch
```

**Use:**

- Download remote changes without merging them.

---

# 📜 History & Debug

### View commit history

```bash
git log
```

**Use:**

- See a visual summary of commits and branches.

### Compact graph-view or history

```bash
git log --oneline --graph --decorate --all
```

**Use:**

- See a visual summary of commits and branches.

### Show changes

```bash
git diff
git diff --staged
```

**Use:**

- See changes that have not been staged.
- See what will be included in the next commit.

### Show commit details

```bash
git show <commit_id>
```

**Use:**

- Inspect a specific commit and its changes.

---

# 🔥 Fix Merge Conflicts

### Update main and merge it into your branch

```bash
git switch main
git pull origin main
git switch my-branch
git merge main
```

**Use:**

- Switch to `main` and update it with the latest changes from GitHub.
- Switch back to your `branch` and merge the updated `main` into it.

### Finish a resolved conflict

```bash
git add .
git commit
git push
```

**Use:**

- Save and upload the conflict resolution after fixing the files.
- Create a Pull Request and merge your branch into `main`

### Abort a merge

```bash
git merge --abort
```

**Use:**

- Cancel the merge and return to the state before it started.

---

# 🧠 Git Mental Model

- `add` → select changes
- `commit` → save snapshot
- `push` → upload to GitHub
- `pull` → download updates
- `branch` → parallel timeline
- `merge` → Combine timelines

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


test one

test nummber 2

test error