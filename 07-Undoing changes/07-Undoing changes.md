# ↩️ Undoing Changes in Git

> Learn how to safely undo changes in Git at every stage of the Git workflow.

---

# 📌 Git Workflow

Before learning the undo commands, remember the Git lifecycle:

```text
Working Directory
        │
        │ git add
        ▼
Staging Area (Index)
        │
        │ git commit
        ▼
Repository (Commit History)
```

Different commands undo changes at different stages.

---

# 1. Undo Changes in the Working Directory

## Scenario

You modified a file but **haven't staged it yet**.

```text
Working Directory
Modified File
```

### Command

```bash
git restore <file>
```

### Example

```bash
git restore README.md
```

### What happens?

Git discards all local modifications and restores the file to its latest committed version.

### Before

```text
README.md

Hello
Git
Oops... deleted everything!
```

### After

```text
README.md

Hello
Git
```

### Visual

```text
Repository
     │
     ▼
Working Directory (Modified)
        │
 git restore
        ▼
Working Directory (Original)
```

> **Warning**
>
> Uncommitted changes discarded with `git restore` cannot be recovered.

---

# 2. Unstage Files

## Scenario

You accidentally staged a file.

```bash
git add app.js
```

### Command

```bash
git restore --staged <file>
```

### Example

```bash
git restore --staged app.js
```

### Result

The file is removed from the staging area, but your code remains unchanged.

### Before

```text
Working Directory ✔ Modified
Staging Area     ✔ Modified
```

### After

```text
Working Directory ✔ Modified
Staging Area     ✖ Original
```

### Visual

```text
Working Directory
      │
      │ git add
      ▼
Staging Area
      │
      │ git restore --staged
      ▼
Working Directory
```

---

# 3. Discard Both Staged and Working Changes

### Command

```bash
git restore --source=HEAD --staged --worktree app.js
```

### Result

- Working Directory restored
- Staging Area restored

Everything returns to the latest commit.

---

# 4. Undo the Last Commit (Keep Changes Staged)

## Scenario

You committed too early.

### Before

```text
A → B → C (HEAD)
```

### Command

```bash
git reset --soft HEAD~1
```

### After

```text
A → B (HEAD)
```

The changes from commit **C** remain staged.

### Use Cases

- Wrong commit message
- Forgot to include another file
- Want to squash commits later

---

# 5. Undo the Last Commit (Keep Changes Unstaged)

### Command

```bash
git reset HEAD~1
```

or

```bash
git reset --mixed HEAD~1
```

### Result

```text
A → B (HEAD)
```

The commit disappears, but your changes stay in the Working Directory.

---

# 6. Undo the Last Commit Completely

> ⚠️ **Dangerous Command**

### Command

```bash
git reset --hard HEAD~1
```

### Before

```text
A → B → C
```

### After

```text
A → B
```

The commit and all associated changes are permanently removed.

> **Warning**
>
> Only use `git reset --hard` when you are absolutely sure you don't need those changes.

---

# 7. Undo Multiple Commits

### Before

```text
A → B → C → D (HEAD)
```

### Command

```bash
git reset --soft HEAD~2
```

### After

```text
A → B (HEAD)
```

Changes from commits **C** and **D** remain staged.

---

# 8. Revert a Commit (Safe for Shared Repositories)

Instead of deleting a commit, Git creates a new commit that reverses it.

### Command

```bash
git revert <commit-hash>
```

### Example

```bash
git revert a45b62f
```

### Before

```text
A → B → C
```

### After

```text
A → B → C → D

(D reverses C)
```

### Why use `git revert`?

- Safe for shared repositories
- Doesn't rewrite history
- Recommended after pushing commits

---

# 9. Restore a File From an Older Commit

### Command

```bash
git restore --source=<commit-hash> <file>
```

### Example

```bash
git restore --source=a45b62f README.md
```

Only the specified file is restored.

The commit history remains unchanged.

---

# 10. `git checkout` vs Modern Commands

Older Git tutorials often use:

```bash
git checkout
```

Modern Git splits responsibilities into two commands:

| Old Command | Modern Replacement |
|-------------|--------------------|
| `git checkout file` | `git restore file` |
| `git checkout branch` | `git switch branch` |

---

# Reset Modes Comparison

| Command | Working Directory | Staging Area | Commit History |
|----------|-------------------|--------------|----------------|
| `git reset --soft` | ✅ Keep | ✅ Keep | ❌ Moves HEAD |
| `git reset --mixed` | ✅ Keep | ❌ Reset | ❌ Moves HEAD |
| `git reset --hard` | ❌ Delete | ❌ Reset | ❌ Moves HEAD |

---

# Restore Commands Comparison

| Command | Purpose |
|----------|---------|
| `git restore file` | Discard local changes |
| `git restore --staged file` | Unstage a file |
| `git restore --source=<commit> file` | Restore file from a specific commit |
| `git restore --source=HEAD --staged --worktree file` | Reset both staging and working directory |

---

# Reset vs Restore vs Revert

| Command | Changes History? | Deletes Commits? | Safe After Push? | Main Purpose |
|----------|------------------|------------------|------------------|--------------|
| `git restore` | ❌ No | ❌ No | ✅ Yes | Undo file changes |
| `git reset` | ✅ Yes | ✅ Yes | ❌ Usually No | Rewrite local history |
| `git revert` | ✅ Adds a new commit | ❌ No | ✅ Yes | Undo pushed commits safely |

---

# Decision Tree

```text
Need to undo something?

│
├── Modified file only?
│      │
│      └── git restore <file>
│
├── Staged by mistake?
│      │
│      └── git restore --staged <file>
│
├── Wrong last commit?
│      │
│      ├── Keep staged
│      │      git reset --soft HEAD~1
│      │
│      ├── Keep unstaged
│      │      git reset HEAD~1
│      │
│      └── Delete everything
│             git reset --hard HEAD~1
│
└── Already pushed?
       │
       └── git revert <commit-hash>
```

---

# Best Practices

- ✅ Use `git restore` to discard local file changes.
- ✅ Use `git restore --staged` to unstage files without losing work.
- ✅ Use `git reset --soft` to redo commits.
- ✅ Use `git reset --mixed` to keep your changes but unstage them.
- ⚠️ Use `git reset --hard` only when you are certain you no longer need the changes.
- ✅ Use `git revert` for commits that have already been pushed.

---

# Quick Cheat Sheet

| Goal | Command |
|------|---------|
| Discard local changes | `git restore <file>` |
| Unstage a file | `git restore --staged <file>` |
| Reset staging and working directory | `git restore --source=HEAD --staged --worktree <file>` |
| Undo last commit (keep staged) | `git reset --soft HEAD~1` |
| Undo last commit (keep unstaged) | `git reset HEAD~1` |
| Undo last commit (delete changes) | `git reset --hard HEAD~1` |
| Undo multiple commits | `git reset --soft HEAD~n` |
| Safely undo a pushed commit | `git revert <commit-hash>` |
| Restore file from an old commit | `git restore --source=<commit-hash> <file>` |

---

# Summary

- **`git restore`** is used to undo changes to files in the Working Directory or Staging Area.
- **`git reset`** moves `HEAD` and can rewrite local history.
- **`git revert`** safely undoes a commit by creating a new commit, making it the preferred choice for shared repositories.
---

![[undoing_changes.png]]