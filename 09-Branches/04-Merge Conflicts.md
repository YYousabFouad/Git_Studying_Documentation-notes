# 🌿 Merge Conflicts

## 📖 Introduction

Git is excellent at automatically combining changes from different branches. However, there are situations where Git cannot determine which changes should be kept.

When this happens, Git stops the merge process and asks you to resolve the conflict manually.

A **merge conflict** is not an error in Git—it is Git asking for your decision because it cannot safely merge the changes on its own.

---

# 🎯 Learning Objectives

After completing this chapter, you will be able to:

- Understand what a merge conflict is.
    
- Learn why merge conflicts occur.
    
- Identify conflict markers.
    
- Resolve conflicts manually.
    
- Continue or abort a merge.
    
- Apply best practices to reduce conflicts.
    

---

# 🤔 What Is a Merge Conflict?

A **merge conflict** occurs when Git cannot automatically combine changes from two branches.

This usually happens when the same part of the same file has been modified differently in each branch.

Instead of guessing which version is correct, Git pauses the merge and lets you decide.

---

# 🌍 Real-World Example

Imagine two authors editing the same paragraph in a document.

- Author A changes the first sentence.
    
- Author B changes that same sentence differently.
    

When it's time to combine both versions, the editor cannot know which sentence should remain.

The editor asks for a decision.

Git behaves in exactly the same way.

---

# 📊 Example Repository

Before merging:

```text
A──B──C (main)
      \
       D──E (feature-login)
```

Suppose both branches modified the same line in `app.js`.

Now run:

```bash
git switch main
git merge feature-login
```

Git attempts to merge the branches.

If it cannot combine the changes safely, the merge stops.

---

# 🚨 What Does Git Display?

Example message:

```text
Auto-merging app.js
CONFLICT (content): Merge conflict in app.js
Automatic merge failed; fix conflicts and then commit the result.
```

Git does **not** lose your work.

It simply waits for you to resolve the conflict.

---

# ⚠️ Conflict Markers

Git marks conflicts directly inside the affected file.

Example:

```text
<<<<<<< HEAD
console.log("Welcome!");
=======
console.log("Welcome Back!");
>>>>>>> feature-login
```

### Understanding the Markers

|Marker|Meaning|
|---|---|
|`<<<<<<< HEAD`|The current branch's version|
|`=======`|Separator between the two versions|
|`>>>>>>> feature-login`|The incoming branch's version|

---

# 📖 Reading the Conflict

Current branch:

```javascript
console.log("Welcome!");
```

Incoming branch:

```javascript
console.log("Welcome Back!");
```

Git cannot determine which version should remain.

You must choose one, combine them, or rewrite the code.

---

# ✅ Resolving a Conflict

The general process is:

1. Open the conflicted file.
    
2. Find the conflict markers.
    
3. Decide which changes to keep.
    
4. Remove the conflict markers.
    
5. Save the file.
    
6. Stage the resolved file.
    
7. Complete the merge.
    

Example:

```bash
git add app.js
git commit
```

Git then creates the merge commit.

---

# 📊 Conflict Resolution Workflow

```text
Start Merge
      │
      ▼
Conflict Found
      │
      ▼
Open File
      │
      ▼
Resolve Conflict
      │
      ▼
Save File
      │
      ▼
git add
      │
      ▼
git commit
      │
      ▼
Merge Complete
```

---

# 🛑 Aborting a Merge

If you decide not to continue the merge, Git can restore the repository to the state before the merge began.

```bash
git merge --abort
```

This command cancels the merge and returns your working tree to its previous state.

Use it only if you no longer want to merge the branches.

---

# 🧠 Why Do Merge Conflicts Happen?

Common causes include:

- Two branches modify the same line.
    
- One branch deletes a file while another edits it.
    
- The same file is renamed differently.
    
- Multiple developers edit the same code simultaneously.
    
- Long-lived branches drift far apart.
    

---
# 🧩 Types of Merge Conflicts

Merge conflicts can occur in several different ways. Understanding the type of conflict helps you resolve it more confidently.

---

## 1️⃣ Content Conflict

A **content conflict** occurs when the same lines of a file are modified differently in two branches.

