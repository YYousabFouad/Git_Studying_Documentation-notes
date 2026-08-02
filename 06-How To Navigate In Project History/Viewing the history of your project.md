# 📌 What is Project History?

Git stores the history of your project by saving a **snapshot** every time you create a **commit**.

Instead of saving the entire project repeatedly, Git remembers:

- Files that changed
- Lines that changed
- Author
- Date & time
- Commit message
- Relationship between commits

Think of it as a **timeline** of your project.

```
Initial Project
      │
      ▼

A ─── B ─── C ─── D ─── E
      ↑                 ↑
  README Added     Login Completed
```

Each circle = **Commit (Snapshot)**

---

# 📌 Why Navigate Project History?

Navigating history helps you:

- ✅ Review previous work
- ✅ Find when a bug was introduced
- ✅ Compare versions
- ✅ Recover lost work
- ✅ Understand how the project evolved
- ✅ Temporarily return to older versions

---

# 📌 Commit Hash

Every commit has a unique identifier called a **Commit Hash**.

Example

```
3f1c5a92b1d48c...
```

Usually, the first **7–8 characters** are enough.

Example

```
git show 3f1c5a9
```

Think of it like:

> 📌 A fingerprint for every commit.

---

# 📌 Viewing Project History

## 1️⃣ git log

Shows the complete commit history.

```
git log
```

Displays:

- Commit Hash
- Author
- Date
- Commit Message

Example

```
commit 1b2c3d4

Author: John

Date: Mon Aug 2

Added Authentication
```

---

## 2️⃣ git log --oneline

Shows a shorter version.

```
git log --oneline
```

Output

```
1b2c3d4 Added Login
5d6e7f8 Create Navbar
8a9b0c1 Initial Commit
```

✔ Easier to read.

---

## 3️⃣ git log --graph

Displays commits as a graph.

```
git log --graph
```

Better version

```
git log --oneline --graph --all
```

Example

```
* e5f6a7 (HEAD -> main)
* d4c3b2
|\
| * a1b2c3 (feature-login)
| *
* |
* |
```

Useful for understanding branches.

---

# 📌 Inspecting a Commit

## git show

Shows everything inside one commit.

```
git show <commit-hash>
```

Example

```
git show a1b2c3
```

Displays

- Commit information
- Author
- Date
- Message
- Changed files
- Added lines
- Deleted lines

Example

```
+ const user = "John";

- const user = "";
```

🟢 Green = Added

🔴 Red = Removed

---

# 📌 Comparing Versions

## git diff

Shows differences between versions.

### Compare Working Directory and Last Commit

```
git diff
```

---

### Compare Two Commits

```
git diff commit1 commit2
```

Example

```
git diff a1b2c3 d4e5f6
```

---

### Compare Two Branches

```
git diff main feature-login
```

Useful before merging branches.

---

# 📌 Moving Through History

## git checkout (Older Command)

Move to an old commit.

```
git checkout a1b2c3
```

Git changes your project files to exactly how they looked in that commit.

Example

Current

```
A ─── B ─── C ─── D ─── E
                    ↑
                  HEAD
```

After checkout

```
A ─── B ─── C ─── D ─── E
      ↑
    HEAD
```

⚠ Important

You did **NOT** delete commits C, D, or E.

You're only **visiting** an old snapshot.

---

# 📌 Detached HEAD

Normally

```
HEAD
 ↓
main
 ↓
A──B──C──D
```

After checking out a commit

```
HEAD
 ↓
A──B──C──D
    ↑
```

HEAD points directly to a commit instead of a branch.

This is called

> **Detached HEAD**

You can explore safely.

If you commit here, the commit won't belong to any branch unless you create one.

---

# 📌 Returning to the Latest Version

Return to your branch.

```
git switch main
```

Older Git

```
git checkout main
```

---

# 📌 HEAD

HEAD is a **pointer**.

It always tells Git:

> "This is where I am currently working."

Example

```
HEAD
 ↓
main
 ↓
A──B──C──D──E
```

When switching branches

HEAD moves.

When checking out a commit

HEAD points directly to that commit.

---

# 📌 Modern Way: git switch

Instead of

```
git checkout
```

Git introduced

```
git switch
```

Examples

```
git switch main
```

```
git switch feature-login
```

Cleaner and easier for switching branches.

---

# 📌 File History

Show history for one file.

```
git log app.js
```

Only commits affecting that file appear.

---

# 📌 Compare One File

```
git diff HEAD~1 app.js
```

Shows changes for a single file.

---

# 📌 git blame

Shows who modified each line.

```
git blame app.js
```

Example

```
3f1c5a9 John line 5

8d7f2c1 Mike line 12
```

Useful for debugging.

---

# 📌 git reflog

Git remembers every place HEAD has visited.

```
git reflog
```

Example

```
HEAD@{0}

HEAD@{1}

HEAD@{2}
```

Works even after:

- reset
- checkout
- switching branches

Think of it as:

> 📌 Git's browsing history.

---

# 📌 Typical Workflow

```
Project Problem
       │
       ▼
git log
       │
       ▼
Find Commit
       │
       ▼
git show
       │
       ▼
Inspect Changes
       │
       ▼
git diff
       │
       ▼
Compare Versions
       │
       ▼
git checkout <commit>
       │
       ▼
Test Old Version
       │
       ▼
git switch main
       │
       ▼
Continue Working
```

---

# 📌 Best Practices

✅ Write meaningful commit messages.

✅ Commit frequently.

✅ Use `git log --oneline` for daily work.

✅ Use `git show` to inspect commits.

✅ Use `git diff` before committing.

✅ Use `git switch` instead of `git checkout` for switching branches.

✅ Use `git reflog` if you think you've lost something.

---

# 📌 Commands Summary

|Command|Purpose|
|---|---|
|`git log`|Show complete commit history|
|`git log --oneline`|Compact history view|
|`git log --graph --all`|Visualize branches and commits|
|`git show <hash>`|Inspect a specific commit|
|`git diff`|Compare changes|
|`git diff A B`|Compare two commits|
|`git checkout <hash>`|Visit an old commit (Detached HEAD)|
|`git switch main`|Return to your branch|
|`git blame file`|See who changed each line|
|`git reflog`|View HEAD history and recover lost locations|

---

# 💡 Real-Life Analogy

Imagine your project is a **photo album**.

- 📸 **Commit** → A photo (snapshot)
- 📚 **git log** → Flip through the album
- 🔍 **git show** → Zoom into one photo
- 🆚 **git diff** → Compare two photos
- 🚶 **git checkout** → Travel back to an old moment
- 🧭 **git switch** → Return to the present
- 📝 **git reflog** → Your travel diary showing every place you've visited

---

# 🎯 Key Takeaways

- Git history is a timeline of snapshots (commits) that lets you explore, inspect, compare, and safely revisit previous versions of your project.
- Master these commands for history navigation:
    - `git log`
    - `git show`
    - `git diff`
    - `git checkout`
    - `git switch`
    - `git blame`
    - `git reflog`

![[NavigateYourProjectHistory.png]]