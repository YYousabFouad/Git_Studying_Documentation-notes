# 🔗 Tracking Branches

## 📖 Introduction

In the previous chapter, you learned about:

- Local branches
    
- Remote branches
    
- Remote-tracking branches (`origin/main`)
    
- Commands such as `git fetch`, `git pull`, and `git push`
    

One important question remains:

> **How does Git know which remote branch your local branch should communicate with?**

The answer is **tracking branches**.

A tracking branch creates a relationship between a **local branch** and a **remote branch**, allowing Git to automatically determine where to push and pull changes.

---

# 🎯 Learning Objectives

After completing this chapter, you will be able to:

- Understand what a tracking branch is.
    
- Understand what an upstream branch is.
    
- Create tracking branches.
    
- View tracking information.
    
- Change an upstream branch.
    
- Remove an upstream branch.
    
- Understand how Git automatically chooses where to push and pull.
    

---

# 🤔 What Is a Tracking Branch?

A **tracking branch** is a local branch that is associated with a specific branch on a remote repository.

Once this relationship exists, Git knows:

- Which branch to pull from.
    
- Which branch to push to.
    
- Which remote branch to compare against.
    

For example:

```text
Local Branch
feature-login
      │
      │ tracks
      ▼
origin/feature-login
```

This relationship is called the **upstream relationship**.

---

# 🌍 What Is an Upstream Branch?

An **upstream branch** is simply the remote branch that your local branch tracks.

Example:

```text
Local Branch
feature-login
      │
      ▼
origin/feature-login
```

Here:

- Local branch → `feature-login`
    
- Upstream branch → `origin/feature-login`
    

Whenever you run:

```bash
git pull
```

Git automatically pulls from:

```text
origin/feature-login
```

Likewise,

```bash
git push
```

automatically pushes to:

```text
origin/feature-login
```

---

# 📊 Without a Tracking Branch

Suppose you create a new branch:

```bash
git switch -c feature-login
```

Repository:

```text
Local

main

feature-login
```

The branch exists only locally.

If you run:

```bash
git push
```

Git responds with an error because it doesn't know where to push.

Example:

```text
fatal: The current branch feature-login has no upstream branch.
```

Git needs you to establish the relationship first.

---

# 🚀 Creating a Tracking Branch

The most common way is:

```bash
git push -u origin feature-login
```

The `-u` option means:

> **Set the upstream branch for this local branch.**

After running the command:

```text
feature-login
      │
      ▼
origin/feature-login
```

The relationship is now stored in your Git configuration.

From this point on, you can simply use:

```bash
git push
```

and

```bash
git pull
```

without specifying the remote or branch name.

---

# 🔍 Viewing Tracking Information

To display upstream information:

```bash
git branch -vv
```

Example output:

```text
* feature-login  3fa8b2d [origin/feature-login] Add login page
  main           9dc21ab [origin/main] Initial commit
```

The information inside the square brackets shows the upstream branch.

---

# ⚙️ Setting an Upstream Branch Manually

If the upstream relationship does not exist or needs to be changed:

```bash
git branch --set-upstream-to=origin/feature-login
```

You can also specify both branches:

```bash
git branch --set-upstream-to=origin/feature-login feature-login
```

Git now associates the local branch with the specified remote branch.

---

# ❌ Removing an Upstream Branch

To remove the tracking relationship:

```bash
git branch --unset-upstream
```

After removing it:

- `git push`
    
- `git pull`
    

will no longer know which remote branch to use automatically.

---

# 🔄 Changing the Upstream Branch

Suppose your local branch currently tracks:

```text
origin/develop
```

but you want it to track:

```text
origin/main
```

Run:

```bash
git branch --set-upstream-to=origin/main
```

Git updates the tracking relationship without changing your commits.

---

# 📊 How Tracking Works

```text
Local Repository

feature-login
      │
      │
      ▼
origin/feature-login
      │
      ▼
Remote Repository
feature-login
```

Notice the flow:

- Your local branch communicates with its **remote-tracking branch**.
    
- The remote-tracking branch represents the corresponding branch on the remote repository.
    

---

# 💡 Why Tracking Branches Are Useful

Tracking branches simplify your workflow.

Instead of typing:

```bash
git push origin feature-login
```

every time,

you can simply write:

```bash
git push
```

The same applies to:

```bash
git pull
```

Git remembers the destination automatically.

---

# ⚠️ Common Mistakes

## ❌ Forgetting to Set an Upstream Branch

Creating a local branch does **not** automatically establish a tracking relationship.

Remember to use:

```bash
git push -u origin <branch-name>
```

the first time you push the branch.

---

## ❌ Confusing `origin/main` with the Upstream Branch

`origin/main` is a **remote-tracking branch** stored in your local repository.

The **upstream branch** is the relationship between your local branch and a remote branch.

They are related concepts, but they are not the same thing.

---

## ❌ Changing the Wrong Upstream Branch

Always verify the current tracking information:

```bash
git branch -vv
```

before changing upstream settings.

---

# 💡 Best Practices

- Use `git push -u` when pushing a branch for the first time.
    
- Check tracking information regularly with `git branch -vv`.
    
- Use descriptive branch names.
    
- Keep tracking relationships simple and consistent.
    
- Avoid changing upstream branches unless necessary.
    

---

# 📋 Useful Commands

|Command|Description|
|---|---|
|`git push -u origin <branch>`|Push a branch and set its upstream|
|`git branch -vv`|View tracking information|
|`git branch --set-upstream-to=<remote>/<branch>`|Change the upstream branch|
|`git branch --unset-upstream`|Remove the upstream relationship|

