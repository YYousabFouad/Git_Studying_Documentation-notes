# Git File States: Delete, Untrack, and Unstage

---

# 1) Delete Files

## What does it do?

- Removes the file from your **working directory**.
- Removes the file from **Git**.
- After committing, the file disappears from the repository history going forward.

## Why is it important?

- Remove files you no longer need.
- Keep the repository clean.
- Avoid unnecessary files in future commits.

## Syntax Versions

### Delete a single file

```bash
git rm <file>
```

### Delete multiple files

```bash
git rm <file1> <file2> <file3>
```

### Delete all files matching a pattern

```bash
git rm *.log
git rm *.tmp
```

### Delete an entire directory

```bash
git rm -r <directory>
```

### Force delete (even if Git thinks it is unsafe)

```bash
git rm -f <file>
```

### Force delete a directory

```bash
git rm -rf <directory>
```

---

# 2) Untrack Files

## What does it do?

- Keeps the file on your computer.
- Removes the file from Git tracking.
- Usually followed by adding the file to `.gitignore`.

## Why is it important?

- Keep secrets out of GitHub (`.env`, API keys).
- Ignore generated files.
- Ignore personal configuration files.
- Reduce unnecessary changes.

## Syntax Versions

### Untrack one file

```bash
git rm --cached <file>
```

### Untrack multiple files

```bash
git rm --cached <file1> <file2>
```

### Untrack an entire directory

```bash
git rm --cached -r <directory>
```

### Untrack everything currently tracked (use carefully)

```bash
git rm --cached -r .
```

Then add your `.gitignore` rules and stage everything again:

```bash
git add .
```

---

# 3) Unstage Files

## What does it do?

- Removes files from the **staging area**.
- Keeps the file.
- Keeps all your changes.
- Only cancels the previous `git add`.

## Why is it important?

- Undo accidental `git add`.
- Choose exactly what will be committed.
- Keep your work without deleting it.

## Modern Syntax (Recommended)

### Unstage one file

```bash
git restore --staged <file>
```

### Unstage multiple files

```bash
git restore --staged <file1> <file2>
```

### Unstage every staged file

```bash
git restore --staged .
```

---

## Legacy Syntax (Older Git)

### Unstage one file

```bash
git reset HEAD <file>
```

### Unstage multiple files

```bash
git reset HEAD <file1> <file2>
```

### Unstage everything

```bash
git reset HEAD .
```

Or simply:

```bash
git reset
```

---

# Comparison Table

| Command                | File stays on computer | Git tracks it | Removed from staging | Recommended            |
| ---------------------- | ---------------------- | ------------- | -------------------- | ---------------------- |
| `git rm`               | ❌ No                  | ❌ No         | ✅ Yes               | Delete unwanted files  |
| `git rm --cached`      | ✅ Yes                 | ❌ No         | ❌ No                | Stop tracking files    |
| `git restore --staged` | ✅ Yes                 | ✅ Yes        | ✅ Yes               | Undo `git add`         |
| `git reset HEAD`       | ✅ Yes                 | ✅ Yes        | ✅ Yes               | Legacy unstage command |

---

# Workflow

```
Working Directory
        │
        │ git add
        ▼
Staging Area
        │
        │ git commit
        ▼
Repository
```

### Where each command works

```
Delete
Working Directory ───► ❌ File Removed

Untrack
Tracked File ───► File stays locally
             └──► Git stops tracking

Unstage
Staging Area ───► Working Directory
(changes stay, only staging is undone)
```

---

# Important Notes

### Delete

✔ Removes the actual file.

### Untrack

✔ Keeps the file locally.
✔ Best used with `.gitignore`.

### Unstage

✔ Never deletes your work.
✔ Only removes the file from the next commit.

---

# Key Takeaways

- **Delete (`git rm`)** → Remove the file completely.
- **Untrack (`git rm --cached`)** → Keep the file, stop Git from tracking it.
- **Unstage (`git restore --staged`)** → Undo `git add` without losing changes.
- Prefer **`git restore --staged`** for unstaging in modern Git, while **`git reset HEAD`** is mainly used for compatibility with older tutorials.

![[DeleteingVsUntrackingVsUnstaging.png]]