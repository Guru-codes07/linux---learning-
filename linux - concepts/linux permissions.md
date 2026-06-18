# Linux Permissions

Linux permissions determine who can read, write, or execute files and directories.

Permissions are one of the core security features of Linux and are used to control access to system resources.

---

## Understanding Permissions

Every file and directory has three permission groups:

| Category   | Description                         |
| ---------- | ----------------------------------- |
| User (u)   | Owner of the file                   |
| Group (g)  | Users belonging to the file's group |
| Others (o) | Everyone else                       |

---

## Permission Types

| Symbol | Meaning       |
| ------ | ------------- |
| r      | Read          |
| w      | Write         |
| x      | Execute       |
| -      | No Permission |

### Example

```text
-rwxr-xr--
```

### Breakdown

```text
-rwxr-xr--
│││ │ │
│││ │ └── Others (r--)
│││ └──── Group (r-x)
│└────── Owner (rwx)
└──────── File Type
```

---

## Read Permission (r)

Allows a user to view the contents of a file.

### Example

```bash
cat notes.txt
```

Without read permission, the file contents cannot be viewed.

---

## Write Permission (w)

Allows a user to modify a file.

### Example

```bash
echo "Linux" >> notes.txt
```

Without write permission, changes cannot be saved.

---

## Execute Permission (x)

Allows a file to be executed as a program or script.

### Example

```bash
chmod +x script.sh
./script.sh
```

---

## Numeric Permissions

Linux represents permissions using numbers.

### Values

| Number | Permission |
| ------ | ---------- |
| 4      | Read       |
| 2      | Write      |
| 1      | Execute    |

Permissions are calculated by adding these values.

### Examples

| Permission | Value |
| ---------- | ----- |
| r--        | 4     |
| rw-        | 6     |
| rwx        | 7     |
| r-x        | 5     |

---

## Common Permission Values

### 777

```text
rwxrwxrwx
```

Everyone can read, write, and execute.

⚠️ Generally not recommended.

---

### 755

```text
rwxr-xr-x
```

Owner has full access.

Group and others can read and execute.

Commonly used for executable files and directories.

---

### 700

```text
rwx------
```

Only the owner has access.

---

### 644

```text
rw-r--r--
```

Owner can read and write.

Everyone else can only read.

Commonly used for text files.

---

### 600

```text
rw-------
```

Only the owner can read and write.

Often used for private files and SSH keys.

---

## File Permissions vs Directory Permissions

### File Permissions

| Permission | Meaning              |
| ---------- | -------------------- |
| r          | Read file contents   |
| w          | Modify file contents |
| x          | Execute the file     |

### Directory Permissions

| Permission | Meaning                         |
| ---------- | ------------------------------- |
| r          | View directory contents         |
| w          | Create, rename, or delete files |
| x          | Enter the directory             |

---

## Viewing Permissions

Use:

```bash
ls -l
```

Example:

```bash
$ ls -l

-rw-r--r-- 1 guruprasad users 120 Jun 15 notes.txt
-rwxr-xr-x 1 guruprasad users 250 Jun 15 script.sh
```

---

## Changing Permissions

Use:

```bash
chmod
```

Examples:

```bash
chmod 755 script.sh
chmod 644 notes.txt
chmod +x script.sh
chmod -w notes.txt
```

---

## Why Permissions Matter

Permissions help:

* Protect sensitive files
* Prevent accidental modifications
* Control access between users
* Improve system security
* Secure servers and applications

Without proper permissions, any user could modify important system files.

---

## Summary

| Permission | Meaning                                    |
| ---------- | ------------------------------------------ |
| r          | Read                                       |
| w          | Write                                      |
| x          | Execute                                    |
| 755        | Owner full access, others read and execute |
| 644        | Owner read/write, others read only         |
| 700        | Owner full access only                     |
| 600        | Owner read/write only                      |

### Important Commands

```bash
ls -l
chmod 755 file.sh
chmod 644 file.txt
chmod +x script.sh
```

Understanding Linux permissions is essential for system administration, software development, shell scripting, and server management.

