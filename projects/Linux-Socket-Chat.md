# Linux Socket Chat

## Overview

**Linux Socket Chat** is my first networking project built using the C programming language and the POSIX Socket API. The project demonstrates the fundamentals of TCP/IP communication by implementing a simple client-server chat application where a single client can connect to a server and exchange messages.

This project served as my introduction to Linux socket programming and laid the foundation for more advanced networking projects such as my multi-client chat server and event-driven chat server.

---

# Project Objectives

The primary goals of this project were to:

- Learn how TCP sockets work.
- Understand the client-server communication model.
- Become familiar with the POSIX Socket API.
- Learn how data is transmitted over a TCP connection.
- Gain hands-on experience with Linux networking system calls.

---

# Features

- TCP-based communication
- IPv4 networking
- Single client connection
- Message exchange between client and server
- Graceful connection termination
- Error handling for socket operations
- Cross-terminal communication

---

# Technologies Used

- C Programming
- POSIX Socket API
- TCP/IP
- IPv4
- GCC
- Linux
- Makefile

---

# Concepts Implemented

This project demonstrates the following networking concepts:

- Client-Server Architecture
- TCP Protocol
- IPv4 Addressing
- Socket Lifecycle
- Blocking Sockets
- Stream Sockets (SOCK_STREAM)
- Network Communication
- System Calls

---

# Socket Lifecycle

The server follows the standard TCP socket lifecycle.

```text
socket()

↓

bind()

↓

listen()

↓

accept()

↓

recv()

↓

send()

↓

close()
```

The client follows a similar process.

```text
socket()

↓

connect()

↓

send()

↓

recv()

↓

close()
```

---

# Project Architecture

```text
               TCP Connection

+-----------+  <-------------->  +-----------+
|  Client   |                    |  Server   |
+-----------+                    +-----------+

       send()            recv()

       recv()            send()
```

The server listens for incoming connections, while the client connects and exchanges messages.

---

# Communication Flow

```text
Start Server

↓

Create Socket

↓

Bind Socket

↓

Listen

↓

Client Connects

↓

Accept Connection

↓

Exchange Messages

↓

Close Connection
```

---

# Directory Structure

```text
linux-socket-chat/

├── client.c
├── server.c
├── Makefile
├── README.md
└── screenshots/ (optional)
```

---

# Linux System Calls Used

| Function | Purpose |
|----------|---------|
| socket() | Create a socket |
| bind() | Bind socket to an IP address and port |
| listen() | Listen for incoming connections |
| accept() | Accept a client connection |
| connect() | Connect to the server |
| send() | Send data |
| recv() | Receive data |
| close() | Close the socket |

---

# Workflow

## Server

```text
Create Socket

↓

Bind

↓

Listen

↓

Accept Client

↓

Receive Message

↓

Send Reply

↓

Close Socket
```

---

## Client

```text
Create Socket

↓

Connect

↓

Send Message

↓

Receive Reply

↓

Close Socket
```

---

# Skills Learned

Through this project, I learned:

- Creating TCP sockets in C
- Understanding the client-server model
- Establishing TCP connections
- Sending and receiving data
- Working with IP addresses and ports
- Handling networking errors
- Compiling networking programs using GCC
- Debugging socket applications on Linux

---

# Challenges Faced

Some of the challenges encountered while developing this project included:

- Understanding the sequence of socket system calls.
- Handling connection failures.
- Managing blocking socket behavior.
- Debugging communication issues between the client and server.
- Learning how TCP establishes and maintains reliable communication.

Overcoming these challenges provided a strong understanding of Linux networking fundamentals.

---

# Possible Improvements

This project represents the foundation of my networking journey. Future improvements could include:

- Supporting multiple clients
- Username support
- Broadcast messaging
- Chat history
- Non-blocking sockets
- Thread-based concurrency
- Event-driven architecture using `poll()`
- TLS/SSL encryption
- File transfer support

Many of these features were later implemented in my subsequent networking projects.

---

# Learning Progression

This project marks the beginning of my systems programming journey.

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

**https://github.com/Guru-codes07/linux-socket-chat**

---

# Related Documentation

This project applies concepts explained elsewhere in this repository, including:

- Client-Server Architecture
- TCP vs UDP
- Socket Programming Basics
- Socket System Calls
- Socket Address Structures
- Byte Order
- TCP Three-Way Handshake
- Blocking vs Non-Blocking Sockets

---

# Key Takeaways

- Learned the fundamentals of Linux socket programming.
- Built a working TCP client-server application from scratch.
- Gained practical experience with the POSIX Socket API.
- Understood the lifecycle of a TCP connection.
- Established the foundation for building scalable network applications.

---

# Conclusion

The **Linux Socket Chat** project was my first practical step into Linux systems programming and computer networking. It introduced me to the core concepts of TCP/IP communication, socket programming, and client-server architecture. The knowledge gained from this project became the basis for developing more advanced networking applications involving multi-threading and event-driven I/O, making it a significant milestone in my learning journey.
