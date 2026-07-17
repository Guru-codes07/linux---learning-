# Event-Driven Chat Server (`poll()`)

## Overview

The **Event-Driven Chat Server** is my most advanced networking project to date. It is a scalable multi-client chat server written in **C** that leverages Linux's **`poll()`** system call for I/O multiplexing instead of creating a dedicated thread for each client.

Unlike my previous project, where every client connection was managed by an individual thread, this server follows an **event-driven architecture**, using a single event loop to efficiently monitor and process multiple client connections simultaneously. This approach improves scalability while reducing the overhead associated with thread creation and context switching.

To make the project more representative of a real-world chat application, I implemented several advanced features, including:

- Event-driven I/O using `poll()`
- TLS encryption using OpenSSL for secure client-server communication
- SQLite database integration for persistent chat history
- A custom binary wire protocol for efficient and structured message exchange
- Public broadcast messaging
- Private messaging between connected users
- Username management and client session handling

Developing this project significantly strengthened my understanding of Linux systems programming, event-driven server architecture, secure network communication, binary protocol design, database integration, and scalable network application development. It represents a major milestone in my journey toward building production-quality networking software.

---

# Project Objectives

The primary goals of this project were to:

- Build a scalable event-driven chat server.
- Learn Linux I/O Multiplexing using `poll()`.
- Design a custom binary communication protocol.
- Secure network communication using TLS.
- Store chat history using SQLite.
- Build a modular networking project similar to real-world servers.

---

# Features

- Multi-client support
- Event-driven architecture
- I/O Multiplexing using `poll()`
- Custom Binary Wire Protocol
- TLS Encryption (OpenSSL)
- SQLite Chat History
- Username Management
- Broadcast Messaging
- Join/Leave Notifications
- Persistent Message Storage
- Binary Packet Parsing
- Error Handling
- Modular Codebase

---

# Technologies Used

- C Programming
- POSIX Sockets
- Linux `poll()`
- OpenSSL
- SQLite3
- TCP/IP
- GCC
- Linux
- Makefile

---

# Concepts Implemented

This project demonstrates:

- Event-Driven Programming
- I/O Multiplexing
- poll()
- TCP Networking
- Binary Protocol Design
- TLS Encryption
- SSL/TLS Handshake
- SQLite Database Programming
- Persistent Storage
- Network Packet Parsing
- Modular Software Design
- Linux System Calls

---

# Project Architecture

```text
                 +----------------------+
                 |      Event Loop      |
                 +----------------------+
                           |
                     poll() monitors
                           |
 -------------------------------------------------------------
 |            |             |             |                  |
 ▼            ▼             ▼             ▼                  ▼
Client A   Client B     Client C     Client D          Client N
```

Instead of one thread per client, a single event loop continuously monitors every connected socket.

---

# Event Loop Workflow

```text
Server Starts

↓

Create Listening Socket

↓

Bind

↓

Listen

↓

Initialize poll()

↓

Wait for Events

↓

Client Connects

↓

Accept Client

↓

Monitor Socket

↓

Receive Packet

↓

Parse Binary Protocol

↓

Broadcast Message

↓

Store in SQLite

↓

Continue Event Loop
```

---

# Why `poll()`?

In my previous project, every client required its own thread.

```text
Client

↓

Thread

↓

Memory

↓

Context Switch
```

As the number of clients increases, thread management becomes expensive.

Using `poll()`:

```text
Multiple Clients

↓

poll()

↓

Single Event Loop
```

This approach is significantly more scalable and efficient.

---

# I/O Multiplexing

The server continuously waits for activity on all connected sockets.

```text
poll()

↓

Socket Ready?

↓

Yes

↓

Read Data

↓

Process Packet

↓

Broadcast
```

Only sockets with available data are processed.

---

# Binary Wire Protocol

Instead of sending plain text, the server communicates using a **custom binary protocol**.

Each packet contains structured metadata.

Example:

```text
+----------+-----------+-----------+--------------+
| Version  | Type      | Length    | Payload      |
+----------+-----------+-----------+--------------+
```

The binary protocol makes communication:

- More structured
- Faster to parse
- Easier to extend
- More suitable for larger applications

---

# Packet Processing

```text
Receive Bytes

↓

Parse Header

↓

Validate Packet

↓

Extract Payload

↓

Process Message

↓

Broadcast
```

---

# TLS Encryption

The server uses **OpenSSL** to encrypt communication between clients and the server.

Without TLS:

```text
Client

↓

Plain Text

↓

Network
```

