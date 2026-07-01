# Ports and Sockets

Ports and sockets are fundamental concepts in computer networking. While an **IP address** identifies a device on a network, a **port** identifies a specific application or service running on that device. A **socket** combines an IP address and a port number, creating a unique endpoint for communication between applications.

Understanding ports and sockets is essential for network programming, client-server applications, and protocols such as HTTP, FTP, SSH, and DNS.

---

# Why Do We Need Ports?

Imagine an apartment building.

* The **building address** represents the IP address.
* Each **apartment number** represents a port.

A postal worker first delivers the mail to the correct building (IP address), then to the correct apartment (port number).

Similarly:

* **IP Address → Identifies the device**
* **Port Number → Identifies the application**

Without ports, a computer would not know which application should receive incoming data.

---

# What is a Port?

A **port** is a **16-bit logical number** used by the Transport Layer (TCP or UDP) to identify a specific process or application on a computer.

Example:

```text
192.168.1.10:80
```

Here:

```text
IP Address : 192.168.1.10
Port       : 80
```

---

# Port Number Range

Ports range from:

```text
0 – 65535
```

They are divided into three categories.

| Range         | Name                      | Description                                      |
| ------------- | ------------------------- | ------------------------------------------------ |
| 0 – 1023      | Well-Known Ports          | Reserved for standard services                   |
| 1024 – 49151  | Registered Ports          | Used by applications                             |
| 49152 – 65535 | Dynamic / Ephemeral Ports | Temporary ports assigned by the operating system |

---

# Well-Known Ports

These ports are reserved for common Internet services.

| Port | Protocol | Service       |
| ---- | -------- | ------------- |
| 20   | TCP      | FTP (Data)    |
| 21   | TCP      | FTP (Control) |
| 22   | TCP      | SSH           |
| 23   | TCP      | Telnet        |
| 25   | TCP      | SMTP          |
| 53   | TCP/UDP  | DNS           |
| 67   | UDP      | DHCP Server   |
| 68   | UDP      | DHCP Client   |
| 80   | TCP      | HTTP          |
| 110  | TCP      | POP3          |
| 143  | TCP      | IMAP          |
| 443  | TCP      | HTTPS         |

---

# Registered Ports

These ports are assigned to software applications.

Examples:

```text
3306 → MySQL

5432 → PostgreSQL

6379 → Redis

8080 → Alternative HTTP

27017 → MongoDB
```

---

# Dynamic (Ephemeral) Ports

These ports are automatically assigned by the operating system when a client initiates a connection.

Example:

```text
Client:
192.168.1.20:52341

↓

Server:
142.250.193.78:443
```

The client's temporary port (`52341`) is automatically selected by the OS.

---

# What is a Socket?

A **socket** is one endpoint of a network communication.

A socket consists of:

```text
IP Address + Port Number
```

Example:

```text
192.168.1.10:8080
```

A socket uniquely identifies an application running on a device.

---

# Socket Communication

Communication always occurs between **two sockets**.

Example:

```text
Client Socket
192.168.1.20:52341
        │
        │
        ▼
Server Socket
142.250.193.78:443
```

---

# Socket Pair

A complete network connection is identified by four values:

```text
Source IP
Source Port
Destination IP
Destination Port
```

Example:

```text
192.168.1.20 : 52341

↓

142.250.193.78 : 443
```

This combination uniquely identifies a TCP connection.

---

# Types of Sockets

## 1. Stream Socket (TCP)

Uses:

* Reliable communication
* Ordered delivery
* Connection-oriented

Examples:

* HTTP
* HTTPS
* SSH
* FTP

In C:

```c
socket(AF_INET, SOCK_STREAM, 0);
```

---

## 2. Datagram Socket (UDP)

Uses:

* Faster communication
* Connectionless communication
* No delivery guarantee

Examples:

* DNS
* Online Games
* Live Streaming
* VoIP

In C:

```c
socket(AF_INET, SOCK_DGRAM, 0);
```

---

# How a Socket Works

A TCP server typically follows this sequence:

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

A TCP client typically follows:

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

# Ports in Client-Server Communication

Suppose a browser accesses:

```text
https://www.google.com
```

The connection might look like:

```text
Client

IP Address : 192.168.1.25
Port       : 52015

↓

Server

IP Address : 142.250.193.78
Port       : 443
```

The browser uses a temporary (ephemeral) port, while the web server listens on port **443**.

---

# Socket Address

In C socket programming, a socket address combines the IP address and port.

Example:

```c
struct sockaddr_in server;

server.sin_family = AF_INET;
server.sin_port = htons(8080);
server.sin_addr.s_addr = INADDR_ANY;
```

Where:

* `AF_INET` specifies IPv4.
* `htons()` converts the port to network byte order.
* `INADDR_ANY` allows the server to accept connections on all available interfaces.

---

# Ports and Protocols

| Protocol | Default Port |
| -------- | -----------: |
| HTTP     |           80 |
| HTTPS    |          443 |
| SSH      |           22 |
| FTP      |           21 |
| DNS      |           53 |
| SMTP     |           25 |
| POP3     |          110 |
| IMAP     |          143 |

---

# Finding Open Ports (Linux)

Display listening TCP and UDP ports:

```bash
ss -tuln
```

Display processes using network ports:

```bash
sudo ss -tulpn
```

Using `netstat` (if installed):

```bash
netstat -tuln
```

List processes using a specific port:

```bash
sudo lsof -i :8080
```

---

# Checking if a Port is Open

Using `nc` (Netcat):

```bash
nc -zv localhost 8080
```

Using `telnet`:

```bash
telnet localhost 8080
```

---

# Real-World Example

Suppose you're running your own TCP chat server.

Server:

```text
IP Address : 192.168.1.100
Port       : 8080
```

Clients connect from:

```text
192.168.1.10 : 52310

192.168.1.15 : 52311

192.168.1.20 : 52312
```

Although all clients communicate with the same server port (`8080`), each client uses a different ephemeral port. This allows the server to distinguish between multiple connections.

---

# Common Terms

| Term           | Meaning                                         |
| -------------- | ----------------------------------------------- |
| IP Address     | Identifies a device                             |
| Port           | Identifies an application                       |
| Socket         | Combination of IP address and port              |
| Endpoint       | One side of a communication                     |
| Client Socket  | Socket created by the client                    |
| Server Socket  | Socket that listens for incoming connections    |
| Ephemeral Port | Temporary port assigned by the operating system |

---

# Advantages of Using Ports and Sockets

* Multiple applications can use the network simultaneously.
* Supports client-server communication.
* Enables process-to-process communication.
* Allows many clients to connect to one server.
* Forms the basis of Internet communication.

---

# Key Takeaways

* An **IP address** identifies a device.
* A **port number** identifies an application running on that device.
* A **socket** is the combination of an IP address and a port number.
* TCP uses **stream sockets (`SOCK_STREAM`)**.
* UDP uses **datagram sockets (`SOCK_DGRAM`)**.
* A TCP connection is uniquely identified by the source IP, source port, destination IP, and destination port.
* Servers usually listen on well-known ports, while clients use temporary (ephemeral) ports.

---

# Conclusion

Ports and sockets are the bridge between applications and the network. IP addresses ensure that data reaches the correct device, while ports ensure it reaches the correct application. Together, they form sockets, which are the fundamental communication endpoints used by client-server applications. Whether you're building a web server, a chat application, or a file transfer program in C, understanding ports and sockets is essential for writing reliable network software.

