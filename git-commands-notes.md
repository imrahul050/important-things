# Git & GitLab Commands – Practical Quick Reference

> Replace `BRANCH_NAME`, `COMMIT_MESSAGE`, `REPO_URL`, etc. with your actual values.

---

## 1. Check Git

```bash
git --version
```

**Why:** Check Git installation/version.

---

## 2. Configure Git

```bash
git config --global user.name "Rahul Kumar"
git config --global user.email "your-email@example.com"
```

Check:

```bash
git config --global --list
```

---

# Repository

## 3. Clone a repository

```bash
git clone REPO_URL
```

Example:

```bash
git clone git@192.168.0.7:group/sathi.git
```

Clone into a specific folder:

```bash
git clone git@192.168.0.7:group/sathi.git dayalProjects/sathi
```

**Why:** Download an existing remote repository to your computer.

---

## 4. Initialize Git

```bash
git init
```

**Why:** Make an existing folder a Git repository.

---

## 5. Check status

```bash
git status
```

**Why:** See modified, new, deleted and staged files.

---

## 6. Check remote

```bash
git remote -v
```

**Why:** See which GitLab/GitHub repository is connected.

---

## 7. Add remote

```bash
git remote add origin REPO_URL
```

Example:

```bash
git remote add origin git@192.168.0.7:group/sathi.git
```

`origin` = name given to the remote repository.

---

# Branches

## 8. Show branches

Local:

```bash
git branch
```

Local + remote:

```bash
git branch -a
```

`-a` = all branches.

---

## 9. Create a branch

```bash
git branch BRANCH_NAME
```

Example:

```bash
git branch feature/user-crud
```

**Important:** This creates the branch but does **not** switch to it.

---

# 10. Checkout a branch ⭐

```bash
git checkout BRANCH_NAME
```

Example:

```bash
git checkout develop
```

**Why:** Switch from your current branch to another branch.

Example:

```text
Current:
feature/login

Run:
git checkout develop

Now:
develop
```

---

## 11. Create + checkout a branch

```bash
git checkout -b BRANCH_NAME
```

Example:

```bash
git checkout -b feature/user-crud
```

`-b` = create a new branch and immediately switch to it.

This is one of the most commonly used `checkout` commands.

---

# `checkout` vs `switch`

Modern Git recommends `switch` for branch operations:

```bash
git switch develop
git switch -c feature/user-crud
```

But you will frequently see older/company projects using:

```bash
git checkout develop
git checkout -b feature/user-crud
```

### Remember:

```text
git checkout BRANCH
        ↓
Switch branch

git checkout -b BRANCH
        ↓
Create + switch branch

git switch BRANCH
        ↓
Switch branch

git switch -c BRANCH
        ↓
Create + switch branch
```

**For your workplace:** Know both.

---

## 12. Delete local branch

Safe:

```bash
git branch -d BRANCH_NAME
```

Example:

```bash
git branch -d feature/user-crud
```

`-d` = safe delete.

Force:

```bash
git branch -D BRANCH_NAME
```

`-D` = force delete.

---

# Pull / Fetch

## 13. Fetch

```bash
git fetch
```

**Why:** Download remote branch/commit information without changing your current files.

All remotes:

```bash
git fetch --all
```

`--all` = fetch from all remotes.

---

## 14. Pull

```bash
git pull
```

**Why:** Get remote changes and merge them into your current branch.

Example:

```bash
git checkout develop
git pull
```

Specific branch:

```bash
git pull origin develop
```

---

# Changes

## 15. Add one file

```bash
git add FILE_NAME
```

Example:

```bash
git add app/Models/User.php
```

**Why:** Put changes into the staging area.

---

## 16. Add everything

```bash
git add .
```

**Why:** Stage all changes in the current directory.

Then check:

```bash
git status
```

---

# Commit

## 17. Commit changes

```bash
git commit -m "COMMIT_MESSAGE"
```

Example:

```bash
git commit -m "Add user CRUD API"
```

`-m` = commit message.

