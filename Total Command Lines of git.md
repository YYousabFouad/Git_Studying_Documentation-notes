🚀 Git & GitHub Handbook

Beginner → Advanced

Goal: Understand Git, not memorize commands.

📚 Table of Contents

🌱 Introduction

🧠 Core Concepts

📂 Git Workflow

📝 Everyday Commands

🌿 Branches

🔀 Merge & Rebase

💾 Reset / Restore / Revert

☁️ GitHub

🏷️ Tags

📌 Best Practices

❓ Interview Questions

📋 Cheat Sheet

🌱 What is Git?

Git is a distributed version control system.

It helps you:

✅ Save project history

✅ Undo mistakes

✅ Work safely

✅ Collaborate with others

🧠 Git vs GitHub

Git GitHub

Installed on your computer Cloud hosting platformTracks project history Stores repositories onlineWorks offline Enables collaboration

📂 Git Workflow

        ✍️ Edit Files
              │
              ▼
     📁 Working Directory
              │
        git add .
              │
              ▼
      📦 Staging Area
              │
     git commit -m ""
              │
              ▼
      💾 Local Repository
              │
         git push
              │
              ▼
        ☁️ GitHub

💡 Memory Tip

Nothing reaches GitHub until you run git push.

📁 File States

State Meaning

⚪ Untracked Git doesn't track it yet🟡 Modified File changed🔵 Staged Ready for commit🟢 Committed Saved locally

📝 Daily Commands

git status
git add .
git commit -m "message"
git push

⭐ These are the commands you'll use most often.

📦 .gitignore

Ignore files Git should never track.

node_modules/
.env
dist/
coverage/
\*.log
.vscode/

✅ Generated files

✅ Build folders

✅ Secrets

🔐 .env

Never upload secrets.

API_KEY=
DATABASE_URL=
JWT_SECRET=

Instead upload:

.env.example

🌿 Branches

git switch -c feature/login
git switch main
git branch
git branch -d feature/login

Why use branches?

Experiment safely

Keep main stable

Work on multiple features

🔀 Merge vs Rebase

Merge Rebase

Preserves history Creates cleaner historyEasier for teams Great for personal branches

💾 Undo Commands

Restore

git restore file

Restores one file.

Revert

git revert HASH

Safely undoes a commit.

Reset

git reset --soft HEAD~1
git reset HEAD~1
git reset --hard HEAD~1

⚠️ Hard reset deletes local changes.

📦 Stash

Temporarily hide your work.

git stash
git stash list
git stash pop

Perfect when you need to switch branches quickly.

☁️ Remote Repositories

git remote add origin URL
git remote -v

🚀 Push Workflow

git status

git add .

git commit -m "feat: add login"

git push

🏷️ Tags

git tag v1.0.0
git push origin v1.0.0

Use tags for releases.

📌 Best Practices

✅ Commit often

✅ Write meaningful commit messages

✅ Pull before pushing

✅ Never commit .env

✅ Keep commits small

✅ Use feature branches

❌ Common Mistakes

Forgetting git status

Working directly on main

Huge commits

Uploading secrets

Using git reset --hard carelessly

❓ Interview Questions

Difference between Fetch and Pull?

Merge vs Rebase?

Reset vs Revert?

What is HEAD?

What is the Staging Area?

What is Cherry-pick?

What is Detached HEAD?

📋 Git Cheat Sheet

Task Command

Check status git statusStage files git add .Commit git commit -m ""Push git pushPull git pullFetch git fetchHistory git log --onelineBranches git branchSwitch git switch nameCreate branch git switch -c nameStash git stashRestore git restore fileRevert git revert HASHReset git reset --soft HEAD~1

🎯 Final Summary

Edit
│
▼
Working Directory
│
▼
git add
│
▼
Staging Area
│
▼
git commit
│
▼
Local Repository
│
▼
git push
│
▼
GitHub

Remember: Every Git command exists to move your project safelyfrom one stage to the next.

![[gitWorkflow.png]]

![[basicCommandLineForGit.png]]
