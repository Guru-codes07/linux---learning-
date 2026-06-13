# Navigation Commands

Navigation commands help you move around the Linux file system and view the contents of directories.

## 1. pwd

**Full Form:** Print Working Directory

Displays the absolute path of the current working directory.

### Syntax

```bash
pwd
```

### Example

```bash
$ pwd
/home/guruprasad
```

---

## 2. ls

**Meaning:** List files and directories

Displays the contents of a directory.

### Syntax

```bash
ls
```

### Example

```bash
$ ls
Documents Downloads Pictures Videos
```

### Common Options

| Command  | Description                                              |
| -------- | -------------------------------------------------------- |
| `ls -l`  | Display files and directories in long format             |
| `ls -a`  | Display all files, including hidden files                |
| `ls -la` | Display all files in long format, including hidden files |
| `ls -lh` | Display file sizes in a human-readable format            |

#### Example: ls -l

```bash
$ ls -l
drwxr-xr-x 2 guruprasad users 4096 Jun 13 Documents
-rw-r--r-- 1 guruprasad users 120 Jun 13 notes.txt
```

#### Example: ls -a

```bash
$ ls -a
.  ..  .bashrc  Documents  Downloads
```

---

## 3. cd

**Full Form:** Change Directory

Used to navigate between directories.

### Syntax

```bash
cd <directory>
```

### Common Usage

| Command                         | Description                     |
| ------------------------------- | ------------------------------- |
| `cd Documents`                  | Move to the Documents directory |
| `cd ..`                         | Move to the parent directory    |
| `cd ~`                          | Move to the home directory      |
| `cd /`                          | Move to the root directory      |
| `cd -`                          | Move to the previous directory  |
| `cd /home/guruprasad/Documents` | Move using an absolute path     |

### Example

```bash
$ cd Documents
$ pwd
/home/guruprasad/Documents
```

---

## 4. clear

**Meaning:** Clear the terminal screen

Clears all visible output from the terminal window.

### Syntax

```bash
clear
```

### Example

```bash
$ clear
```

The terminal screen is cleared.

---

## Summary

| Command  | Purpose                               |
| -------- | ------------------------------------- |
| `pwd`    | Display the current working directory |
| `ls`     | List files and directories            |
| `ls -l`  | Long listing format                   |
| `ls -a`  | Show hidden files                     |
| `ls -la` | Long listing including hidden files   |
| `ls -lh` | Human-readable file sizes             |
| `cd`     | Change directory                      |
| `cd ..`  | Move to the parent directory          |
| `cd ~`   | Move to the home directory            |
| `cd /`   | Move to the root directory            |
| `cd -`   | Move to the previous directory        |
| `clear`  | Clear the terminal screen             |

```
```

