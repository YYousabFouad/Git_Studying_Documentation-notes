# 🌿 Rebasing

## 📖 Introduction

As multiple developers work on different branches, the project's history begins to diverge. Eventually, those branches need to be synchronized.

Git provides two primary ways to combine work from different branches:

- **Merge**
    
- **Rebase**
    

While a merge combines histories by creating a merge commit, a **rebase** rewrites a branch's history by moving its commits to a new base commit.

The result is a cleaner, more linear commit history.

> **Important:** Rebasing changes commit history. Because of this, it should be used with care, especially on branches that have already been shared with others.

---

# 🎯 Learning Objectives

After completing this chapter, you will be able to:

- Understand what rebasing is.
    
- Learn how rebasing works internally.
    
- Rebase one branch onto another.
    
- Understand the difference between Merge and Rebase.
    
- Resolve conflicts during a rebase.
    
- Learn when rebasing is appropriate.
    
- Understand the basics of Interactive Rebase.
    

---

# 🤔 What Is Rebasing?

A **rebase** moves or reapplies the commits from one branch onto another base commit.

Instead of combining histories with a merge commit, Git **replays your commits** one by one on top of another branch.

This creates a cleaner and more linear project history.

---

# 🌍 Real-World Example

Imagine you're writing a report based on version 1 of a document.

Before you finish, the original document is updated to version 2.

Instead of combining two separate reports, you copy your changes and apply them to the latest version of the document.

That's essentially what Git does during a rebase.

---

# 📊 Example Repository

Initial history:

```text
A──B──C (main)
      \
       D──E (feature-login)
```

While you're working, someone adds another commit to `main`:

```text
A──B──C──F (main)
      \
       D──E (feature-login)
```

Your branch is now behind `main`.

---

# 🔄 Rebasing the Branch

Switch to your feature branch:

```bash
git switch feature-login
```

Run:

```bash
git rebase main
```

Git performs these steps:

1. Temporarily saves commits `D` and `E`.
    
2. Moves the branch to commit `F`.
    
3. Replays `D`.
    
4. Replays `E`.
    

Result:

```text
A──B──C──F (main)
            \
             D'──E' (feature-login)
```

Notice the apostrophes (`'`).

These are **new commits**, not the original ones.

Git recreated them on top of the latest version of `main`.

---

# ⚙️ How Rebasing Works Internally

When Git rebases a branch, it does **not** move the existing commits.

Instead, it:

- Finds the common ancestor.
    
- Saves your branch's commits.
    
- Moves your branch pointer.
    
- Recreates each commit one at a time.
    
- Updates the branch pointer to the new commits.
    

This process is why rebasing **rewrites commit history**.

---

# 🔀 Merge vs Rebase

Suppose the history looks like this:

```text
A──B──C──F (main)
      \
       D──E (feature-login)
```

## Using Merge

```bash
git switch main
git merge feature-login
```

Result:

```text
A──B──C──F────────M
      \          /
       D────────E
```

Git creates a **merge commit** (`M`) that preserves the original branch structure.

---

## Using Rebase

```bash
git switch feature-login
git rebase main
```

Result:

```text
A──B──C──F──D'──E'
```

The history becomes linear.

No merge commit is created during the rebase itself.

If you later merge this rebased branch into `main` and `main` has not advanced, Git can usually perform a **Fast-Forward Merge**.

---

# 📊 Merge vs Rebase Comparison

|Feature|Merge|Rebase|
|---|---|---|
|Creates a merge commit|✅ Usually|❌ No|
|Preserves original history|✅ Yes|❌ No|
|Rewrites commit history|❌ No|✅ Yes|
|Produces linear history|❌ Not always|✅ Yes|
|Safer for shared branches|✅ Yes|❌ No|

---

# ⚠️ Rebase Conflicts

Rebasing may produce conflicts, just like merging.

If Git cannot replay a commit automatically, it pauses the rebase.

Example:

```text
CONFLICT (content): Merge conflict in app.js
```

Resolve the conflict.

Then continue:

```bash
git rebase --continue
```

If another conflict occurs, repeat the process.

---

# 🛑 Aborting a Rebase

If you no longer want to continue the rebase:

```bash
git rebase --abort
```

Git restores your branch to its state before the rebase began.

---

# ⏭️ Skipping a Commit

Occasionally you may decide not to replay the commit that caused the conflict.

```bash
git rebase --skip
```

Git skips the current commit and continues with the remaining commits.

> **Warning:** Skipping a commit permanently omits that commit from the rebased branch. Use this command only if you intentionally want to discard the changes introduced by that commit.

---

# ✨ Interactive Rebase

Interactive Rebase allows you to edit commit history before sharing it.

Start an interactive rebase:

```bash
git rebase -i HEAD~3
```

This opens an editor showing the last three commits.

You can:

- Reorder commits.
    
- Edit commit messages.
    
- Combine multiple commits.
    
- Remove unnecessary commits.
    

Interactive Rebase is commonly used to clean up a branch before opening a Pull Request.

---

# ⚠️ When Should You Use Rebase?

Rebasing is a good choice when:

- Updating a feature branch with the latest changes from `main`.
    
- Cleaning up your commit history.
    
- Preparing a branch before merging.
    
- Working on your own local branch.
    

---

# 🚫 When Should You Avoid Rebase?

Avoid rebasing when:

- The branch has already been pushed and shared with other developers.
    
- Other developers may have based work on your commits.
    
- Preserving the exact historical record is important.
    

Because rebasing creates new commits, anyone who has the old commits will need to reconcile the rewritten history.

---

# 💡 Best Practices

- Rebase **before** opening a Pull Request if your team prefers a linear history.
    
- Keep feature branches short-lived.
    
- Test your project after a rebase.
    
- Resolve conflicts carefully.
    
