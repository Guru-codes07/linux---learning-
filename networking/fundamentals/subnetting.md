# Subnetting

Subnetting is the process of dividing a large network into **smaller, manageable networks** called **subnets**. It improves network performance, enhances security, reduces broadcast traffic, and makes efficient use of IP addresses.

Subnetting is one of the most important concepts in networking and is widely used in enterprise networks, data centers, cloud computing, and system administration.

---

# What is a Subnet?

A **subnet (subnetwork)** is a smaller network created from a larger network.

For example, instead of having one large network with 500 devices, you can divide it into several smaller networks:

```text
Network
│
├── Subnet A
├── Subnet B
├── Subnet C
└── Subnet D
```

Each subnet acts as its own network.

---

# Why Do We Need Subnetting?

Without subnetting:

* Large broadcast domains
* More network congestion
* Difficult network management
* Poor security
* Wasted IP addresses

With subnetting:

* Better performance
* Improved security
* Easier administration
* Efficient IP utilization
* Reduced broadcast traffic

---

# Understanding Network and Host Portions

Every IPv4 address has two parts:

* **Network ID**
* **Host ID**

Example:

```text
IP Address : 192.168.1.25
Subnet Mask: 255.255.255.0
```

```text
192.168.1 | 25
 Network     Host
```

Devices with the same Network ID belong to the same subnet.

---

# What is a Subnet Mask?

A **subnet mask** determines which part of an IP address represents the network and which part represents the host.

Example:

```text
255.255.255.0
```

Binary:

```text
11111111.11111111.11111111.00000000
```

* `1` = Network bit
* `0` = Host bit

---

# Common Subnet Masks

| CIDR | Subnet Mask     | Host Bits |
| ---- | --------------- | --------- |
| /8   | 255.0.0.0       | 24        |
| /16  | 255.255.0.0     | 16        |
| /24  | 255.255.255.0   | 8         |
| /25  | 255.255.255.128 | 7         |
| /26  | 255.255.255.192 | 6         |
| /27  | 255.255.255.224 | 5         |
| /28  | 255.255.255.240 | 4         |
| /29  | 255.255.255.248 | 3         |
| /30  | 255.255.255.252 | 2         |
| /31  | 255.255.255.254 | 1         |
| /32  | 255.255.255.255 | 0         |

---

# CIDR Notation

CIDR stands for:

> **Classless Inter-Domain Routing**

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
| /30  | 255.255.255.252 |
| /32  | 255.255.255.255 |

---

# Number of Hosts

The formula for calculating usable hosts is:

```text
Usable Hosts = 2^(Host Bits) − 2
```

The subtraction of **2** accounts for:

* Network Address
* Broadcast Address

Examples:

| CIDR | Host Bits | Usable Hosts |
| ---- | --------- | ------------ |
| /24  | 8         | 254          |
| /25  | 7         | 126          |
| /26  | 6         | 62           |
| /27  | 5         | 30           |
| /28  | 4         | 14           |
| /29  | 3         | 6            |
| /30  | 2         | 2            |

---

# Network Address

The **Network Address** identifies the subnet itself.

Example:

```text
IP Address : 192.168.1.50
Subnet Mask: /24
```

Network Address:

```text
192.168.1.0
```

It cannot be assigned to a host.

---

# Broadcast Address

The **Broadcast Address** is used to send packets to every device in the subnet.

Example:

```text
192.168.1.255
```

It also cannot be assigned to a host.

---

# Host Range

Example:

```text
Network Address   : 192.168.1.0
Broadcast Address : 192.168.1.255
```

Valid host addresses:

```text
192.168.1.1
↓

192.168.1.254
```

---

# Example 1 (/24 Network)

Given:

```text
IP Address : 192.168.1.100
Subnet Mask: /24
```

