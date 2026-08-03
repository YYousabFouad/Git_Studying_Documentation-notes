# 🌿 Merging Branches

## 📖 Introduction

Creating branches allows developers to work independently, but those changes eventually need to become part of the main project.

This is where **merging** comes in.

A merge combines the history of one branch into another, allowing completed work to become part of the target branch while preserving Git's commit history.

Merging is one of the most common Git operations and is used daily in both personal and collaborative projects.

---

# 🎯 Learning Objectives

After completing this chapter, you will be able to:

- Understand what a merge is.
    
- Learn why merging is necessary.
    
- Merge one branch into another.
    
- Understand how Git performs a merge.
    
- Recognize different merge types.
    
- Read merge history.
    
- Apply merge best practices.
    

---

# 🤔 What Is a Merge?

A **merge** combines the changes from one branch into another.

Imagine you created a branch to build a login feature.

```text
main
  │
  └── feature-login
```

After finishing the feature, you want the login system to become part of your application.

Instead of copying files manually, Git combines the histories for you.

This process is called **merging**.

---

# 🌍 Real-World Example

Imagine a team writing a book.

- One author edits Chapter 1.
    
- Another edits Chapter 2.
    
- A third corrects spelling mistakes.
    

Everyone works independently.

When everyone finishes, the editor combines all approved changes into the final book.

Git merges branches in the same way.

---

# 🔀 Basic Merge Workflow

The general workflow is:

1. Create a branch.
    
2. Make changes.
    
3. Commit your work.
    
4. Switch to the destination branch.
    
5. Merge the feature branch.
    

Example:

```bash
git switch main
git merge feature-login
```

Git attempts to combine the commits from `feature-login` into `main`.

---

# 📊 Visual Example

Before merging:

```text
A──B──C  (main)
      \
       D──E  (feature-login)
```

Current branch:

```text
HEAD → main
```

Run:

```bash
git merge feature-login
```

After merging:

```text
A──B──C────────M  (main)
      \        /
       D──────E  (feature-login)
```

`M` is called a **merge commit**.

It combines the histories of both branches.

---

# ⚙️ How Git Performs a Merge

When you run:

```bash
git merge feature-login
```

Git performs several steps:

1. Finds the common ancestor of both branches.
    
2. Compares the changes made since that commit.
    
3. Combines the changes automatically whenever possible.
    
4. Creates a merge commit if necessary.
    

If Git cannot combine the changes automatically, a **merge conflict** occurs.

Merge conflicts are covered in the next chapter.

---

# 🌳 The Three Commits Git Uses

Git performs a **three-way merge**.

Suppose the history is:

```text
        D──E
       /
A──B──C
```

Git compares:

- Common ancestor (**C**)
    
- Current branch
    
- Branch being merged
    

Using these three commits, Git determines how to combine the changes.

This is why Git can merge branches intelligently instead of simply replacing files.

---

# 🧠 Merge Direction Matters

A common misconception is that Git merges _into_ the branch you specify.

This is **not** how `git merge` works.

The branch you are **currently on** receives the changes.

Example:

```bash
git switch main
git merge feature-login
```

Result:

- `main` receives the commits.
    
- `feature-login` does not change.
    

Think of it as:

```text
Current Branch
      ▲
      │
Receive Changes
```

Always verify your current branch before running a merge.

---

# 📋 Checking the Current Branch

Before merging:

```bash
git branch
```

or

```bash
git status
```

Confirm that you are on the correct destination branch.

---

# 🌟 Fast-Forward Merge

Sometimes Git does **not** need a merge commit.

Example:

```text
A──B──C (main)
         \
          D──E (feature)
```

If `main` has not changed since the branch was created, Git simply moves the `main` pointer forward.

Result:

```text
A──B──C──D──E (main)
```

This is called a **Fast-Forward Merge**.

No extra merge commit is created.

A dedicated chapter explains Fast-Forward Merges in detail.

---

# 🌟 Three-Way Merge

If both branches have new commits:

```text
A──B──C──F (main)
      \
       D──E (feature)
```

Git cannot simply move the pointer.

Instead, it creates a merge commit.

```text
A──B──C──F────M
      \      /
       D────E
```

This is the most common merge type in collaborative projects.

---

# 💡 Advantages of Merging

- Combines completed work safely.
    
- Preserves project history.
    
- Supports team collaboration.
    
- Keeps feature development isolated.
    
- Allows multiple developers to work simultaneously.
    
- Records when different lines of development were combined.
    

---

# ⚠️ Common Mistakes

### ❌ Merging into the wrong branch

Always switch to the destination branch first.

Incorrect:

```bash
git merge main
```

while on the feature branch.

Always verify your current branch.

---

### ❌ Merging unfinished work

Only merge branches that have been tested and reviewed.

---

### ❌ Deleting branches before merging

Deleting a branch before merging may make recent work harder to access.

Merge first.

Delete later.

---

### ❌ Ignoring merge conflicts

Never skip conflict resolution.

Carefully review every conflicting change before completing the merge.

---

# 💡 Best Practices

- Merge completed features only.
    
- Keep feature branches small.
    
- Pull the latest changes before merging.
    
- Test your project after every merge.
    
- Delete merged branches to keep the repository clean.
    
- Write meaningful commit messages before merging.
    

---

# 📋 Command Summary

|Command|Description|
|---|---|
|`git merge <branch>`|Merge the specified branch into the current branch|
|`git branch`|View the current branch|
|`git status`|Check repository status before merging|

---

# 📝 Summary

A merge combines the history of two branches into one. Git automatically compares the commit histories, determines what has changed, and combines those changes whenever possible. Depending on the commit history, Git may perform a Fast-Forward Merge or create a Merge Commit through a Three-Way Merge.

Understanding how merges work is essential before learning about merge conflicts, rebasing, and collaborative workflows.

---

# 📚 Key Takeaways

- A **merge** combines one branch into another.
    
- The **current branch** always receives the changes.
    
- Git compares commit history rather than simply copying files.
    
- Git performs either a **Fast-Forward Merge** or a **Three-Way Merge** depending on the branch history.
    
- Merge conflicts occur only when Git cannot combine changes automatically.