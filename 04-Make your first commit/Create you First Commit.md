The best practice is:

> **1. Create your project folder first.**  
> **2. Run `git init` inside the project.**  
> **3. Make your first commit.**  
> **4. Then create a new repository on GitHub.**  
> **5. Connect them and push.**

### Why?

Think of it like this:

```
Your Computer                    GitHub

Project Folder
      │
      ├── git init   ✅
      │      ↓
      ├── .git (local repository)
      │
      ├── add files
      ├── git add .
      ├── git commit
      │
      └──────────────► Create New Repo on GitHub
                             │
                             ▼
                     Empty Remote Repository
                             │
                             ▼
                     git remote add origin ...
                     git push -u origin main
```

### Why not create the GitHub repo first?

You _can_ create the GitHub repository first, and many people do. It isn't wrong.

However, for learning Git, I recommend this order because it helps you understand that:

- **Git works locally.**
- **GitHub is just a remote place to store your Git repository.**

Many beginners mistakenly think GitHub is Git. It isn't.

- **Git** = version control on your computer.
- **GitHub** = website that hosts Git repositories.

### My usual workflow

```
mkdir my-project
cd my-project

git init
git add .
git commit -m "Initial commit"

# Then go to GitHub
# Create New Repository

git remote add origin <repo-url>
git push -u origin main
```

---

### There is one exception

If you are starting from an existing GitHub repository (for example, an open-source project or a template), then you **don't** use `git init`.

Instead, you clone it:

```
git clone <repo-url>
```

because the repository already exists on GitHub.

---

### Key Takeaway

- ✅ For a **new project**: `git init` → first commit → create GitHub repo → push.
- ✅ For an **existing GitHub project**: use `git clone` instead of `git init`.

```
New Project
    │
    ▼
Create Folder
    │
    ▼
git init
    │
    ▼
First Commit
    │
    ▼
Create GitHub Repo
    │
    ▼
git remote add origin
    │
    ▼
git push
```


---

# What is a Commit?

A **commit** is a **snapshot** (or checkpoint) of your project at a specific moment.

Think of it as pressing **"Save Game"** in a video game.

Instead of saving only the latest version, Git saves a history of your project.

```
Project

Version 1
   │
   ▼
Commit A

Version 2
   │
   ▼
Commit B

Version 3
   │
   ▼
Commit C
```

Every commit gets a unique ID and a message describing what changed.

Example:

```
git commit -m "Add login page"
```

This tells Git:

> "Remember exactly how my project looks right now."

---

# Why Do We Need Commits?

Imagine you're building a blog website.
	
### Day 1

```
✓ Home Page
✓ Navbar
✓ Footer
```

You create a commit.

```
Commit:
"Initial website"
```

---

### Day 2

You add a Login page.

Everything works.

You create another commit.

```
Commit:
"Add login page"
```

---

### Day 3

You try adding authentication.

Suddenly...

💥 Everything breaks.

```
Home ❌
Login ❌
CSS ❌
```

Without commits...

```
😭 You don't know what changed.
```

With commits...

```
Commit 1
│
├── Initial website
│
├── Add login page
│
└── Authentication (Broken)

        ▲
        │
Go back here
```

Git lets you return to the last working version.

---

# Imagine There Were No Commits

```
Project

Current Version
        │
        ▼
Broken
```

There is no history.

No backup.

No way back.

You may spend hours finding the mistake.

---

# Think of Commits Like Google Docs

When using Google Docs, you can view:

```
Version History

Monday
Tuesday
Wednesday
Thursday
```

You can restore Tuesday's version.

Git commits work the same way, but for code.

---

# What Does a Commit Save?

A commit saves:

```
✓ Files
✓ Folder structure
✓ Changes
✓ Commit message
✓ Author
✓ Date & Time
```

It does **not** just save one file.

It saves the **entire project state**.

---

# How Commits Affect Your Daily Work

Imagine you're working for a company.

Morning:

```
Add Navbar
```

Commit

```
"Add responsive navbar"
```

After lunch:

```
Fix login bug
```

Commit

```
"Fix login validation"
```

Evening:

```
Add dashboard
```

Commit

```
"Create dashboard layout"
```

Your history becomes:

```
Project

● Add responsive navbar
        │
● Fix login validation
        │
● Create dashboard layout
```

This makes it easy to:

- Find bugs
- Undo mistakes
- Review changes
- Work with teammates
- Deploy stable versions

---

# Why Small Commits Are Better

Bad:

```
Commit:
"Update project"
```

What changed?

🤷 Nobody knows.

---

Good:

```
Add authentication

Fix navbar mobile bug

Refactor user service

Update README
```

Each commit tells a clear story.

---

# Commits Help Teams

Imagine two developers.

```
Ali
```

Adds a Login page.

```
Sara
```

Adds Dark Mode.

Git records:

```
Commit
Author: Ali
Message:
Add login page

-------------------

Commit
Author: Sara
Message:
Implement dark mode
```

Everyone knows who changed what.

---

# Commits Build a Timeline

```
Start Project
      │
      ▼
Initial Commit
      │
      ▼
Add Navbar
      │
      ▼
Add Login
      │
      ▼
Fix Bugs
      │
      ▼
Deploy Version 1.0
```

Instead of one huge save, you build a complete history of your project.

---

# A Real-Life Analogy

Imagine writing a book.

Without commits:

```
Book.docx
```

Every day you overwrite the same file.

If chapter 10 gets deleted...

😱 It's gone.

With commits:

```
Book v1
Book v2
Book v3
Book v4
```

You can always return to an earlier version.

Git does this automatically.

---

# Best Practice

A good rule is:

> **Make one commit for one logical change.**

For example:

```
❌ One commit:
"Finished project"

✅ Better:

Initial project setup

Add authentication

Fix login validation

Create profile page

Update documentation
```

This makes your project's history clean and easy to understand.

---

# Key Takeaway

- **A commit is a snapshot (checkpoint) of your entire project at a specific moment.**
- **Commits let you track history, undo mistakes, understand changes, and collaborate safely with others.**

### Simple Visual

```
Working on Project
        │
        ▼
Make a Change
        │
        ▼
git add .
        │
        ▼
git commit -m "Describe the change"
        │
        ▼
Git saves a snapshot
        │
        ▼
Continue working...
        │
        ▼
Another Commit
        │
        ▼
Another Snapshot

History:
● Initial setup
● Add login page
● Fix authentication bug
● Update README
```

![[Infographic - Git & GitHub Workflow.png]]