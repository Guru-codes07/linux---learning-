# Network Interfaces

A **Network Interface** is the connection point between a computer and a network. It allows a device to send and receive data over a network using technologies such as Ethernet, Wi-Fi, or the Loopback interface.

Every network interface has its own configuration, including an IP address, MAC address, subnet mask, and operational state.

---

# Why Do We Need Network Interfaces?

Without a network interface, a computer cannot communicate with other devices.

Example:

```text
Computer

↓

Network Interface

↓

Router

↓

Internet
```

The network interface acts as the bridge between the operating system and the physical or virtual network.

---

# Types of Network Interfaces

Linux supports several types of network interfaces.

| Interface | Purpose |
|-----------|---------|
| Ethernet (`eth0`, `enp...`) | Wired networking |
| Wi-Fi (`wlan0`, `wlp...`) | Wireless networking |
| Loopback (`lo`) | Internal communication |
| Virtual Interface | Virtual machines and containers |
| Bridge Interface | Connects multiple interfaces |
| Tunnel Interface | VPN and tunneling |

---

# Ethernet Interface

An Ethernet interface connects a computer to a wired network.

Example:

```text
Computer

↓

Ethernet Cable

↓

Router
```

Typical names:

```text
eth0

enp3s0

eno1
```

---

# Wi-Fi Interface

A wireless network interface connects using radio signals.

Example:

```text
Computer

↓

Wi-Fi

↓

Router
```

Typical names:

```text
wlan0

wlp2s0
```

---

# Loopback Interface

The loopback interface is a virtual interface used for communication within the same computer.

Name:

```text
lo
```

IP Address:

```text
127.0.0.1
```

Example:

```text
Application A

↓

Loopback

↓

Application B
```

The loopback interface never sends traffic onto the physical network.

---

# Virtual Interfaces

Virtual interfaces are created by software.

Examples:

- Docker
- VirtualBox
- VMware
- KVM
- VPNs

Example:

```text
Docker

↓

docker0
```

---

# Interface Components

Each network interface has:

- Interface Name
- MAC Address
- IP Address
- Subnet Mask
- MTU
- State (UP/DOWN)

---

# Interface Naming

Older Linux systems:

```text
eth0

eth1

wlan0
```

Modern Linux systems:

```text
enp3s0

eno1

wlp2s0
```

These names are based on hardware location and are more predictable.

---

# Viewing Interfaces

Display all interfaces:

```bash
ip addr
```

Example:

```text
1: lo

2: enp3s0

3: wlp2s0
```

---

# Display Interface Details

```bash
ip addr show
```

Display a specific interface:

```bash
ip addr show enp3s0
```

---

# Show Link Information

```bash
ip link
```

Example:

```text
1: lo

2: enp3s0

3: wlp2s0
```

This displays:

- Interface name
- MAC address
- State
- MTU

---

# Interface States

| State | Meaning |
|--------|---------|
| UP | Interface is enabled |
| DOWN | Interface is disabled |
| UNKNOWN | State cannot be determined |

---

# Bringing an Interface Up

```bash
sudo ip link set enp3s0 up
```

---

# Bringing an Interface Down

```bash
sudo ip link set enp3s0 down
```

---

# Assigning an IP Address

Example:

```bash
sudo ip addr add 192.168.1.100/24 dev enp3s0
```

---

# Removing an IP Address

```bash
sudo ip addr del 192.168.1.100/24 dev enp3s0
```

---

# MAC Address

Every physical network interface has a unique hardware address.

Example:

```text
08:00:27:12:34:56
```

Used by Ethernet for local communication.

---

# Viewing MAC Address

```bash
ip link show
```

Example:

```text
link/ether 08:00:27:12:34:56
```

---

# MTU (Maximum Transmission Unit)

MTU specifies the largest packet that can be transmitted.

Typical Ethernet MTU:

```text
1500 Bytes
```

Larger packets improve efficiency but may not be supported by every network.

---

# Viewing MTU

```bash
ip link show
```

Example:

```text
mtu 1500
```

---

# Changing MTU

```bash
sudo ip link set dev enp3s0 mtu 9000
```

A larger MTU (Jumbo Frames) is commonly used in data centers.

---

# Interface Statistics

Linux provides statistics such as:

- Packets Sent
- Packets Received
- Errors
- Dropped Packets

View statistics:

```bash
ip -s link
```

---

# Loopback Example

Running:

```bash
ping 127.0.0.1
```

Produces:

```text
Packets Never Leave The Computer
```

This is useful for testing networking software.

---

# Useful Linux Commands

| Command | Purpose |
|----------|---------|
| `ip addr` | Show IP addresses |
| `ip link` | Show interfaces |
| `ip -s link` | Show interface statistics |
| `hostname -I` | Display assigned IP addresses |
| `ping 127.0.0.1` | Test loopback interface |

---

# Real-World Applications

Network interfaces are used by:

- Desktop computers
- Servers
- Cloud instances
- Containers
- Virtual machines
- Routers
- IoT devices

---

# Summary

| Component | Purpose |
|-----------|---------|
| Ethernet | Wired networking |
| Wi-Fi | Wireless networking |
| Loopback | Local communication |
| Virtual Interface | Virtual networking |
| MAC Address | Hardware identifier |
| IP Address | Network identifier |
| MTU | Maximum packet size |

---

# Key Takeaways

- A network interface connects a device to a network.
- Linux supports physical, virtual, and loopback interfaces.
- Each interface has its own MAC address, IP address, and MTU.
- The `ip` command is the primary utility for viewing and managing network interfaces.
- Interfaces can be brought **UP** or **DOWN** and configured dynamically.
- Understanding network interfaces is essential for network programming, Linux administration, and troubleshooting.

---

# Conclusion

Network interfaces form the foundation of all network communication in Linux. Every packet sent or received passes through a network interface, making them one of the most important concepts in networking and system administration. Learning how to inspect, configure, and manage interfaces is a fundamental skill for every Linux user and systems programmer.
