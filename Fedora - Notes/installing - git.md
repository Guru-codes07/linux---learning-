# Installing Git on Fedora

Git is a distributed version control system used to track changes in source code and collaborate on software projects.

It is one of the most important tools for developers and is widely used with platforms such as GitHub, GitLab, and Bitbucket.

---

## What is Git?

Git allows you to:

* Track changes in files
* Create project snapshots (commits)
* Collaborate with other developers
* Manage project history
* Work with remote repositories

Official Website:

```text
https://git-scm.com
```

---

## Check if Git is Already Installed

Before installing Git, verify whether it is already available on your system.

### Command

```bash
git --version
```

### Example Output

```text
git version 2.50.1
```

If Git is installed, the version number will be displayed.

---

## Install Git on Fedora

### Step 1: Update Package Information

```bash
sudo dnf check-update
```

This refreshes package information from Fedora repositories.

---

### Step 2: Install Git

```bash
sudo dnf install git
```

DNF will automatically download and install Git and its dependencies.

---

### Step 3: Verify Installation

```bash
git --version
```

### Example Output

```text
git version 2.50.1
```

---

## Configure Git

After installation, configure your username and email address.

### Set Username

```bash
git config --global user.name "Guru Prasad Mishra"
```

### Set Email Address

```bash
git config --global user.email "your-email@example.com"
```

### Verify Configuration

```bash
git config --list
```

Example Output:

```text
user.name=Guru Prasad Mishra
user.email=your-email@example.com
```

---

## Understanding Git Configuration Levels

Git supports three configuration levels.

| Level  | Scope                                 |
| ------ | ------------------------------------- |
| System | Applies to all users                  |
| Global | Applies to the current user           |
| Local  | Applies only to a specific repository |

### Examples

Global:

```bash
git config --global user.name "Guru Prasad Mishra"
```

Local:

```bash
git config user.name "Guru"
```

---

## Create Your First Git Repository

### Create a Project Directory

```bash
mkdir my-project
cd my-project
```

### Initialize Git

```bash
git init
```

Output:

```text
Initialized empty Git repository
```

---

## Check Repository Status

```bash
git status
```

This command displays:

* Modified files
* New files
* Staged files
* Current branch information

---

## Create Your First Commit

### Create a File

```bash
touch README.md
```

### Add the File

```bash
git add README.md
```

### Commit the Changes

```bash
git commit -m "Initial commit"
```

---

## Common Git Commands

### Repository Commands

| Command           | Description                  |
| ----------------- | ---------------------------- |
| `git init`        | Create a new repository      |
| `git clone <url>` | Clone an existing repository |
| `git status`      | Display repository status    |

### Staging Commands

| Command        | Description       |
| -------------- | ----------------- |
| `git add file` | Stage a file      |
| `git add .`    | Stage all changes |

### Commit Commands

| Command                   | Description         |
| ------------------------- | ------------------- |
| `git commit -m "message"` | Create a commit     |
| `git log`                 | View commit history |

### Branch Commands

| Command             | Description     |
| ------------------- | --------------- |
| `git branch`        | List branches   |
| `git branch name`   | Create a branch |
| `git checkout name` | Switch branches |

---

## Working with GitHub

### Clone a Repository

```bash
git clone https://github.com/username/repository.git
```

### Add a Remote Repository

```bash
git remote add origin https://github.com/username/repository.git
```

### Verify Remote

```bash
git remote -v
```

---

## Push Changes to GitHub

### Stage Changes

```bash
git add .
```

### Commit Changes

```bash
git commit -m "Add new content"
```

### Push Changes

```bash
git push origin main
```

---

## Pull Changes from GitHub

```bash
git pull origin main
```

Downloads and merges changes from the remote repository.

---

## Useful Git Commands

### View Commit History

```bash
git log
```

### Display One-Line History

```bash
git log --oneline
```

### Show Differences

```bash
git diff
```

### View Branches

```bash
git branch
```

---

## Uninstall Git

Remove Git from Fedora:

```bash
sudo dnf remove git
```

---

## Troubleshooting

### Git Command Not Found

Error:

```text
git: command not found
```

Verify installation:

```bash
rpm -qa | grep git
```

Check executable location:

```bash
which git
```

Expected Output:

```text
/usr/bin/git
```

---

### Verify Git Configuration

```bash
git config --list
```

Ensure that username and email are configured correctly.

---

## Summary

| Command                          | Purpose                 |
| -------------------------------- | ----------------------- |
| `sudo dnf install git`           | Install Git             |
| `git --version`                  | Check installed version |
| `git config --global user.name`  | Configure username      |
| `git config --global user.email` | Configure email         |
| `git init`                       | Initialize repository   |
| `git status`                     | View repository status  |
| `git add .`                      | Stage changes           |
| `git commit -m`                  | Create a commit         |
| `git log`                        | View commit history     |
| `git clone`                      | Clone a repository      |
| `git pull`                       | Download changes        |
| `git push`                       | Upload changes          |
| `git remote -v`                  | View configured remotes |

Git is an essential tool for software development and open-source contributions. Learning Git alongside Linux will significantly improve your development workflow and collaboration skills.

