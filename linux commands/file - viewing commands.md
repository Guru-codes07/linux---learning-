
# File Viewing Commands

File viewing commands are used to read, inspect, and monitor the contents of files without modifying them.

## 1. cat

**Full Form:** Concatenate

Displays the contents of a file on the terminal.

### Syntax

```bash
cat <file_name>
```

### Example

```bash
$ cat notes.txt
Linux is awesome!
```

### Common Options

| Command           | Description                             |
| ----------------- | --------------------------------------- |
| `cat file.txt`    | Display file contents                   |
| `cat file1 file2` | Display multiple files                  |
| `cat -n file.txt` | Display file contents with line numbers |

#### Example: cat -n

```bash
$ cat -n notes.txt
1 Linux is awesome!
2 Learning Linux daily.
```

---

## 2. less

**Meaning:** View file contents one page at a time

Useful for viewing large files.

### Syntax

```bash
less <file_name>
```

### Example

```bash
$ less logfile.txt
```

### Common Usage

| Command            | Description               |
| ------------------ | ------------------------- |
| `less file.txt`    | View a file page by page  |
| `less +G file.txt` | Open at the end of a file |

#### Navigation Inside less

| Key     | Action        |
| ------- | ------------- |
| `Space` | Next page     |
| `b`     | Previous page |
| `q`     | Quit          |

---

## 3. head

**Meaning:** Display the beginning of a file

Shows the first 10 lines of a file by default.

### Syntax

```bash
head <file_name>
```

### Example

```bash
$ head notes.txt
Line 1
Line 2
Line 3
...
```

### Common Options

| Command              | Description            |
| -------------------- | ---------------------- |
| `head file.txt`      | Display first 10 lines |
| `head -n 5 file.txt` | Display first 5 lines  |

#### Example: head -n 5

```bash
$ head -n 5 notes.txt
```

---

## 4. tail

**Meaning:** Display the end of a file

Shows the last 10 lines of a file by default.

### Syntax

```bash
tail <file_name>
```

### Example

```bash
$ tail notes.txt
Last line
```

### Common Options

| Command               | Description                 |
| --------------------- | --------------------------- |
| `tail file.txt`       | Display last 10 lines       |
| `tail -n 5 file.txt`  | Display last 5 lines        |
| `tail -f logfile.txt` | Monitor a file in real time |

#### Example: tail -f

```bash
$ tail -f server.log
```

Useful for monitoring logs as new entries are added.

---

## Summary

| Command   | Purpose                                               |
| --------- | ----------------------------------------------------- |
| `cat`     | Display file contents                                 |
| `cat -n`  | Display contents with line numbers                    |
| `less`    | View large files page by page                         |
| `head`    | Display the beginning of a file                       |
| `head -n` | Display a specific number of lines from the beginning |
| `tail`    | Display the end of a file                             |
| `tail -n` | Display a specific number of lines from the end       |
| `tail -f` | Monitor a file in real time                           |
