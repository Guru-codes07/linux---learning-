# Byte Order (Endianness)

Computers store multi-byte values (such as integers and port numbers) in memory using a specific **byte order**. Different computer architectures use different byte orders, which can cause communication problems when data is transmitted over a network.

To solve this problem, the Internet uses a standard byte order called **Network Byte Order**.

Understanding byte order is essential for socket programming because functions such as `htons()`, `htonl()`, `ntohs()`, and `ntohl()` rely on it.

---

# What is a Byte?

A **byte** is the basic unit of memory and consists of **8 bits**.

Example:

```text
00000001
```

= 1 Byte

Larger data types occupy multiple bytes.

| Data Type | Size |
|-----------|------|
| char | 1 Byte |
| short | 2 Bytes |
| int | 4 Bytes |
| long long | 8 Bytes |

---

# What is Byte Order?

Byte order is the order in which multiple bytes of a number are stored in memory.

Consider the hexadecimal number:

```text
0x12345678
```

This occupies four bytes:

```text
12
34
56
78
```

Different CPUs store these bytes differently.

---

# Types of Byte Order

There are two major byte orders:

- Big Endian
- Little Endian

---

# Big Endian

Big Endian stores the **Most Significant Byte (MSB)** first.

Example:

```text
Value

0x12345678
```

Memory Layout:

```text
Address

1000 → 12

1001 → 34

1002 → 56

1003 → 78
```

The highest-order byte comes first.

---

# Little Endian

Little Endian stores the **Least Significant Byte (LSB)** first.

Memory Layout:

```text
Address

1000 → 78

1001 → 56

1002 → 34

1003 → 12
```

The lowest-order byte comes first.

---

# Comparison

Suppose we store:

```text
0x12345678
```

| Address | Big Endian | Little Endian |
|---------|------------|---------------|
| 1000 | 12 | 78 |
| 1001 | 34 | 56 |
| 1002 | 56 | 34 |
| 1003 | 78 | 12 |

The value is identical.

Only the storage order changes.

---

# Why Does This Matter?

Suppose:

A Little Endian computer sends:

```text
0x1234
```

without converting it.

The bytes sent are:

```text
34

12
```

A Big Endian computer interprets those bytes as:

```text
0x3412
```

instead of

```text
0x1234
```

This produces incorrect results.

---

# Network Byte Order

To avoid compatibility problems, all Internet protocols use a standard byte order.

**Network Byte Order = Big Endian**

Every computer converts data to Big Endian before sending it over the network.

The receiving computer converts it back to its own byte order.

---

# Host Byte Order

The byte order used internally by your CPU is called **Host Byte Order**.

Examples:

| Architecture | Byte Order |
|-------------|------------|
| x86 | Little Endian |
| x86-64 | Little Endian |
| ARM (most systems) | Little Endian |
| PowerPC | Big Endian |

Most modern desktop computers use **Little Endian**.

---

# Host vs Network Byte Order

```text
Application

↓

Host Byte Order

↓

htons()

↓

Network Byte Order

↓

Internet

↓

ntohs()

↓

Host Byte Order
```

---

# Why Do We Need Conversion?

Suppose:

Server:

```text
Port 8080
```

Binary:

```text
0001111110010000
```

A Little Endian CPU stores it differently from a Big Endian CPU.

Without conversion, the receiving system may interpret the wrong port number.

---

# htons()

**Host To Network Short**

Converts a 16-bit integer from host byte order to network byte order.

Prototype:

```c
uint16_t htons(uint16_t hostshort);
```

Example:

```c
server.sin_port = htons(8080);
```

This is why every socket program uses:

```c
htons(PORT);
```

---

# ntohs()

**Network To Host Short**

Converts a 16-bit integer received from the network into host byte order.

Prototype:

```c
uint16_t ntohs(uint16_t netshort);
```

Example:

```c
uint16_t port = ntohs(server.sin_port);
```

---

# htonl()

**Host To Network Long**

Converts a 32-bit integer.

Prototype:

```c
uint32_t htonl(uint32_t hostlong);
```

Example:

```c
uint32_t number = htonl(123456);
```

---

# ntohl()

**Network To Host Long**

Converts a 32-bit integer from network byte order.

Prototype:

```c
uint32_t ntohl(uint32_t netlong);
```

Example:

```c
uint32_t number = ntohl(received_number);
```

---

# Summary of Conversion Functions

| Function | Meaning | Size |
|----------|---------|------|
| `htons()` | Host to Network Short | 16-bit |
| `ntohs()` | Network to Host Short | 16-bit |
| `htonl()` | Host to Network Long | 32-bit |
| `ntohl()` | Network to Host Long | 32-bit |

---

# Why Don't We Convert Characters?

Characters occupy only **1 byte**.

Example:

```text
'A'
```

A single byte has only one possible ordering.

Therefore, conversion is unnecessary.

---

# Socket Programming Example

```c
struct sockaddr_in server;

server.sin_family = AF_INET;

server.sin_port = htons(8080);

server.sin_addr.s_addr = INADDR_ANY;
```

Notice:

Only the port uses `htons()`.

The address is handled separately.

---

# What About IP Addresses?

IP addresses are usually converted using:

```c
inet_pton()

inet_ntop()

inet_addr()

inet_aton()
```

Example:

```c
inet_pton(AF_INET,
          "192.168.1.100",
          &server.sin_addr);
```

These functions handle byte order internally.

---

# Real Example

Suppose:

```text
Port = 8080
```

Hexadecimal:

```text
0x1F90
```

Little Endian Memory:

```text
90

1F
```

Network Byte Order:

```text
1F

90
```

`htons()` performs this conversion automatically.

---

# Checking Your System's Byte Order

Example program:

```c
#include <stdio.h>

int main()
{
    unsigned int x = 1;

    char *c = (char *)&x;

    if (*c)
        printf("Little Endian\n");
    else
        printf("Big Endian\n");

    return 0;
}
```

Most Linux PCs will print:

```text
Little Endian
```

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

### Using `htonl()` for a Port

Incorrect:

```c
server.sin_port = htonl(8080);
```

Correct:

```c
server.sin_port = htons(8080);
```

Ports are **16-bit**, so use `htons()`.

---

### Forgetting `ntohs()` When Reading Data

Incorrect:

```c
printf("%d\n", server.sin_port);
```

Correct:

```c
printf("%d\n", ntohs(server.sin_port));
```

---

# Key Terms

| Term | Meaning |
|------|---------|
| Byte Order | Order of bytes in memory |
| Big Endian | Most Significant Byte first |
| Little Endian | Least Significant Byte first |
| Host Byte Order | Native byte order of the CPU |
| Network Byte Order | Standard byte order used on networks (Big Endian) |
| Endianness | The byte ordering used by a system |

---

# Key Takeaways

- Multi-byte values can be stored using different byte orders.
- The two common byte orders are **Big Endian** and **Little Endian**.
- Most modern computers use **Little Endian** internally.
- The Internet uses **Big Endian**, known as **Network Byte Order**.
- `htons()` and `htonl()` convert data from host to network byte order before sending.
- `ntohs()` and `ntohl()` convert received data back to the host's native byte order.
- Correct byte order conversion is essential for interoperable network communication.

---

# Conclusion

Byte order is a fundamental concept in network programming that ensures systems with different architectures can communicate correctly. By converting values to Network Byte Order before transmission and back to Host Byte Order after reception, applications maintain compatibility across platforms. Functions such as `htons()`, `htonl()`, `ntohs()`, and `ntohl()` are therefore an essential part of every socket programmer's toolkit.
