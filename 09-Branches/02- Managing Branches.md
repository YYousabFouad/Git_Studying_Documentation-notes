# 🌿 Managing Branches

## 📖 Introduction

As your project grows, you'll create many branches for features, bug fixes, experiments, and releases. Managing these branches helps keep your repository organized and easy to navigate.

Git provides several commands to list, inspect, rename, and delete branches.

---

# 🎯 Learning Objectives

After completing this chapter, you will be able to:

- List local and remote branches.
    
- Identify the current branch.
    
- View additional branch information.
    
- Rename branches safely.
    
- Delete branches that are no longer needed.
    
- Force delete branches when necessary.
    
- Follow good branch naming practices.
    

---

# 📋 Listing Local Branches

To display all local branches, use:

```bash
git branch
```

Example output:

```text
* main
  feature-login
  bugfix-navbar
```

### Understanding the Output

- `*` indicates your **current branch**.
    
- The remaining branches exist locally but are not currently checked out.
    

---

## View the Current Branch

Although `git branch` highlights the active branch, you can also use:

```bash
git status
```

Example:

```text
On branch feature-login
nothing to commit, working tree clean
```

---

# 📊 Viewing Branch Details

To display the latest commit on each branch:

```bash
git branch -v
```

Example:

```text
* main            5f8d7c1 Initial project setup
  feature-login   a93bc2e Add login page
```

This is useful for quickly seeing where each branch currently points.

---

## View Tracking Information

To display additional information such as upstream branches:

```bash
git branch -vv
```

Example:

```text
* main            5f8d7c1 [origin/main] Initial project setup
  feature-login   a93bc2e [origin/feature-login] Add login page
```

This command is especially helpful when working with remote repositories.

---

# 🌐 Listing Remote Branches

To list remote branches only:

```bash
git branch -r
```

Example:

```text
origin/main
origin/feature-login
origin/release-v1
```

---

# 🌍 Listing All Branches

To display both local and remote branches:

```bash
git branch -a
```

Example:

```text
* main
  feature-login
  remotes/origin/main
  remotes/origin/feature-login
```

---

# ✏️ Renaming a Branch

## Rename the Current Branch

If you're currently on the branch you want to rename:

```bash
git branch -m new-name
```

Example:

```bash
git branch -m feature-authentication
```

The current branch is immediately renamed.

---

## Rename Another Branch

If you're **not** on the branch:

```bash
git branch -m old-name new-name
```

Example:

```bash
git branch -m feature-login feature-authentication
```

---

# ⚠️ Force Renaming

If a branch with the new name already exists, Git normally prevents the rename.

To overwrite it:

```bash
git branch -M new-name
```

Use this command carefully, as it replaces an existing branch name.

---

# 🗑️ Deleting Branches

Once a branch has been merged and is no longer needed, it can be deleted.

## Safe Delete

```bash
git branch -d branch-name
```

Example:

```bash
git branch -d feature-login
```

Git only deletes the branch if it has already been fully merged.

This helps prevent accidental data loss.

---

## Why Does Git Sometimes Refuse?

Example:

```text
error: The branch 'feature-login' is not fully merged.
```

Git protects your work by refusing to delete branches that still contain unmerged commits.

---

# 🚨 Force Delete

If you intentionally want to remove an unmerged branch:

```bash
git branch -D branch-name
```

Example:

```bash
git branch -D experimental-feature
```

This permanently removes the branch reference.

> **Warning:** If the commits exist only on this branch and nowhere else, they may become difficult to recover.

---

# 📌 What Happens Internally?

Suppose the repository looks like this:

```text
A──B──C (main)
       \
        D──E (feature-login)
```

Deleting `feature-login` removes only the **branch pointer**.

The commits are not immediately deleted.

After deletion:

```text
A──B──C (main)

D──E (unreferenced)
```

Git eventually cleans up unreachable commits through **garbage collection**, but they may still be recoverable for some time using tools like `git reflog`.

---

# 🏷️ Branch Naming Conventions

Good branch names make repositories easier to understand.

Recommended examples:

```text
feature/login

feature/payment

bugfix/navbar

hotfix/security

release/v2.0
```

Avoid names such as:

```text
test

branch1

new

temp

mybranch
```

Branch names should clearly describe their purpose.

---

# 💡 Best Practices

- Keep branch names descriptive.
    
- Delete branches after they are merged.
    
- Use prefixes such as `feature/`, `bugfix/`, or `hotfix/`.
    
- Avoid keeping old branches that are no longer useful.
    
- Periodically review and clean up unused branches.
    

---

# ⚠️ Common Mistakes

### ❌ Force deleting without checking

Using:

```bash
git branch -D
```

can permanently remove access to work that hasn't been merged.

Always verify that the branch is no longer needed.

---

### ❌ Leaving dozens of unused branches

Repositories become harder to navigate when old branches accumulate.

Delete branches that have served their purpose.

---

### ❌ Using unclear branch names

Poor branch names make collaboration difficult.

Prefer descriptive names that explain the work being done.

---

# 📋 Command Summary

|Command|Description|
|---|---|
|`git branch`|List local branches|
|`git branch -v`|Show latest commit for each branch|
|`git branch -vv`|Show tracking information|
|`git branch -r`|List remote branches|
|`git branch -a`|List all branches|
|`git branch -m`|Rename a branch|
|`git branch -M`|Force rename a branch|
|`git branch -d`|Safely delete a merged branch|
|`git branch -D`|Force delete a branch|

---

# 📝 Summary

Managing branches is an essential part of maintaining a clean Git repository. Git provides commands to inspect, rename, and delete branches while protecting your work from accidental loss. By using descriptive names and removing obsolete branches, you keep your project organized and easier to collaborate on.

---

# 📚 Key Takeaways

- Use `git branch` to view local branches.
    
- Use `git branch -v` or `-vv` to inspect branch information.
    
- Rename branches with `git branch -m`.
    
- Delete merged branches with `git branch -d`.
    
- Use `git branch -D` only when you intentionally want to remove an unmerged branch.
    
- Keep your repository clean by deleting branches that are no longer needed.