# IP Addressing

An **IP Address (Internet Protocol Address)** is a unique numerical identifier assigned to every device connected to a network. It allows devices to identify each other and communicate over local networks and the Internet.

Every computer, smartphone, server, router, and IoT device connected to a network requires an IP address.

---

# What is an IP Address?

Think of an IP address as the **postal address** of a house.

* A house address tells the postal service where to deliver mail.
* An IP address tells the network where to deliver data.

Without IP addresses, computers would not know where to send or receive information.

---

# Why Do We Need IP Addresses?

IP addresses help devices:

* Identify each other
* Send and receive data
* Communicate over local and global networks
* Route packets correctly
* Access Internet services

---

# Versions of IP

There are two major versions of IP currently in use:

| Version | Name                        | Address Length |
| ------- | --------------------------- | -------------- |
| IPv4    | Internet Protocol Version 4 | 32 bits        |
| IPv6    | Internet Protocol Version 6 | 128 bits       |

IPv4 is still the most commonly used, while IPv6 was introduced to solve the shortage of IPv4 addresses.

---

# IPv4 Address

An IPv4 address consists of **32 bits**, divided into **4 octets** (8 bits each).

Example:

```text
192.168.1.10
```

Binary representation:

```text
11000000.10101000.00000001.00001010
```

Each octet can have a value between:

```text
0 - 255
```

---

# IPv4 Structure

```text
192 . 168 . 1 . 10
 |      |     |    |
Octet Octet Octet Octet
```

Each octet contains **8 bits**.

---

# IPv6 Address

IPv6 addresses are **128 bits** long.

Example:

```text
2001:0db8:85a3:0000:0000:8a2e:0370:7334
```

IPv6 supports a vastly larger number of unique addresses than IPv4.

Advantages of IPv6:

* Larger address space
* Better security support
* Improved routing efficiency
* No need for NAT in many cases
* Automatic address configuration

---

# IPv4 Address Classes

Originally, IPv4 addresses were divided into classes.

| Class | First Octet Range | Default Subnet Mask | Purpose         |
| ----- | ----------------- | ------------------- | --------------- |
| A     | 1 - 126           | 255.0.0.0           | Large Networks  |
| B     | 128 - 191         | 255.255.0.0         | Medium Networks |
| C     | 192 - 223         | 255.255.255.0       | Small Networks  |
| D     | 224 - 239         | N/A                 | Multicast       |
| E     | 240 - 255         | N/A                 | Experimental    |

---

# Class A

Example:

```text
10.20.30.40
```

Characteristics:

* Large organizations
* Millions of hosts
* First octet identifies the network

---

# Class B

Example:

```text
172.16.25.8
```

Characteristics:

* Medium-sized organizations
* Thousands of hosts

---

# Class C

Example:

```text
192.168.1.15
```

Characteristics:

* Home networks
* Small businesses
* Most common private network range

---

# Class D

Used for:

* Multicasting
* Streaming
* Video conferencing

Example:

```text
239.10.20.30
```

---

# Class E

Reserved for:

* Research
* Experimental purposes

Not normally used on public networks.

---

# Public IP Address

A Public IP Address is globally unique and reachable over the Internet.

Example:

```text
142.250.193.78
```

Public IP addresses are assigned by Internet Service Providers (ISPs).

---

# Private IP Address

Private IP addresses are used inside local networks and are **not routable on the Internet**.

Private ranges:

| Range                         | Purpose                 |
| ----------------------------- | ----------------------- |
| 10.0.0.0 – 10.255.255.255     | Large Private Networks  |
| 172.16.0.0 – 172.31.255.255   | Medium Private Networks |
| 192.168.0.0 – 192.168.255.255 | Home Networks           |

Example:

```text
192.168.1.100
```

---

# Static IP Address

A Static IP Address remains the same unless manually changed.

Common uses:

* Servers
* Routers
* Network printers
* CCTV systems

Advantages:

* Consistent address
* Easier remote access
* Better for hosting services

---

# Dynamic IP Address

