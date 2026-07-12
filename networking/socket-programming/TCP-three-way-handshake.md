# TCP Three-Way Handshake

The **TCP Three-Way Handshake** is the process used by the Transmission Control Protocol (TCP) to establish a reliable connection between a client and a server before any data is exchanged.

This handshake ensures that both devices are ready to communicate, agree on initial sequence numbers, and verify that the communication path is working.

---

# Why Do We Need the Three-Way Handshake?

Unlike UDP, TCP is a **connection-oriented protocol**.

Before sending data, TCP must ensure that:

- The server is available.
- The client is ready.
- Both sides can send and receive data.
- Sequence numbers are synchronized.
- A reliable communication channel is established.

This is accomplished using the **Three-Way Handshake**.

---

# The Three Steps

The handshake consists of three messages:

1. SYN
2. SYN-ACK
3. ACK

After these three messages, the TCP connection is established.

---

# Step 1: SYN (Synchronize)

The client wants to establish a connection.

It sends a **SYN** packet to the server.

```text
Client                        Server

  SYN  ----------------------->
```

The SYN packet contains:

- SYN flag = 1
- Initial Sequence Number (ISN)

Example:

```text
SYN

Sequence Number = 1000
```

The client says:

> "I want to connect. My first sequence number is 1000."

---

# Step 2: SYN-ACK (Synchronize Acknowledge)

The server receives the SYN packet.

If it is ready to accept connections, it responds with:

```text
SYN + ACK
```

```text
Client                        Server

  SYN  ----------------------->

       <------------------  SYN + ACK
```

The server sends:

```text
Sequence Number = 5000

Acknowledgment Number = 1001
```

The acknowledgment number is:

```text
Client Sequence Number + 1
```

because the SYN consumes one sequence number.

The server says:

> "I received your SYN. My sequence number is 5000."

---

# Step 3: ACK (Acknowledge)

The client receives the SYN-ACK.

It sends one final ACK packet.

```text
Client                        Server

  SYN ----------------------->

       <------------------ SYN + ACK

  ACK ----------------------->
```

The client sends:

```text
Sequence Number = 1001

Acknowledgment Number = 5001
```

Now both sides know:

- The connection works.
- Both devices are synchronized.
- Data transmission can begin.

---

# Complete Handshake

```text
                TCP Three-Way Handshake

Client                                 Server

   SYN (Seq = 1000)
--------------------------------------------->

                     SYN + ACK
          (Seq = 5000, Ack = 1001)
<---------------------------------------------

   ACK (Seq = 1001, Ack = 5001)
--------------------------------------------->

        Connection Established
```

---

# Sequence Numbers

Every byte sent over a TCP connection has a sequence number.

Example:

```text
Client

Sequence Number = 1000
```

If the client sends:

```text
Hello
```

which contains 5 bytes,

the next sequence number becomes:

```text
1005
```

Sequence numbers help TCP:

- Detect lost packets
- Detect duplicate packets
- Reassemble packets in order

---

# Acknowledgment Numbers

The acknowledgment number tells the sender:

> "I have received everything up to this point."

Example:

Client sends:

```text
Sequence = 1000

Length = 5 Bytes
```

Server replies:

```text
ACK = 1005
```

This means:

> "I have received bytes 1000–1004. Send byte 1005 next."

---

# TCP Flags Used During the Handshake

TCP packets contain control flags.

| Flag | Meaning |
|------|---------|
| SYN | Synchronize sequence numbers |
| ACK | Acknowledge received data |
| FIN | Finish connection |
| RST | Reset connection |
| PSH | Push data immediately |
| URG | Urgent data |

Only **SYN** and **ACK** are used during the Three-Way Handshake.

---

# Why Can't TCP Use Two Steps?

Suppose only:

```text
Client

↓

SYN

↓

Server

↓

ACK
```

The client would not know whether the server's acknowledgment was actually received.

