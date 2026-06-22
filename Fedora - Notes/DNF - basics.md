# DNF Basics

DNF (Dandified YUM) is the default package manager used in Fedora.

It is responsible for installing, updating, removing, and managing software packages on the system.

---

## What is DNF?

DNF helps users:

* Install software
* Update software
* Remove software
* Search for packages
* Manage dependencies
* Update the operating system

---

## Check DNF Version

### Command

```bash
dnf --version
```

### Example Output

```text
4.23.0
```

---

## Refresh Package Information

Before installing software, refresh repository metadata.

### Command

```bash
sudo dnf check-update
```

This checks for available package updates.

---

## Install a Package

### Syntax

```bash
sudo dnf install <package_name>
```

### Example

```bash
sudo dnf install git
```

---

## Install Multiple Packages

### Example

```bash
sudo dnf install git gcc gcc-c++
```

---

## Remove a Package

### Syntax

```bash
sudo dnf remove <package_name>
```

### Example

```bash
sudo dnf remove git
```

---

## Search for a Package

### Syntax

```bash
dnf search <package_name>
```

### Example

```bash
dnf search vscode
```

---

## View Package Information

### Syntax

```bash
dnf info <package_name>
```

### Example

```bash
dnf info git
```

This displays:

* Package version
* Description
* Repository information
* Package size

---

## List Installed Packages

### Command

```bash
dnf list installed
```

---

## Update All Packages

### Command

```bash
sudo dnf update
```

This downloads and installs available updates.

---

## Upgrade the System

### Command

```bash
sudo dnf upgrade
```

Updates packages and performs system upgrades.

---

## Clean DNF Cache

DNF stores downloaded metadata and packages in a cache.

### Command

```bash
sudo dnf clean all
```

Useful when troubleshooting repository issues.

---

## Rebuild Cache

### Command

```bash
sudo dnf makecache
```

Downloads fresh repository metadata.

---

## List Available Repositories

### Command

```bash
dnf repolist
```

Example Output:

```text
fedora
updates
rpmfusion-free
```

---

## Enable a Repository

### Syntax

```bash
sudo dnf config-manager --set-enabled repository
```

---

## Display Package Dependencies

### Example

```bash
dnf repoquery --requires git
```

Shows packages required by Git.

---

## Common DNF Workflow

### Update Repository Information

```bash
sudo dnf check-update
```

### Install Software

```bash
sudo dnf install git
```

### Verify Installation

```bash
git --version
```

### Update Software

```bash
sudo dnf update
```

---

## Common Errors

### Failed to Download Metadata

Possible causes:

* Internet connection problems
* Repository issues

Solution:

```bash
sudo dnf clean all
sudo dnf makecache
```

---

### Transaction Lock Error

Example:

```text
Failed to obtain transaction lock
```

Cause:

Another DNF process is already running.

Check:

```bash
ps aux | grep dnf
```

---

## Summary

| Command                    | Purpose                   |
| -------------------------- | ------------------------- |
| `dnf --version`            | Display DNF version       |
| `sudo dnf install package` | Install a package         |
| `sudo dnf remove package`  | Remove a package          |
| `dnf search package`       | Search for packages       |
| `dnf info package`         | View package information  |
| `dnf list installed`       | List installed packages   |
| `sudo dnf update`          | Update installed packages |
| `sudo dnf upgrade`         | Upgrade the system        |
| `sudo dnf clean all`       | Clean DNF cache           |
| `sudo dnf makecache`       | Rebuild package cache     |
| `dnf repolist`             | Display repositories      |

DNF is one of the most important tools in Fedora because nearly all software installation and system maintenance tasks are performed through it.

