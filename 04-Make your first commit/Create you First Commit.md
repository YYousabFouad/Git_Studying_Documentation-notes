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


---

# What Does a Commit Contain?

A commit contains these main fields:

```
Commit
│
├── Commit Hash (ID)
├── Parent Commit
├── Tree Hash
├── Author
├── Committer
├── Date & Time
└── Commit Message
```

Let's explain each one.

---

# 1. Commit Hash (Unique ID)

Every commit has a unique identifier.

Example:

```
8d7f4c9d62d8f87ab48f2d0d4ab2d8f2b56e91c4
```

Usually you'll only see the first few characters:

```
8d7f4c9
```

Think of it as the commit's fingerprint.

```
Commit
┌──────────────────────┐
│ ID: 8d7f4c9          │
└──────────────────────┘
```

No two commits have the same hash.

Even changing **one character** in one file creates a completely different hash.

---

# 2. Parent Commit

Every commit remembers **which commit came before it**.

Example:

```
Commit C
     │
Parent
     ▼
Commit B
     │
Parent
     ▼
Commit A
```

This is how Git builds your project's history.

Without the parent reference, Git wouldn't know the order of commits.

---

# 3. Tree Hash

Remember:

```
Commit
   │
   ▼
 Tree
```

The commit does **not** store your files directly.

Instead, it stores the hash of the **tree** object.

The tree contains:

- file names
- folders
- references to blobs

Example:

```
Commit

Tree:
a91c74...
```

Git follows that tree to find your entire project.

---

# 4. Author

Git records **who originally wrote the change**.

Example:

```
Author

Yosab Fouad
yosab@example.com
```

This is especially useful when many developers work together.

---

# 5. Committer

This surprises many beginners.

Git stores both:

```
Author
```

and

```
Committer
```

Sometimes they are the same person.

Example:

```
Author:
Alice

Committer:
Alice
```

But imagine Bob applies Alice's work using another Git command.

```
Author:
Alice

Committer:
Bob
```

- **Author** = who wrote the change.
- **Committer** = who actually created the commit in the repository.

---

# 6. Date & Time

Git records exactly when the commit was created.

Example:

```
Sat Aug 2 16:15:41 2026
```

This helps you understand when changes happened.

---

# 7. Commit Message

The message explains **why** the change was made.

Example:

```
Add login page
```

or

```
Fix authentication bug
```

This is why good commit messages are important.

---

# Putting It All Together

Imagine this command:

```
git commit -m "Add login page"
```

Git creates something conceptually like:

```
Commit

Hash:
8d7f4c9

Parent:
5ab9321

Tree:
9bc7412

Author:
Yosab Fouad

Committer:
Yosab Fouad

Date:
2026-08-02 16:15

Message:
Add login page
```

Notice what's **missing**:

❌ The actual contents of `index.html`

❌ The actual contents of `style.css`

Those are stored in **blobs**, not in the commit.

The commit simply points to the tree, and the tree points to the blobs.

---

# The Relationship

```
Commit
│
├── Hash
├── Parent
├── Tree ───────────────┐
├── Author              │
├── Committer           │
├── Date                │
└── Message             │
                         ▼
                      Tree
                   /    |    \
                  ▼     ▼     ▼
              Blob   Blob   Blob
```

This design is what makes Git so efficient.

The commit itself is tiny because it mostly contains **references** (hashes and metadata), not copies of your files.

---

# Example from `git log`

When you run:

```
git log
```

You might see:

```
commit 8d7f4c9d62d8f87ab48f2d0d4ab2d8f2b56e91c4
Author: Yosab Fouad <yosab@example.com>
Date:   Sat Aug 2 16:15:41 2026

    Add login page
```

What `git log` is showing is information stored in the **commit object**.

The **parent commit** and **tree hash** also exist, but `git log` hides them by default to keep the output simple.

---

# Key Takeaway

- A **commit** is a small metadata object, **not** a copy of your project.
- It contains:
    - A unique **hash (ID)**
    - A reference to its **parent commit**
    - A reference to the **tree**
    - **Author**
    - **Committer**
    - **Date & Time**
    - **Commit message**

### Visual Summary

```
               Commit
        ┌───────────────────────┐
        │ Hash (Unique ID)       │
        │ Parent Commit          │
        │ Tree Hash              │
        │ Author                 │
        │ Committer              │
        │ Date & Time            │
        │ Message                │
        └──────────┬─────────────┘
                   │
                   ▼
                 Tree
            ┌────┼────┐
            ▼    ▼    ▼
         Blob  Blob  Blob
```


---

# View the History

The most common command is:

```
git log
```

Example output:

```
commit 8d7f4c9b4e...
Author: Yosab Fouad
Date: Sat Aug 2 15:30:21 2026

    Update README

commit c2a9f4b8d...
Author: Yosab Fouad
Date: Sat Aug 2 14:10:05 2026

    Fix login bug

commit a18b72e3...
Author: Yosab Fouad
Date: Sat Aug 2 12:45:30 2026

    Add login page
```

Each entry contains:

- **Commit hash** (a unique ID)
- **Author**
- **Date**
- **Commit message**

---

# A Shorter Version

If you only want a quick overview:

```
git log --oneline
```

Output:

```
8d7f4c9 Update README
c2a9f4b Fix login bug
a18b72e Add login page
7fd10e2 Add navbar
2bc19a4 Initial project setup
```

This is the command developers use most often.

---

# A Graph View

When working with branches, this is very helpful:

```
git log --oneline --graph --all
```

Example:

```
* 8d7f4c9 Update README
* c2a9f4b Fix login bug
* a18b72e Add login page
* 7fd10e2 Add navbar
* 2bc19a4 Initial project setup
```

Later, when you learn branches, you'll see graphs like:

```
* Merge feature-login
|\
| * Fix login bug
| * Add login page
|/
* Add navbar
* Initial project setup
```

---

# View a Specific Commit

Suppose you want details about this commit:

```
c2a9f4b
```

Run:

```
git show c2a9f4b
```

Git will display:

- The commit message
- The author
- The date
- Exactly which lines were added or removed

---

# See What Changed Between Commits

You can compare two commits:

```
git diff <commit1> <commit2>
```

For example:

```
git diff a18b72e c2a9f4b
```

Git will show the differences between those two snapshots.

---

# Where Is the History Stored?

Remember what we discussed:

```
Commit
   │
   ▼
 Tree
 / | \
▼ ▼ ▼
Blob Blob Blob
```

Every new commit points to a new snapshot of your project.

The history is simply a chain of commits:

```
Commit 5
   │
   ▼
Commit 4
   │
   ▼
Commit 3
   │
   ▼
Commit 2
   │
   ▼
Commit 1
```

Git starts at the latest commit (called **HEAD**) and follows the chain backward to reconstruct the entire history.

---

# Useful Commands to Remember

| Command                           | What it does                  |
| --------------------------------- | ----------------------------- |
| `git log`                         | Shows the full commit history |
| `git log --oneline`               | Shows a compact history       |
| `git log --graph --oneline --all` | Shows history with branches   |
| `git show <hash>`                 | Shows details of one commit   |
| `git diff <commit1> <commit2>`    | Compares two commits          |

---

## Key Takeaway

- **The project's history is the sequence of commits Git has recorded.**
- **You can explore that history with `git log`, inspect individual commits with `git show`, and compare snapshots with `git diff`.**

### Simple Visual

```
Working on Project
       │
       ▼
Commit A
       │
       ▼
Commit B
       │
       ▼
Commit C
       │
       ▼
Commit D (HEAD)
       │
       ▼
git log
       │
       ▼
Displays the complete timeline of your project's changes
```