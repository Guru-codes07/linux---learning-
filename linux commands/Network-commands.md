# Networking Commands

Networking commands are used to test connectivity, inspect network settings, transfer data, and connect to remote systems.

## 1. ping

**Meaning:** Test network connectivity

Sends packets to a host and measures the response time.

### Syntax

```bash
ping <host>
```

### Example

```bash
$ ping google.com
```

### Common Usage

| Command                | Description                        |
| ---------------------- | ---------------------------------- |
| `ping google.com`      | Test internet connectivity         |
| `ping 8.8.8.8`         | Test connectivity to a specific IP |
| `ping -c 4 google.com` | Send only 4 packets                |

#### Example: ping -c 4

```bash
$ ping -c 4 google.com
```

---

## 2. curl

**Meaning:** Transfer data from or to a server

Commonly used to test APIs and download content.

### Syntax

```bash
curl <url>
```

### Example

```bash
$ curl https://api.github.com
```

### Common Usage

| Command                       | Description           |
| ----------------------------- | --------------------- |
| `curl https://example.com`    | Fetch webpage content |
| `curl -I https://example.com` | Display HTTP headers  |
| `curl -O <url>`               | Download a file       |

#### Example: Display Headers

```bash
$ curl -I https://github.com
```

---

## 3. wget

**Meaning:** Download files from the internet

Downloads files and supports resuming interrupted downloads.

### Syntax

```bash
wget <url>
```

### Example

```bash
$ wget https://example.com/file.zip
```

### Common Usage

| Command                  | Description                 |
| ------------------------ | --------------------------- |
| `wget <url>`             | Download a file             |
| `wget -c <url>`          | Resume a download           |
| `wget -O file.zip <url>` | Save with a custom filename |

#### Example: Resume a Download

```bash
$ wget -c https://example.com/file.zip
```

---

## 4. ip

**Meaning:** Display and manage network interfaces

Used to view IP addresses, routes, and network devices.

### Syntax

```bash
ip <option>
```

### Example

```bash
$ ip a
```

### Common Usage

| Command    | Description                |
| ---------- | -------------------------- |
| `ip a`     | Display IP addresses       |
| `ip link`  | Display network interfaces |
| `ip route` | Display routing table      |

#### Example: Display IP Addresses

```bash
$ ip a
```

---

## 5. ss

**Meaning:** Socket Statistics

Displays active network connections and listening ports.

### Syntax

```bash
ss
```

### Example

```bash
$ ss -tuln
```

### Common Usage

| Command    | Description                         |
| ---------- | ----------------------------------- |
| `ss -tuln` | Display listening TCP and UDP ports |
| `ss -t`    | Display TCP connections             |
| `ss -u`    | Display UDP connections             |

#### Example: View Listening Ports

```bash
$ ss -tuln
```

---

## 6. ssh

**Full Form:** Secure Shell

Connects securely to a remote computer.

### Syntax

```bash
ssh <user>@<host>
```

### Example

```bash
$ ssh guruprasad@192.168.1.10
```

### Common Usage

| Command                 | Description                 |
| ----------------------- | --------------------------- |
| `ssh user@host`         | Connect to a remote system  |
| `ssh -p 2222 user@host` | Connect using a custom port |

#### Example: Connect Using a Custom Port

```bash
$ ssh -p 2222 guruprasad@server.com
```

---

## 7. scp

**Full Form:** Secure Copy

Copies files between local and remote systems using SSH.

### Syntax

```bash
scp <source> <destination>
```

### Example

```bash
$ scp file.txt user@server:/home/user/
```

### Common Usage

| Command                          | Description                      |
| -------------------------------- | -------------------------------- |
| `scp file.txt user@host:/path/`  | Copy a file to a remote system   |
| `scp user@host:/path/file.txt .` | Copy a file from a remote system |
| `scp -r folder user@host:/path/` | Copy a directory recursively     |

#### Example: Copy a Directory

```bash
$ scp -r Projects user@server:/home/user/
```

---

## Summary

| Command    | Purpose                           |
| ---------- | --------------------------------- |
| `ping`     | Test network connectivity         |
| `ping -c`  | Send a specific number of packets |
| `curl`     | Transfer data from a server       |
| `curl -I`  | Display HTTP headers              |
| `curl -O`  | Download a file                   |
| `wget`     | Download files                    |
| `wget -c`  | Resume downloads                  |
| `ip a`     | Display IP addresses              |
| `ip link`  | Display network interfaces        |
| `ip route` | Display routing information       |
| `ss`       | Display network connections       |
| `ss -tuln` | Display listening ports           |
| `ssh`      | Connect to a remote system        |
| `scp`      | Securely transfer files           |
| `scp -r`   | Transfer directories recursively  |

