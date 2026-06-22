# Updating Fedora

Keeping Fedora updated is important for security, stability, bug fixes, and access to the latest software features.

This guide explains how to update Fedora using DNF.

---

## Why Update Fedora?

Updating Fedora provides:

* Security patches
* Bug fixes
* Performance improvements
* New software features
* Hardware compatibility updates

Regular updates help keep your system secure and stable.

---

## Check for Available Updates

Before updating, check whether updates are available.

### Command

```bash
sudo dnf check-update
```

### Example Output

```text
git.x86_64            2.50.1-1.fc42
firefox.x86_64        141.0-1.fc42
```

This indicates that newer versions are available.

---

## Update Installed Packages

Update all installed packages:

```bash
sudo dnf update
```

DNF will:

* Download available updates
* Resolve dependencies
* Install updated packages

---

## Upgrade the System

Fedora also supports:

```bash
sudo dnf upgrade
```

This performs a full system upgrade and is commonly used to keep the system current.

---

## Update a Specific Package

### Syntax

```bash
sudo dnf update <package_name>
```

### Example

```bash
sudo dnf update git
```

Only the specified package will be updated.

---

## Update VS Code

Example:

```bash
sudo dnf update code
```

This updates Visual Studio Code if a newer version is available.

---

## Update Git

Example:

```bash
sudo dnf update git
```

---

## Refresh Repository Metadata

Sometimes package information becomes outdated.

Refresh repository metadata:

```bash
sudo dnf makecache
```

---

## Clean DNF Cache

DNF stores downloaded metadata and packages in a cache.

Clear cached data:

```bash
sudo dnf clean all
```

This is useful when troubleshooting update issues.

---

## Recommended Update Workflow

### Step 1: Refresh Package Information

```bash
sudo dnf check-update
```

### Step 2: Update Packages

```bash
sudo dnf update
```

### Step 3: Reboot if Necessary

```bash
sudo reboot
```

A reboot may be required after:

* Kernel updates
* System library updates
* Major system updates

---

## Check Fedora Version

Display the current Fedora version:

```bash
cat /etc/fedora-release
```

Example Output:

```text
Fedora Linux 42 (Workstation Edition)
```

---

## Check Installed Kernel Version

Display the currently running kernel:

```bash
uname -r
```

Example Output:

```text
6.15.3-200.fc42.x86_64
```

---

## View Update History

List recent DNF transactions:

```bash
dnf history
```

Example Output:

```text
ID | Command Line      | Date and Time
1  | install git       | 2025-06-15
2  | update            | 2025-06-20
```

---

## Upgrade to a New Fedora Release

Example:

```bash
sudo dnf system-upgrade download --releasever=43
```

Then reboot:

```bash
sudo dnf system-upgrade reboot
```

This is used when moving from one Fedora release to another.

---

## Common Problems

### Failed to Download Metadata

Example:

```text
Failed to download metadata
```

### Solution

```bash
sudo dnf clean all
sudo dnf makecache
```

Then retry:

```bash
sudo dnf update
```

---

### Transaction Lock Error

Example:

```text
Failed to obtain transaction lock
```

### Cause

Another DNF process is already running.

### Check Running Processes

```bash
ps aux | grep dnf
```

Wait for the existing process to finish.

---

### Curl Error While Updating

Example:

```text
Curl error (56): Failure when receiving data from the peer
```

### Possible Causes

* Temporary repository issues
* Internet connectivity problems
* Server-side issues

### Solution

```bash
sudo dnf clean all
sudo dnf makecache
sudo dnf update
```

---

## Useful Commands

### Check Updates

```bash
sudo dnf check-update
```

### Update Everything

```bash
sudo dnf update
```

### Upgrade System

```bash
sudo dnf upgrade
```

### Clean Cache

```bash
sudo dnf clean all
```

### Rebuild Cache

```bash
sudo dnf makecache
```

### View Fedora Version

```bash
cat /etc/fedora-release
```

### View Kernel Version

```bash
uname -r
```

---

## Summary

| Command                   | Purpose                     |
| ------------------------- | --------------------------- |
| `sudo dnf check-update`   | Check available updates     |
| `sudo dnf update`         | Update installed packages   |
| `sudo dnf upgrade`        | Upgrade the system          |
| `sudo dnf update package` | Update a specific package   |
| `sudo dnf clean all`      | Clean DNF cache             |
| `sudo dnf makecache`      | Refresh repository metadata |
| `dnf history`             | View update history         |
| `cat /etc/fedora-release` | Display Fedora version      |
| `uname -r`                | Display kernel version      |
| `sudo reboot`             | Reboot the system           |

Updating Fedora regularly helps maintain a secure, stable, and up-to-date Linux system. It is one of the most important maintenance tasks for any Fedora user.

