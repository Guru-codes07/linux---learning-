# Common Fixes on Fedora

This document contains common Linux and Fedora issues that I encountered while learning Linux, along with their solutions.

---

# VS Code Repository Error

## Problem

While updating or installing Visual Studio Code, DNF displayed the following error:

```text
Curl error (56): Failure when receiving data from the peer
```

## Cause

Possible causes:

* Temporary Microsoft server issues
* Internet connectivity problems
* Repository synchronization issues
* Corrupted DNF cache

## Solution

Clean DNF cache:

```bash
sudo dnf clean all
```

Rebuild package cache:

```bash
sudo dnf makecache
```

Update repositories:

```bash
sudo dnf check-update
```

Try again:

```bash
sudo dnf install code
```

---

# GCC Command Not Found

## Problem

```text
gcc: command not found
```

## Cause

GCC compiler is not installed.

## Solution

Install GCC:

```bash
sudo dnf install gcc
```

Verify installation:

```bash
gcc --version
```

---

# G++ Command Not Found

## Problem

```text
g++: command not found
```

## Cause

C++ compiler is not installed.

## Solution

Install G++:

```bash
sudo dnf install gcc-c++
```

Verify installation:

```bash
g++ --version
```

---

# Git Command Not Found

## Problem

```text
git: command not found
```

## Cause

Git is not installed.

## Solution

Install Git:

```bash
sudo dnf install git
```

Verify installation:

```bash
git --version
```

---

# Permission Denied While Running a Script

## Problem

```text
Permission denied
```

Example:

```bash
./script.sh
```

## Cause

The script does not have execute permission.

## Solution

Grant execute permission:

```bash
chmod +x script.sh
```

Run again:

```bash
./script.sh
```

---

# Permission Denied While Accessing a File

## Problem

```text
Permission denied
```

## Cause

Current user does not have the required permissions.

## Solution

Check permissions:

```bash
ls -l
```

Modify permissions:

```bash
chmod 644 filename
```

Or use administrative privileges:

```bash
sudo command
```

---

# DNF Lock Error

## Problem

```text
Waiting for process with pid ...
```

or

```text
Failed to obtain the transaction lock
```

## Cause

Another DNF process is already running.

## Solution

Wait for the current update process to finish.

Check running DNF processes:

```bash
ps aux | grep dnf
```

---

# Unable to Install Packages

## Problem

```text
Failed to download metadata
```

## Cause

Internet connection problems or repository issues.

## Solution

Check connectivity:

```bash
ping google.com
```

Refresh repositories:

```bash
sudo dnf clean all
sudo dnf makecache
```

---

# VS Code C/C++ Extension Not Working

## Problem

IntelliSense, debugging, or compilation features do not work.

## Cause

Required extensions or compilers are missing.

## Solution

Install:

* C/C++ Extension
* C/C++ Extension Pack

Install required compilers:

```bash
sudo dnf install gcc
sudo dnf install gcc-c++
```

---

# Launch.json Not Found

## Problem

VS Code asks for configuration again when opening a new folder.

## Cause

The `.vscode` directory is created per project folder.

Each folder has its own configuration.

## Solution

Create a `.vscode` directory inside the project.

Or keep multiple programs inside one workspace folder.

Example:

```text
c-programming/
├── .vscode/
├── basics/
├── pointers/
└── arrays/
```

---

# Code Command Not Found

## Problem

```text
code: command not found
```

## Cause

VS Code is not properly installed or the executable is not in the PATH.

## Solution

Check installation:

```bash
which code
```

Expected output:

```text
/usr/bin/code
```

Reinstall VS Code if necessary:

```bash
sudo dnf reinstall code
```

---

# Git Push Authentication Error

## Problem

```text
Authentication failed
```

## Cause

Incorrect credentials or missing GitHub authentication setup.

## Solution

Verify remote repository:

```bash
git remote -v
```

Use GitHub Personal Access Tokens (PAT) instead of passwords.

Check Git configuration:

```bash
git config --list
```

---

# SSH Connection Refused

## Problem

```text
Connection refused
```

## Cause

SSH service is not running on the target machine.

## Solution

Check SSH service:

```bash
sudo systemctl status sshd
```

Start SSH service:

```bash
sudo systemctl start sshd
```

Enable it at boot:

```bash
sudo systemctl enable sshd
```

---

# Summary

| Problem                  | Solution                        |
| ------------------------ | ------------------------------- |
| VS Code Curl Error       | Clean DNF cache and retry       |
| GCC Not Found            | Install GCC                     |
| G++ Not Found            | Install GCC-C++                 |
| Git Not Found            | Install Git                     |
| Permission Denied        | Fix permissions with chmod      |
| DNF Lock Error           | Wait for DNF process to finish  |
| Package Install Failure  | Refresh repositories            |
| VS Code Extension Issues | Install required extensions     |
| Launch.json Missing      | Configure each project folder   |
| Code Command Not Found   | Reinstall VS Code               |
| Git Authentication Error | Configure GitHub authentication |
| SSH Connection Refused   | Start SSH service               |

As I continue learning Linux and Fedora, I will update this document with additional issues and their solutions.

