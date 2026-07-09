# Socket Address Structures

Socket address structures are data structures used by the Linux kernel to represent the address of a socket. They store information such as the **IP address**, **port number**, and **address family** required for network communication.

Every network application written in C uses socket address structures when creating servers and clients.

---

# Why Do We Need Socket Address Structures?

When a server starts, it must tell the operating system:

- Which IP address to use
- Which port to listen on
- Which protocol family (IPv4 or IPv6)

Similarly, when a client connects, it must specify:

- The server's IP address
- The server's port number

Instead of passing these values individually, Linux stores them inside **socket address structures**.

---

# Common Socket Address Structures

Linux provides several socket address structures.

| Structure | Purpose |
|-----------|---------|
| `sockaddr` | Generic socket address |
| `sockaddr_in` | IPv4 socket address |
| `sockaddr_in6` | IPv6 socket address |
| `sockaddr_un` | UNIX domain socket address |

The most commonly used structure is:

```c
struct sockaddr_in
```

because it is used for IPv4 networking.

---

# The Generic `sockaddr`

```c
struct sockaddr
{
    sa_family_t sa_family;
    char sa_data[14];
};
```

## Members

| Member | Description |
|--------|-------------|
| `sa_family` | Address family (`AF_INET`, `AF_INET6`, etc.) |
| `sa_data` | Generic address data |

### Why does it exist?

The kernel needs one common structure that can represent **any** type of socket address.

Because different protocols require different address information, `sockaddr` acts as a generic wrapper.

Normally, programmers **do not fill this structure directly**.

---

# The IPv4 `sockaddr_in`

The IPv4 address structure is:

```c
struct sockaddr_in
{
    sa_family_t    sin_family;
    in_port_t      sin_port;
    struct in_addr sin_addr;
    unsigned char  sin_zero[8];
};
```

This is the structure used in almost every TCP or UDP IPv4 program.

---

# Members of `sockaddr_in`

## 1. `sin_family`

Specifies the address family.

Example:

```c
server.sin_family = AF_INET;
```

Common values:

| Constant | Meaning |
|----------|---------|
| `AF_INET` | IPv4 |
| `AF_INET6` | IPv6 |
| `AF_UNIX` | UNIX Domain Sockets |

---

## 2. `sin_port`

Stores the port number.

Example:

```c
server.sin_port = htons(8080);
```

The port **must** be converted into **network byte order** using `htons()`.

---

## 3. `sin_addr`

Stores the IPv4 address.

Example:

```c
server.sin_addr.s_addr = INADDR_ANY;
```

or

```c
inet_pton(AF_INET, "192.168.1.10", &server.sin_addr);
```

---

## 4. `sin_zero`

```c
unsigned char sin_zero[8];
```

This field exists only to make the structure the same size as `struct sockaddr`.

Most programs simply initialize it to zero.

```c
memset(server.sin_zero, 0, sizeof(server.sin_zero));
```

Or more commonly:

```c
memset(&server, 0, sizeof(server));
```

This initializes every member, including `sin_zero`, to zero.

---

# Visual Representation

```text
+--------------------------------------+
| sin_family = AF_INET                 |
+--------------------------------------+
| sin_port = htons(8080)               |
+--------------------------------------+
| sin_addr = 192.168.1.100             |
+--------------------------------------+
| sin_zero = {0}                       |
+--------------------------------------+
```

---

# Creating an IPv4 Socket Address

```c
struct sockaddr_in server;

memset(&server, 0, sizeof(server));

server.sin_family = AF_INET;
server.sin_port = htons(8080);
server.sin_addr.s_addr = INADDR_ANY;
```

This prepares the server to listen on port **8080** on all available network interfaces.

---

# Using a Specific IP Address

Instead of `INADDR_ANY`, you can specify a particular address.

```c
inet_pton(AF_INET,
          "192.168.1.100",
          &server.sin_addr);
```

The server will now accept connections only on that IP address.

---

# `INADDR_ANY`

```c
server.sin_addr.s_addr = INADDR_ANY;
```

This tells the kernel:

> "Accept incoming connections on every available network interface."

Example:

