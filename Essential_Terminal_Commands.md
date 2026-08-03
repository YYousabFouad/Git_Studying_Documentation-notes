🖥️ Chapter 0 -- Essential Terminal Commands

Before learning Git, you should know how to navigate your computerfrom the terminal.

📌 Terminal Navigation Workflow

Open Terminal
│
▼
Check Current Location (pwd)
│
▼
List Files (ls)
│
▼
Move Between Folders (cd)
│
▼
Create Files/Folders
│
▼
Manage Files
│
▼
Start Using Git

📍 pwd (Print Working Directory)

Purpose: Shows your current location.

Syntax

pwd

Example

pwd

# /home/username/Documents

💡 Use it whenever you are unsure where you are.

📂 ls

Purpose: List files and folders.

ls

Useful options

ls -l # detailed list
ls -a # include hidden files
ls -la # detailed + hidden

Hidden files start with . such as:

.git
.gitignore
.env

📁 cd (Change Directory)

Purpose: Move between folders.

cd folder-name
cd ..
cd ~
cd /
cd ~/Projects/MyProject

Command Meaning

cd folder Enter foldercd .. Parent foldercd ~ Home directorycd / Root directory

📦 mkdir

Create a new folder.

mkdir project
mkdir src

📄 touch

Create an empty file.

touch index.js
touch README.md
touch .gitignore

📋 cp

Copy files.

cp app.js backup.js
cp -r src backup

✏️ mv

Move or rename files.

mv app.js src/app.js
mv old.txt new.txt

🗑️ rm

Delete files.

rm app.js
rm -r dist
rm -rf node_modules

⚠️ rm -rf permanently deletes files.

📖 cat

Display file contents.

cat README.md
cat package.json

🧹 clear

Clear the terminal.

clear

Shortcut:

Ctrl + L

📜 history

Show previously executed commands.

history

🔎 find

Find files.

find . -name "\*.js"
find . -name README.md

📍 which

Find the location of an installed command.

which git
which node
which code

🎯 Essential Commands Cheat Sheet

Task Command

Current folder pwdList files lsShow hidden files ls -laEnter folder cd folderGo back cd ..Home cd ~Create folder mkdir folderCreate file touch fileCopy cpMove/Rename mvDelete file rm fileDelete folder rm -r folderShow file cat fileClear terminal clearHistory historyFind file findLocate program which

🚀 Preparing a Project for Git

Open Terminal
│
▼
cd ~/Projects/MyProject
│
▼
pwd
│
▼
ls -la
│
▼
git init

📌 Next Chapter

Now you're ready to start learning:

What Git is

How Git stores project history

The .git folder

Working Directory

Staging Area

Commits

GitHub

![[TerminalNavigationWorkflow.png]]