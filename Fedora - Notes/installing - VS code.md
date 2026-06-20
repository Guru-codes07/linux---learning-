# Installing Visual Studio Code on Fedora

This guide explains how to install Visual Studio Code (VS Code) on Fedora Linux using the official Microsoft repository.

---

## What is Visual Studio Code?

Visual Studio Code (VS Code) is a free and lightweight source code editor developed by Microsoft.

It supports multiple programming languages and provides features such as:

* Syntax Highlighting
* IntelliSense
* Debugging
* Extensions
* Git Integration
* Integrated Terminal

Official Website:

```text
https://code.visualstudio.com
```

---

## Method 1: Install Using the Official Microsoft Repository (Recommended)

### Step 1: Import Microsoft's GPG Key

```bash
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
```

This key is used to verify packages downloaded from Microsoft's repository.

---

### Step 2: Add the VS Code Repository

Create the repository file:

```bash
sudo nano /etc/yum.repos.d/vscode.repo
```

Add the following content:

```ini
[code]
name=Visual Studio Code
baseurl=https://packages.microsoft.com/yumrepos/vscode
enabled=1
gpgcheck=1
gpgkey=https://packages.microsoft.com/keys/microsoft.asc
```

Save and exit.

---

### Step 3: Update Package Information

```bash
sudo dnf check-update
```

This refreshes package information from all configured repositories.

---

### Step 4: Install VS Code

```bash
sudo dnf install code
```

The package manager will automatically download and install VS Code and its dependencies.

---

### Step 5: Verify Installation

Check the installed version:

```bash
code --version
```

Example Output:

```text
1.124.2
xxxxxxxxxxxxxxxx
x64
```

---

## Launching VS Code

### From the Terminal

```bash
code
```

### Open Current Directory

```bash
code .
```

This opens the current folder in VS Code.

### From the Applications Menu

1. Press the Super (Windows) key.
2. Search for "Visual Studio Code".
3. Click the application icon.

---

## Updating VS Code

Since VS Code was installed through DNF, updates can be installed using:

```bash
sudo dnf update
```

Or update only VS Code:

```bash
sudo dnf update code
```

---

## Uninstalling VS Code

Remove VS Code from the system:

```bash
sudo dnf remove code
```

---

## Common Issues

### Repository Connection Error

Example:

```text
Curl error (56): Failure when receiving data from the peer
```

Possible causes:

* Temporary Microsoft server issues
* Network connectivity problems
* Firewall restrictions
* Proxy configuration issues

Solutions:

```bash
sudo dnf clean all
sudo dnf makecache
sudo dnf update
```

Then try installing again:

```bash
sudo dnf install code
```

---

### Command Not Found

Error:

```text
code: command not found
```

Verify installation:

```bash
rpm -qa | grep code
```

Check executable location:

```bash
which code
```

Expected Output:

```text
/usr/bin/code
```

---

## Useful VS Code Commands

### Open Current Folder

```bash
code .
```

### Open a Specific File

```bash
code main.cpp
```

### Open a Specific Directory

```bash
code ~/Projects
```

### Display Version Information

```bash
code --version
```

---

## Recommended Extensions for C/C++ Development

### C/C++ Extension

Provides:

* IntelliSense
* Debugging
* Code Navigation

### C/C++ Extension Pack

Includes several Microsoft C/C++ development tools.

### GitHub Copilot

AI-powered code suggestions.

### GitLens

Enhanced Git integration.

---

## Summary

| Command                 | Purpose                     |
| ----------------------- | --------------------------- |
| `sudo rpm --import`     | Import Microsoft GPG key    |
| `sudo dnf check-update` | Refresh package information |
| `sudo dnf install code` | Install VS Code             |
| `code`                  | Launch VS Code              |
| `code .`                | Open current directory      |
| `code --version`        | Display version             |
| `sudo dnf update code`  | Update VS Code              |
| `sudo dnf remove code`  | Uninstall VS Code           |

Visual Studio Code is one of the most popular code editors available on Linux and is widely used for C, C++, Python, Web Development, and Open Source projects.

