# Linux Processes

A process is a running instance of a program in Linux.

Whenever you execute a command or start an application, Linux creates a process to manage its execution.

Processes are one of the core concepts of Linux because the operating system uses them to manage CPU usage, memory, and system resources.

---

## Understanding Processes

A program is a file stored on disk.

A process is a program that is currently running.

Example:

```bash
firefox
```

The Firefox application stored on disk is a **program**.

When you open Firefox, Linux creates a **process**.

---

## Process Components

Every process contains:

| Component | Description |
| --------- | ----------- |
| PID       | Unique process ID |
| PPID      | Parent process ID |
| User      | User who started the process |
| State     | Current process status |
| Memory    | RAM used by process |
| CPU       | Processor usage |

---

## Process ID (PID)

Every running process has a unique number called a PID.

Example:

```bash
ps
```

Output:

```text
PID   TTY      TIME     CMD
1234  pts/0    00:00    bash
5678  pts/0    00:01    firefox
```

Here:

```text
1234
```

is the process ID of bash.

---

## Parent Process ID (PPID)

A process can create another process.

The process that creates another process is called the parent process.

Example:

```text
systemd
   |
   └── bash
          |
          └── firefox
```

`systemd` is the parent of bash.

bash is the parent of firefox.

---

# Process States

Linux processes can have different states.

| State | Meaning |
| ----- | ------- |
| R | Running |
| S | Sleeping |
| D | Waiting for I/O |
| Z | Zombie process |
| T | Stopped |

---

## Viewing Processes

### ps command

Shows running processes.

```bash
ps
```

Example:

```text
PID   CMD
1001  bash
1002  vim
```

---

## Viewing All Processes

```bash
ps aux
```

Example:

```text
USER     PID   %CPU  %MEM COMMAND

root     1     0.0   0.1  systemd
guru     2000  2.5   1.0  firefox
```

---

## Real-Time Process Monitoring

Use:

```bash
top
```

Example:

```text
PID USER CPU MEM COMMAND

2000 guru 15% 5% firefox
3000 guru 2% 1% gcc
```

`top` continuously updates process information.

---

## Better Process Viewer

Install and use:

```bash
htop
```

Features:

* Interactive interface
* Process searching
* Easy process management
* CPU and memory graphs

---

# Starting Processes

When you run a command:

```bash
ls
```

Linux creates a process.

Example:

```bash
./program
```

Creates a new process to execute the program.

---

# Foreground Processes

A foreground process runs directly in the terminal.

Example:

```bash
vim file.txt
```

The terminal is occupied until vim exits.

---

# Background Processes

A background process runs without blocking the terminal.

Example:

```bash
firefox &
```

Output:

```text
[1] 2345
```

`2345` is the process ID.

---

# Managing Background Processes

## View Background Jobs

```bash
jobs
```

Example:

```text
[1]+ Running firefox &
```

---

## Bring Process to Foreground

```bash
fg
```

Example:

```bash
fg %1
```

---

## Send Process to Background

Press:

```text
CTRL + Z
```

Then:

```bash
bg
```

---

# Killing Processes

A process can be stopped using:

```bash
kill
```

Example:

```bash
kill 1234
```

Kills process with PID 1234.

---

## Force Kill a Process

```bash
kill -9 1234
```

SIGKILL immediately terminates the process.

---

## Kill by Name

```bash
pkill firefox
```

Stops all processes named firefox.

---

# Process Signals

Linux uses signals to communicate with processes.

| Signal | Number | Meaning |
| ------ | ------ | ------- |
| SIGTERM | 15 | Graceful termination |
| SIGKILL | 9 | Force termination |
| SIGSTOP | 19 | Stop process |
| SIGCONT | 18 | Continue process |

---

# System Processes

Linux has important system processes.

Example:

```bash
systemd
```

PID:

```text
1
```

Responsibilities:

* Starts system services
* Manages background services
* Controls system startup

---

# Process Priority

Linux allows changing process priority.

Priority is controlled using:

```bash
nice
```

and

```bash
renice
```

---

## Starting Process with Priority

Example:

```bash
nice -n 10 program
```

Higher nice value = lower priority.

---

## Changing Running Process Priority

Example:

```bash
renice 5 -p 1234
```

Changes priority of PID 1234.

---

# Checking Process Information

## Using pidof

Find PID of a program.

Example:

```bash
pidof firefox
```

Output:

```text
2345
```

---

## Using pgrep

Search processes.

Example:

```bash
pgrep ssh
```

---

# Process Tree

Processes have a parent-child relationship.

View process tree:

```bash
pstree
```

Example:

```text
systemd
 ├── sshd
 ├── bash
 │    └── vim
 └── firefox
```

---

# Zombie Processes

A zombie process is a process that has finished execution but still exists in the process table.

Example:

```text
Z state
```

Zombie processes usually happen when the parent process does not collect the child's exit status.

---

# Daemon Processes

A daemon is a background process that runs without user interaction.

Examples:

```text
sshd
cron
networkd
```

Check services:

```bash
systemctl status service_name
```

---

# Process vs Thread

| Process | Thread |
| ------- | ------ |
| Independent program execution | Smaller execution unit |
| Has separate memory | Shares process memory |
| More resource usage | Less resource usage |

Example:

A browser is a process.

Each browser tab may run as a separate process or thread.

---

# Important Commands

| Command | Purpose |
| ------- | ------- |
| ps | View processes |
| ps aux | View all processes |
| top | Real-time monitoring |
| htop | Interactive monitoring |
| kill | Stop process |
| kill -9 | Force kill |
| jobs | View background jobs |
| fg | Move process to foreground |
| bg | Move process to background |
| pstree | Show process tree |
| pidof | Find process ID |
| pgrep | Search processes |

---

# Why Processes Matter

Understanding processes helps with:

* System administration
* Debugging applications
* Server management
* Performance monitoring
* Kernel development
* Resource management

Linux manages thousands of processes at the same time, making process management a fundamental part of the operating system.
