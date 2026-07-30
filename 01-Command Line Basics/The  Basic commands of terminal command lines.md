# Step 0: Navigate to Your Project Folder

Git commands always work on the **current folder**.

## 1. Check where you are

```
pwd
```

**Meaning:** Print Working Directory

Example:

```
/home/yosab
```

---

## 2. See the folders/files

```
ls
```

Example:

```
Documents
Downloads
Projects
Desktop
```

---

## 3. Go to your project folder

```
cd Projects
```

or

```
cd MyProject
```

Example:

```
cd ~/Projects/MyWebsite
```

`cd` means:

> **Change Directory**

---

## 4. Make sure you're inside the correct folder

```
pwd
```

Example:

```
/home/yosab/Projects/MyWebsite
```

Now every Git command will work **inside this project**.

---

# If the folder does not exist

Create it:

```
mkdir MyProject
```

Go inside it:

```
cd MyProject
```

---

# If you already have a project

```
cd path/to/project
```

Example:

```
cd ~/Documents/React-App
```

---

# If the folder name contains spaces

Use quotes:

```
cd "My React Project"
```

or escape the spaces:

```
cd My\ React\ Project
```

---

# Your First Git Workflow

```
Open Terminal
      │
      ▼
Navigate to Project
(cd MyProject)
      │
      ▼
Check Location
(pwd)
      │
      ▼
Initialize Git
(git init)
      │
      ▼
Check Status
(git status)
      │
      ▼
Stage Changes
(git add .)
      │
      ▼
Create Snapshot
(git commit -m "Initial commit")
      │
      ▼
Connect to GitHub
(git remote add origin <repository-url>)
      │
      ▼
Upload to GitHub
(git push -u origin main)
```

---

## 💡 Beginner Tip

Always remember this order:

```
Open Terminal
        ↓
cd your-project
        ↓
pwd (optional)
        ↓
git commands
```

If you're in the **wrong folder**, Git will also work in the **wrong folder**, so getting used to `cd` and `pwd` is one of the most important habits when using Git from the command line.

### Key Takeaway

- `cd` changes the folder you're working in.
- Always run `pwd` (or `ls`) to confirm you're in the correct project before running any Git command.


![[howToNavigateToYourFolder.png]]