- Communicate with your team before rebasing shared branches.
    

---

# ⚠️ Common Mistakes

### ❌ Rebasing the wrong branch

Always check your current branch before starting a rebase.

---

### ❌ Rebasing shared branches

Rewriting public history can create confusion for other developers.

---

### ❌ Ignoring conflicts

Resolve every conflict carefully before continuing.

---

### ❌ Assuming rebasing modifies existing commits

Rebase creates **new commits** with new commit IDs.

---

# 📋 Useful Commands

|Command|Description|
|---|---|
|`git rebase main`|Rebase the current branch onto `main`|
|`git rebase -i HEAD~3`|Start an interactive rebase for the last three commits|
|`git rebase --continue`|Continue after resolving a conflict|
|`git rebase --abort`|Cancel the rebase|
|`git rebase --skip`|Skip the current commit during a rebase|


---
# 🚀 Complete Rebase Workflow Example

The following example demonstrates a typical development workflow using **Git Rebase**.

---

## Step 1: Create a Feature Branch

Start from the latest version of the `main` branch.

```bash
git switch main
git switch -c feature-login
```

Repository:

```text
A──B──C (main, feature-login)
```

At this point, both branches point to the same commit.

---

## Step 2: Work on the Feature

Make changes and create a few commits.

```bash
git add .
git commit -m "Add login page"

git add .
git commit -m "Connect login API"
```

Repository:

```text
A──B──C (main)
        \
         D──E (feature-login)
```

Your feature branch now contains two commits that do not exist on `main`.

---

## Step 3: Another Developer Updates `main`

While you're still working, another developer pushes new commits to the `main` branch.

Repository:

```text
A──B──C──F──G (main)
        \
         D──E (feature-login)
```

Your feature branch is now **behind** `main`.

If you open a Pull Request now, Git may report that your branch is out of date.

---

## Step 4: Rebase onto `main`

Switch to your feature branch if you're not already on it.

```bash
git switch feature-login
```

Start the rebase:

```bash
git rebase main
```

Git temporarily removes commits `D` and `E`, moves the branch to commit `G`, and then reapplies your commits one by one.

Result:

```text
A──B──C──F──G (main)
              \
               D'──E' (feature-login)
```

Notice that `D'` and `E'` are **new commits**.

Although they contain the same changes, they have different commit hashes because Git recreated them.

---

## Step 5: Resolve Conflicts (If Necessary)

If Git encounters conflicting changes while replaying a commit, it pauses the rebase.

Example message:

```text
CONFLICT (content): Merge conflict in app.js
```

Resolve the conflict in your editor.

After resolving it, stage the file:

```bash
git add app.js
```

Then continue the rebase:

```bash
git rebase --continue
```

If another conflict occurs, repeat the same process.

---

## Step 6: Complete the Rebase

Once every commit has been replayed successfully, Git reports that the rebase has finished.

Your history is now linear.

```text
A──B──C──F──G──D'──E'
```

Notice there is **no merge commit**.

Your feature branch now appears as though it was created from the latest version of `main`.

---

## Step 7: Merge the Rebased Branch

Switch back to the `main` branch.

```bash
git switch main
```

Merge the rebased feature branch.

```bash
git merge feature-login
```

Because `main` has not advanced since the rebase, Git can usually perform a **Fast-Forward Merge**.

Final history:

```text
A──B──C──F──G──D'──E' (main)
```

No additional merge commit is created.

The project history remains clean and linear.

---

# 📊 Complete Rebase Workflow

```text
Create Feature Branch
        │
        ▼
Make Commits
        │
        ▼
main Receives New Commits
        │
        ▼
git rebase main
        │
        ▼
Resolve Conflicts (if any)
        │
        ▼
git rebase --continue
        │
        ▼
Feature Branch Updated
        │
        ▼
git merge feature-login
        │
        ▼
Fast-Forward Merge
        │
        ▼
Linear Git History ✅
```

---

# 💡 Why Many Teams Prefer This Workflow

Using a rebase before merging offers several advantages:

- Produces a clean, easy-to-read commit history.
    
- Reduces unnecessary merge commits.
    
- Makes `git log` easier to follow.
    
- Simplifies debugging by presenting commits in chronological order.
    
- Keeps feature branches up to date with the latest changes from `main`.
    

---

# ⚠️ Important Reminder

Although rebasing creates a cleaner history, it **rewrites commits**.

For this reason, follow one simple rule:

> **Rebase local branches that only you are working on.**
> 
> **Avoid rebasing branches that have already been shared with other developers unless your team has agreed on that workflow.**

Following this guideline helps prevent unnecessary conflicts and confusion when collaborating with others.

---

# 📚 Key Takeaways

- A typical rebase workflow is:
    
    1. Create a feature branch.
        
    2. Make commits.
        
    3. Update the feature branch with `git rebase main`.
        
    4. Resolve conflicts if they occur.
        
    5. Merge the rebased branch.
        
- Rebasing creates **new commits** with new commit hashes.
    
- A successful rebase often allows Git to perform a **Fast-Forward Merge**, resulting in a clean, linear project history.


---

# 📝 Summary

Rebasing is a powerful Git operation that creates a clean, linear commit history by replaying commits on top of a new base. Unlike merging, rebasing rewrites commit history, making it ideal for updating local feature branches and preparing them for integration. However, because it changes commit identities, it should be avoided on branches that have already been shared with others.

---

# 📚 Key Takeaways

- A **rebase** replays commits on top of a new base commit.
    
- Rebasing rewrites commit history by creating new commits.
    
- A rebased branch often leads to a cleaner, linear history.
    
- Resolve conflicts with `git rebase --continue`.
    
- Cancel a rebase with `git rebase --abort`.
    
- Avoid rebasing branches that have already been shared with other developers.