# Socket Options

Socket options are configuration settings that control the behavior of sockets. They allow developers to customize how sockets operate, improve performance, enable specific networking features, and modify default kernel behavior.

Socket options are configured using the `setsockopt()` system call and can be queried using `getsockopt()`.

---

# Why Do We Need Socket Options?

By default, sockets use the operating system's default settings.

However, applications often need to:

- Reuse ports after restarting
- Detect broken connections
- Disable Nagle's Algorithm
- Increase buffer sizes
- Configure timeouts
- Control packet transmission

Socket options provide these capabilities.

---

# Socket Option Functions

Linux provides two functions:

- `setsockopt()`
- `getsockopt()`

---

# setsockopt()

`setsockopt()` configures a socket option.

### Prototype

```c
#include <sys/socket.h>

int setsockopt(int sockfd,
               int level,
               int optname,
               const void *optval,
               socklen_t optlen);
```

---

# Parameters

| Parameter | Description |
|-----------|-------------|
| `sockfd` | Socket file descriptor |
| `level` | Protocol level |
| `optname` | Socket option to configure |
| `optval` | Pointer to option value |
| `optlen` | Size of the option value |

---

# Return Value

| Value | Meaning |
|-------|---------|
| `0` | Success |
| `-1` | Error |

---

# getsockopt()

Retrieves the current value of a socket option.

### Prototype

```c
int getsockopt(int sockfd,
               int level,
               int optname,
               void *optval,
               socklen_t *optlen);
```

---

# Socket Levels

Socket options belong to different protocol levels.

| Level | Description |
|--------|-------------|
| `SOL_SOCKET` | General socket options |
| `IPPROTO_TCP` | TCP-specific options |
| `IPPROTO_IP` | IPv4 options |
| `IPPROTO_IPV6` | IPv6 options |

---

# SO_REUSEADDR

Allows a socket to bind to an address that is still in the `TIME_WAIT` state.

Without this option:

```text
Server Stops

↓

Restart Immediately

↓

bind()

↓

Address already in use
```

With `SO_REUSEADDR`:

```text
Server Stops

↓

Restart

↓

bind()

↓

Success
```

### Example

```c
int opt = 1;

setsockopt(server_fd,
           SOL_SOCKET,
           SO_REUSEADDR,
           &opt,
           sizeof(opt));
```

This option is commonly used by almost every TCP server.

---

# SO_REUSEPORT

Allows multiple sockets to bind to the same port.

Useful for:

- Load balancing
- Multi-process servers
- High-performance applications

### Example

```c
int opt = 1;

setsockopt(server_fd,
           SOL_SOCKET,
           SO_REUSEPORT,
           &opt,
           sizeof(opt));
```

---

# SO_KEEPALIVE

Enables TCP Keep-Alive messages.

If a client disconnects unexpectedly without closing the connection, the kernel periodically sends small packets to determine whether the peer is still alive.

### Example

```c
int opt = 1;

setsockopt(sockfd,
           SOL_SOCKET,
           SO_KEEPALIVE,
           &opt,
           sizeof(opt));
```

---

# SO_RCVBUF

Changes the socket receive buffer size.

Larger buffers improve performance for high-speed networks.

### Example

```c
int size = 65536;

setsockopt(sockfd,
           SOL_SOCKET,
           SO_RCVBUF,
           &size,
           sizeof(size));
```

---

# SO_SNDBUF

Changes the socket send buffer size.

### Example

```c
int size = 65536;

setsockopt(sockfd,
           SOL_SOCKET,
           SO_SNDBUF,
           &size,
           sizeof(size));
```

---

# TCP_NODELAY

TCP normally groups small packets before sending them. This behavior is called **Nagle's Algorithm**.

For applications such as:

- Online games
- SSH
- Chat applications
- Voice calls

low latency is more important than bandwidth efficiency.

`TCP_NODELAY` disables Nagle's Algorithm.

### Example

```c
#include <netinet/tcp.h>

int opt = 1;

setsockopt(sockfd,
           IPPROTO_TCP,
           TCP_NODELAY,
           &opt,
           sizeof(opt));
```

---

# SO_LINGER

Controls what happens when `close()` is called on a socket.

Normally:

```text
close()

↓

Return Immediately

↓

Kernel Sends Remaining Data
```

With `SO_LINGER`, the application can wait until pending data has been transmitted or specify a timeout before forcefully closing the connection.

### Example

```c
struct linger lg;

lg.l_onoff = 1;
lg.l_linger = 5;

setsockopt(sockfd,
           SOL_SOCKET,
           SO_LINGER,
           &lg,
           sizeof(lg));
```

---

# SO_BROADCAST

Allows sending broadcast packets over UDP.