| Item              | Value         |
| ----------------- | ------------- |
| Network Address   | 192.168.1.0   |
| First Host        | 192.168.1.1   |
| Last Host         | 192.168.1.254 |
| Broadcast Address | 192.168.1.255 |
| Total Hosts       | 254           |

---

# Example 2 (/26 Network)

Given:

```text
192.168.1.70/26
```

Subnet size:

```text
64 addresses
```

Subnets:

```text
192.168.1.0

192.168.1.64

192.168.1.128

192.168.1.192
```

The IP `192.168.1.70` belongs to:

```text
Network Address : 192.168.1.64
```

Broadcast:

```text
192.168.1.127
```

Host range:

```text
192.168.1.65

↓

192.168.1.126
```

---

# Example 3 (/30 Network)

A `/30` network provides:

```text
Network
Host
Host
Broadcast
```

Example:

```text
10.0.0.0/30
```

| Address  | Purpose   |
| -------- | --------- |
| 10.0.0.0 | Network   |
| 10.0.0.1 | Host      |
| 10.0.0.2 | Host      |
| 10.0.0.3 | Broadcast |

Used mainly for **point-to-point links** between routers.

---

# Binary Example

IP Address:

```text
192.168.1.25
```

Binary:

```text
11000000.10101000.00000001.00011001
```

Subnet Mask (/24):

```text
11111111.11111111.11111111.00000000
```

Using a bitwise **AND** operation:

```text
11000000.10101000.00000001.00011001
11111111.11111111.11111111.00000000
-----------------------------------
11000000.10101000.00000001.00000000
```

Result:

```text
192.168.1.0
```

This is the **Network Address**.

---

# Benefits of Subnetting

* Better network performance
* Reduced broadcast traffic
* Improved security
* Efficient use of IP addresses
* Easier troubleshooting
* Better scalability
* Simplified network management

---

# Real-World Example

Suppose a company has four departments:

```text
Administration
Sales
HR
Development
```

Instead of placing everyone on one network:

```text
192.168.1.0/24
```

The administrator creates:

```text
192.168.1.0/26

192.168.1.64/26

192.168.1.128/26

192.168.1.192/26
```

Each department receives its own subnet, reducing unnecessary traffic and improving security.

---

# Quick Reference

| CIDR | Subnet Mask     | Usable Hosts |
| ---- | --------------- | -----------: |
| /24  | 255.255.255.0   |          254 |
| /25  | 255.255.255.128 |          126 |
| /26  | 255.255.255.192 |           62 |
| /27  | 255.255.255.224 |           30 |
| /28  | 255.255.255.240 |           14 |
| /29  | 255.255.255.248 |            6 |
| /30  | 255.255.255.252 |            2 |

---

# Key Terms

| Term              | Meaning                                                  |
| ----------------- | -------------------------------------------------------- |
| Subnet            | A smaller network created from a larger network          |
| Subnet Mask       | Separates the network and host portions of an IP address |
| CIDR              | Prefix notation for subnet masks                         |
| Network Address   | Identifies the subnet                                    |
| Broadcast Address | Sends packets to all devices in the subnet               |
| Host Address      | Assigned to an individual device                         |
| Host Bits         | Bits available for host addresses                        |
| Network Bits      | Bits used to identify the network                        |

---

# Key Takeaways

* Subnetting divides a large network into smaller subnets.
* Every subnet has a **Network Address**, **Host Range**, and **Broadcast Address**.
* A subnet mask determines the boundary between the network and host portions of an IP address.
* CIDR notation is the standard way to represent subnet masks.
* The formula **2^(Host Bits) − 2** calculates the number of usable host addresses.
* Subnetting improves network performance, security, and scalability.

---

# Conclusion

Subnetting is a fundamental networking skill that allows administrators to organize and optimize IP networks. By dividing large networks into smaller subnets, organizations can reduce broadcast traffic, improve security, and make better use of available IP addresses. Mastering subnetting is essential for network engineers, system administrators, cybersecurity professionals, and anyone working with TCP/IP networks.

