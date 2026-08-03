# 🚫 .gitignore in Git

## 📌 What is `.gitignore`?

A `.gitignore` file is a special text file that tells **Git which files  
or folders should NOT be tracked**.

Think of it as a **"Do Not Save" list** for your Git repository.

Without a `.gitignore` file, Git will try to track every file that you  
add to the staging area.

---

## 🧠 Simple Example

Imagine your project contains:

```
my-project/
│
├── src/
│   └── app.js
│
├── package.json
├── package-lock.json
├── node_modules/
├── .env
└── README.md
```

Some files are important:

- ✅ Source code
- ✅ README
- ✅ `package.json`

Some files should **NOT** be uploaded:

- ❌ `node_modules/`
- ❌ `.env`
- ❌ Temporary files

Instead of manually ignoring them every time, create a `.gitignore`  
file.

```
my-project/
│
├── .gitignore
```

Example:

```
node_modules/
.env
```

Now Git simply ignores those files and folders.

---

# 🎯 Why Is `.gitignore` Important?

Many files **do not belong** in a Git repository.

Examples include:

- Generated files
- Temporary files
- Cache files
- Build output
- Personal IDE settings
- Secret credentials

These files usually:

- Can be recreated automatically
- Are different on every computer
- Make the repository much larger
- May expose sensitive information

Using `.gitignore` keeps your repository:

- ✅ Clean
- ✅ Secure
- ✅ Smaller
- ✅ Easier to collaborate on

---

# ❌ Problems Without `.gitignore`

Imagine you install project dependencies:

```
npm install
```

This creates:

```
node_modules/
```

That folder can contain:

```
100,000+ files
```

If you commit them:

- Repository becomes huge
- Uploads become slower
- Cloning takes longer
- Git history becomes noisy

Instead, Git should only track:

```
package.json
package-lock.json
```

Every developer can recreate the dependencies by running:

```
npm install
```

---

# ⚙️ How Git Uses `.gitignore`

Whenever Git scans your project, it asks:

```
Should I track this file?
```

If the file matches a rule inside `.gitignore`:

```
Git ignores it.
```

Example:

```
Project
│
├── app.js          ✅ Track
├── README.md       ✅ Track
├── node_modules/   ❌ Ignore
├── .env            ❌ Ignore
└── build/          ❌ Ignore
```

---

# 📝 How to Create a `.gitignore`

Create a file named exactly:

```
.gitignore
```

Notice:

- Starts with a dot (`.`)
- Has no filename before the dot
- Has no file extension

✅ Correct

```
.gitignore
```

❌ Wrong

```
gitignore
.gitignore.txt
ignore.git
```

---
## 📚 Useful Resources

### Official GitHub `.gitignore` Templates

GitHub provides an official repository that contains a collection of useful `.gitignore` templates for different programming languages, frameworks, IDEs, and operating systems.

- **GitHub gitignore Templates:** https://github.com/github/gitignore
---
# 📚 Basic Syntax

## Ignore a single file

```
.env
```

---

## Ignore a folder

```
node_modules/
```

---

## Ignore multiple folders

```
node_modules/
dist/
build/
coverage/
```

---

## Ignore all files with a specific extension

```
*.log
```

Git ignores:

```
server.log
debug.log
app.log
```

---

## Ignore temporary files

```
*.tmp
```

---

# 📂 Ignore an Entire Directory

```
build/
```

Everything inside that folder will be ignored.

```
build/
├── index.html
├── style.css
└── main.js
```

---

# 📁 Ignore a Nested Folder

```
src/temp/
```

Only that folder is ignored.

---

# 📄 Ignore All Files Inside a Folder

```
images/*
```

Ignored:

```
images/a.png
images/b.png
images/c.png
```

---

# 🔒 Ignore Environment Files

Ignore a single environment file:

```
.env
```

Ignore every environment file:

```
.env*
```

Matches:

```
.env
.env.local
.env.production
.env.test
```

---

# ⭐ Wildcards

## `*` (Any Characters)

```
*.log
```

Matches:

```
app.log
server.log
test.log
```

---

## `?` (Exactly One Character)

```
file?.txt
```

Matches:

```
file1.txt
fileA.txt
```

