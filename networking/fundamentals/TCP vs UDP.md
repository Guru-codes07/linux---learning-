# TCP vs UDP

**TCP (Transmission Control Protocol)** and **UDP (User Datagram Protocol)** are the two primary transport layer protocols in the TCP/IP model. They are responsible for transferring data between applications running on different devices.

Although both protocols serve the same purpose, they differ significantly in terms of reliability, speed, connection management, and use cases.

---

# What is TCP?

**TCP (Transmission Control Protocol)** is a **connection-oriented** protocol that provides **reliable**, **ordered**, and **error-checked** delivery of data.

Before transmitting data, TCP establishes a connection between the sender and the receiver.

---

# Features of TCP

* Connection-oriented
* Reliable communication
* Error detection
* Ordered delivery
* Flow control
* Congestion control
* Retransmission of lost packets
* Acknowledgements (ACKs)

---

# How TCP Works

TCP communication follows these steps:

```text
Client

↓

Three-Way Handshake

↓

Connection Established

↓

Data Transfer

↓

Four-Way Termination

↓

Connection Closed
```

---

# TCP Header

A TCP packet contains information such as:

* Source Port
* Destination Port
* Sequence Number
* Acknowledgement Number
* Flags (SYN, ACK, FIN, RST)
* Window Size
* Checksum

---

# Common Applications Using TCP

| Application | Port |
| ----------- | ---: |
| HTTP        |   80 |
| HTTPS       |  443 |
| SSH         |   22 |
| FTP         |   21 |
| SMTP        |   25 |
| POP3        |  110 |
| IMAP        |  143 |

These applications require reliable communication, where losing data is unacceptable.

---

# Advantages of TCP

* Reliable communication
* Guarantees packet delivery
* Packets arrive in order
* Detects transmission errors
* Automatic retransmission
* Suitable for large file transfers

---

# Disadvantages of TCP

* Higher overhead
* Slower than UDP
* Requires connection establishment
* More bandwidth used for acknowledgements

---

# What is UDP?

**UDP (User Datagram Protocol)** is a **connectionless** transport layer protocol.

Unlike TCP, UDP sends data without establishing a connection first.

There is no guarantee that packets will reach the destination or arrive in order.

---

# Features of UDP

* Connectionless
* Faster communication
* Low overhead
* No acknowledgements
* No retransmission
* No flow control
* No congestion control

---

# How UDP Works

```text
Sender

↓

Send Datagram

↓

Receiver
```

If a packet is lost, UDP does not resend it.

---

# UDP Header

The UDP header is much smaller than the TCP header and contains only:

* Source Port
* Destination Port
* Length
* Checksum

Because of its smaller header, UDP is faster and more efficient.

---

# Common Applications Using UDP

| Application     |    Port |
| --------------- | ------: |
| DNS             |      53 |
| DHCP            | 67 / 68 |
| TFTP            |      69 |
| SNMP            |     161 |
| VoIP            | Various |
| Online Gaming   | Various |
| Video Streaming | Various |

These applications prioritize speed over guaranteed delivery.

---

# Advantages of UDP

* Very fast
* Low latency
* Minimal overhead
* Suitable for real-time applications
* Efficient for broadcasting and multicasting

---

# Disadvantages of UDP

* No delivery guarantee
* Packets may be lost
* Packets may arrive out of order
* No retransmission
* No acknowledgement mechanism

---

# TCP vs UDP Comparison

| Feature            | TCP                           | UDP                    |
| ------------------ | ----------------------------- | ---------------------- |
| Full Form          | Transmission Control Protocol | User Datagram Protocol |
| Connection         | Connection-oriented           | Connectionless         |
| Reliability        | Reliable                      | Unreliable             |
| Speed              | Slower                        | Faster                 |
| Packet Order       | Guaranteed                    | Not guaranteed         |
| Error Recovery     | Yes                           | No                     |
| Flow Control       | Yes                           | No                     |
| Congestion Control | Yes                           | No                     |
| Acknowledgements   | Yes                           | No                     |
| Retransmission     | Yes                           | No                     |
| Header Size        | 20–60 bytes                   | 8 bytes                |
| Overhead           | High                          | Low                    |

