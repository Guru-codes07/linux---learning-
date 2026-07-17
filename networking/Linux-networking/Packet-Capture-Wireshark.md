# Packet Capture using Wireshark

**Wireshark** is the world's most popular **network protocol analyzer**. It allows you to capture, inspect, and analyze network traffic in real time.

Wireshark is widely used by:

- Network Engineers
- System Administrators
- Cybersecurity Professionals
- Penetration Testers
- Software Developers
- Linux Kernel Developers

It helps you understand exactly what happens on the network by displaying every packet exchanged between devices.

---

# Why Use Wireshark?

Suppose your web application cannot connect to a server.

Without Wireshark:

```text
Application Error

↓

Unknown Cause
```

With Wireshark:

```text
Application

↓

Network Packets

↓

Wireshark

↓

Find the Problem
```

You can inspect every packet and determine where communication fails.

---

# What is a Packet?

A **packet** is a small unit of data transmitted over a network.

Example:

```text
Large File

↓

Split into Packets

↓

Sent Across Network

↓

Reassembled
```

Every packet contains:

- Headers
- Payload

---

# Packet Structure

```text
Ethernet Header

↓

IP Header

↓

TCP/UDP Header

↓

Application Data
```

Wireshark displays every layer separately.

---

# Installing Wireshark

### Fedora

```bash
sudo dnf install wireshark wireshark-cli
```

---

### Ubuntu

```bash
sudo apt install wireshark
```

---

### Arch Linux

```bash
sudo pacman -S wireshark-qt
```

---

# Starting Wireshark

Launch:

```bash
wireshark
```

or

```bash
sudo wireshark
```

You will see a list of available network interfaces.

Example:

```text
lo

wlp2s0

enp3s0

docker0
```

---

# Selecting an Interface

Choose the interface you want to monitor.

Examples:

| Interface | Purpose |
|-----------|---------|
| lo | Loopback |
| wlp2s0 | Wi-Fi |
| enp3s0 | Ethernet |
| docker0 | Docker Network |

Double-click the desired interface to begin capturing packets.

---

# Wireshark Interface

The Wireshark window consists of three main sections.

```text
Packet List

↓

Packet Details

↓

Packet Bytes
```

---

## Packet List

Displays all captured packets.

Information includes:

- Packet Number
- Time
- Source
- Destination
- Protocol
- Length
- Info

---

## Packet Details

Displays protocol information layer by layer.

Example:

```text
Ethernet

↓

IPv4

↓

TCP

↓

HTTP
```

---

## Packet Bytes

Displays the raw packet in hexadecimal and ASCII format.

---

# Starting a Capture

1. Select an interface.
2. Click **Start Capturing**.
3. Perform a network activity.
4. Observe packets appearing in real time.

---

# Stopping a Capture

Click the **Stop** button or press:

```text
Ctrl + E
```

---

# Display Filters

Display filters allow you to show only packets of interest.

---

## Show TCP Packets

```text
tcp
```

---

## Show UDP Packets

```text
udp
```

---

## Show HTTP Packets

```text
http
```

---

## Show HTTPS Packets

```text
tls
```

---

## Show DNS Packets

```text
dns
```

---

## Show DHCP Packets

```text
dhcp
```

---

## Show ARP Packets

```text
arp
```

---

## Show ICMP Packets

```text
icmp
```

---

## Show Traffic for One IP

```text
ip.addr == 192.168.1.100
```

---

## Show Traffic on Port 80

```text
tcp.port == 80
```

---

## Show Traffic on Port 443

```text
tcp.port == 443
```

---

# TCP Three-Way Handshake

Capture:

```text
tcp
```

You will observe:

```text
SYN

↓

SYN ACK

↓

ACK
```

This establishes a TCP connection.

---

# TCP Four-Way Termination

When a TCP connection closes:

```text
FIN

↓

ACK

↓

FIN

↓

ACK
```

---

# DNS Lookup

Open a website.

Filter:

```text
dns
```

Example:

```text
Query

↓

example.com

↓

Response

↓

93.184.216.34
```

---

