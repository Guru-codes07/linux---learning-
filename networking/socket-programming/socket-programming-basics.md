# Socket Programming Basics

Socket programming is the foundation of network communication in modern operating systems. It allows applications running on different computers (or on the same computer) to communicate over a network using protocols such as **TCP** and **UDP**.

Almost every network application—including web browsers, chat applications, SSH, FTP, email clients, and online games—uses socket programming.

---

# What is Socket Programming?

**Socket Programming** is the process of writing programs that communicate with other programs over a network using **sockets**.

A socket acts as a communication endpoint between two applications.

For example:

```text
Laptop (Client)
        │
        │
     Internet
        │
        │
Server
```

The client and server communicate by sending and receiving data through sockets.

---

# Why Do We Need Socket Programming?

Without socket programming:

* Applications cannot communicate over a network.
* No web browsing.
* No online gaming.
* No chat applications.
* No remote login (SSH).
* No file transfer.

Socket programming provides a standard interface for network communication.

---

# What is a Socket?

A **socket** is an endpoint for sending and receiving data across a network.

It is uniquely identified by:

```text
IP Address + Port Number
```

Example:

```text
192.168.1.100:8080
```

---

# Socket Programming in Linux

Linux provides socket programming through **system calls**.

Your C program requests networking services from the Linux kernel using functions like:

```c
socket()
bind()
listen()
accept()
connect()
send()
recv()
close()
```

These functions are defined in:

```c
#include <sys/socket.h>
```

---

# Client-Server Model

Socket programming follows the Client-Server Architecture.

```text
           Server
              ▲
              │
     Accept Connection
              │
     ┌────────┴────────┐
     │                 │
  Client 1         Client 2
```

Clients request services.

Servers provide services.

---

# Types of Socket Communication

## TCP Socket

* Reliable
* Ordered delivery
* Connection-oriented

Created using:

```c
socket(AF_INET, SOCK_STREAM, 0);
```

---

## UDP Socket

* Faster
* Connectionless
* No delivery guarantee

Created using:

```c
socket(AF_INET, SOCK_DGRAM, 0);
```

---

# Socket Lifecycle

A TCP connection follows this lifecycle.

## Server

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

---

## Client

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

# Step 1 — socket()

Creates a socket.

```c
int sockfd;

sockfd = socket(AF_INET, SOCK_STREAM, 0);
```

Returns:

* File descriptor on success
* -1 on failure

The kernel allocates a new socket object and returns a file descriptor.

---

# Step 2 — bind()

Associates the socket with an IP address and port.

```c
bind(sockfd,
     (struct sockaddr *)&server,
     sizeof(server));
```

Without `bind()`, the server has no address to listen on.

---

# Step 3 — listen()

Marks the socket as a listening socket.

```c
listen(sockfd, 5);
```

The server now waits for incoming client connections.

---

# Step 4 — accept()

Accepts a client connection.

```c
int clientfd;

clientfd = accept(sockfd,
                  NULL,
                  NULL);
```

`accept()` returns a **new socket descriptor** for communicating with the connected client.

The original listening socket remains available to accept more connections.

---

# Step 5 — connect()

Used by the client to establish a connection with the server.

```c
connect(sockfd,
        (struct sockaddr *)&server,
        sizeof(server));
```

This initiates the TCP Three-Way Handshake.

---

# Step 6 — send()

Sends data.

```c
send(sockfd,
     buffer,
     strlen(buffer),
     0);
```

---

# Step 7 — recv()

Receives data.

```c
recv(sockfd,
     buffer,
     sizeof(buffer),
     0);
```

---

# Step 8 — close()

Releases the socket.

```c
close(sockfd);
```

The kernel frees all resources associated with the socket.

---

# Communication Flow

```text
Client

socket()

↓

connect()

↓

send()

↓

recv()

↓

close()



Server

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

---

# Common Header Files

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#include <unistd.h>

#include <arpa/inet.h>

#include <netinet/in.h>

#include <sys/socket.h>
```

