# ARP (Address Resolution Protocol)

**ARP (Address Resolution Protocol)** is a network-layer support protocol used to map an **IPv4 address** to a **MAC (Media Access Control) address** within a Local Area Network (LAN).

When a device knows the destination IP address but not the corresponding MAC address, it uses ARP to discover the destination's hardware address.

---

# Why Do We Need ARP?

Computers communicate differently at different layers.

At the Network Layer:

```text
IP Address

192.168.1.20
```

At the Data Link Layer:

```text
MAC Address

00:1A:2B:3C:4D:5E
```

To send an Ethernet frame, the sender must know the destination MAC address.

ARP performs this translation.

---

# Example

Suppose:

```text
PC A

IP : 192.168.1.10

MAC : AA:AA:AA:AA:AA:AA
```

wants to send data to:

```text
PC B

IP : 192.168.1.20

MAC : BB:BB:BB:BB:BB:BB
```

PC A knows:

```text
Destination IP

↓

192.168.1.20
```

But does **not** know:

```text
Destination MAC
```

ARP solves this problem.

---

# How ARP Works

```text
PC A

↓

ARP Request

↓

LAN Broadcast

↓

PC B

↓

ARP Reply

↓

MAC Address

↓

Ethernet Frame Sent
```

---

# Step 1 – ARP Request

The sender broadcasts:

```text
Who has 192.168.1.20?

Tell 192.168.1.10
```

Every device on the LAN receives this broadcast.

---

# Step 2 – ARP Reply

Only the device with the requested IP responds.

Example:

```text
192.168.1.20

is

BB:BB:BB:BB:BB:BB
```

The reply is sent directly back to the sender (unicast).

---

# Step 3 – ARP Cache Update

The sender stores the mapping.

```text
192.168.1.20

↓

BB:BB:BB:BB:BB:BB
```

Future packets can be sent immediately without another ARP request.

---

# Complete ARP Process

```text
Need MAC Address

↓

Check ARP Cache

↓

Found?

↓

Yes

↓

Send Frame

------------------------

No

↓

Broadcast ARP Request

↓

Receive ARP Reply

↓

Update ARP Cache

↓

Send Frame
```

---

# ARP Request

An ARP Request is always:

```text
Broadcast
```

Destination MAC:

```text
FF:FF:FF:FF:FF:FF
```

Every device on the local network receives it.

---

# ARP Reply

An ARP Reply is:

```text
Unicast
```

It is sent only to the device that made the request.

---

# Broadcast vs Unicast

| Packet | Type |
|----------|------|
| ARP Request | Broadcast |
| ARP Reply | Unicast |

---

# ARP Cache

Each operating system maintains an ARP cache.

Example:

```text
IP Address        MAC Address

192.168.1.1       08:00:27:12:34:56

192.168.1.20      BB:BB:BB:BB:BB:BB
```

The cache reduces network traffic by avoiding repeated ARP requests.

---

# Viewing the ARP Cache

Linux:

```bash
arp -a
```

or

```bash
ip neigh
```

Example output:

```text
192.168.1.1 dev wlan0 lladdr 08:00:27:12:34:56 REACHABLE
```

---

# ARP Cache Timeout

ARP entries are temporary.

After a timeout:

```text
Entry Removed

↓

Next Communication

↓

New ARP Request
```

This ensures the cache stays up to date.

---

# Gratuitous ARP

A device may send an ARP request for **its own IP address**.

Uses include:

- Detecting duplicate IP addresses
- Updating neighboring ARP caches
- High-availability systems
- Virtual IP failover

---

# Proxy ARP

In Proxy ARP, a router answers ARP requests on behalf of another device.

```text
Client

↓

ARP Request

↓

Router Replies

↓

Router Forwards Traffic
```

Proxy ARP is commonly used in certain enterprise network configurations.

---

# ARP Packet

An ARP packet contains:

- Hardware Type
- Protocol Type
- Hardware Address Length
- Protocol Address Length
- Operation (Request or Reply)
- Sender MAC Address
- Sender IP Address
- Target MAC Address
- Target IP Address

---

# ARP Packet Flow

```text
Sender

↓

Broadcast

↓

Switch

↓

All Devices

↓

Correct Device

↓

Unicast Reply

↓

Sender Learns MAC
```

---

# Example

Suppose:

```text
PC A

IP

192.168.1.5
```

needs to send data to:

```text
192.168.1.8
```

Sequence:

```text
ARP Request

↓

Who has 192.168.1.8?

↓

PC B Replies

↓

MAC = 00:11:22:33:44:55

↓

Data Sent
```

---

# ARP and Routers

ARP works only within the local network.

When sending data to another network:

```text
PC

↓

Default Gateway

↓

Router

↓

Destination Network
```

The sender resolves the **MAC address of the default gateway**, not the remote host.

---

# Advantages

- Automatic IP-to-MAC mapping
- Transparent to applications
- Simple protocol
- Reduces manual configuration

---

# Limitations

- Works only with IPv4
- Broadcast traffic increases on large LANs
- Vulnerable to ARP spoofing attacks

---

# ARP Spoofing

An attacker sends fake ARP replies.

Example:

```text
Victim

↓

Fake ARP Reply

↓

Incorrect MAC Stored

↓

Traffic Redirected
```

This can lead to **Man-in-the-Middle (MITM)** attacks.

Modern networks often use security mechanisms such as **Dynamic ARP Inspection (DAI)** to help prevent ARP spoofing.

---

# ARP vs DNS

| Feature | ARP | DNS |
|----------|-----|-----|
| Converts | IP → MAC | Domain → IP |
| Scope | Local Network | Internet |
| Layer | Network Support | Application |
| Uses Broadcast | Yes | No |

---

# ARP vs RARP

| Feature | ARP | RARP |
|----------|-----|------|
| Converts | IP → MAC | MAC → IP |
| Status | Widely Used | Obsolete |

RARP has largely been replaced by protocols such as BOOTP and DHCP.

---

# Summary

| Component | Purpose |
|-----------|---------|
| ARP | Maps IP addresses to MAC addresses |
| ARP Request | Broadcast asking for a MAC address |
| ARP Reply | Unicast reply containing the MAC address |
| ARP Cache | Stores recently learned mappings |
| Gratuitous ARP | Announces or verifies a device's own IP |
| Proxy ARP | Router answers ARP requests on behalf of another device |

---

# Key Takeaways

- ARP stands for **Address Resolution Protocol**.
- It maps **IPv4 addresses** to **MAC addresses** on a local network.
- ARP Requests are **broadcast**, while ARP Replies are **unicast**.
- Operating systems maintain an **ARP cache** to reduce repeated lookups.
- ARP operates only within a **Local Area Network (LAN)**.
- ARP is essential for Ethernet communication because frames require destination MAC addresses.
- Security features such as **Dynamic ARP Inspection (DAI)** help protect against ARP spoofing.

---

# Conclusion

ARP is a fundamental protocol that enables communication on IPv4 Ethernet networks by translating IP addresses into MAC addresses. Every device on a LAN relies on ARP before transmitting Ethernet frames, making it a critical component of everyday networking. Understanding ARP is essential for network troubleshooting, socket programming, and Linux system administration.