The third ACK confirms that both sides are synchronized.

---

# Why Is It Called "Three-Way"?

Because three packets are exchanged:

```text
1. SYN

2. SYN + ACK

3. ACK
```

Only after all three packets does the connection become active.

---

# What Happens After the Handshake?

Once the connection is established:

```text
Client

↓

Send Data

↓

Receive Data

↓

Server
```

TCP guarantees:

- Reliable delivery
- Ordered delivery
- Error checking
- Flow control
- Congestion control

---

# Handshake in Socket Programming

When a client calls:

```c
connect(sockfd,
        (struct sockaddr *)&server,
        sizeof(server));
```

the operating system automatically performs the Three-Way Handshake.

The programmer does **not** manually send SYN or ACK packets.

---

On the server:

```c
listen(sockfd, 5);
```

waits for incoming connection requests.

When:

```c
accept(sockfd,
       NULL,
       NULL);
```

is called, the kernel completes the handshake and returns a new connected socket.

---

# Connection States

During the handshake, TCP moves through several states.

### Client

```text
CLOSED

↓

SYN_SENT

↓

ESTABLISHED
```

---

### Server

```text
LISTEN

↓

SYN_RECEIVED

↓

ESTABLISHED
```

---

# Visual State Diagram

```text
Client                     Server

CLOSED                     LISTEN

   │                           │
   │------ SYN --------------->│
   │                           │
SYN_SENT                  SYN_RECEIVED
   │                           │
   │<---- SYN + ACK -----------│
   │                           │
   │------ ACK --------------->│
   │                           │
ESTABLISHED              ESTABLISHED
```

---

# Real-World Example

Imagine making a phone call.

**Step 1**

You call your friend.

> "Hello?"

---

**Step 2**

Your friend answers.

> "Hi! I can hear you."

---

**Step 3**

You reply.

> "Great! I can hear you too."

Now both of you know that communication works in both directions.

This is exactly how the TCP Three-Way Handshake works.

---

# Advantages

- Reliable connection establishment
- Synchronizes sequence numbers
- Prevents old duplicate packets from creating false connections
- Verifies both client and server are ready
- Enables reliable data transfer

---

# Common Misconceptions

### Does the Programmer Send SYN Packets?

No.

The operating system automatically handles the handshake when using:

```c
connect()
```

and

```c
accept()
```

---

### Is the Handshake Used by UDP?

No.

UDP is **connectionless**.

It immediately sends data without establishing a connection.

---

# Comparison: TCP vs UDP

| Feature | TCP | UDP |
|---------|-----|-----|
| Connection | Required | Not Required |
| Handshake | Three-Way Handshake | None |
| Reliability | Yes | No |
| Ordered Delivery | Yes | No |
| Speed | Slower | Faster |

---

# Summary

| Step | Packet | Purpose |
|------|--------|---------|
| 1 | SYN | Client requests connection |
| 2 | SYN + ACK | Server acknowledges and responds |
| 3 | ACK | Client confirms connection |

---

# Key Takeaways

- TCP is a connection-oriented protocol.
- Before data transfer, TCP establishes a connection using the Three-Way Handshake.
- The handshake consists of **SYN**, **SYN-ACK**, and **ACK** packets.
- Sequence numbers synchronize communication between the client and server.
- Acknowledgment numbers confirm successful packet reception.
- Functions such as `connect()` and `accept()` automatically trigger the handshake.
- Once the handshake is complete, both client and server enter the **ESTABLISHED** state and can exchange data reliably.

---

# Conclusion

The TCP Three-Way Handshake is the foundation of reliable communication in TCP. By synchronizing sequence numbers, confirming bidirectional communication, and ensuring that both endpoints are ready, it creates a dependable connection before any application data is transmitted. Understanding this process is essential for learning advanced networking topics such as **TCP Connection Termination**, **Flow Control**, **Congestion Control**, and **Packet Analysis using Wireshark**.
