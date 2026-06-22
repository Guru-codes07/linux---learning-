# Configuring GCC on Fedora

GCC (GNU Compiler Collection) is the standard compiler used to compile C programs on Linux systems.

This guide explains how to install, verify, and use GCC on Fedora.

---

## What is GCC?

GCC stands for **GNU Compiler Collection**.

It supports multiple programming languages including:

* C
* C++
* Objective-C
* Fortran
* Ada

For C programming, GCC is the most commonly used compiler on Linux.

---

## Check if GCC is Installed

Before installing GCC, check whether it is already available on your system.

### Command

```bash
gcc --version
```

### Example Output

```text
gcc (GCC) 15.1.1
```

If a version number is displayed, GCC is already installed.

---

## Install GCC

### Update Package Information

```bash
sudo dnf check-update
```

### Install GCC

```bash
sudo dnf install gcc
```

DNF will download and install GCC along with required dependencies.

---

## Verify Installation

```bash
gcc --version
```

### Check GCC Location

```bash
which gcc
```

Expected Output:

```text
/usr/bin/gcc
```

---

## Create Your First C Program

Create a file:

```bash
nano hello.c
```

Add the following code:

```c
#include <stdio.h>

int main()
{
    printf("Hello, Linux!\n");
    return 0;
}
```

Save the file.

---

## Compile a C Program

### Syntax

```bash
gcc source_file.c -o output_file
```

### Example

```bash
gcc hello.c -o hello
```

This creates an executable file named:

```text
hello
```

---

## Run the Program

```bash
./hello
```

Output:

```text
Hello, Linux!
```

---

## Useful GCC Commands

### Compile a Program

```bash
gcc program.c -o program
```

### Compile with Warnings Enabled

```bash
gcc -Wall program.c -o program
```

### Compile and Generate Debug Information

```bash
gcc -g program.c -o program
```

### Compile Multiple Source Files

```bash
gcc main.c helper.c -o app
```

---

## Understanding Common Options

| Option  | Purpose                        |
| ------- | ------------------------------ |
| `-o`    | Specify output filename        |
| `-Wall` | Enable common warnings         |
| `-g`    | Generate debugging information |
| `-c`    | Compile without linking        |
| `-O2`   | Optimize generated code        |

### Example

```bash
gcc -Wall -g main.c -o main
```

---

## Common Errors

### gcc: command not found

Install GCC:

```bash
sudo dnf install gcc
```

---

### Undefined Reference Error

Example:

```text
undefined reference to 'printf'
```

Possible causes:

* Missing header file
* Incorrect source code
* Compilation mistakes

Verify source code and compile again.

---

## Summary

| Command                   | Purpose                    |
| ------------------------- | -------------------------- |
| `gcc --version`           | Check GCC version          |
| `which gcc`               | Locate GCC                 |
| `sudo dnf install gcc`    | Install GCC                |
| `gcc file.c -o app`       | Compile a program          |
| `./app`                   | Run the executable         |
| `gcc -Wall file.c -o app` | Compile with warnings      |
| `gcc -g file.c -o app`    | Compile with debug symbols |

GCC is the foundation of C development on Linux and an essential tool for systems programming, networking, and open-source development.