---

# 🚀 Complete Tracking Workflow

```text
Create Local Branch
        │
        ▼
Make Commits
        │
        ▼
git push -u origin feature-login
        │
        ▼
Tracking Relationship Created
        │
        ▼
git push
        │
        ▼
git pull
        │
        ▼
Git Automatically Knows
Where to Push and Pull ✅
```

---

# 📊 Tracking Branch vs Remote-Tracking Branch

These two terms sound similar, but they describe different things.

|Tracking Branch|Remote-Tracking Branch|
|---|---|
|A local branch that has an upstream relationship with a remote branch.|A local reference (such as `origin/main`) that stores Git's last known state of a remote branch.|
|Represents a relationship.|Represents a snapshot of a remote branch.|
|Used by `git push` and `git pull` to determine the default destination.|Updated by `git fetch` to reflect changes on the remote repository.|

Understanding this distinction makes Git's behavior much easier to predict.

---

# ⚙️ What Happens Internally?

To understand how Git synchronizes your work with a remote repository, let's look at what happens behind the scenes.

Suppose your repository contains the following:

```text
Local Repository

feature-login
      │
      ▼
origin/feature-login
      │
      ▼
Remote Repository (GitHub)

feature-login
```

Although these names are similar, each one has a different purpose.

- **`feature-login`** is your local branch where you make commits.
    
- **`origin/feature-login`** is your local remote-tracking branch. It stores Git's last known state of the remote branch.
    
- **`feature-login` on GitHub** is the actual branch stored on the remote repository.
    

Git keeps these three references synchronized using different commands.

---

## 📥 What Happens During `git fetch`

When you run:

```bash
git fetch
```

Git contacts the remote repository and downloads the latest information.

If another developer has pushed new commits, Git updates the corresponding **remote-tracking branch**.

Example:

Before fetching:

```text
Local Repository

feature-login
      │
      ▼
A──B──C

origin/feature-login
      │
      ▼
A──B──C

Remote Repository

A──B──C──D
```

After fetching:

```text
Local Repository

feature-login
      │
      ▼
A──B──C

origin/feature-login
      │
      ▼
A──B──C──D

Remote Repository

A──B──C──D
```

Notice that:

- Your **local branch did not change**.
    
- Only the **remote-tracking branch** was updated.
    

This is why `git fetch` is considered a safe operation.

---

## 📤 What Happens During `git push`

When you run:

```bash
git push
```

Git sends commits from your **local branch** to the corresponding branch on the remote repository.

Example:

Before pushing:

```text
Local Repository

feature-login
      │
      ▼
A──B──C──D

Remote Repository

A──B──C
```

After pushing:

```text
Local Repository

feature-login
      │
      ▼
A──B──C──D

Remote Repository

A──B──C──D
```

After a successful `git push`, Git updates your local remote-tracking branch to reflect the new state of the remote branch. If another developer pushes changes, you'll need to run `git fetch` (or `git pull`) to update your remote-tracking branch.

---

## 🔄 What Happens During `git pull`

When you run:

```bash
git pull
```

Git performs two operations:

1. Downloads the latest changes from the remote repository (`git fetch`).
    
2. Integrates those changes into your current local branch (usually with a merge, or a rebase if configured).
    

Example:

Before pulling:

```text
Local Repository

feature-login
      │
      ▼
A──B──C

origin/feature-login
      │
      ▼
A──B──C

Remote Repository

A──B──C──D
```

After pulling:

```text
Local Repository

feature-login
      │
      ▼
A──B──C──D

origin/feature-login
      │
      ▼
A──B──C──D

Remote Repository

A──B──C──D
```

All three references are synchronized again.

---

# 📊 Internal Synchronization Flow

```text
                Remote Repository
             feature-login
                    ▲
                    │
                git push
                    │
                    │
Local Branch ───────┘
feature-login
      │
      │
git pull
      │
      ▼
origin/feature-login
(Remote-Tracking Branch)
      ▲
      │
  git fetch
      │
      └────────────── Remote Repository
```

---

# 💡 Key Idea

Think of Git synchronization as a conversation between three different references:

- Your **local branch**, where you make changes.
    
- Your **remote-tracking branch**, which remembers the last known state of the remote branch.
    
- The **actual remote branch** stored on GitHub.
    

Each Git command updates a different part of this relationship:

|Command|What It Updates|
|---|---|
|`git fetch`|Updates the remote-tracking branch (`origin/feature-login`)|
|`git push`|Updates the remote branch on GitHub|
|`git pull`|Updates both the remote-tracking branch and your local branch by fetching and integrating changes|

Understanding these relationships makes Git's behavior much easier to predict and helps explain why commands like `git push` and `git pull` work automatically after an upstream branch has been configured.

---

# 📝 Summary

Tracking branches allow Git to automatically associate a local branch with a remote branch. Once the upstream relationship is established, commands like `git push` and `git pull` no longer require you to specify the remote repository or branch name each time. This simplifies everyday workflows and makes collaboration more efficient.

---

# 📚 Key Takeaways

- A **tracking branch** is a local branch associated with a specific remote branch.
    
- The associated remote branch is called the **upstream branch**.
    
- Use `git push -u origin <branch>` to create the tracking relationship.
    
- View tracking information with `git branch -vv`.
    
- Remove the relationship with `git branch --unset-upstream`.
    
- Tracking branches and remote-tracking branches are related, but they are **not the same thing**.