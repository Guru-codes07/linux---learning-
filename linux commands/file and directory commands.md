# File & Directory Operations

File and directory operation commands are used to create, copy, move, rename, and delete files and directories.

## 1. mkdir

**Full Form:** Make Directory

Creates a new directory.

### Syntax

```bash
mkdir <directory_name>
```

### Example

```bash
$ mkdir projects
```

### Common Options

| Command                 | Description                   |
| ----------------------- | ----------------------------- |
| `mkdir test`            | Create a directory named test |
| `mkdir dir1 dir2`       | Create multiple directories   |
| `mkdir -p parent/child` | Create nested directories     |

#### Example: mkdir -p

```bash
$ mkdir -p cpp/basics
```

---

## 2. rmdir

**Full Form:** Remove Directory

Removes an empty directory.

### Syntax

```bash
rmdir <directory_name>
```

### Example

```bash
$ rmdir projects
```

### Common Options

| Command                 | Description                     |
| ----------------------- | ------------------------------- |
| `rmdir test`            | Remove an empty directory       |
| `rmdir -p parent/child` | Remove nested empty directories |

---

## 3. touch

**Meaning:** Create an empty file or update file timestamps

Creates a new empty file if it does not exist.

### Syntax

```bash
touch <file_name>
```

### Example

```bash
$ touch notes.txt
```

### Common Usage

| Command             | Description           |
| ------------------- | --------------------- |
| `touch file.txt`    | Create a file         |
| `touch file1 file2` | Create multiple files |

---

## 4. cp

**Full Form:** Copy

Copies files and directories from one location to another.

### Syntax

```bash
cp <source> <destination>
```

### Example

```bash
$ cp notes.txt backup.txt
```

### Common Options

| Command             | Description                  |
| ------------------- | ---------------------------- |
| `cp file1 file2`    | Copy a file                  |
| `cp -r dir1 dir2`   | Copy a directory recursively |
| `cp -i file1 file2` | Ask before overwriting       |

#### Example: cp -r

```bash
$ cp -r Projects Backup
```

---

## 5. mv

**Full Form:** Move

Moves or renames files and directories.

### Syntax

```bash
mv <source> <destination>
```

### Example

```bash
$ mv notes.txt Documents/
```

### Common Usage

| Command                  | Description        |
| ------------------------ | ------------------ |
| `mv file.txt Documents/` | Move a file        |
| `mv old.txt new.txt`     | Rename a file      |
| `mv dir1 dir2`           | Rename a directory |

#### Example: Rename a File

```bash
$ mv notes.txt notes_old.txt
```

---

## 6. rm

**Full Form:** Remove

Deletes files and directories.

### Syntax

```bash
rm <file_name>
```

### Example

```bash
$ rm notes.txt
```

### Common Options

| Command          | Description                          |
| ---------------- | ------------------------------------ |
| `rm file.txt`    | Delete a file                        |
| `rm -r folder`   | Delete a directory and its contents  |
| `rm -f file.txt` | Force delete without confirmation    |
| `rm -rf folder`  | Force delete a directory recursively |

#### Example: rm -r

```bash
$ rm -r old_projects
```

---

## Summary

| Command    | Purpose                              |
| ---------- | ------------------------------------ |
| `mkdir`    | Create a directory                   |
| `mkdir -p` | Create nested directories            |
| `rmdir`    | Remove an empty directory            |
| `touch`    | Create a file                        |
| `cp`       | Copy files and directories           |
| `cp -r`    | Copy directories recursively         |
| `mv`       | Move or rename files and directories |
| `rm`       | Delete a file                        |
| `rm -r`    | Delete a directory recursively       |
| `rm -f`    | Force delete a file                  |
| `rm -rf`   | Force delete a directory recursively |