**Why:** Save staged changes in Git history.

---

## 18. View commit history

```bash
git log
```

Short:

```bash
git log --oneline
```

`--oneline` = one-line format.

---

# Push

## 19. Push current branch

```bash
git push
```

**Why:** Upload local commits to remote.

---

## 20. First push of new branch

```bash
git push -u origin BRANCH_NAME
```

Example:

```bash
git push -u origin feature/user-crud
```

`-u` = set the remote branch as the upstream/tracking branch.

After this:

```bash
git push
```

is enough.

---

## 21. Push without setting upstream

```bash
git push origin BRANCH_NAME
```

Example:

```bash
git push origin feature/user-crud
```

---

# Merge

## 22. Merge a branch

Example: merge feature into `develop`.

```bash
git checkout develop
git pull
git merge feature/user-crud
```

Then:

```bash
git push origin develop
```

**Company practice:** Usually create a **GitLab Merge Request** instead of directly merging into `develop/main`.

---

# Undo / Restore

## 23. Unstage a file

```bash
git restore --staged FILE_NAME
```

Example:

```bash
git restore --staged app/Models/User.php
```

**Why:** Remove the file from staging but keep your code changes.

---

## 24. Discard changes

```bash
git restore FILE_NAME
```

Example:

```bash
git restore app/Models/User.php
```

⚠️ This removes your uncommitted changes in that file.

---

## 25. Change last commit message

```bash
git commit --amend -m "Correct message"
```

**Why:** Modify the latest commit message.

---

# Stash

## 26. Temporarily save changes

```bash
git stash
```

**Why:** Temporarily put your uncommitted changes aside.

Example:

```bash
git stash
git checkout develop
git pull
```

---

## 27. See stashes

```bash
git stash list
```

---

## 28. Restore latest stash

```bash
git stash pop
```

**Why:** Bring the latest stashed changes back.

---

# Compare

## 29. See unstaged changes

```bash
git diff
```

**Why:** See what you changed but haven't staged.

---

## 30. See staged changes

```bash
git diff --staged
```

**Why:** See what will go into the next commit.

---

# Remote

## 31. Change remote URL

```bash
git remote set-url origin REPO_URL
```

Example:

```bash
git remote set-url origin git@192.168.0.7:group/sathi.git
```

---

## 32. Remove remote

```bash
git remote remove origin
```

---

# ⭐ Typical Dayal Company Workflow

### Start new feature

```bash
git checkout develop
git pull
git checkout -b feature/FEATURE_NAME
```

Example:

```bash
git checkout develop
git pull
git checkout -b feature/student-crud
```

Then develop your feature.

### Save and push

```bash
git status
git add .
git commit -m "Add student CRUD"
git push -u origin feature/student-crud
```

After the first push:

```bash
git push
```

Then create a **GitLab Merge Request**:

```text
feature/student-crud
        ↓
     develop
```

---

# ⭐ Most Important Commands

```bash
# Check
git status

# Switch
git checkout develop

# Create + switch
git checkout -b feature/login

# Get latest code
git pull

# Stage
git add .

# Commit
git commit -m "Add login API"

# First push
git push -u origin feature/login

# Later push
git push

# History
git log --oneline

# Branches
git branch -a
```

### Common flags

| Flag        | Meaning                     | Example                            |
| ----------- | --------------------------- | ---------------------------------- |
| `-m`        | Commit message              | `git commit -m "Fix API"`          |
| `-u`        | Set upstream                | `git push -u origin feature/login` |
| `-b`        | Create branch               | `git checkout -b feature/login`    |
| `-c`        | Create branch with `switch` | `git switch -c feature/login`      |
| `-a`        | All branches                | `git branch -a`                    |
| `-d`        | Safe delete                 | `git branch -d feature/login`      |
| `-D`        | Force delete                | `git branch -D feature/login`      |
| `--all`     | All remotes                 | `git fetch --all`                  |
| `--oneline` | Compact log                 | `git log --oneline`                |
| `--staged`  | Staged changes              | `git diff --staged`                |