Anyone intercepting traffic can read the messages.

With TLS:

```text
Client

↓

Encrypted Data

↓

Server

↓

Decrypt
```

Communication remains secure.

---

# TLS Workflow

```text
Client Connects

↓

TLS Handshake

↓

Certificate Verification

↓

Secure Session Created

↓

Encrypted Communication
```

---

# OpenSSL Functions Used

Examples include:

- SSL_library_init()
- SSL_CTX_new()
- SSL_new()
- SSL_accept()
- SSL_connect()
- SSL_read()
- SSL_write()
- SSL_shutdown()

These functions establish and manage encrypted client-server communication.

---

# SQLite Integration

Unlike previous projects, messages are permanently stored in a SQLite database.

```text
Client Message

↓

Server

↓

SQLite

↓

Database File
```

---

# Database Workflow

```text
Receive Message

↓

Insert into Database

↓

Commit

↓

Continue Chat
```

This allows chat history to persist even after the server restarts.

---

# Database Features

- Chat history
- Persistent storage
- Automatic database creation
- SQL queries
- Message logging

---

# Socket Lifecycle

```text
socket()

↓

bind()

↓

listen()

↓

accept()

↓

poll()

↓

recv()

↓

Parse Packet

↓

Broadcast

↓

close()
```

---

# Communication Flow

```text
Client Connects

↓

TLS Handshake

↓

Binary Packet Sent

↓

Server Parses Packet

↓

Store in SQLite

↓

Broadcast to Clients

↓

Repeat
```

---

# Skills Learned

This project helped me gain practical experience with:

- Event-driven programming
- Linux `poll()`
- I/O Multiplexing
- Binary Protocol Design
- SQLite Database Programming
- TLS Encryption
- OpenSSL
- Packet Parsing
- Secure Socket Programming
- Modular Project Architecture
- Linux System Programming

---

# Improvements Over Previous Project

Compared to the Multi-Client Chat Server, this project introduces:

- Event-driven architecture
- `poll()` instead of POSIX Threads
- Better scalability
- Binary Wire Protocol
- TLS Encryption
- SQLite Database
- Persistent Chat History
- Secure Communication
- Modular networking architecture

---

# Challenges Faced

Some challenges encountered during development included:

- Understanding event-driven programming
- Managing multiple file descriptors
- Designing a binary protocol
- Implementing TLS correctly
- Debugging SSL handshake issues
- Integrating SQLite with the server
- Parsing binary packets
- Handling disconnected clients
- Managing dynamic client lists
- Debugging complex networking issues

These challenges significantly strengthened my understanding of Linux systems programming.

---

# Possible Future Improvements

Planned enhancements include:

- epoll() implementation
- Authentication system
- User accounts
- Rooms / Channels
- File sharing
- Message compression
- IPv6 support
- Thread pool architecture
- Configuration files
- Logging framework
- Admin commands

---

# Learning Progression

```text
Linux Socket Chat

↓

Multi-Client Chat Server (Threads)

↓

Event-Driven Chat Server (poll())

```

Each project builds upon the knowledge gained from the previous one.

---

# Repository

GitHub Repository:

**https://github.com/Guru-codes07/c-event-loop-chat**

---

# Related Documentation

This project applies concepts explained throughout this repository, including:

- Socket Programming Basics
- Socket System Calls
- Client-Server Architecture
- TCP Three-Way Handshake
- I/O Multiplexing
- poll()
- Blocking vs Non-Blocking Sockets
- TLS & HTTPS
- SQLite Basics
- Byte Order
- Binary Protocol Design

---

# Key Takeaways

- Built an event-driven TCP server using Linux `poll()`.
- Designed and implemented a custom binary wire protocol.
- Added TLS encryption using OpenSSL for secure communication.
- Integrated SQLite for persistent chat history.
- Learned scalable server architecture without relying on one thread per client.
- Strengthened knowledge of Linux networking, secure communication, database integration, and systems programming.

---

# Conclusion

The **Event-Driven Chat Server** is the culmination of my networking and Linux systems programming journey so far. By combining **I/O multiplexing (`poll()`), TLS encryption with OpenSSL, SQLite database integration, and a custom binary wire protocol**, I built a significantly more scalable and feature-rich chat server than my previous projects.

This project gave me hands-on experience with many of the technologies and design patterns used in real-world network servers. It also laid a strong foundation for future work involving **`epoll()`**, asynchronous I/O, high-performance servers, Linux kernel development, and distributed systems.
