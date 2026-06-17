# Process Management Commands

Process management commands help monitor, control, and manage running programs (processes) in Linux.

## 1. ps

**Full Form:** Process Status

Displays information about currently running processes.

### Syntax

```bash
ps
```

### Example

```bash
$ ps
PID TTY          TIME CMD
1234 pts/0    00:00:00 bash
5678 pts/0    00:00:00 ps
```

### Common Options

| Command  | Description                                   |
| -------- | --------------------------------------------- |
| `ps`     | Show processes in the current terminal        |
| `ps -e`  | Show all running processes                    |
| `ps -ef` | Show detailed information about all processes |
| `ps aux` | Display all processes with resource usage     |

#### Example: ps aux

```bash
$ ps aux
```

---

## 2. top

**Meaning:** Display running processes in real time

Provides a live view of CPU usage, memory usage, and active processes.

### Syntax

```bash
top
```

### Example

```bash
$ top
```

### Common Usage

| Key | Action               |
| --- | -------------------- |
| `q` | Quit                 |
| `k` | Kill a process       |
| `M` | Sort by memory usage |
| `P` | Sort by CPU usage    |

---

## 3. htop

**Meaning:** Interactive process viewer

An improved and more user-friendly alternative to `top`.

### Syntax

```bash
htop
```

### Example

```bash
$ htop
```

### Installation (Fedora)

```bash
$ sudo dnf install htop
```

### Common Features

| Feature    | Description        |
| ---------- | ------------------ |
| Arrow Keys | Navigate processes |
| F9         | Kill a process     |
| F6         | Change sorting     |
| F10        | Quit               |

---

## 4. kill

**Meaning:** Terminate a process using its PID

Sends a signal to a running process.

### Syntax

```bash
kill <PID>
```

### Example

```bash
$ kill 1234
```

### Common Usage

| Command       | Description                    |
| ------------- | ------------------------------ |
| `kill PID`    | Gracefully terminate a process |
| `kill -9 PID` | Forcefully terminate a process |

#### Example: Force Kill

```bash
$ kill -9 1234
```

---

## 5. killall

**Meaning:** Terminate processes by name

Kills all processes with a specified name.

### Syntax

```bash
killall <process_name>
```

### Example

```bash
$ killall firefox
```

### Common Usage

| Command           | Description                 |
| ----------------- | --------------------------- |
| `killall firefox` | Close all Firefox processes |
| `killall code`    | Close all VS Code processes |

---

## 6. jobs

**Meaning:** Display background jobs

Shows jobs running in the current shell session.

### Syntax

```bash
jobs
```

### Example

```bash
$ jobs
[1]+ Running sleep 100 &
```

### Common Usage

| Command   | Description                  |
| --------- | ---------------------------- |
| `jobs`    | List current jobs            |
| `jobs -l` | Show job IDs and process IDs |

---

## 7. bg

**Meaning:** Background

Resumes a suspended job in the background.

### Syntax

```bash
bg %job_number
```

### Example

```bash
$ bg %1
```

### Common Usage

| Command | Description                    |
| ------- | ------------------------------ |
| `bg %1` | Resume job 1 in the background |

---

## 8. fg

**Meaning:** Foreground

Brings a background job to the foreground.

### Syntax

```bash
fg %job_number
```

### Example

```bash
$ fg %1
```

### Common Usage

| Command | Description                   |
| ------- | ----------------------------- |
| `fg %1` | Bring job 1 to the foreground |

---

## Summary

| Command   | Purpose                        |
| --------- | ------------------------------ |
| `ps`      | Display running processes      |
| `ps -e`   | Display all processes          |
| `ps aux`  | Detailed process information   |
| `top`     | Real-time process monitoring   |
| `htop`    | Interactive process viewer     |
| `kill`    | Terminate a process by PID     |
| `kill -9` | Forcefully terminate a process |
| `killall` | Terminate processes by name    |
| `jobs`    | Display background jobs        |
| `bg`      | Resume a job in the background |
| `fg`      | Bring a job to the foreground  |