### Example

**main**

```javascript
console.log("Welcome!");
```

**feature-login**

```javascript
console.log("Welcome Back!");
```

Since both branches changed the same line, Git cannot determine which version should be kept.

This is the **most common** type of merge conflict.

---

## 2️⃣ Modify/Delete Conflict

A **modify/delete conflict** happens when one branch modifies a file while another branch deletes it.

### Example

```text
main
└── config.js   ❌ Deleted

feature-login
└── config.js   ✏️ Modified
```

Git cannot know whether the file should exist or be removed, so it asks you to decide.

---

## 3️⃣ Rename Conflict

A **rename conflict** occurs when the same file is renamed differently in separate branches.

### Example

```text
Original File
│
└── app.js

main
└── index.js

feature-login
└── application.js
```

Git detects that both branches renamed the same file but to different names, requiring manual resolution.

---

## 4️⃣ File Location Conflict

A **file location conflict** occurs when the same file is moved to different directories in different branches.

### Example

```text
main
src/components/Button.js

feature-login
src/ui/Button.js
```

Git cannot determine the correct final location automatically.

---

## 5️⃣ Directory/File Conflict

A **directory/file conflict** happens when one branch creates a file with a name that another branch uses as a directory.

### Example

```text
main
docs

feature-login
docs/
    README.md
```

Since a path cannot be both a file and a directory at the same time, Git requires manual intervention.

---

# 📌 Summary of Conflict Types

|Conflict Type|Description|
|---|---|
|**Content Conflict**|The same lines are modified differently in both branches.|
|**Modify/Delete Conflict**|One branch edits a file while the other deletes it.|
|**Rename Conflict**|The same file is renamed differently in separate branches.|
|**File Location Conflict**|The same file is moved to different locations.|
|**Directory/File Conflict**|One branch creates a file while another creates a directory with the same name.|

---

# 💡 Good to Know

Most day-to-day merge conflicts are **Content Conflicts**.

The other conflict types are less common, but they become more likely in larger projects where many developers are working on the same codebase simultaneously.

Understanding these conflict types will make it easier to interpret Git's conflict messages and choose the appropriate resolution.

---

# 💻 Using Visual Merge Tools

Many editors provide graphical tools for resolving conflicts.

Examples include:

- Visual Studio Code Merge Editor
    
- GitKraken
    
- Sourcetree
    

These tools highlight the conflicting sections and make it easier to compare both versions.

Even when using a visual tool, understanding the conflict markers is important.

---

# 💡 How to Reduce Merge Conflicts

Although conflicts are sometimes unavoidable, you can reduce them by following good practices:

- Merge frequently.
    
- Pull the latest changes before starting new work.
    
- Keep branches short-lived.
    
- Work on small, focused features.
    
- Communicate with teammates when editing shared files.
    

---

# ⚠️ Common Mistakes

### ❌ Deleting the wrong code

Do not remove code without understanding what each branch changed.

Review both versions carefully.

---

### ❌ Leaving conflict markers in the file

Your code should **never** contain markers like:

```text
<<<<<<<
=======
>>>>>>>
```

Always remove them before committing.

---

### ❌ Forgetting to stage the resolved file

After fixing the conflict, Git still considers the file unresolved until it is staged.

Use:

```bash
git add <file-name>
```

---

### ❌ Continuing without testing

Always test your project after resolving conflicts to ensure the combined code works correctly.

---

# 📋 Useful Commands

|Command|Description|
|---|---|
|`git merge <branch>`|Start a merge|
|`git status`|Show conflicted files|
|`git add <file>`|Mark a conflict as resolved|
|`git merge --abort`|Cancel the merge|
|`git commit`|Complete the merge after resolving conflicts|

---

# 📝 Summary

A merge conflict occurs when Git cannot automatically combine changes from different branches. Instead of making an unsafe decision, Git pauses the merge and asks you to resolve the conflict manually. By understanding conflict markers and following the correct resolution process, you can safely combine changes while preserving your project's integrity.

---

# 📚 Key Takeaways

- A **merge conflict** happens when Git cannot automatically combine changes.
    
