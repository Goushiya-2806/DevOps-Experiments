
Here is a simple, exam-ready lab write-up in plain text format. You can directly copy and paste it into MS Word.

# EXPERIMENT – 2

TITLE: Explore Git and GitHub Commands

AIM:

To explore and execute basic Git and GitHub commands for version control and repository management.

SOFTWARE REQUIREMENTS:

1. Git
2. GitHub Account
3. Visual Studio Code
4. Command Prompt / Git Bash

PROCEDURE:

Step 1: Install Git

Download Git from [https://git-scm.com](https://git-scm.com?utm_source=chatgpt.com) and install it using the default settings.

Step 2: Verify Git Installation

Open Git Bash or Command Prompt and execute:

```
git --version
```

Step 3: Configure Git

Set username and email:

```
git config --global user.name "Your Name"
git config --global user.email "yourmail@gmail.com"
```

Check configuration:

```
git config --list
```

Step 4: Create a Project Folder

```
mkdir GitDemo
cd GitDemo
```

Step 5: Initialize Git Repository

```
git init
```

This command creates a new Git repository.

Step 6: Check Repository Status

```
git status
```

This command displays the current status of files.

Step 7: Add Files to Staging Area

```
git add .
```

This command adds all files to the staging area.

Step 8: Commit Changes

```
git commit -m "Initial commit"
```

This command saves changes to the local repository.

Step 9: View Commit History

```
git log --oneline
```

This command displays the commit history.

Step 10: Create and Switch Branch

Create a new branch:

```
git branch feature
```

Switch to the branch:

```
git switch feature
```

Step 11: Merge Branch

Switch to the main branch:

```
git switch main
```

Merge the feature branch:

```
git merge feature
```

Step 12: Create GitHub Repository

1. Open [https://github.com](https://github.com?utm_source=chatgpt.com)
2. Login to your GitHub account.
3. Click on New Repository.
4. Enter the repository name.
5. Click Create Repository.

Step 13: Connect Local Repository to GitHub

Add the GitHub repository URL:

```
git remote add origin https://github.com/username/GitDemo.git
```

Check the remote repository:

```
git remote -v
```

Step 14: Push Files to GitHub

```
git push -u origin main
```

This command uploads local commits to GitHub.

Step 15: Pull Latest Changes

```
git pull origin main
```

This command downloads and merges the latest changes from GitHub.

Step 16: Clone Repository

```
git clone https://github.com/username/GitDemo.git
```

This command copies a remote repository to the local system.

IMPORTANT GIT COMMANDS AND THEIR PURPOSES:

| Command              | Purpose                    |
| -------------------- | -------------------------- |
| git init             | Initialize repository      |
| git clone URL        | Copy repository            |
| git status           | Check file status          |
| git add .            | Add all files              |
| git commit -m "msg"  | Save changes               |
| git log --oneline    | View commit history        |
| git diff             | Show changes               |
| git restore file     | Restore modified file      |
| git branch           | List branches              |
| git switch branch    | Switch branch              |
| git merge branch     | Merge branches             |
| git push origin main | Upload commits             |
| git pull origin main | Download and merge changes |
| git fetch            | Download changes           |
| git remote -v        | Show remote repository     |
| git rm file          | Remove tracked file        |

RESULT:

Thus, the basic Git and GitHub commands were explored and executed successfully. A local Git repository was created, files were added and committed, branches were managed, and the repository was connected to GitHub for uploading and downloading changes.

Note: Replace `username`, `Your Name`, and `yourmail@gmail.com` with your actual details. Use `main` or `master` according to your repository's branch name.