---

# Important Data Structures

## sockaddr

Generic socket address.

```c
struct sockaddr
```

---

## sockaddr_in

IPv4 socket address.

```c
struct sockaddr_in
```

Contains:

* IP address
* Port
* Address family

---

# Address Families

| Constant | Meaning            |
| -------- | ------------------ |
| AF_INET  | IPv4               |
| AF_INET6 | IPv6               |
| AF_UNIX  | Local UNIX sockets |

---

# Socket Types

| Constant    | Protocol |
| ----------- | -------- |
| SOCK_STREAM | TCP      |
| SOCK_DGRAM  | UDP      |

---

# Network Byte Order

Ports must be converted before sending over the network.

```c
htons(PORT);
```

IP addresses are converted using:

```c
inet_pton()

inet_addr()

inet_aton()
```

---

# File Descriptor

A socket is represented by a **file descriptor**.

Example:

```c
int sockfd = socket(...);
```

Suppose:

```text
sockfd = 3
```

The value `3` is simply a file descriptor returned by the Linux kernel.

The kernel internally keeps track of everything related to that socket.

---

# How the Kernel Sees a Socket

```text
Application

↓

socket()

↓

Linux Kernel

↓

Socket Object

↓

TCP/IP Stack

↓

Network Interface Card

↓

Network
```

Your application never talks directly to the network hardware.

Everything goes through the kernel.

---

# Example TCP Server

```text
Server Starts

↓

Create Socket

↓

Bind Port 8080

↓

Listen

↓

Wait

↓

Client Connects

↓

Accept Connection

↓

Receive Message

↓

Send Reply

↓

Close Client

↓

Wait Again
```

---

# Example TCP Client

```text
Client Starts

↓

Create Socket

↓

Connect to Server

↓

Send Message

↓

Receive Reply

↓

Close Connection
```

---

# Real-World Examples

Socket programming is used in:

* Web browsers
* Web servers
* SSH
* FTP
* Online games
* Messaging applications
* Database servers
* Cloud services
* Video conferencing
* Remote desktop software

---

# Advantages

* Fast communication
* Standard networking interface
* Portable across operating systems
* Supports TCP and UDP
* Efficient for client-server applications

---

# Common Errors

| Error               | Cause                           |
| ------------------- | ------------------------------- |
| `socket()` failed   | Unable to create socket         |
| `bind()` failed     | Port already in use             |
| `listen()` failed   | Socket not properly initialized |
| `accept()` failed   | Client connection error         |
| `connect()` failed  | Server unreachable              |
| `send()` failed     | Connection closed               |
| `recv()` returned 0 | Peer closed the connection      |

---

# Key Terms

| Term            | Meaning                                                |
| --------------- | ------------------------------------------------------ |
| Socket          | Communication endpoint                                 |
| Client          | Requests a service                                     |
| Server          | Provides a service                                     |
| Port            | Identifies an application                              |
| IP Address      | Identifies a device                                    |
| File Descriptor | Integer used by the kernel to represent an open socket |
| Address Family  | Type of addressing (IPv4, IPv6, UNIX)                  |
| Socket Type     | Communication method (TCP or UDP)                      |

---

# Key Takeaways

* Socket programming enables communication between applications over a network.
* Linux exposes networking through socket-related system calls.
* A socket is represented by a file descriptor.
* TCP uses `SOCK_STREAM`; UDP uses `SOCK_DGRAM`.
* A typical TCP server follows: `socket() → bind() → listen() → accept() → recv() → send() → close()`.
* A typical TCP client follows: `socket() → connect() → send() → recv() → close()`.
* The Linux kernel manages all socket resources and interacts with the network hardware on behalf of user programs.

---

# Conclusion

Socket programming is the bridge between user applications and the operating system's networking stack. By using a small set of system calls, applications can establish connections, exchange data, and build powerful network services. A solid understanding of socket programming basics is essential before learning individual socket system calls, TCP handshakes, I/O multiplexing, and advanced network programming techniques.

