# Routing

**Routing** is the process of forwarding network packets from one network to another. It enables devices on different networks to communicate by determining the best path for data to travel.

Routers use **routing tables** to decide where packets should be sent.

---

# Why Do We Need Routing?

Suppose your computer wants to access a website on the Internet.

Your computer:

```text
IP Address

192.168.1.100
```

Google's server:

```text
IP Address

142.250.xxx.xxx
```

These devices are on different networks.

Your computer cannot send data directly to Google.

Instead:

```text
Computer

↓

Router

↓

Internet

↓

Google Server
```

The router forwards the packets to their destination.

---

# What is a Router?

A **router** is a network device that connects multiple networks and forwards packets between them.

Example:

```text
Laptop

↓

Home Router

↓

ISP

↓

Internet

↓

Web Server
```

Routers operate at the **Network Layer (Layer 3)** of the OSI model.

---

# Routing Process

When a packet arrives:

```text
Packet Received

↓

Read Destination IP

↓

Check Routing Table

↓

Choose Best Route

↓

Forward Packet
```

---

# Routing Table

A routing table contains information about where packets should be sent.

Example:

```text
Destination        Gateway          Interface

192.168.1.0/24    Direct           wlan0

0.0.0.0/0         192.168.1.1      wlan0
```

---

# Components of a Routing Table

Each route contains:

- Destination Network
- Subnet Mask (or Prefix Length)
- Gateway
- Network Interface
- Metric

---

# Destination Network

The network that the route applies to.

Example:

```text
192.168.1.0/24
```

---

# Gateway

The next device that should receive the packet.

Example:

```text
192.168.1.1
```

Usually, this is your router.

---

# Interface

The network interface used to send the packet.

Example:

```text
wlan0

or

enp3s0
```

---

# Metric

The metric represents the cost of a route.

Lower metrics are preferred.

Example:

```text
Metric = 10

↓

Preferred
```

---

# Default Gateway

When no specific route matches the destination, the packet is sent to the **default gateway**.

Example:

```text
0.0.0.0/0

↓

192.168.1.1
```

This route is commonly known as the **default route**.

---

# Example

Your PC:

```text
192.168.1.50
```

Router:

```text
192.168.1.1
```

Google:

```text
142.250.xxx.xxx
```

Flow:

```text
Computer

↓

Default Gateway

↓

ISP Router

↓

Internet

↓

Google
```

---

# Routing Decision

Suppose a packet is destined for:

```text
192.168.1.25
```

The routing table contains:

```text
192.168.1.0/24
```

The packet is sent directly over the local network.

---

Suppose the destination is:

```text
8.8.8.8
```

No local route matches.

The packet follows:

```text
Default Route

↓

Router

↓

Internet
```

---

# Types of Routing

## Static Routing

Routes are manually configured by an administrator.

Example:

```bash
sudo ip route add 10.0.0.0/24 via 192.168.1.1
```

Advantages:

- Simple
- Predictable

Disadvantages:

- Difficult to maintain in large networks

---

## Dynamic Routing

Routes are learned automatically using routing protocols.

Examples:

- RIP
- OSPF
- BGP
- EIGRP

Dynamic routing is used in enterprise and Internet-scale networks.

---

# Longest Prefix Match

Routers choose the **most specific** matching route.

Example:

Routing Table:

```text
192.168.0.0/16

192.168.1.0/24
```

Destination:

```text
192.168.1.25
```

Chosen route:

```text
192.168.1.0/24
```

because it is more specific.

---

# Viewing the Routing Table

Linux:

```bash
ip route
```

Example:

```text
default via 192.168.1.1 dev wlan0

192.168.1.0/24 dev wlan0
```

---

# Adding a Route

```bash
sudo ip route add 10.10.0.0/16 via 192.168.1.1
```

---

# Deleting a Route

```bash
sudo ip route del 10.10.0.0/16
```

---

# Changing the Default Gateway

```bash
sudo ip route replace default via 192.168.1.254
```

---

# Viewing the Default Gateway

```bash
ip route

or

ip route show default
```

---

# Tracing a Route

Linux:

```bash
traceroute google.com
```

Example:

```text
Computer

↓

Home Router

↓

ISP

↓

Internet

↓

Google
```

This command shows each router (hop) the packet passes through.

---

# Packet Forwarding

Every router repeats the same process:

```text
Receive Packet

↓

Read Destination IP

↓

Routing Table Lookup

↓

Forward Packet
```

until the packet reaches its destination.

---

# Routing vs Switching

| Feature | Routing | Switching |
|----------|----------|-----------|
| OSI Layer | Layer 3 | Layer 2 |
| Uses | IP Address | MAC Address |
| Device | Router | Switch |
| Connects | Different Networks | Same Network |

---

# Real-World Example

Home Network:

```text
Laptop

↓

Wi-Fi Router

↓

ISP

↓

Internet

↓

Web Server
```

Office Network:

```text
PC

↓

Office Router

↓

Corporate Network

↓

Internet

↓

Cloud Server
```

---

# Advantages

- Connects multiple networks
- Enables Internet communication
- Supports scalable networks
- Chooses efficient paths
- Supports redundant routes

---

# Limitations

- Incorrect routing tables can prevent communication
- Dynamic routing protocols increase complexity
- Misconfigured routes can create routing loops

---

# Summary

| Component | Purpose |
|-----------|---------|
| Router | Forwards packets |
| Routing Table | Stores routes |
| Gateway | Next hop |
| Interface | Sends packets |
| Metric | Route cost |
| Default Route | Used when no specific route matches |

---

# Key Takeaways

- Routing is the process of forwarding packets between different networks.
- Routers make forwarding decisions using **routing tables**.
- The **default gateway** is used when no specific route matches the destination.
- Linux provides the `ip route` command to view and manage routes.
- Routes can be **static** (manually configured) or **dynamic** (learned automatically).
- Routers select the best route using the **Longest Prefix Match** rule.

---

# Conclusion

Routing is one of the core concepts of computer networking. It allows devices on different networks to communicate by forwarding packets toward their destination. Understanding routing, routing tables, gateways, and Linux routing commands is essential for network administration, troubleshooting, socket programming, and systems programming.