Does **NOT** match:

```
file10.txt
```

---

# 🚀 Negation (`!`)

Sometimes you want to ignore everything except one file.

```
*.log
!important.log
```

Ignored:

```
app.log
```

Tracked:

```
important.log
```

---

# 🌍 Common `.gitignore` for Node.js

```
# Dependencies
node_modules/

# Environment Variables
.env

# Logs
*.log

# Build Output
dist/
build/

# Coverage Reports
coverage/

# IDE Settings
.vscode/
.idea/

# OS Files
.DS_Store
Thumbs.db
```

---

# 🐍 Common `.gitignore` for Python

```
__pycache__/
*.pyc
.env
venv/
```

---

# ☕ Common `.gitignore` for Java

```
target/
*.class
```

---

# ⚙️ Common `.gitignore` for C/C++

```
*.o
*.exe
build/
```

---

# ⚛️ Common `.gitignore` for React

```
node_modules/
.env
build/
coverage/
```

---

# ❓ Does `.gitignore` Delete Files?

**No.**

It only tells Git **not to track them**.

Your files remain safely on your computer.

```
Git Ignore
      │
      ▼
File Still Exists
      │
      ▼
Git Doesn't Track It
```

---

# ⚠️ Important Rule

`.gitignore` only affects **untracked files**.

Example:

```
git add .env
git commit -m "Add environment file"
```

Now `.env` is already tracked.

Later you add:

```
.env
```

Git **will continue tracking it** because it was already committed.

---

# 🛠 Stop Tracking an Already Tracked File

Keep the file on your computer but remove it from Git's tracking.

```
git rm --cached .env
```

Then commit the change:

```
git commit -m "Stop tracking .env"
```

Now `.gitignore` will work correctly.

---

# 🔍 Check Ignored Files

To see ignored files:

```
git status --ignored
```

This is useful when testing your `.gitignore` rules.

---

# 🌐 Global `.gitignore`

You can create one global ignore file for **all repositories** on your  
computer.

Useful for:

- `.DS_Store`
- `Thumbs.db`
- `.vscode/`
- `.idea/`

Configure it:

```
git config --global core.excludesfile ~/.gitignore_global
```

Then create:

```
~/.gitignore_global
```

---

# ✅ Best Practices

- Ignore dependencies like `node_modules/`
- Ignore secret files like `.env`
- Ignore build folders (`dist/`, `build/`)
- Ignore cache files
- Ignore temporary files
- Ignore IDE-specific settings when appropriate
- Always commit the `.gitignore` file itself

---

# ❌ Common Mistakes

### Committing `.env`

May expose passwords, API keys, and secrets.

---

### Committing `node_modules`

Makes the repository unnecessarily large.

---

### Forgetting `.gitignore`

Leads to accidental commits of generated files.

---

### Expecting `.gitignore` to Untrack Files

`.gitignore` does **not** stop tracking files that were already  
committed.

Use:

```
git rm --cached <file>
```

first.

---

# 💼 Real Project Example

```
blog-api/
│
├── src/
├── package.json
├── package-lock.json
├── node_modules/
├── .env
├── dist/
├── README.md
└── .gitignore
```

`.gitignore`

```
node_modules/
.env
dist/
coverage/
*.log
.vscode/
```

Git tracks:

- ✅ src/
- ✅ package.json
- ✅ package-lock.json
- ✅ README.md
- ✅ .gitignore

Git ignores:

- ❌ node_modules/
- ❌ .env
- ❌ dist/
- ❌ coverage/
- ❌ \*.log
- ❌ .vscode/

---

# 📋 Summary Table

---

Feature Description

---

Purpose Prevent Git from tracking unwanted files  
and folders

File Name `.gitignore`

Affects Only untracked files

Deletes Files ❌ No

Keeps Files Locally ✅ Yes

Common Uses `node_modules/`, `.env`, `dist/`,  
`build/`, logs, cache, IDE settings

Wildcard `*` matches any characters

Negation `!` re-includes ignored files

## Stop Tracking `git rm --cached <file>`

---

# 📝 Key Takeaways

- `.gitignore` tells Git **what not to track**.
- It does **not** delete files or untrack files already committed.

---

![[gitignore.png]]