Without this option:

```text
sendto()

↓

Permission Denied
```

With `SO_BROADCAST` enabled:

```c
int opt = 1;

setsockopt(sockfd,
           SOL_SOCKET,
           SO_BROADCAST,
           &opt,
           sizeof(opt));
```

---

# SO_RCVTIMEO

Sets a timeout for receiving data.

Example:

```c
struct timeval tv;

tv.tv_sec = 5;
tv.tv_usec = 0;

setsockopt(sockfd,
           SOL_SOCKET,
           SO_RCVTIMEO,
           &tv,
           sizeof(tv));
```

If no data arrives within five seconds, `recv()` returns with an error.

---

# SO_SNDTIMEO

Sets a timeout for sending data.

```c
struct timeval tv;

tv.tv_sec = 5;
tv.tv_usec = 0;

setsockopt(sockfd,
           SOL_SOCKET,
           SO_SNDTIMEO,
           &tv,
           sizeof(tv));
```

---

# Example: Typical TCP Server

```c
int opt = 1;

setsockopt(server_fd,
           SOL_SOCKET,
           SO_REUSEADDR,
           &opt,
           sizeof(opt));

setsockopt(server_fd,
           SOL_SOCKET,
           SO_KEEPALIVE,
           &opt,
           sizeof(opt));
```

These are two of the most commonly configured socket options in production servers.

---

# Common Socket Options

| Option | Purpose |
|--------|---------|
| `SO_REUSEADDR` | Reuse local address |
| `SO_REUSEPORT` | Multiple sockets on the same port |
| `SO_KEEPALIVE` | Detect dead peers |
| `SO_RCVBUF` | Receive buffer size |
| `SO_SNDBUF` | Send buffer size |
| `SO_RCVTIMEO` | Receive timeout |
| `SO_SNDTIMEO` | Send timeout |
| `SO_LINGER` | Control socket close behavior |
| `SO_BROADCAST` | Enable UDP broadcast |
| `TCP_NODELAY` | Disable Nagle's Algorithm |

---

# getsockopt() Example

Retrieve the receive buffer size.

```c
int size;

socklen_t len = sizeof(size);

getsockopt(sockfd,
           SOL_SOCKET,
           SO_RCVBUF,
           &size,
           &len);

printf("Receive Buffer: %d\n", size);
```

---

# Real-World Applications

Socket options are used in:

- Web servers
- Chat servers
- Database servers
- Online games
- SSH servers
- FTP servers
- Proxy servers

---

# Best Practices

- Enable `SO_REUSEADDR` for TCP servers.
- Use `SO_KEEPALIVE` for long-lived connections.
- Increase buffer sizes for high-throughput applications.
- Use `TCP_NODELAY` only when low latency is more important than bandwidth efficiency.
- Configure timeouts to prevent applications from blocking indefinitely.

---

# Comparison

| Option | Level | Typical Use |
|--------|-------|-------------|
| `SO_REUSEADDR` | `SOL_SOCKET` | Restart servers quickly |
| `SO_REUSEPORT` | `SOL_SOCKET` | Multi-process servers |
| `SO_KEEPALIVE` | `SOL_SOCKET` | Detect broken connections |
| `SO_RCVBUF` | `SOL_SOCKET` | Increase receive performance |
| `SO_SNDBUF` | `SOL_SOCKET` | Increase send performance |
| `SO_LINGER` | `SOL_SOCKET` | Control connection termination |
| `SO_RCVTIMEO` | `SOL_SOCKET` | Receive timeout |
| `SO_SNDTIMEO` | `SOL_SOCKET` | Send timeout |
| `SO_BROADCAST` | `SOL_SOCKET` | UDP broadcasting |
| `TCP_NODELAY` | `IPPROTO_TCP` | Disable Nagle's Algorithm |

---

# Key Takeaways

- Socket options customize the behavior of sockets.
- `setsockopt()` configures socket options, while `getsockopt()` retrieves their values.
- `SO_REUSEADDR` allows servers to restart without waiting for the `TIME_WAIT` state to expire.
- `SO_KEEPALIVE` helps detect broken TCP connections.
- `TCP_NODELAY` disables Nagle's Algorithm to reduce latency.
- Buffer size and timeout options can significantly affect application performance and responsiveness.
- Proper use of socket options is essential for building robust, efficient, and production-ready network applications.

---

# Conclusion

Socket options provide fine-grained control over socket behavior and are an essential part of network programming. Whether improving performance with larger buffers, enabling quick server restarts with `SO_REUSEADDR`, or reducing latency using `TCP_NODELAY`, these options allow developers to optimize applications for a wide range of networking scenarios. Mastering socket options is a key step toward writing reliable, high-performance Linux network servers.
