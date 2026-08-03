# 🌿 Creating and Switching Branches

## 📖 Introduction

Once you understand what a branch is, the next step is learning how to create one and move between branches.

Creating a branch allows you to start a new line of development without affecting the current branch. Switching branches changes your working directory so you can continue working on a different line of development.

---

# 🎯 Learning Objectives

After completing this chapter, you will be able to:

- Create new branches.
    
- Switch between existing branches.
    
- Create and switch in a single command.
    
- Understand the difference between `git switch` and `git checkout`.
    
- Understand what happens internally when changing branches.
    
- Recognize a Detached HEAD state.
    

---

# 🌱 Creating a Branch

To create a new branch, use:

```bash
git branch <branch-name>
```

Example:

```bash
git branch feature-login
```

This command creates a new branch named `feature-login`.

> **Important:** Creating a branch does **not** switch to it. You remain on your current branch.

---

## Visual Example

Current history:

```text
A──B──C (main)
        ▲
       HEAD
```

After creating a new branch:

```text
A──B──C (main)
        │
        └── (feature-login)
```

Both branches point to the same commit.

HEAD is still on **main**.

---

# 🔍 Listing All Branches

To see all local branches:

```bash
git branch
```

Example output:

```text
* main
  feature-login
  bugfix-navbar
```

The `*` indicates the branch you're currently using.

---

# 🔄 Switching Branches

To move to another branch:

```bash
git switch <branch-name>
```

Example:

```bash
git switch feature-login
```

Now Git changes your working directory to match that branch.

HEAD also moves to the selected branch.

---

## Visual Example

Before switching:

```text
              HEAD
               │
               ▼
A──B──C (main)
      \
       (feature-login)
```

After switching:

```text
A──B──C (main)
      \
       (feature-login)
              ▲
              │
             HEAD
```

---

# 🚀 Creating and Switching at the Same Time

Instead of creating a branch first and switching later, Git allows both operations in one command.

```bash
git switch -c <branch-name>
```

Example:

```bash
git switch -c feature-payment
```

Git will:

1. Create the branch.
    
2. Switch to it immediately.
    

---

## Visual Flow

```text
Current Branch
      │
      ▼
git switch -c feature-payment
      │
      ▼
New Branch Created
      │
      ▼
HEAD Moves Automatically
```

---

# 📜 Using `git checkout`

Before Git 2.23, developers used:

```bash
git checkout <branch-name>
```

Example:

```bash
git checkout feature-login
```

To create and switch:

```bash
git checkout -b feature-login
```

These commands are still supported.

---

# 🔄 `git switch` vs `git checkout`

|Feature|`git switch`|`git checkout`|
|---|---|---|
|Switch branches|✅|✅|
|Create and switch|✅|✅|
|Restore files|❌|✅|
|Simpler for beginners|✅|❌|
|Introduced in Git 2.23|✅|❌|

### Why was `git switch` introduced?

`git checkout` performs multiple unrelated tasks:

- Switching branches
    
- Restoring files
    
- Checking out commits
    

This made it confusing for beginners.

Git introduced `git switch` to provide a dedicated command for changing branches.

---

# ⚙️ What Happens Internally?

Suppose your repository looks like this:

```text
A──B──C (main)
```

Create a branch:

```bash
git branch feature-login
```

Result:

```text
A──B──C
   ▲  ▲
   │  │
main feature-login
```

No files are copied.

No commits are created.

Git only creates another pointer.

---

Now switch:

```bash
git switch feature-login
```

HEAD changes:

```text
A──B──C
   ▲  ▲
   │  │
main feature-login
        ▲
        │
       HEAD
```

---

Create a new commit:

```text
A──B──C (main)
       \
        D (feature-login)
```

Only **feature-login** moves forward.

The **main** branch remains unchanged.

---

# ⚠️ Detached HEAD (Introduction)

Normally, HEAD points to a branch.

Example:

```text
HEAD → main
```

Sometimes developers checkout a specific commit:

```bash
git checkout a1b2c3d
```

Now HEAD points directly to a commit instead of a branch.

This is called a **Detached HEAD** state.

```text
A──B──C──D
      ▲
     HEAD
```

Detached HEAD is useful for inspecting old commits, but commits made in this state are not attached to any branch unless a new branch is created.

A dedicated chapter will cover this topic in more detail.

---

# 💡 Best Practices

- Use descriptive branch names.
    
- Create a new branch for each feature or bug fix.
    
- Switch branches only when your working directory is clean or your changes are committed/stashed.
    
- Prefer `git switch` for branch operations in modern Git.
    
- Keep branch names short, meaningful, and consistent.
    

Examples:

```text
feature/login
feature/payment

bugfix/navbar

hotfix/api-timeout

release/v2.0
```

---

# ⚠️ Common Mistakes

### ❌ Assuming `git branch` switches branches

It doesn't.

It only creates a new branch.

---

### ❌ Forgetting which branch you're on

Always check:

```bash
git branch
```

or

```bash
git status
```

---

### ❌ Creating branches with unclear names

Avoid names like:

```text
test

new

branch1

temp
```

Choose names that describe the purpose of the work.

---

# 📝 Summary

- `git branch` creates a new branch.
    
- Creating a branch does **not** switch to it.
    
- `git switch` changes your current branch.
    
- `git switch -c` creates and switches in one command.
    
- `git checkout` can also switch branches but has multiple responsibilities.
    
- Git branches are lightweight pointers, not copies of your project.
    

---

# 📚 Key Takeaways

- **Create:** `git branch <name>`
    
- **Switch:** `git switch <name>`
    
- **Create & Switch:** `git switch -c <name>`
    
- `git switch` is the recommended modern command for changing branches.
    
- Switching branches moves **HEAD** to the selected branch without copying the repository.