# Package Management Commands

Package management commands are used to install, update, remove, and manage software packages in Linux.

## 1. dnf

**Full Form:** Dandified YUM

DNF is the default package manager for Fedora and is used to manage software packages and dependencies.

### Syntax

```bash
dnf <command>
```

### Example

```bash
$ sudo dnf install git
```

### Common Usage

| Command                    | Description                   |
| -------------------------- | ----------------------------- |
| `sudo dnf install package` | Install a package             |
| `sudo dnf remove package`  | Remove a package              |
| `sudo dnf update`          | Update all installed packages |
| `sudo dnf upgrade`         | Upgrade the system            |
| `dnf search package`       | Search for a package          |
| `dnf info package`         | Display package information   |
| `dnf list installed`       | List installed packages       |

#### Example: Install a Package

```bash
$ sudo dnf install htop
```

#### Example: Remove a Package

```bash
$ sudo dnf remove htop
```

#### Example: Search for a Package

```bash
$ dnf search vscode
```

---

## 2. rpm

**Full Form:** RPM Package Manager

RPM is a low-level package management tool used to install, query, verify, and remove RPM packages.

### Syntax

```bash
rpm <option>
```

### Example

```bash
$ rpm -qa
```

### Common Usage

| Command                | Description                       |
| ---------------------- | --------------------------------- |
| `rpm -qa`              | List all installed packages       |
| `rpm -qi package`      | Display package information       |
| `rpm -ql package`      | List files installed by a package |
| `rpm -qf file`         | Find which package owns a file    |
| `rpm -ivh package.rpm` | Install an RPM package            |
| `rpm -e package`       | Remove an installed package       |

#### Example: View Package Information

```bash
$ rpm -qi git
```

#### Example: List Files Installed by a Package

```bash
$ rpm -ql git
```

---

## 3. dnf update

**Meaning:** Update installed packages

Downloads and installs the latest available versions of installed packages.

### Syntax

```bash
sudo dnf update
```

### Example

```bash
$ sudo dnf update
```

### Common Usage

| Command                   | Description                   |
| ------------------------- | ----------------------------- |
| `sudo dnf update`         | Update all installed packages |
| `sudo dnf update package` | Update a specific package     |

---

## 4. dnf install

**Meaning:** Install a package

Installs software from Fedora repositories.

### Syntax

```bash
sudo dnf install <package_name>
```

### Example

```bash
$ sudo dnf install git
```

### Common Usage

| Command                    | Description     |
| -------------------------- | --------------- |
| `sudo dnf install git`     | Install Git     |
| `sudo dnf install firefox` | Install Firefox |
| `sudo dnf install htop`    | Install htop    |

---

## 5. dnf remove

**Meaning:** Remove a package

Uninstalls software from the system.

### Syntax

```bash
sudo dnf remove <package_name>
```

### Example

```bash
$ sudo dnf remove htop
```

### Common Usage

| Command                   | Description                |
| ------------------------- | -------------------------- |
| `sudo dnf remove package` | Remove a package           |
| `sudo dnf autoremove`     | Remove unused dependencies |

---

## 6. dnf search

**Meaning:** Search for packages

Searches Fedora repositories for available packages.

### Syntax

```bash
dnf search <package_name>
```

### Example

```bash
$ dnf search docker
```

### Common Usage

| Command             | Description                        |
| ------------------- | ---------------------------------- |
| `dnf search vscode` | Search for VS Code                 |
| `dnf search python` | Search for Python-related packages |

---

## 7. dnf info

**Meaning:** Display package information

Shows details about a package.

### Syntax

```bash
dnf info <package_name>
```

### Example

```bash
$ dnf info git
```

### Common Usage

| Command           | Description                   |
| ----------------- | ----------------------------- |
| `dnf info git`    | View information about Git    |
| `dnf info docker` | View information about Docker |

---

## Summary

| Command              | Purpose                           |
| -------------------- | --------------------------------- |
| `dnf install`        | Install a package                 |
| `dnf remove`         | Remove a package                  |
| `dnf update`         | Update installed packages         |
| `dnf upgrade`        | Upgrade the system                |
| `dnf search`         | Search for packages               |
| `dnf info`           | View package information          |
| `dnf list installed` | List installed packages           |
| `rpm -qa`            | List all installed packages       |
| `rpm -qi`            | View package details              |
| `rpm -ql`            | List files installed by a package |
| `rpm -qf`            | Find which package owns a file    |
| `rpm -ivh`           | Install an RPM package            |
| `rpm -e`             | Remove an RPM package             |
