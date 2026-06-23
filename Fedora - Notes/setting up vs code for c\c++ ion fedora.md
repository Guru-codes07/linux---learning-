# Setting Up VS Code for C/C++ on Fedora

This guide explains how to configure Visual Studio Code for C and C++ development on Fedora Linux.

After completing this setup, you will be able to:

* Write C and C++ programs
* Compile programs using GCC/G++
* Run programs inside VS Code
* Debug programs using GDB
* Use IntelliSense and code completion

---

# Prerequisites

Before configuring VS Code, ensure the following are installed:

* Visual Studio Code
* GCC
* G++
* GDB

---

## Verify VS Code Installation

```bash
code --version
```

Example Output:

```text
1.124.2
```

---

## Install GCC

```bash
sudo dnf install gcc
```

Verify:

```bash
gcc --version
```

---

## Install G++

```bash
sudo dnf install gcc-c++
```

Verify:

```bash
g++ --version
```

---

## Install GDB

GDB (GNU Debugger) is required for debugging.

```bash
sudo dnf install gdb
```

Verify:

```bash
gdb --version
```

---

# Install Required VS Code Extensions

Open VS Code and navigate to:

```text
View → Extensions
```

Install the following extension:

### C/C++ (Microsoft)

Provides:

* IntelliSense
* Code navigation
* Debugging support
* Syntax highlighting

Extension ID:

```text
ms-vscode.cpptools
```

---

# Create a Project Folder

Example:

```text
c-programming/
├── .vscode/
├── basics/
├── pointers/
└── arrays/
```

Open the folder in VS Code:

```bash
code ~/c-programming
```

---

# Create a Simple Program

Create:

```text
hello.c
```

Add:

```c
#include <stdio.h>

int main()
{
    printf("Hello, Linux!\n");
    return 0;
}
```

---

# Compile Using the Terminal

```bash
gcc hello.c -o hello
```

Run:

```bash
./hello
```

Output:

```text
Hello, Linux!
```

---

# Configure VS Code Build Tasks

Create:

```text
.vscode/tasks.json
```

Example:

```json
{
    "version": "2.0.0",
    "tasks": [
        {
            "label": "Build C Program",
            "type": "shell",
            "command": "gcc",
            "args": [
                "${file}",
                "-o",
                "${fileDirname}/${fileBasenameNoExtension}"
            ],
            "group": {
                "kind": "build",
                "isDefault": true
            }
        }
    ]
}
```

This allows VS Code to compile the currently open C file.

---

# Configure Debugging

Create:

```text
.vscode/launch.json
```

Example:

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Debug C Program",
            "type": "cppdbg",
            "request": "launch",
            "program": "${fileDirname}/${fileBasenameNoExtension}",
            "args": [],
            "stopAtEntry": false,
            "cwd": "${fileDirname}",
            "externalConsole": false,
            "MIMode": "gdb",
            "miDebuggerPath": "/usr/bin/gdb"
        }
    ]
}
```

---

# Running a Program

### Build

Press:

```text
Ctrl + Shift + B
```

VS Code compiles the current file.

### Run

Open Terminal:

```bash
./program_name
```

Example:

```bash
./hello
```

---

# Debugging a Program

### Add a Breakpoint

Click to the left of a line number.

A red dot appears.

### Start Debugging

Press:

```text
F5
```

VS Code launches GDB and pauses at breakpoints.

---

# Common Problems

## gcc: command not found

Install GCC:

```bash
sudo dnf install gcc
```

---

## g++: command not found

Install G++:

```bash
sudo dnf install gcc-c++
```

---

## gdb: command not found

Install GDB:

```bash
sudo dnf install gdb
```

---

## VS Code Asks for launch.json Again

Cause:

VS Code stores configuration per project folder.

When opening a new folder, the `.vscode` directory may not exist.

Solution:

Create:

```text
.vscode/
├── tasks.json
└── launch.json
```

inside the new project folder.

---

## Program Does Not Run

Verify compilation:

```bash
gcc hello.c -o hello
```

Verify executable exists:

```bash
ls -l
```

Run:

```bash
./hello
```

---

# Useful Shortcuts

| Shortcut           | Action            |
| ------------------ | ----------------- |
| `Ctrl + Shift + B` | Build program     |
| `Ctrl + Shift + P` | Command palette   |
| `Ctrl + ``         | Open terminal     |
| `F5`               | Start debugging   |
| `Shift + F5`       | Stop debugging    |
| `F9`               | Toggle breakpoint |

---

# Recommended Folder Structure

```text
c-programming/
├── .vscode/
│   ├── tasks.json
│   └── launch.json
├── basics/
├── arrays/
├── pointers/
├── structures/
└── projects/
```

This allows a single VS Code configuration to be reused for multiple C and C++ programs.

---

# Summary

| Tool        | Purpose             |
| ----------- | ------------------- |
| VS Code     | Code editor         |
| GCC         | C compiler          |
| G++         | C++ compiler        |
| GDB         | Debugger            |
| tasks.json  | Build configuration |
| launch.json | Debug configuration |

### Important Commands

```bash
sudo dnf install gcc
sudo dnf install gcc-c++
sudo dnf install gdb

gcc hello.c -o hello
g++ main.cpp -o main

./hello
./main
```

With GCC, G++, GDB, and the C/C++ extension installed, Fedora provides a complete development environment for learning C, C++, Linux systems programming, networking, and open-source development.

