# Help Commands

Help commands provide documentation, usage information, and guidance for Linux commands and utilities.

## 1. man

**Full Form:** Manual

Displays the manual page for a command.

### Syntax

```bash
man <command>
```

### Example

```bash
$ man ls
```

### Common Usage

| Command    | Description                     |
| ---------- | ------------------------------- |
| `man ls`   | View the manual page for `ls`   |
| `man cp`   | View the manual page for `cp`   |
| `man grep` | View the manual page for `grep` |

#### Navigation Inside man

| Key        | Action               |
| ---------- | -------------------- |
| `Space`    | Next page            |
| `b`        | Previous page        |
| `/keyword` | Search for a keyword |
| `n`        | Next search result   |
| `q`        | Quit                 |

---

## 2. --help

**Meaning:** Display command help information

Most Linux commands support the `--help` option, which displays a brief description of the command and its available options.

### Syntax

```bash
<command> --help
```

### Example

```bash
$ ls --help
```

### Common Usage

| Command       | Description             |
| ------------- | ----------------------- |
| `ls --help`   | Display help for `ls`   |
| `cp --help`   | Display help for `cp`   |
| `grep --help` | Display help for `grep` |

#### Example Output

```bash
$ mkdir --help
Usage: mkdir [OPTION]... DIRECTORY...
Create the DIRECTORY(ies), if they do not already exist.
```

---

## 3. info

**Meaning:** Display detailed documentation

Provides more detailed and structured documentation than `man` for supported commands.

### Syntax

```bash
info <command>
```

### Example

```bash
$ info ls
```

### Common Usage

| Command          | Description                               |
| ---------------- | ----------------------------------------- |
| `info ls`        | View detailed documentation for `ls`      |
| `info coreutils` | View documentation for GNU Core Utilities |

#### Navigation Inside info

| Key         | Action        |
| ----------- | ------------- |
| `Space`     | Next page     |
| `Backspace` | Previous page |
| `n`         | Next node     |
| `p`         | Previous node |
| `q`         | Quit          |

---

## 4. whatis

**Meaning:** Display a short description of a command

Provides a one-line description of a command from the manual database.

### Syntax

```bash
whatis <command>
```

### Example

```bash
$ whatis grep
grep (1) - print lines that match patterns
```

### Common Usage

| Command        | Description                         |
| -------------- | ----------------------------------- |
| `whatis ls`    | Show a short description of `ls`    |
| `whatis chmod` | Show a short description of `chmod` |

---

## 5. apropos

**Meaning:** Search manual pages by keyword

Searches manual page descriptions for a given keyword.

### Syntax

```bash
apropos <keyword>
```

### Example

```bash
$ apropos copy
```

### Common Usage

| Command           | Description                               |
| ----------------- | ----------------------------------------- |
| `apropos file`    | Search for commands related to files      |
| `apropos network` | Search for commands related to networking |
| `apropos copy`    | Search for commands related to copying    |

#### Example Output

```bash
$ apropos copy
cp (1) - copy files and directories
dd (1) - convert and copy a file
```

---

## Summary

| Command   | Purpose                               |
| --------- | ------------------------------------- |
| `man`     | Display a command's manual page       |
| `--help`  | Display quick help information        |
| `info`    | Display detailed documentation        |
| `whatis`  | Show a short description of a command |
| `apropos` | Search commands by keyword            |

