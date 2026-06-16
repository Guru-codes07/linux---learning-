# Permission Commands

Permission commands are used to control access to files and directories by managing permissions, ownership, and groups.

## 1. chmod

**Full Form:** Change Mode

Changes the permissions of a file or directory.

### Syntax

```bash
chmod <permissions> <file_name>
```

### Example

```bash
$ chmod 755 script.sh
```

### Common Usage

| Command              | Description                                     |
| -------------------- | ----------------------------------------------- |
| `chmod 755 file.sh`  | Give owner full access, others read and execute |
| `chmod 644 file.txt` | Owner can read/write, others can only read      |
| `chmod +x script.sh` | Make a file executable                          |
| `chmod -w file.txt`  | Remove write permission                         |

#### Example: Make a Script Executable

```bash
$ chmod +x script.sh
$ ./script.sh
```

### Permission Numbers

| Number | Permission  |
| ------ | ----------- |
| 4      | Read (r)    |
| 2      | Write (w)   |
| 1      | Execute (x) |

#### Common Permission Sets

| Value | Meaning                                            |
| ----- | -------------------------------------------------- |
| 777   | Read, write, execute for everyone                  |
| 755   | Full access for owner, read and execute for others |
| 644   | Owner can read/write, others can read              |
| 600   | Only owner can read/write                          |

---

## 2. chown

**Full Form:** Change Owner

Changes the owner of a file or directory.

### Syntax

```bash
chown <owner> <file_name>
```

### Example

```bash
$ sudo chown guruprasad notes.txt
```

### Common Usage

| Command                          | Description                  |
| -------------------------------- | ---------------------------- |
| `sudo chown user file.txt`       | Change file owner            |
| `sudo chown user:group file.txt` | Change owner and group       |
| `sudo chown -R user folder`      | Change ownership recursively |

#### Example: Change Owner and Group

```bash
$ sudo chown guruprasad:developers project.txt
```

---

## 3. chgrp

**Full Form:** Change Group

Changes the group ownership of a file or directory.

### Syntax

```bash
chgrp <group> <file_name>
```

### Example

```bash
$ chgrp developers project.txt
```

### Common Usage

| Command                      | Description              |
| ---------------------------- | ------------------------ |
| `chgrp developers file.txt`  | Change file group        |
| `chgrp -R developers folder` | Change group recursively |

#### Example: Recursive Group Change

```bash
$ chgrp -R developers Projects/
```

---

## 4. umask

**Full Form:** User File Creation Mask

Controls the default permissions assigned to newly created files and directories.

### Syntax

```bash
umask
```

### Example

```bash
$ umask
0022
```

### Common Usage

| Command     | Description                   |
| ----------- | ----------------------------- |
| `umask`     | Display current umask value   |
| `umask 022` | Set default permission mask   |
| `umask 077` | Restrict access to owner only |

#### Example: Set a New Umask

```bash
$ umask 077
```

Newly created files will only be accessible by the owner.

---

## 5. ls -l

**Meaning:** View file permissions

Displays detailed information about file permissions, ownership, and groups.

### Syntax

```bash
ls -l
```

### Example

```bash
$ ls -l
-rwxr-xr-x 1 guruprasad users 120 Jun 15 script.sh
```

### Permission Breakdown

```text
-rwxr-xr-x
│││ │ │
│││ │ └── Others (r-x)
│││ └──── Group (r-x)
│└────── Owner (rwx)
└──────── File Type
```

#### Permission Symbols

| Symbol | Meaning       |
| ------ | ------------- |
| r      | Read          |
| w      | Write         |
| x      | Execute       |
| -      | No permission |

---

## Summary

| Command     | Purpose                             |
| ----------- | ----------------------------------- |
| `chmod`     | Change file permissions             |
| `chmod +x`  | Make a file executable              |
| `chmod 755` | Set common executable permissions   |
| `chmod 644` | Set common file permissions         |
| `chown`     | Change file owner                   |
| `chown -R`  | Change ownership recursively        |
| `chgrp`     | Change group ownership              |
| `chgrp -R`  | Change group recursively            |
| `umask`     | View or set default permissions     |
| `ls -l`     | View file permissions and ownership |

