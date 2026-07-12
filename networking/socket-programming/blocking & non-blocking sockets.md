# Blocking vs Non-Blocking Sockets

When writing network applications, a socket can operate in one of two modes:

- **Blocking Mode**
- **Non-Blocking Mode**

The mode determines how socket functions such as `accept()`, `connect()`, `recv()`, and `send()` behave when the requested operation cannot be completed immediately.

Understanding the difference is essential for building efficient and scalable network applications.

---

# What is a Blocking Socket?

A **blocking socket** causes the program to wait until the requested operation completes.

If data is not available, the program stops executing until data arrives.

This is the default behavior of sockets in Linux.

---

# Blocking Socket Example

Suppose a client is waiting for a message.

```c
recv(sockfd, buffer, sizeof(buffer), 0);
```

If no data is available:

```text
Program

↓

recv()

↓

Wait...

↓

Wait...

↓

Wait...

↓

Data Arrives

↓

Continue Execution
```

The thread remains blocked until data is received.

---

# Blocking Operations

The following socket functions block by default.

| Function | Waits For |
|----------|-----------|
| `accept()` | A client connection |
| `connect()` | Connection establishment |
| `recv()` | Incoming data |
| `send()` | Buffer space if full |

---

# Example: Blocking `accept()`

```c
int client = accept(server_fd, NULL, NULL);
```

If no client is trying to connect:

```text
Server

↓

accept()

↓

Waiting...

↓

Waiting...

↓

Client Connects

↓

accept() Returns
```

The server cannot execute the next line until a client connects.

---

# Example: Blocking `recv()`

```c
char buffer[1024];

recv(sockfd, buffer, sizeof(buffer), 0);
```

If the client sends nothing:

```text
recv()

↓

Waiting...

↓

Waiting...

↓

Waiting...

↓

Message Received

↓

Continue
```

---

# Advantages of Blocking Sockets

- Simple to understand
- Easy to implement
- Suitable for small applications
- Ideal for learning socket programming

---

# Disadvantages of Blocking Sockets

- Cannot handle many clients efficiently
- One slow client can block an entire thread
- Poor scalability
- Higher memory usage when combined with threads

---

# What is a Non-Blocking Socket?

A **non-blocking socket** never waits for an operation to complete.

If an operation cannot proceed immediately, the function returns without blocking.

Example:

```text
recv()

↓

No Data Available

↓

Return Immediately
```

The application decides what to do next.

---

# How to Create a Non-Blocking Socket

Linux provides the `fcntl()` system call.

Example:

```c
#include <fcntl.h>

int flags = fcntl(sockfd, F_GETFL, 0);

fcntl(sockfd, F_SETFL, flags | O_NONBLOCK);
```

This enables non-blocking mode for the socket.

---

# Using `recv()` in Non-Blocking Mode

```c
int bytes = recv(sockfd,
                 buffer,
                 sizeof(buffer),
                 0);
```

If data exists:

```text
recv()

↓

Returns Data
```

If no data exists:

```text
recv()

↓

Returns -1

errno = EAGAIN
```

The program continues running instead of waiting.

---

# Common Return Values

| Return Value | Meaning |
|--------------|---------|
| > 0 | Data received |
| 0 | Connection closed |
| -1 | Error or operation would block |

---

# Checking `errno`

```c
#include <errno.h>

int bytes = recv(sockfd, buffer, sizeof(buffer), 0);

if (bytes == -1)
{
    if (errno == EAGAIN || errno == EWOULDBLOCK)
    {
        printf("No data available.\n");
    }
}
```

`EAGAIN` and `EWOULDBLOCK` indicate that no data is currently available.

---

# Blocking vs Non-Blocking

Blocking:

```text
recv()

↓

Wait

↓

Wait

↓

Data Arrives

↓

Continue
```

---

Non-Blocking:

```text
recv()

↓

No Data

↓

Return Immediately

↓

Continue Executing
```

---

# Why Use Non-Blocking Sockets?

Imagine a chat server with 5,000 connected users.

If every socket blocks:

```text
Client 1

↓

Waiting

↓

Thread Blocked
```

Thousands of blocked threads waste system resources.

With non-blocking sockets:

```text
Client 1

↓

No Data

↓

Move to Client 2

↓

Move to Client 3

↓

Continue
```

The server remains responsive.

---

# Combining Non-Blocking Sockets with I/O Multiplexing

Modern servers rarely use non-blocking sockets alone.

They combine them with:

- `select()`
- `poll()`
- `epoll()`

Workflow:

```text
Clients

↓

epoll()

↓

Ready Socket

↓

recv()

↓

Process Data
```

The server only reads sockets that are ready.

---

# Blocking Server

```text
Client 1

↓

recv()

↓

Waiting...

↓

Server Stops
```

---

# Non-Blocking Server

```text
Client 1

↓

No Data

↓

Check Client 2

↓

Check Client 3

↓

Continue
```

---

# Example

Blocking:

```c
recv(sockfd, buffer, sizeof(buffer), 0);
printf("Message received\n");
```

The program waits.

---

Non-Blocking:

```c
int bytes = recv(sockfd,
                 buffer,
                 sizeof(buffer),
                 0);

if (bytes > 0)
{
    printf("Message received\n");
}
```

The program continues immediately if no data is available.

---

# When Should You Use Blocking Sockets?

Blocking sockets are suitable for:

- Simple TCP clients
- Small servers
- Learning socket programming
- Programs with only one client

---

# When Should You Use Non-Blocking Sockets?

Non-blocking sockets are preferred for:

- Chat servers
- Web servers
- Proxy servers
- Multiplayer game servers
- High-performance applications
- Event-driven architectures

---

# Real-World Examples

| Application | Socket Type |
|-------------|-------------|
| Nginx | Non-Blocking |
| Redis | Non-Blocking |
| HAProxy | Non-Blocking |
| Node.js | Non-Blocking |
| Apache (Prefork) | Mostly Blocking |
| Simple Echo Server | Blocking |

---

# Advantages and Disadvantages

## Blocking Sockets

### Advantages

- Simple code
- Easier debugging
- Straightforward programming model

### Disadvantages

- Poor scalability
- Threads spend time waiting
- Higher memory usage

---

## Non-Blocking Sockets

### Advantages

- High scalability
- Better CPU utilization
- Suitable for event-driven programming
- Handles thousands of connections

### Disadvantages

- More complex code
- Requires handling `EAGAIN` and `EWOULDBLOCK`
- Usually combined with `select()`, `poll()`, or `epoll()`

---

# Comparison

| Feature | Blocking | Non-Blocking |
|---------|----------|--------------|
| Waits for data | Yes | No |
| Returns immediately | No | Yes |
| Easier to program | Yes | No |
| High scalability | No | Yes |
| Used in modern servers | Rarely | Yes |
| CPU efficiency | Lower | Higher |

---

# Summary

| Feature | Blocking Socket | Non-Blocking Socket |
|---------|-----------------|---------------------|
| Waits for operations | Yes | No |
| Suitable for beginners | Yes | Moderate |
| Thread blocking | Yes | No |
| Scalability | Low | High |
| Typical use | Small applications | High-performance servers |

---

# Key Takeaways

- Sockets operate in either **blocking** or **non-blocking** mode.
- Blocking sockets wait until an operation completes.
- Non-blocking sockets return immediately if an operation cannot be completed.
- `fcntl()` with `O_NONBLOCK` enables non-blocking mode.
- `recv()` on a non-blocking socket returns `-1` with `errno` set to `EAGAIN` or `EWOULDBLOCK` when no data is available.
- Modern network servers combine non-blocking sockets with I/O multiplexing APIs such as `select()`, `poll()`, and `epoll()` for high performance.

---

# Conclusion

Blocking sockets are simple and well-suited for learning and small-scale applications, while non-blocking sockets provide the scalability required for modern network servers. By avoiding unnecessary waiting and integrating with event-driven mechanisms like `epoll()`, non-blocking sockets enable efficient handling of thousands of simultaneous client connections.