- Conflict markers show the differences between the current and incoming branches.
    
- Resolve conflicts by editing the file, removing the markers, and keeping the desired code.
    
- Use `git add` to mark the conflict as resolved.
    
- Use `git merge --abort` if you decide to cancel the merge.
    
- Frequent merges and short-lived branches help reduce the likelihood of conflicts.

---

# 🚀 Complete Conflict Resolution Walkthrough

The following example demonstrates the complete lifecycle of a merge conflict, from creating a branch to successfully completing the merge.

---

## Step 1: Create a New Branch

Start from the `main` branch and create a feature branch.

```bash
git switch -c feature-login
```

Repository:

```text
A──B──C (main, feature-login)
```

---

## Step 2: Modify a File

Suppose `app.js` contains:

```javascript
console.log("Welcome!");
```

On the `feature-login` branch, change it to:

```javascript
console.log("Welcome Back!");
```

Commit the change:

```bash
git add app.js
git commit -m "Update welcome message"
```

Repository:

```text
A──B──C
        \
         D (feature-login)
```

---

## Step 3: Switch Back to `main`

```bash
git switch main
```

Modify the **same line** in the same file:

```javascript
console.log("Hello!");
```

Commit the change:

```bash
git add app.js
git commit -m "Change welcome message"
```

Repository:

```text
A──B──C──E (main)
        \
         D (feature-login)
```

Now both branches have changed the same line differently.

---

## Step 4: Merge the Feature Branch

```bash
git merge feature-login
```

Git attempts to merge the changes.

Instead of completing the merge, Git reports a conflict.

Example output:

```text
Auto-merging app.js
CONFLICT (content): Merge conflict in app.js
Automatic merge failed; fix conflicts and then commit the result.
```

---

## Step 5: Inspect the Conflict

Open `app.js`.

Git inserts conflict markers:

```text
<<<<<<< HEAD
console.log("Hello!");
=======
console.log("Welcome Back!");
>>>>>>> feature-login
```

These markers indicate that Git found two different versions of the same code.

---

## Step 6: Resolve the Conflict

Decide which code should remain.

You might:

- Keep the current branch's version.
    
- Keep the incoming branch's version.
    
- Combine both changes.
    
- Rewrite the code entirely.
    

After making your decision, remove **all** conflict markers and save the file.

---

## Step 7: Mark the Conflict as Resolved

Stage the resolved file:

```bash
git add app.js
```

Git now considers the conflict resolved.

---

## Step 8: Complete the Merge

Finish the merge by creating the merge commit:

```bash
git commit
```

Git opens your configured editor with a default merge commit message. Save the message (or edit it if needed) and close the editor to complete the merge.

Repository:

```text
A──B──C──E────────M (main)
        \        /
         D──────/
```

`M` is the **merge commit**, which records that the histories of both branches have been combined.

---

# 📋 End-to-End Workflow

```text
Create Branch
      │
      ▼
Make Changes
      │
      ▼
Commit Changes
      │
      ▼
Switch Branch
      │
      ▼
Modify Same File
      │
      ▼
Commit Changes
      │
      ▼
Merge Branches
      │
      ▼
Conflict Detected
      │
      ▼
Open Conflicted File
      │
      ▼
Read Conflict Markers
      │
      ▼
Resolve Conflict
      │
      ▼
git add
      │
      ▼
git commit
      │
      ▼
Merge Completed ✅
```

---

# 💡 Tips for Resolving Conflicts

- Read both versions carefully before making changes.
    
- Remove **all** conflict markers before saving the file.
    
- Test your project after resolving the conflict.
    
- If you're unsure about the correct resolution, discuss it with your teammates before completing the merge.
    
- If you decide not to continue the merge, you can cancel it with:
    

```bash
git merge --abort
```

---

# 📚 Key Takeaways

- A merge conflict is a normal part of collaborative development.
    
- Git never guesses which conflicting change is correct—it asks you to decide.
    
- The conflict resolution process is:
    
    1. Open the conflicted file.
        
    2. Resolve the conflict.
        
    3. Stage the resolved file with `git add`.
        
    4. Complete the merge with `git commit`.
        
- Always test your application before considering the merge complete.