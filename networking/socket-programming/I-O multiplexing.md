# I/O Multiplexing

I/O Multiplexing (Input/Output Multiplexing) is a technique that allows a single process or thread to monitor multiple file descriptors simultaneously. It enables a server to handle multiple clients efficiently without creating a separate thread or process for every connection.

I/O Multiplexing is widely used in high-performance servers such as **Nginx**, **Redis**, **HAProxy**, and modern network applications.

---

# Why Do We Need I/O Multiplexing?

Imagine a chat server with 1,000 connected clients.

Without I/O Multiplexing, the server has two common choices:

- Create one thread for each client.
- Create one process for each client.

Both approaches consume significant CPU time and memory.

Instead, the server can monitor all client sockets using a single thread and only process those that are ready.

---

# Traditional Approach

One Thread Per Client

```text
             Server
                │
     ┌──────────┼──────────┐
     │          │          │
 Thread 1   Thread 2   Thread 3
     │          │          │
 Client 1   Client 2   Client 3
```

Problems:

- High memory usage
- Frequent context switching
- Limited scalability
- Thousands of threads become expensive

---

# I/O Multiplexing Approach

```text
                 Server
                    │
          I/O Multiplexing
                    │
     ┌──────────────┼──────────────┐
     │              │              │
 Client 1       Client 2       Client 3
```

One thread monitors all sockets.

The kernel informs the server when a socket becomes ready.

---

# What is a File Descriptor?

In Linux, almost everything is represented as a **file descriptor**.

Examples:

- Files
- Pipes
- Terminals
- Sockets

Example:

```c
int sockfd = socket(AF_INET, SOCK_STREAM, 0);
```

Suppose:

```text
sockfd = 3
```

The integer `3` is a file descriptor managed by the kernel.

---

# What Does "Ready" Mean?

A socket is considered ready when an operation can be performed without blocking.

Examples:

| Ready For | Meaning |
|-----------|---------|
| Read | Data is available |
| Write | Data can be sent |
| Accept | A client is waiting to connect |
| Error | An error occurred |

---

# How I/O Multiplexing Works

```text
Clients

↓

Kernel

↓

Checks Every Socket

↓

Returns Ready Sockets

↓

Server Processes Them
```

Instead of repeatedly checking every socket manually, the server asks the kernel to notify it when something happens.

---

# Common I/O Multiplexing APIs

Linux provides several APIs.

| API | Operating System | Scalability |
|-----|------------------|-------------|
| select() | POSIX | Small number of sockets |
| poll() | POSIX | Medium workloads |
| epoll() | Linux | Very large workloads |

---

# 1. select()

The oldest I/O multiplexing API.

Example:

```text
Monitor:

Socket 3

Socket 4

Socket 5

↓

select()

↓

Socket 5 Ready

↓

Read Data
```

Advantages:

- Portable
- Easy to understand

Disadvantages:

- Maximum file descriptor limit (`FD_SETSIZE`)
- Scans every descriptor on each call
- Slower for many clients

---

# 2. poll()

Improves on `select()`.

Instead of using bit masks, it uses an array of structures.

Advantages:

- No `FD_SETSIZE` limitation
- Simpler API

Disadvantages:

- Still scans every socket
- Performance decreases as the number of connections grows

---

# 3. epoll()

Linux's high-performance I/O multiplexing API.

Instead of scanning every socket, the kernel notifies the application only when events occur.

```text
Clients

↓

Kernel

↓

epoll_wait()

↓

Ready Clients

↓

Process Requests
```

Advantages:

- Excellent scalability
- Low CPU usage
- Event-driven
- Handles tens of thousands of connections efficiently

---

# Why epoll() is Faster

Suppose a server has:

```text
10,000 Clients
```

Only:

```text
12 Clients
```

are sending data.

### select()

Checks all 10,000 sockets.

### poll()

Checks all 10,000 sockets.

### epoll()

Returns only the 12 sockets that are ready.

No unnecessary scanning is performed.

---

# Server Workflow Using I/O Multiplexing

```text
Create Socket

↓

Bind

↓

Listen

↓

Create Multiplexer

↓

Add Listening Socket

↓

Wait for Events

↓

Process Ready Sockets

↓

Repeat
```

---

# Event Loop

The heart of I/O multiplexing is the **event loop**.

```text
while (1)
{
    Wait for Events

    Process Ready Sockets

    Go Back to Waiting
}
```

The server sleeps while waiting for events, reducing CPU usage.

---

# Blocking vs I/O Multiplexing

Blocking Server:

```text
Receive Client 1

↓

Wait

↓

Receive Client 2

↓

Wait

↓

Receive Client 3
```

Only one client is handled at a time.

---

Multiplexed Server:

```text
Wait for Events

↓

Client 2 Ready

↓

Read

↓

Client 8 Ready

↓

Read

↓

Client 3 Ready

↓

Write

↓

Repeat
```

Only active clients are processed.

---

# Real-World Applications

I/O Multiplexing is used in:

- Nginx
- Redis
- HAProxy
- Node.js
- Memcached
- PostgreSQL
- Chat servers
- Proxy servers
- Multiplayer game servers

---

# Advantages

- Handles many clients efficiently
- Low memory usage
- Fewer threads
- Lower CPU overhead
- Event-driven architecture
- Better scalability
- High performance

---

# Disadvantages

- More difficult to implement
- Event-driven programming is more complex
- Different APIs on different operating systems

---

# Comparison

| Feature | Thread Per Client | I/O Multiplexing |
|---------|-------------------|------------------|
| Threads | Many | One or Few |
| Memory Usage | High | Low |
| CPU Usage | High | Low |
| Context Switching | Frequent | Minimal |
| Scalability | Moderate | Excellent |
| Complexity | Easier | More Complex |

---

# Which API Should You Use?

| Number of Clients | Recommended API |
|-------------------|-----------------|
| Less than 100 | select() |
| 100 – 1,000 | poll() |
| More than 1,000 | epoll() |

---

# I/O Multiplexing in Your Chat Server

Your current chat server likely creates a thread for each connected client.

With I/O Multiplexing:

```text
Current Server

Client

↓

Thread

↓

Server

Improved Server

Clients

↓

epoll()

↓

One Event Loop

↓

Server
```

This approach scales much better as the number of clients increases.

---

# Key Terms

| Term | Meaning |
|------|---------|
| File Descriptor | Integer representing an open resource |
| Event | A socket becoming ready for an operation |
| Event Loop | Continuously waits for and processes events |
| Multiplexing | Monitoring multiple file descriptors simultaneously |
| Blocking | Waiting until an operation completes |
| Non-Blocking | Returning immediately if an operation cannot proceed |

---

# Key Takeaways

- I/O Multiplexing allows one process or thread to monitor multiple sockets simultaneously.
- It improves scalability by avoiding one thread or process per client.
- Linux provides three major I/O multiplexing APIs: `select()`, `poll()`, and `epoll()`.
- `select()` is simple but has scalability limitations.
- `poll()` removes descriptor limits but still scans all sockets.
- `epoll()` is Linux-specific and designed for high-performance servers.
- Modern network servers rely on event loops and I/O multiplexing to efficiently handle thousands of concurrent connections.

---

# Conclusion

I/O Multiplexing is a fundamental concept in high-performance network programming. By allowing a single thread to manage many client connections, it significantly reduces memory usage, minimizes CPU overhead, and enables servers to scale efficiently. Mastering I/O Multiplexing is an essential step toward understanding advanced topics such as **select()**, **poll()**, **epoll()**, asynchronous I/O, and event-driven server design.
