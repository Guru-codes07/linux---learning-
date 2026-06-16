# Search Commands

Search commands help you locate files, directories, commands, and specific text within files.

## 1. find

**Meaning:** Search for files and directories

Searches for files and directories in a specified location.

### Syntax

```bash
find <path> <options>
```

### Example

```bash
$ find . -name "notes.txt"
./Documents/notes.txt
```

### Common Options

| Command                   | Description               |
| ------------------------- | ------------------------- |
| `find . -name "file.txt"` | Search for a file by name |
| `find . -type d`          | Search for directories    |
| `find . -type f`          | Search for files          |
| `find . -name "*.cpp"`    | Search for all C++ files  |

#### Example: Find All C++ Files

```bash
$ find . -name "*.cpp"
./main.cpp
./DSA/arrays.cpp
```

---

## 2. grep

**Full Form:** Global Regular Expression Print

Searches for specific text patterns inside files.

### Syntax

```bash
grep <pattern> <file>
```

### Example

```bash
$ grep "Linux" notes.txt
Linux is awesome!
```

### Common Options

| Command                   | Description                       |
| ------------------------- | --------------------------------- |
| `grep "text" file.txt`    | Search for text in a file         |
| `grep -i "text" file.txt` | Ignore case while searching       |
| `grep -n "text" file.txt` | Show line numbers                 |
| `grep -r "text" folder`   | Search recursively in directories |

#### Example: grep -n

```bash
$ grep -n "Linux" notes.txt
5: Linux is awesome!
```

---

## 3. locate

**Meaning:** Quickly find files using a database

Searches for files using a pre-built database, making it faster than `find`.

### Syntax

```bash
locate <file_name>
```

### Example

```bash
$ locate notes.txt
/home/guruprasad/Documents/notes.txt
```

### Common Usage

| Command           | Description             |
| ----------------- | ----------------------- |
| `locate file.txt` | Locate a file           |
| `locate "*.cpp"`  | Locate C++ source files |

#### Update Database

```bash
$ sudo updatedb
```

Updates the locate database.

---

## 4. which

**Meaning:** Locate the executable path of a command

Displays the path of the command that will be executed.

### Syntax

```bash
which <command>
```

### Example

```bash
$ which python
/usr/bin/python
```

### Common Usage

| Command        | Description                 |
| -------------- | --------------------------- |
| `which python` | Show Python executable path |
| `which gcc`    | Show GCC executable path    |
| `which git`    | Show Git executable path    |

---

## 5. whereis

**Meaning:** Locate a command, source files, and manual pages

Displays the binary, source code, and manual page locations of a command.

### Syntax

```bash
whereis <command>
```

### Example

```bash
$ whereis gcc
gcc: /usr/bin/gcc /usr/share/man/man1/gcc.1.gz
```

### Common Usage

| Command          | Description         |
| ---------------- | ------------------- |
| `whereis gcc`    | Locate GCC files    |
| `whereis python` | Locate Python files |
| `whereis git`    | Locate Git files    |

---

## Summary

| Command        | Purpose                                        |
| -------------- | ---------------------------------------------- |
| `find`         | Search for files and directories               |
| `find -name`   | Search by file name                            |
| `find -type f` | Search for files only                          |
| `find -type d` | Search for directories only                    |
| `grep`         | Search for text inside files                   |
| `grep -i`      | Ignore case while searching                    |
| `grep -n`      | Show line numbers                              |
| `grep -r`      | Search recursively                             |
| `locate`       | Quickly find files using a database            |
| `updatedb`     | Update the locate database                     |
| `which`        | Show the executable path of a command          |
| `whereis`      | Show binary, source, and manual page locations |
