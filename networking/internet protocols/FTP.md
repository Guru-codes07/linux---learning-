# FTP (File Transfer Protocol)

**FTP (File Transfer Protocol)** is an application-layer protocol used to transfer files between a client and a server over a TCP/IP network.

FTP allows users to upload, download, rename, delete, and manage files on a remote server.

Although FTP is still used in some environments, it has largely been replaced by **SFTP** and **FTPS** because standard FTP does not encrypt data.

---

# Why Do We Need FTP?

Suppose you want to upload a website to a web server.

Without FTP:

```text
Copy Files Manually

↓

Physical Access Required
```

With FTP:

```text
Computer

↓

Internet

↓

FTP Server

↓

Upload Files
```

FTP makes remote file transfers simple.

---

# FTP Architecture

FTP follows a **client-server model**.

```text
FTP Client

↓

TCP Connection

↓

FTP Server

↓

File Transfer
```

Examples of FTP clients:

- FileZilla
- WinSCP
- Cyberduck
- Linux `ftp` command

---

# Default Ports

| Protocol | Port |
|----------|------|
| FTP Control Connection | TCP 21 |
| FTP Data Connection | TCP 20 (Active Mode) |

---

# FTP Components

FTP uses two separate TCP connections.

- Control Connection
- Data Connection

---

# Control Connection

The control connection is responsible for:

- Login
- Commands
- Server responses

It remains open throughout the session.

```text
Client

↓

TCP Port 21

↓

FTP Server
```

---

# Data Connection

The data connection transfers:

- Files
- Directory listings

A new data connection is created whenever data needs to be transferred.

---

# FTP Communication

```text
Client

↓

Control Connection

↓

Authentication

↓

Data Connection

↓

File Transfer
```

---

# FTP Session

Typical FTP session:

```text
Connect

↓

Login

↓

Navigate Directories

↓

Upload / Download Files

↓

Disconnect
```

---

# Authentication

FTP usually requires:

```text
Username

Password
```

Example:

```text
Username: guru

Password: ********
```

Some servers allow:

```text
Anonymous Login
```

using:

```text
Username: anonymous
```

---

# Active Mode

In Active Mode:

1. Client connects to server on port 21.
2. Server opens the data connection from port 20.

```text
Client

↓

Port 21

↓

Server

↓

Port 20

↓

Client
```

This can cause problems with firewalls because the server initiates the data connection.

---

# Passive Mode

Passive Mode is more commonly used today.

1. Client connects to port 21.
2. Server provides a random port.
3. Client connects to that port.

```text
Client

↓

Port 21

↓

Server

↓

Random Port

↓

Client Connects
```

Passive Mode works better with NAT and firewalls.

---

# Common FTP Commands

| Command | Purpose |
|----------|---------|
| `USER` | Send username |
| `PASS` | Send password |
| `LIST` | List directory contents |
| `PWD` | Print working directory |
| `CWD` | Change directory |
| `RETR` | Download file |
| `STOR` | Upload file |
| `DELE` | Delete file |
| `MKD` | Create directory |
| `RMD` | Remove directory |
| `QUIT` | Close connection |

---

# Example FTP Session

```text
Client

↓

USER guru

↓

331 Password Required

↓

PASS password

↓

230 Login Successful

↓

LIST

↓

Directory Listing

↓

RETR file.txt

↓

File Downloaded

↓

QUIT
```

---

# Uploading a File

```text
Client

↓

STOR report.pdf

↓

Server Receives File

↓

Upload Complete
```

---

# Downloading a File

```text
Client

↓

RETR notes.txt

↓

Server Sends File

↓

Download Complete
```

---

# Directory Listing

The client requests:

```text
LIST
```

Server responds:

```text
Documents

Downloads

notes.txt

project.zip
```

---

# FTP Status Codes

FTP servers return status codes.

| Code | Meaning |
|------|---------|
| 220 | Service Ready |
| 221 | Service Closing |
| 230 | Login Successful |
| 331 | Password Required |
| 425 | Cannot Open Data Connection |
| 530 | Login Incorrect |
| 550 | File Not Found |

---

# FTP Commands in Linux

Connect to an FTP server:

```bash
ftp ftp.example.com
```

Download a file:

```text
get file.txt
```

Upload a file:

```text
put report.pdf
```

List files:

```text
ls
```

Exit:

```text
bye
```

---

# Anonymous FTP

Some public servers allow anonymous access.

Login:

```text
Username: anonymous

Password: your_email@example.com
```

Commonly used for downloading public software.

---

# FTP vs HTTP

| Feature | FTP | HTTP |
|----------|------|-------|
| Primary Purpose | File Transfer | Web Pages |
| Upload Files | Yes | Limited |
| Download Files | Yes | Yes |
| Authentication | Usually Required | Optional |
| Multiple Connections | Yes | No |

---

# FTP vs SFTP

| Feature | FTP | SFTP |
|----------|------|-------|
| Encryption | No | Yes |
| Default Port | 21 | 22 |
| Security | Low | High |
| Protocol | FTP | SSH |

---

# FTP vs FTPS

| Feature | FTP | FTPS |
|----------|------|-------|
| Encryption | No | Yes |
| Uses TLS | No | Yes |
| Default Port | 21 | 21 (with TLS) |

---

# Advantages

- Simple file transfers
- Supports uploads and downloads
- Directory management
- Widely supported
- Efficient for large file transfers

---

# Limitations

- Data is transmitted in plain text
- Passwords are unencrypted
- Uses multiple TCP connections
- Firewall and NAT issues in Active Mode
- Largely replaced by secure alternatives

---

# Real-World Applications

FTP has been used for:

- Website deployment
- File sharing
- Software distribution
- Enterprise backups
- Remote file management

Today, many organizations prefer **SFTP** or **FTPS** for improved security.

---

# Summary

| Component | Purpose |
|-----------|---------|
| FTP Client | Sends commands and transfers files |
| FTP Server | Stores and serves files |
| Control Connection | Sends commands |
| Data Connection | Transfers files |
| Active Mode | Server initiates data connection |
| Passive Mode | Client initiates data connection |

---

# Key Takeaways

- FTP stands for **File Transfer Protocol**.
- It is an application-layer protocol used for transferring files over TCP/IP.
- FTP uses **TCP port 21** for the control connection and **TCP port 20** for data transfer in Active Mode.
- FTP establishes separate control and data connections.
- Passive Mode is preferred in modern networks because it works better with NAT and firewalls.
- Standard FTP does **not** encrypt data, making it unsuitable for transferring sensitive information.
- Secure alternatives such as **SFTP** and **FTPS** are recommended for modern applications.

---

# Conclusion

FTP is one of the oldest Internet protocols and played a major role in enabling remote file transfers. While it remains useful for understanding network communication and legacy systems, its lack of built-in security has led most organizations to adopt encrypted alternatives such as SFTP and FTPS. Understanding FTP provides valuable insight into client-server communication and application-layer protocols.
