# 🌿 Git Branches Cheatsheet

> A quick reference for the most commonly used Git branching commands.
> 
> Use this cheatsheet after studying the Branches documentation.

---

# 🌱 Create Branches

## Create a New Branch

```bash
git branch <branch-name>
```

Example:

```bash
git branch feature/login
```

---

## Create and Switch

```bash
git switch -c <branch-name>
```

Example:

```bash
git switch -c feature/login
```

---

# 🔄 Switch Branches

```bash
git switch <branch-name>
```

Example:

```bash
git switch main
```

---

## Using `checkout`

```bash
git checkout <branch-name>
```

Create and switch:

```bash
git checkout -b <branch-name>
```

---

# 📋 View Branches

## List Local Branches

```bash
git branch
```

---

## List Remote Branches

```bash
git branch -r
```

---

## List All Branches

```bash
git branch -a
```

---

## View Tracking Information

```bash
git branch -vv
```

---

# ✏️ Rename Branches

Rename the current branch:

```bash
git branch -m <new-name>
```

Rename another branch:

```bash
git branch -m <old-name> <new-name>
```

Force rename:

```bash
git branch -M <new-name>
```

---

# 🗑 Delete Branches

Delete a merged branch:

```bash
git branch -d <branch-name>
```

Force delete:

```bash
git branch -D <branch-name>
```

Delete a remote branch:

```bash
git push origin --delete <branch-name>
```

---

# 🔀 Merge Branches

Merge into the current branch:

```bash
git merge <branch-name>
```

Abort a merge:

```bash
git merge --abort
```

---

# 🌿 Rebase

Rebase onto another branch:

```bash
git rebase <branch-name>
```

Interactive rebase:

```bash
git rebase -i HEAD~3
```

Continue:

```bash
git rebase --continue
```

Abort:

```bash
git rebase --abort
```

Skip current commit:

```bash
git rebase --skip
```

---

# 🌍 Remote Branches

Push a branch:

```bash
git push origin <branch-name>
```

Push and create upstream:

```bash
git push -u origin <branch-name>
```

Fetch updates:

```bash
git fetch
```

Pull updates:

```bash
git pull
```

---

# 🔗 Tracking Branches

View upstream information:

```bash
git branch -vv
```

Set upstream:

```bash
git branch --set-upstream-to=origin/<branch-name>
```

Unset upstream:

```bash
git branch --unset-upstream
```

---

# 🌳 Common Branch Naming

## Features

```text
feature/login

feature/payment

feature/profile
```

---

## Bug Fixes

```text
bugfix/navbar

bugfix/login-validation
```

---

## Hotfixes

```text
hotfix/security

hotfix/api-timeout
```

---

## Releases

```text
release/v1.0

release/v2.1
```

---

# 🚀 Common Workflows

## Create a Feature

```text
Create Branch
      │
      ▼
Develop
      │
      ▼
Commit
      │
      ▼
Push
      │
      ▼
Pull Request
      │
      ▼
Merge
      │
      ▼
Delete Branch
```

---

## Update a Feature Branch

```bash
git switch feature/login
git fetch
git rebase main
```

or

```bash
git switch feature/login
git pull
```

_(Depending on your team's workflow.)_

---

## Merge a Completed Feature

```bash
git switch main
git merge feature/login
git branch -d feature/login
```

---

# 📊 Merge vs Rebase

|Merge|Rebase|
|---|---|
|Preserves history|Rewrites history|
|Creates merge commits|Creates a linear history|
|Safe for shared branches|Best for local branches|
|Easier for beginners|Requires more care|

---

# 🌍 Local vs Remote

|Local|Remote|
|---|---|
|`main`|`origin/main`|
|Your working branch|Remote-tracking branch|
|You commit here|Updated by `git fetch`|

---

# ⚠️ Remember

### `git branch`

Creates a branch.

**Does NOT switch to it.**

---

### `git switch`

Switches branches.

---

### `git switch -c`

Creates **and** switches.

---

### `git fetch`

Downloads information from the remote repository.

Does **not** modify your working directory.

---

### `git pull`

Fetches changes and integrates them into your current branch.

---

### `git push`

Uploads your local commits to the remote repository.

---

# 💡 Best Practices

- ✅ Keep `main` stable.
    
- ✅ Create one branch per feature.
    
- ✅ Commit frequently.
    
- ✅ Pull before starting new work.
    
- ✅ Push regularly.
    
- ✅ Review code before merging.
    
- ✅ Delete merged branches.
    
- ✅ Keep branches short-lived.
    

---

# 📚 Quick Command Reference

```bash
# Create
git branch feature/login

# Create & Switch
git switch -c feature/login

# Switch
git switch main

# List
git branch
git branch -a
git branch -r
git branch -vv

# Rename
git branch -m new-name

# Delete
git branch -d feature/login
git branch -D feature/login

# Merge
git merge feature/login

# Abort Merge
git merge --abort

# Rebase
git rebase main
git rebase --continue
git rebase --abort

# Push
git push origin feature/login

# Push & Track
git push -u origin feature/login

# Fetch
git fetch

# Pull
git pull
```