---

# TCP vs UDP in Real Life

Imagine sending an important document.

### TCP

Like sending a registered courier.

* Tracking available
* Signature required
* Guaranteed delivery
* If lost, it is resent

Reliable but slower.

---

### UDP

Like making a live announcement over a loudspeaker.

* Message is spoken once
* No confirmation
* Fast communication
* Missed words are not repeated

Fast but less reliable.

---

# TCP Packet Flow

```text
Client

↓

SYN

↓

Server

↓

SYN + ACK

↓

Client

↓

ACK

↓

Connection Established

↓

Data Transfer

↓

FIN

↓

Connection Closed
```

---

# UDP Packet Flow

```text
Sender

↓

Send Packet

↓

Receiver
```

No connection setup.

No acknowledgements.

No retransmission.

---

# TCP in Socket Programming

Creating a TCP socket in C:

```c
int sockfd = socket(AF_INET, SOCK_STREAM, 0);
```

Server workflow:

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

Client workflow:

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

# UDP in Socket Programming

Creating a UDP socket in C:

```c
int sockfd = socket(AF_INET, SOCK_DGRAM, 0);
```

Typical workflow:

```text
socket()

↓

bind() (server only)

↓

sendto()

↓

recvfrom()

↓

close()
```

Since UDP is connectionless, there is no `listen()`, `accept()`, or `connect()` step in the basic communication flow.

---

# When Should You Use TCP?

Choose TCP when:

* Building a web server
* File transfer
* Email services
* Remote login (SSH)
* Database communication
* Banking applications
* Chat applications where message delivery matters

---

# When Should You Use UDP?

Choose UDP when:

* Online gaming
* Video streaming
* Audio streaming
* Live broadcasts
* DNS lookups
* Voice over IP (VoIP)
* Real-time sensor data

---

# Examples

### Example 1: Downloading a File

A missing packet would corrupt the file.

**Protocol Used:** TCP

---

### Example 2: Watching a Live Football Match

A lost video frame is usually less noticeable than buffering.

**Protocol Used:** UDP

---

### Example 3: Video Call

Small packet loss is acceptable if it keeps the conversation smooth.

**Protocol Used:** UDP

---

### Example 4: Online Banking

Every transaction must be delivered accurately.

**Protocol Used:** TCP

---

# Key Differences

| TCP                      | UDP               |
| ------------------------ | ----------------- |
| Reliable                 | Faster            |
| Connection-oriented      | Connectionless    |
| Larger header            | Smaller header    |
| Uses ACKs                | No ACKs           |
| Ordered packets          | Unordered packets |
| Retransmits lost packets | No retransmission |
| Better for accuracy      | Better for speed  |

---

# Key Takeaways

* TCP and UDP operate at the **Transport Layer** of the TCP/IP model.
* TCP establishes a connection before sending data, while UDP does not.
* TCP guarantees reliable and ordered delivery of packets.
* UDP prioritizes speed and low latency over reliability.
* TCP uses **`SOCK_STREAM`** in socket programming.
* UDP uses **`SOCK_DGRAM`** in socket programming.
* Choose TCP when data integrity is important, and choose UDP when low latency is the priority.

---

# Conclusion

TCP and UDP are the foundation of transport-layer communication in modern networks. TCP provides reliable, ordered, and error-checked delivery, making it ideal for applications where every byte of data matters. UDP sacrifices reliability to achieve lower latency and higher performance, making it the preferred choice for real-time applications such as streaming, gaming, and voice communication. Understanding the strengths and trade-offs of both protocols is essential for networking, Linux system programming, and socket programming in C.

