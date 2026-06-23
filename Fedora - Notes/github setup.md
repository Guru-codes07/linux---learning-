# GitHub Setup on Fedora

GitHub is a cloud-based platform used to host Git repositories and collaborate on software projects.

This guide explains how to configure Git, connect GitHub, create repositories, and push code from Fedora Linux.

---

# What is GitHub?

GitHub is a platform built around Git that allows developers to:

* Store code online
* Track project history
* Collaborate with others
* Contribute to open source projects
* Showcase projects through repositories

Official Website:

```text
https://github.com
```

---

# Prerequisites

Before using GitHub, ensure the following are installed:

* Git
* GitHub Account
* Internet Connection

Verify Git installation:

```bash
git --version
```

Example Output:

```text
git version 2.50.1
```

---

# Configure Git

Git uses a username and email address to identify commits.

## Set Username

```bash
git config --global user.name "Guru Prasad Mishra"
```

---

## Set Email

```bash
git config --global user.email "your-email@example.com"
```

Replace the email with the one associated with your GitHub account.

---

## Verify Configuration

```bash
git config --list
```

Example Output:

```text
user.name=Guru Prasad Mishra
user.email=your-email@example.com
```

---

# Create a GitHub Repository

## Step 1

Log in to GitHub.

## Step 2

Click:

```text
New Repository
```

## Step 3

Fill in:

* Repository Name
* Description
* Visibility (Public or Private)

Example:

```text
Repository Name: linux-learning

Description: My Linux learning journey, notes, commands, and concepts.
```

## Step 4

Click:

```text
Create Repository
```

---

# Create a Local Project

Create a project directory:

```bash
mkdir linux-learning
cd linux-learning
```

Initialize Git:

```bash
git init
```

Output:

```text
Initialized empty Git repository
```

---

# Create a README File

```bash
touch README.md
```

Add content:

```markdown
# Linux Learning

My Linux learning journey and notes.
```

---

# Check Repository Status

```bash
git status
```

This displays:

* New files
* Modified files
* Staged files

---

# Add Files to Staging Area

Add a specific file:

```bash
git add README.md
```

Add all files:

```bash
git add .
```

---

# Create Your First Commit

```bash
git commit -m "Initial commit"
```

Example Output:

```text
[main abc1234] Initial commit
```

---

# Connect Local Repository to GitHub

Copy your repository URL from GitHub.

Example:

```text
https://github.com/username/linux-learning.git
```

Add remote origin:

```bash
git remote add origin https://github.com/username/linux-learning.git
```

Verify:

```bash
git remote -v
```

Example Output:

```text
origin  https://github.com/username/linux-learning.git
```

---

# Push to GitHub

## Rename Branch to Main

```bash
git branch -M main
```

---

## Push Repository

```bash
git push -u origin main
```

After the first push, future pushes can be done with:

```bash
git push
```

---

# Daily GitHub Workflow

After making changes:

## Check Status

```bash
git status
```

---

## Add Files

```bash
git add .
```

---

## Commit Changes

```bash
git commit -m "Add Linux file system notes"
```

---

## Push Changes

```bash
git push
```

This is the workflow you will use most often.

---

# Clone an Existing Repository

Download a repository from GitHub:

```bash
git clone https://github.com/username/repository.git
```

Example:

```bash
git clone https://github.com/username/linux-learning.git
```

---

# Pull Latest Changes

Download updates from GitHub:

```bash
git pull
```

Or:

```bash
git pull origin main
```

---

# View Commit History

Display commit history:

```bash
git log
```

Compact view:

```bash
git log --oneline
```

Example:

```text
abc1234 Add Linux networking notes
def5678 Add package management notes
```

---

# Useful Git Commands

## Repository Information

```bash
git status
```

```bash
git remote -v
```

```bash
git branch
```

---

## Staging

```bash
git add file.txt
```

```bash
git add .
```

---

## Commits

```bash
git commit -m "message"
```

```bash
git log
```

---

## Synchronization

```bash
git push
```

```bash
git pull
```

```bash
git clone <repository_url>
```

---

# Common Problems

## Authentication Failed

Example:

```text
Authentication failed
```

### Cause

GitHub no longer supports password authentication for Git operations.

### Solution

Use:

* Personal Access Tokens (PAT)
* SSH Authentication

---

## Remote Already Exists

Example:

```text
remote origin already exists
```

### View Existing Remote

```bash
git remote -v
```

### Remove Existing Remote

```bash
git remote remove origin
```

Add it again:

```bash
git remote add origin <repository_url>
```

---

## Nothing to Commit

Example:

```text
nothing to commit, working tree clean
```

### Meaning

No files have changed since the last commit.

---

## Push Rejected

Example:

```text
failed to push some refs
```

### Solution

Pull latest changes first:

```bash
git pull origin main
```

Then push again:

```bash
git push
```

---

# Recommended Commit Messages

Good Examples:

```text
Add Linux navigation commands
Add file viewing commands
Add Linux file system concepts
Add Fedora update notes
Fix README formatting
```

Avoid:

```text
update
changes
test
asdf
```

Meaningful commit messages make project history easier to understand.

---

# Summary

| Command                 | Purpose                   |
| ----------------------- | ------------------------- |
| `git init`              | Initialize repository     |
| `git status`            | View repository status    |
| `git add .`             | Stage all changes         |
| `git commit -m`         | Create commit             |
| `git log`               | View commit history       |
| `git remote add origin` | Connect GitHub repository |
| `git push`              | Upload changes            |
| `git pull`              | Download changes          |
| `git clone`             | Download repository       |
| `git branch -M main`    | Rename branch             |

### Daily Workflow

```bash
git status
git add .
git commit -m "Meaningful message"
git push
```

GitHub is one of the most important tools for software development, open-source contributions, and showcasing projects. Learning Git and GitHub early will significantly improve your development workflow.