A Dynamic IP Address is assigned automatically by a **DHCP (Dynamic Host Configuration Protocol)** server.

Advantages:

* Automatic configuration
* Efficient address management
* Common for home users

---

# Loopback Address

The loopback address refers to the local machine itself.

IPv4:

```text
127.0.0.1
```

Hostname:

```text
localhost
```

Purpose:

* Testing network software
* Local communication
* Troubleshooting

---

# APIPA Address

APIPA stands for:

> Automatic Private IP Addressing

Range:

```text
169.254.0.0 - 169.254.255.255
```

An APIPA address is automatically assigned when:

* DHCP server is unavailable
* Device cannot obtain an IP address

---

# Network Address

The Network Address identifies the entire network.

Example:

```text
192.168.1.0
```

It cannot be assigned to a host.

---

# Broadcast Address

The Broadcast Address is used to send data to **every device** on the network.

Example:

```text
192.168.1.255
```

It also cannot be assigned to a host.

---

# Host Address

A Host Address identifies an individual device on a network.

Example:

```text
192.168.1.25
```

This address can be assigned to:

* Computers
* Servers
* Routers
* Smartphones
* Printers

---

# Subnet Mask

A subnet mask separates the **network portion** of an IP address from the **host portion**.

Example:

```text
255.255.255.0
```

This subnet mask indicates:

```text
Network: 192.168.1
Host:    X
```

Subnet masks are covered in detail in **Subnetting.md**.

---

# CIDR Notation

CIDR stands for:

> Classless Inter-Domain Routing

Instead of writing:

```text
255.255.255.0
```

we write:

```text
/24
```

Examples:

| CIDR | Subnet Mask     |
| ---- | --------------- |
| /8   | 255.0.0.0       |
| /16  | 255.255.0.0     |
| /24  | 255.255.255.0   |
| /32  | 255.255.255.255 |

---

# Finding Your IP Address (Linux)

Private IP:

```bash
ip addr show
```

or

```bash
hostname -I
```

Public IP:

```bash
curl ifconfig.me
```

---

# Real-World Example

Suppose your laptop has:

```text
IP Address : 192.168.1.15
Subnet Mask: 255.255.255.0
Gateway    : 192.168.1.1
```

* The router uses the **gateway** to forward packets to other networks.
* Devices on the same subnet can communicate directly.
* Traffic destined for other networks is sent to the gateway.

---

# Advantages of IP Addressing

* Enables device communication
* Supports Internet connectivity
* Facilitates routing
* Provides unique device identification
* Scales to networks of all sizes

---

# Key Terms

| Term              | Meaning                             |
| ----------------- | ----------------------------------- |
| IP Address        | Unique identifier for a device      |
| IPv4              | 32-bit Internet Protocol            |
| IPv6              | 128-bit Internet Protocol           |
| Public IP         | Internet-routable address           |
| Private IP        | Local network address               |
| Static IP         | Manually assigned address           |
| Dynamic IP        | Automatically assigned address      |
| Loopback          | Address for the local machine       |
| APIPA             | Automatic private addressing        |
| Network Address   | Identifies the network              |
| Broadcast Address | Sends data to all hosts             |
| Host Address      | Identifies a specific device        |
| Subnet Mask       | Separates network and host portions |
| CIDR              | Prefix notation for network size    |

---

# Summary

* Every network device requires an IP address.
* IPv4 uses **32-bit** addresses, while IPv6 uses **128-bit** addresses.
* IP addresses can be **public** or **private**.
* Static IPs remain fixed; dynamic IPs are assigned by DHCP.
* The loopback address (`127.0.0.1`) refers to the local machine.
* Subnet masks divide the network and host portions of an address.
* CIDR notation provides a compact way to represent subnet masks.

---

# Conclusion

IP addressing is the foundation of modern networking. Every packet sent across a network relies on IP addresses to reach the correct destination. A solid understanding of IPv4, IPv6, private and public addressing, subnet masks, and CIDR notation is essential before learning subnetting, routing, socket programming, and advanced networking concepts.

