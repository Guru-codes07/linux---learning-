# Linux Networking Basics

Networking allows computers and devices to communicate with each other and exchange data.

Linux provides powerful networking tools and utilities to configure, monitor, troubleshoot, and manage network connections.

Understanding networking is essential for:

* System administration
* Server management
* Cloud computing
* Cybersecurity
* Socket programming
* Kernel development

---

# What is a Network?

A network is a group of connected devices that can communicate with each other.

Example:

```text
Computer
    |
    |
Router
    |
    |
Internet
```

Devices communicate using:

* IP addresses
* Protocols
* Ports
* Network interfaces

---

# Network Interface

A network interface is a hardware or virtual device used for network communication.

Examples:

```text
eth0   → Ethernet connection
wlan0  → Wireless connection
lo     → Loopback interface
```

View interfaces:

```bash
ip link
```

Example:

```text
1: lo
2: eth0
3: wlan0
```

---

# IP Address

An IP address identifies a device on a network.

Example:

```text
192.168.1.10
```

IPv4 address format:

```text
xxx.xxx.xxx.xxx
```

Example:

```text
192.168.0.5
```

---

# IPv4 vs IPv6

| IPv4 | IPv6 |
| ---- | ---- |
| 32-bit address | 128-bit address |
| Example: 192.168.1.1 | Example: 2001:db8::1 |
| Limited addresses | Huge address space |

---

# Checking IP Address

Use:

```bash
ip addr
```

Example:

```text
inet 192.168.1.20/24
```

---

# Loopback Address

The loopback address is used for communication inside the same machine.

IPv4:

```text
127.0.0.1
```

Hostname:

```bash
localhost
```

Example:

```bash
ping localhost
```

---

# MAC Address

A MAC address is the physical address of a network interface.

Example:

```text
00:1A:2B:3C:4D:5E
```

View MAC address:

```bash
ip link
```

---

# Ports

A port identifies a specific application or service.

Example:

```text
IP Address + Port = Application
```

Example:

```text
192.168.1.10:8080
```

Common ports:

| Port | Service |
| ---- | ------- |
| 22 | SSH |
| 80 | HTTP |
| 443 | HTTPS |
| 53 | DNS |
| 25 | SMTP |

---

# Protocols

A protocol defines rules for communication between devices.

Examples:

| Protocol | Purpose |
| -------- | ------- |
| TCP | Reliable communication |
| UDP | Fast communication |
| HTTP | Web communication |
| HTTPS | Secure web communication |
| DNS | Domain name resolution |
| SSH | Remote login |

---

# TCP (Transmission Control Protocol)

TCP provides reliable communication.

Features:

* Connection-based
* Error checking
* Ordered data delivery
* Retransmission of lost packets

Example:

```text
Client
   |
   |
 TCP Connection
   |
   |
Server
```

Used by:

* Web servers
* File transfers
* Chat applications

---

# UDP (User Datagram Protocol)

UDP provides faster communication without guaranteeing delivery.

Features:

* No connection setup
* Low latency
* No retransmission

Used by:

* Online games
* Video streaming
* Voice calls

---

# TCP Connection Process

TCP uses a three-way handshake.

```text
Client                 Server

 SYN  ------------->

       <------------- SYN + ACK

 ACK  ------------->

Connection Established
```

---

# Network Commands

## ping

Tests connectivity between devices.

Example:

```bash
ping google.com
```

Output:

```text
64 bytes from google.com
```

---

# traceroute

Shows the path packets take.

Example:

```bash
traceroute google.com
```

---

# netstat

Displays network connections.

Example:

```bash
netstat -tuln
```

Shows:

* Listening ports
* Active connections

---

# ss Command

Modern replacement for netstat.

Example:

```bash
ss -tuln
```

---

# Checking Open Ports

Example:

```bash
ss -tulnp
```

Output:

```text
LISTEN 0.0.0.0:22 sshd
LISTEN 0.0.0.0:80 nginx
```

---

# DNS (Domain Name System)

DNS converts domain names into IP addresses.

Example:

```text
google.com
       |
       |
142.250.x.x
```

Check DNS:

```bash
nslookup google.com
```

---

# DHCP

DHCP automatically assigns IP addresses.

Example:

```text
Device
   |
DHCP Server
   |
IP Address Assigned
```

---

# Routing

Routing decides where network packets should go.

View routing table:

```bash
ip route
```

Example:

```text
default via 192.168.1.1
```

---

# Gateway

A gateway connects different networks.

Example:

```text
Computer
    |
Router (Gateway)
    |
Internet
```

---

# Firewall

A firewall controls network traffic.

Linux commonly uses:

```bash
iptables
```

or:

```bash
ufw
```

Example:

Allow SSH:

```bash
sudo ufw allow ssh
```

Enable firewall:

```bash
sudo ufw enable
```

---

# Network Services

A service is a program that listens for network requests.

Examples:

```text
sshd
nginx
apache
mysql
```

Check services:

```bash
systemctl status service_name
```

---

# Socket Concept

A socket is an endpoint for communication between programs.

A socket contains:

```text
IP Address
+
Port Number
+
Protocol
```

Example:

```text
192.168.1.5:8080
```

---

# Client-Server Model

Most network applications follow this model.

Example:

```text
Client
   |
   |
Request
   |
   |
Server
   |
   |
Response
```

Examples:

* Web browsers
* Chat applications
* APIs

---

# Socket Programming

Socket programming allows programs to communicate over a network.

Basic TCP server flow:

```text
socket()

bind()

listen()

accept()

recv()

send()

close()
```

TCP client flow:

```text
socket()

connect()

send()

recv()

close()
```

---

# Network Troubleshooting Commands

| Command | Purpose |
| ------- | ------- |
| ping | Test connectivity |
| ip addr | Show IP addresses |
| ip route | Show routing table |
| ss | Show connections |
| netstat | Network statistics |
| traceroute | Trace packet path |
| nslookup | DNS lookup |
| curl | Test HTTP requests |

---

# Important Networking Files

Network configuration:

```bash
/etc/network/
```

DNS configuration:

```bash
/etc/resolv.conf
```

Hosts file:

```bash
/etc/hosts
```

---

# Why Networking Matters

Linux networking knowledge helps with:

* Running servers
* Building applications
* Socket programming
* Cloud infrastructure
* Cybersecurity
* System administration

Networking is one of the most important foundations for understanding how Linux systems communicate.
