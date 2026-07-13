# epoll()

`epoll()` is a high-performance I/O Multiplexing API available on Linux. It is designed to efficiently monitor large numbers of file descriptors and is the preferred choice for building scalable network servers.

Unlike `select()` and `poll()`, `epoll()` does **not** repeatedly scan every file descriptor. Instead, the Linux kernel notifies the application only when an event occurs.

Modern servers such as **Nginx**, **Redis**, **HAProxy**, and many game servers use `epoll()` because it can efficiently handle tens of thousands of simultaneous connections.

---

# Why Was epoll() Introduced?

Although `select()` and `poll()` support monitoring multiple file descriptors, they become inefficient as the number of connections grows.

Suppose a server has:

```text
10,000 Connected Clients
```

Only:

```text
15 Clients
```

are sending data.

### select()

Checks all 10,000 sockets.

### poll()

Checks all 10,000 sockets.

### epoll()

Returns only the 15 sockets that are ready.

This makes `epoll()` significantly more efficient.

---

# How epoll() Works

```text
Clients

↓

Linux Kernel

↓

epoll()

↓

Ready File Descriptors

↓

Application
```

Instead of asking:

> "Is socket 1 ready?"

> "Is socket 2 ready?"

> "Is socket 3 ready?"

The application simply asks:

> "Tell me which sockets are ready."

---

# epoll Workflow

```text
Create epoll Instance

↓

Register File Descriptors

↓

Wait for Events

↓

Process Ready Events

↓

Repeat
```

---

# epoll API

Linux provides three main functions:

- `epoll_create1()`
- `epoll_ctl()`
- `epoll_wait()`

---

# epoll_create1()

Creates a new epoll instance.

### Prototype

```c
#include <sys/epoll.h>

int epoll_create1(int flags);
```

### Example

```c
int epfd = epoll_create1(0);
```

### Return Value

| Value | Meaning |
|-------|---------|
| ≥ 0 | epoll file descriptor |
| -1 | Error |

The returned file descriptor represents the epoll instance.

---

# epoll_ctl()

Adds, modifies, or removes file descriptors from the epoll instance.

### Prototype

```c
int epoll_ctl(int epfd,
              int op,
              int fd,
              struct epoll_event *event);
```

---

# Parameters

| Parameter | Description |
|-----------|-------------|
| `epfd` | epoll instance |
| `op` | Operation |
| `fd` | File descriptor |
| `event` | Event configuration |

---

# Operations

| Operation | Meaning |
|-----------|---------|
| `EPOLL_CTL_ADD` | Add a file descriptor |
| `EPOLL_CTL_MOD` | Modify an existing descriptor |
| `EPOLL_CTL_DEL` | Remove a descriptor |

---

# Example

```c
struct epoll_event ev;

ev.events = EPOLLIN;

ev.data.fd = server_fd;

epoll_ctl(epfd,
          EPOLL_CTL_ADD,
          server_fd,
          &ev);
```

The server socket is now monitored for incoming data.

---

# struct epoll_event

```c
struct epoll_event
{
    uint32_t events;

    epoll_data_t data;
};
```

---

# Important Events

| Event | Meaning |
|--------|---------|
| `EPOLLIN` | Ready for reading |
| `EPOLLOUT` | Ready for writing |
| `EPOLLERR` | Error occurred |
| `EPOLLHUP` | Connection closed |
| `EPOLLET` | Edge-triggered mode |

---

# epoll_wait()

Waits until one or more events occur.

### Prototype

```c
int epoll_wait(int epfd,
               struct epoll_event *events,
               int maxevents,
               int timeout);
```

---

# Parameters

| Parameter | Description |
|-----------|-------------|
| `epfd` | epoll instance |
| `events` | Array for ready events |
| `maxevents` | Maximum events returned |
| `timeout` | Wait time in milliseconds |

---

# Example

```c
struct epoll_event events[64];

int n = epoll_wait(epfd,
                   events,
                   64,
                   -1);
```

`-1` means wait forever.

---

# Processing Events

```c
for (int i = 0; i < n; i++)
{
    if (events[i].events & EPOLLIN)
    {
        printf("Socket Ready\n");
    }
}
```

Only ready sockets are returned.

---

# Complete Workflow

```text
Create Socket

↓

Bind

↓

Listen

↓

epoll_create1()

↓

epoll_ctl(ADD)

↓

epoll_wait()

↓

Ready Events

↓

Process Clients

↓

Repeat
```

