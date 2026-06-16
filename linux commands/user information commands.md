# User Information Commands

User information commands provide details about the current user, system identity, and operating environment.

## 1. whoami

**Full Form:** Who Am I

Displays the username of the currently logged-in user.

### Syntax

```bash
whoami
```

### Example

```bash
$ whoami
guruprasad
```

### Common Usage

| Command  | Description                  |
| -------- | ---------------------------- |
| `whoami` | Display the current username |

---

## 2. id

**Meaning:** Display user and group information

Shows the user ID (UID), group ID (GID), and groups the user belongs to.

### Syntax

```bash
id
```

### Example

```bash
$ id
uid=1000(guruprasad) gid=1000(guruprasad) groups=1000(guruprasad),10(wheel)
```

### Common Options

| Command  | Description                       |
| -------- | --------------------------------- |
| `id`     | Display complete user information |
| `id -u`  | Display only the user ID          |
| `id -g`  | Display only the group ID         |
| `id -nG` | Display group names               |

#### Example: id -u

```bash
$ id -u
1000
```

---

## 3. hostname

**Meaning:** Display or set the system hostname

Shows the name assigned to the computer on a network.

### Syntax

```bash
hostname
```

### Example

```bash
$ hostname
fedora-workstation
```

### Common Usage

| Command       | Description                                 |
| ------------- | ------------------------------------------- |
| `hostname`    | Display the system hostname                 |
| `hostname -I` | Display IP addresses assigned to the system |

#### Example: hostname -I

```bash
$ hostname -I
192.168.1.5
```

---

## 4. uname

**Full Form:** Unix Name

Displays information about the operating system and kernel.

### Syntax

```bash
uname [option]
```

### Example

```bash
$ uname
Linux
```

### Common Options

| Command    | Description                              |
| ---------- | ---------------------------------------- |
| `uname`    | Display operating system name            |
| `uname -r` | Display kernel version                   |
| `uname -a` | Display all available system information |
| `uname -m` | Display system architecture              |

#### Example: uname -a

```bash
$ uname -a
Linux fedora 6.15.3-200.fc42.x86_64 #1 SMP PREEMPT_DYNAMIC x86_64 GNU/Linux
```

---

## 5. users

**Meaning:** Display currently logged-in users

Shows usernames of users currently logged into the system.

### Syntax

```bash
users
```

### Example

```bash
$ users
guruprasad
```

### Common Usage

| Command | Description             |
| ------- | ----------------------- |
| `users` | Display logged-in users |

---

## 6. logname

**Meaning:** Display the login name

Shows the name of the user who originally logged into the session.

### Syntax

```bash
logname
```

### Example

```bash
$ logname
guruprasad
```

### Common Usage

| Command   | Description                |
| --------- | -------------------------- |
| `logname` | Display the login username |

---

## Summary

| Command       | Purpose                              |
| ------------- | ------------------------------------ |
| `whoami`      | Display the current username         |
| `id`          | Display user and group information   |
| `id -u`       | Display the user ID                  |
| `id -g`       | Display the group ID                 |
| `id -nG`      | Display group names                  |
| `hostname`    | Display the system hostname          |
| `hostname -I` | Display system IP addresses          |
| `uname`       | Display operating system information |
| `uname -r`    | Display kernel version               |
| `uname -a`    | Display complete system information  |
| `users`       | Display logged-in users              |
| `logname`     | Display the login username           |
