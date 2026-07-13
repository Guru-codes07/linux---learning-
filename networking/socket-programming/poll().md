# poll()

`poll()` is an I/O Multiplexing system call that allows a process to monitor multiple file descriptors simultaneously. It was introduced to overcome some of the limitations of `select()` while maintaining a similar programming model.

Unlike `select()`, `poll()` does not use `fd_set` and is not limited by `FD_SETSIZE`.

---

# Why Was poll() Introduced?

`select()` has two major limitations:

- Maximum number of file descriptors (`FD_SETSIZE`)
- Scans every descriptor on every call

`poll()` removes the descriptor limit and provides a cleaner interface.

---

# Function Prototype

```c
#include <poll.h>

int poll(struct pollfd *fds,
         nfds_t nfds,
         int timeout);
```

---

# Parameters

| Parameter | Description |
|-----------|-------------|
| `fds` | Array of pollfd structures |
| `nfds` | Number of file descriptors |
| `timeout` | Time to wait (milliseconds) |

---

# Return Value

| Value | Meaning |
|-------|---------|
| > 0 | Number of ready descriptors |
| 0 | Timeout occurred |
| -1 | Error |

---

# struct pollfd

`poll()` uses the following structure.

```c
struct pollfd
{
    int fd;
    short events;
    short revents;
};
```

---

# Members

| Member | Description |
|--------|-------------|
| `fd` | File descriptor |
| `events` | Events to monitor |
| `revents` | Events returned by the kernel |

---

# Common Events

| Event | Meaning |
|--------|---------|
| `POLLIN` | Data available to read |
| `POLLOUT` | Ready for writing |
| `POLLERR` | Error occurred |
| `POLLHUP` | Connection closed |
| `POLLNVAL` | Invalid file descriptor |

---

# Example

```c
struct pollfd fds[2];

fds[0].fd = server_fd;
fds[0].events = POLLIN;

fds[1].fd = client_fd;
fds[1].events = POLLIN;
```

---

# Calling poll()

```c
poll(fds,
     2,
     -1);
```

`-1` means wait forever.

---

# Checking Events

```c
if (fds[0].revents & POLLIN)
{
    printf("Server socket is ready.\n");
}
```

---

# Monitoring Multiple Clients

```text
Server

↓

poll()

↓

Client 3 Ready

↓

Process Client 3
```

---

# Timeout

Wait forever:

```c
poll(fds, count, -1);
```

Wait 5 seconds:

```c
poll(fds, count, 5000);
```

Do not wait:

```c
poll(fds, count, 0);
```

---

# Example Server Loop

```text
while (1)
{
    poll()

    Check revents

    Process Ready Clients
}
```

---

# Advantages

- No `FD_SETSIZE` limitation
- Easier API
- Supports many descriptors
- Portable across POSIX systems

---

# Disadvantages

- Still scans every descriptor
- Slower than `epoll()` for very large servers
- Higher CPU usage with thousands of connections

---

# poll() vs select()

| Feature | select() | poll() |
|----------|----------|---------|
| Uses `fd_set` | Yes | No |
| Uses Array | No | Yes |
| FD Limit | Yes | No |
| Portable | Yes | Yes |
| Performance | Moderate | Better |
| Used in Large Servers | Rarely | Sometimes |

---

# poll() vs epoll()

| Feature | poll() | epoll() |
|----------|---------|----------|
| Scans Every Descriptor | Yes | No |
| Event Driven | No | Yes |
| Linux Specific | No | Yes |
| Scalability | Good | Excellent |
| Large Servers | Moderate | Excellent |

---

# Real-World Usage

`poll()` is commonly used in:

- Network utilities
- Embedded Linux applications
- Medium-sized servers
- Terminal applications

Most modern Linux servers prefer `epoll()` for better scalability.

---

# Key Takeaways

- `poll()` is an improved version of `select()`.
- It uses an array of `pollfd` structures instead of `fd_set`.
- It removes the file descriptor limit imposed by `select()`.
- The kernel reports events through the `revents` field.
- Although better than `select()`, `poll()` still scans all descriptors, making `epoll()` the preferred choice for high-performance servers.

---

# Conclusion

`poll()` provides a cleaner and more scalable interface than `select()`, making it suitable for applications that need to monitor many file descriptors. However, for servers handling thousands of concurrent connections, Linux developers typically use `epoll()`, which offers significantly better performance through an event-driven design.