```text
Wi-Fi      : 192.168.1.100

Ethernet   : 10.0.0.15

Loopback   : 127.0.0.1
```

The server listens on all of them.

---

# Why Do We Cast to `struct sockaddr *`?

Functions like `bind()`, `connect()`, and `accept()` expect a generic socket address.

Prototype:

```c
int bind(int sockfd,
         const struct sockaddr *addr,
         socklen_t addrlen);
```

But our variable is:

```c
struct sockaddr_in server;
```

So we cast it:

```c
bind(sockfd,
     (struct sockaddr *)&server,
     sizeof(server));
```

The kernel reads the first field (`sin_family`) to determine what type of address structure it has received.

---

# IPv6 Address Structure

For IPv6 networking:

```c
struct sockaddr_in6
```

Example:

```c
struct sockaddr_in6 server6;

server6.sin6_family = AF_INET6;
server6.sin6_port = htons(8080);
```

This structure stores a 128-bit IPv6 address.

---

# UNIX Domain Socket Address

For communication between processes on the same machine:

```c
struct sockaddr_un
```

Instead of an IP address, it stores a filesystem path.

Example:

```c
struct sockaddr_un local;
```

UNIX domain sockets are commonly used for Inter-Process Communication (IPC).

---

# Relationship Between Structures

```text
                sockaddr
                    ▲
                    │
        ┌───────────┼───────────┐
        │           │           │
 sockaddr_in   sockaddr_in6  sockaddr_un
   (IPv4)         (IPv6)      (UNIX IPC)
```

---

# Address Family Summary

| Address Family | Structure | Usage |
|---------------|-----------|-------|
| `AF_INET` | `sockaddr_in` | IPv4 |
| `AF_INET6` | `sockaddr_in6` | IPv6 |
| `AF_UNIX` | `sockaddr_un` | Local IPC |

---

# Example Server Initialization

```c
struct sockaddr_in server;

memset(&server, 0, sizeof(server));

server.sin_family = AF_INET;
server.sin_port = htons(8080);
server.sin_addr.s_addr = INADDR_ANY;

bind(sockfd,
     (struct sockaddr *)&server,
     sizeof(server));
```

This is the standard way to initialize an IPv4 server socket.

---

# Common Mistakes

### Forgetting `htons()`

Incorrect:

```c
server.sin_port = 8080;
```

Correct:

```c
server.sin_port = htons(8080);
```

---

### Not Initializing the Structure

Incorrect:

```c
struct sockaddr_in server;
```

Correct:

```c
memset(&server, 0, sizeof(server));
```

---

### Forgetting the Cast

Incorrect:

```c
bind(sockfd, &server, sizeof(server));
```

Correct:

```c
bind(sockfd,
     (struct sockaddr *)&server,
     sizeof(server));
```

---

# Summary

| Structure | Purpose |
|-----------|---------|
| `sockaddr` | Generic socket address |
| `sockaddr_in` | IPv4 socket address |
| `sockaddr_in6` | IPv6 socket address |
| `sockaddr_un` | UNIX domain socket |
| `sin_family` | Address family |
| `sin_port` | Port number |
| `sin_addr` | IPv4 address |
| `INADDR_ANY` | Listen on all interfaces |
| `htons()` | Convert port to network byte order |

---

# Key Takeaways

- Socket address structures identify network endpoints.
- `sockaddr` is the generic structure used by Linux socket APIs.
- `sockaddr_in` is the most commonly used structure for IPv4 programming.
- `sin_family` specifies the protocol family.
- `sin_port` stores the port number and should always use `htons()`.
- `sin_addr` stores the IPv4 address.
- `INADDR_ANY` allows the server to accept connections on all available interfaces.
- Functions such as `bind()`, `connect()`, and `accept()` require a `struct sockaddr *`, so `sockaddr_in` must be cast before being passed.

---

# Conclusion

Socket address structures are the foundation of socket programming in C. They package all the information required to identify communication endpoints, allowing the Linux kernel to establish network connections. Understanding these structures is essential before moving on to topics such as **Byte Order**, **TCP Three-Way Handshake**, **Blocking vs Non-Blocking Sockets**, and **I/O Multiplexing**.