# HTTP Request

Visit a website using HTTP.

Filter:

```text
http
```

You can inspect:

```text
GET /index.html

↓

HTTP/1.1
```

---

# HTTP Response

Example:

```text
HTTP/1.1 200 OK
```

Response headers and content are visible.

---

# HTTPS Traffic

Filter:

```text
tls
```

You will observe:

```text
Client Hello

↓

Server Hello

↓

Certificate

↓

Encrypted Data
```

The application data remains encrypted.

---

# ARP Request

Filter:

```text
arp
```

Example:

```text
Who has 192.168.1.1?

Tell 192.168.1.100
```

---

# ARP Reply

```text
192.168.1.1

is

08:00:27:12:34:56
```

---

# DHCP DORA Process

Filter:

```text
dhcp
```

Observe:

```text
Discover

↓

Offer

↓

Request

↓

ACK
```

---

# ICMP (Ping)

Run:

```bash
ping google.com
```

Filter:

```text
icmp
```

Packets:

```text
Echo Request

↓

Echo Reply
```

---

# Following a TCP Stream

Right-click a TCP packet.

Select:

```text
Follow

↓

TCP Stream
```

This reconstructs the full conversation between client and server.

Useful for viewing:

- HTTP Requests
- HTTP Responses
- Text Protocols

---

# Packet Coloring

Wireshark automatically colors packets.

Example:

| Color | Protocol |
|--------|----------|
| Green | HTTP |
| Blue | DNS |
| Black | TCP Errors |
| Purple | UDP |

---

# Saving a Capture

Go to:

```text
File

↓

Save As
```

Packets are saved in:

```text
.pcapng
```

format.

---

# Opening a Capture

```text
File

↓

Open

↓

capture.pcapng
```

---

# Useful Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| Ctrl + E | Start/Stop Capture |
| Ctrl + F | Find Packet |
| Ctrl + S | Save Capture |
| Ctrl + O | Open Capture |

---

# Common Use Cases

Wireshark is used for:

- Debugging applications
- Network troubleshooting
- Protocol analysis
- Security investigations
- Malware analysis
- Performance optimization
- Learning networking

---

# Advantages

- Free and open-source
- Supports thousands of protocols
- Powerful filtering
- Real-time packet capture
- Cross-platform
- Detailed protocol decoding

---

# Limitations

- Cannot decrypt encrypted traffic without keys
- Large captures consume significant memory
- Requires administrator privileges for live capture
- Capturing on busy networks can produce massive amounts of data

---

# Best Practices

- Capture only the required interface.
- Apply display filters to reduce clutter.
- Save important captures for later analysis.
- Avoid capturing sensitive data on production networks without authorization.
- Stop captures when finished to reduce file size.

---

# Summary

| Feature | Purpose |
|---------|---------|
| Packet Capture | Records network traffic |
| Display Filters | Show specific packets |
| TCP Stream | Reconstruct communication |
| Packet Details | Inspect protocol headers |
| Packet Bytes | View raw hexadecimal data |
| PCAPNG | Standard capture file format |

---

# Key Takeaways

- Wireshark is a powerful packet analyzer used to inspect network traffic.
- It captures packets from network interfaces such as Ethernet, Wi-Fi, and Loopback.
- Display filters make it easy to analyze specific protocols like TCP, UDP, HTTP, DNS, DHCP, ARP, ICMP, and TLS.
- Wireshark allows you to visualize TCP handshakes, DNS lookups, HTTP requests, and TLS negotiations.
- Captured traffic can be saved in **.pcapng** format for future analysis.
- Packet analysis is an essential skill for networking, cybersecurity, Linux system administration, and systems programming.

---

# Conclusion

Wireshark is one of the most valuable tools for anyone working with computer networks. It provides deep insight into how protocols such as ARP, DHCP, DNS, TCP, HTTP, HTTPS, and ICMP operate in real-world environments. By combining the networking concepts you've learned with hands-on packet analysis, Wireshark bridges the gap between theory and practice, making it an indispensable tool for debugging, troubleshooting, and mastering network communication.
