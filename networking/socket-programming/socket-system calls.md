# Socket System Calls

Socket programming in Linux is built around a small set of **system calls** that allow applications to communicate over a network. These functions act as the interface between a user-space program and the Linux kernel's networking stack.

Every TCP or UDP application—whether it's a web server, SSH server, chat application, or browser—uses these system calls to create connections and exchange data.

---

# What are System Calls?

A **system call** is a function through which a user program requests a service from the Linux kernel.

Examples of system calls include:

* `open()`
* `read()`
* `write()`
* `close()`
* `fork()`
* `socket()`

For networking, Linux provides a dedicated set of socket-related system calls.

---

# Socket Programming Workflow

A typical TCP server follows this sequence:

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

A TCP client follows:

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

# socket()

## Purpose

Creates a new socket.

### Prototype

```c
int socket(int domain, int type, int protocol);
```

### Parameters

| Parameter  | Description     |
| ---------- | --------------- |
| `domain`   | Address family  |
| `type`     | Socket type     |
| `protocol` | Protocol to use |

Example:

```c
int sockfd = socket(AF_INET, SOCK_STREAM, 0);
```

### Return Value

Success:

```c
>= 0
```

Failure:

```c
-1
```

---

## Common Domains

| Constant   | Meaning            |
| ---------- | ------------------ |
| `AF_INET`  | IPv4               |
| `AF_INET6` | IPv6               |
| `AF_UNIX`  | UNIX Domain Socket |

---

## Common Socket Types

| Constant      | Protocol   |
| ------------- | ---------- |
| `SOCK_STREAM` | TCP        |
| `SOCK_DGRAM`  | UDP        |
| `SOCK_RAW`    | Raw Socket |

---

# bind()

## Purpose

Associates a socket with an IP address and port.

### Prototype

```c
int bind(int sockfd,
         const struct sockaddr *addr,
         socklen_t addrlen);
```

Example:

```c
bind(sockfd,
     (struct sockaddr *)&server,
     sizeof(server));
```

Without `bind()`, the server does not know which port to use.

### Return Value

Success:

```c
0
```

Failure:

```c
-1
```

---

# listen()

## Purpose

Marks a socket as a **listening socket**.

### Prototype

```c
int listen(int sockfd, int backlog);
```

Example:

```c
listen(sockfd, 5);
```

The second argument (`backlog`) specifies the maximum number of pending connection requests that can be queued before they are accepted.

### Return Value

Success:

```c
0
```

Failure:

```c
-1
```

---

# accept()

## Purpose

Accepts an incoming client connection.

### Prototype

```c
int accept(int sockfd,
           struct sockaddr *addr,
           socklen_t *addrlen);
```

Example:

```c
int clientfd = accept(sockfd,
                      NULL,
                      NULL);
```

### Important

`accept()` creates a **new socket** for the connected client.

The original listening socket remains open for future connections.

```text
Listening Socket
       │
       ├── Client Socket 1
       ├── Client Socket 2
       └── Client Socket 3
```

### Return Value

Success:

```c
New client socket descriptor
```

Failure:

```c
-1
```

---

# connect()

## Purpose

Connects a client socket to a remote server.

### Prototype

```c
int connect(int sockfd,
            const struct sockaddr *addr,
            socklen_t addrlen);
```

Example:

```c
connect(sockfd,
        (struct sockaddr *)&server,
        sizeof(server));
```

For TCP, this initiates the **Three-Way Handshake**.

### Return Value

Success:

```c
0
```

Failure:

```c
-1
```

---

# send()

## Purpose

Sends data through a connected socket.

### Prototype

```c
ssize_t send(int sockfd,
             const void *buf,
             size_t len,
             int flags);
```

Example:

```c
send(sockfd,
     message,
     strlen(message),
     0);
```

### Return Value

Returns the number of bytes sent.

---

# recv()

## Purpose

Receives data from a connected socket.

### Prototype

```c
ssize_t recv(int sockfd,
             void *buf,
             size_t len,
             int flags);
```

Example:

```c
recv(sockfd,
     buffer,
     sizeof(buffer),
     0);
```

### Return Value

| Value | Meaning                |
| ----- | ---------------------- |
| > 0   | Bytes received         |
| 0     | Peer closed connection |
| -1    | Error                  |

---

# sendto()

Used mainly with **UDP**.

### Prototype

```c
ssize_t sendto(int sockfd,
               const void *buf,
               size_t len,
               int flags,
               const struct sockaddr *dest_addr,
               socklen_t addrlen);
```

Unlike TCP, UDP specifies the destination address with every packet.

---

# recvfrom()

Receives UDP datagrams.

### Prototype

```c
ssize_t recvfrom(int sockfd,
                 void *buf,
                 size_t len,
                 int flags,
                 struct sockaddr *src_addr,
                 socklen_t *addrlen);
```

---

# close()

## Purpose

Closes a socket and releases kernel resources.

### Prototype

```c
int close(int fd);
```

Example:

```c
close(sockfd);
```

Always close sockets when they are no longer needed.

---

# shutdown()

Gracefully disables communication on a socket without immediately releasing it.

### Prototype

```c
int shutdown(int sockfd, int how);
```

Common values:

| Constant    | Meaning         |
| ----------- | --------------- |
| `SHUT_RD`   | Disable reading |
| `SHUT_WR`   | Disable writing |
| `SHUT_RDWR` | Disable both    |

---

# Common Socket System Calls

| Function     | Purpose                       |
| ------------ | ----------------------------- |
| `socket()`   | Create a socket               |
| `bind()`     | Assign address and port       |
| `listen()`   | Wait for incoming connections |
| `accept()`   | Accept a client               |
| `connect()`  | Connect to a server           |
| `send()`     | Send data                     |
| `recv()`     | Receive data                  |
| `sendto()`   | Send UDP data                 |
| `recvfrom()` | Receive UDP data              |
| `shutdown()` | Disable communication         |
| `close()`    | Close socket                  |

---

# Complete TCP Server Flow

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

close(client)

↓

accept()

↓

...
```

---

# Complete TCP Client Flow

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

# Common Errors

| Error          | Reason                     |
| -------------- | -------------------------- |
| `EADDRINUSE`   | Port already in use        |
| `ECONNREFUSED` | Server not running         |
| `ETIMEDOUT`    | Connection timed out       |
| `ECONNRESET`   | Peer reset the connection  |
| `EPIPE`        | Writing to a closed socket |

Use `perror()` to print human-readable error messages:

```c
perror("connect");
```

---

# Key Takeaways

* Socket programming relies on a small set of Linux system calls.
* `socket()` creates a communication endpoint.
* `bind()` assigns an address to a server socket.
* `listen()` prepares the server for incoming connections.
* `accept()` creates a new socket for each connected client.
* `connect()` establishes a connection from the client to the server.
* `send()` and `recv()` exchange data over TCP.
* `sendto()` and `recvfrom()` are commonly used with UDP.
* `close()` releases socket resources when communication is finished.

---

# Conclusion

Socket system calls form the core API for network programming in Linux. By combining functions such as `socket()`, `bind()`, `listen()`, `accept()`, `connect()`, `send()`, and `recv()`, developers can build everything from simple echo servers to scalable web servers and distributed systems. A solid understanding of these calls is essential before exploring socket address structures, byte order, non-blocking sockets, and I/O multiplexing.