---

# Example Server Loop

```text
while (1)
{
    epoll_wait()

    for each ready socket

        Handle Event
}
```

The server sleeps until the kernel reports an event.

---

# Level-Triggered Mode

This is the default mode.

If data remains unread, `epoll_wait()` continues reporting the socket as ready.

Example:

```text
Data Available

↓

epoll_wait()

↓

Read Half

↓

epoll_wait()

↓

Still Ready
```

---

# Edge-Triggered Mode

Enabled using:

```c
EPOLLET
```

The kernel reports an event **only once** when new data arrives.

Example:

```text
Data Arrives

↓

epoll_wait()

↓

Read Data

↓

No More Events Until New Data Arrives
```

Applications using edge-triggered mode should read until `recv()` returns `EAGAIN` or `EWOULDBLOCK`.

---

# Level vs Edge Triggered

| Feature | Level Triggered | Edge Triggered |
|---------|-----------------|----------------|
| Default | Yes | No |
| Repeated Notifications | Yes | No |
| Faster | No | Yes |
| Easier to Program | Yes | No |
| Common in Beginners | Yes | No |

---

# Why epoll() is Fast

Suppose:

```text
100,000 Clients
```

Only:

```text
25 Clients
```

send data.

### select()

Checks all 100,000 sockets.

### poll()

Checks all 100,000 sockets.

### epoll()

Returns only the 25 active sockets.

The CPU performs far less work.

---

# epoll and Non-Blocking Sockets

`epoll()` is usually used with non-blocking sockets.

Example:

```text
Socket

↓

fcntl()

↓

O_NONBLOCK

↓

epoll()
```

This combination prevents the server from blocking while processing events.

---

# Real-World Applications

`epoll()` is used by:

- Nginx
- Redis
- HAProxy
- Memcached
- Node.js (Linux)
- MQTT Brokers
- Multiplayer Game Servers
- Chat Servers
- Reverse Proxies

---

# Advantages

- Extremely scalable
- Event-driven
- Low CPU usage
- Handles thousands of connections
- Linux kernel optimization
- Minimal memory overhead

---

# Disadvantages

- Linux-specific
- More complex than `select()` or `poll()`
- Edge-triggered mode requires careful programming

---

# Comparison

| Feature | select() | poll() | epoll() |
|---------|----------|---------|----------|
| Linux Only | No | No | Yes |
| File Descriptor Limit | Yes | No | No |
| Scans Every Descriptor | Yes | Yes | No |
| Event Driven | No | No | Yes |
| High Scalability | No | Moderate | Excellent |
| Performance | Moderate | Good | Excellent |

---

# Typical epoll Server

```text
Create Listening Socket

↓

Create epoll Instance

↓

Register Listening Socket

↓

Wait for Events

↓

Accept New Clients

↓

Register Client Socket

↓

Wait for Events

↓

Read Data

↓

Send Response

↓

Repeat
```

---

# epoll in Your Chat Server

Instead of creating one thread for every client:

```text
Client 1 → Thread 1

Client 2 → Thread 2

Client 3 → Thread 3
```

You can use:

```text
Clients

↓

epoll_wait()

↓

Ready Clients

↓

Single Event Loop
```

This greatly reduces memory usage and improves scalability.

---

# Key Terms

| Term | Meaning |
|------|---------|
| epoll Instance | Kernel object that monitors file descriptors |
| Event | A file descriptor becoming ready |
| Level Triggered | Reports events until data is consumed |
| Edge Triggered | Reports events only when state changes |
| Event Loop | Continuously waits for and processes events |

---

# Key Takeaways

- `epoll()` is Linux's high-performance I/O Multiplexing API.
- It is designed for applications with thousands of simultaneous connections.
- The three main functions are `epoll_create1()`, `epoll_ctl()`, and `epoll_wait()`.
- Unlike `select()` and `poll()`, `epoll()` returns only the file descriptors that are ready.
- It supports both **Level-Triggered** and **Edge-Triggered** modes.
- `epoll()` is commonly used with non-blocking sockets to build scalable event-driven servers.

---

# Conclusion

`epoll()` is the foundation of modern Linux network programming. By eliminating unnecessary scanning of file descriptors and providing an event-driven interface, it enables applications to efficiently handle massive numbers of concurrent connections. Mastering `epoll()` is an essential step toward building production-grade servers and understanding the architecture of high-performance networking software such as Nginx, Redis, and HAProxy.
