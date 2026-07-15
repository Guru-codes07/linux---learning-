# DHCP (Dynamic Host Configuration Protocol)

**DHCP (Dynamic Host Configuration Protocol)** is an application-layer protocol that automatically assigns IP addresses and other network configuration information to devices on a network.

Without DHCP, every device would need to be configured manually.

---

# Why Do We Need DHCP?

Suppose you connect your laptop to a Wi-Fi network.

Without DHCP:

```text
Choose an IP Address

↓

Configure Gateway

↓

Configure DNS

↓

Configure Subnet Mask
```

Everything must be entered manually.

With DHCP:

```text
Connect to Wi-Fi

↓

DHCP Server

↓

Automatic Configuration
```

The entire process happens automatically.

---

# Information Provided by DHCP

A DHCP server typically assigns:

- IP Address
- Subnet Mask
- Default Gateway
- DNS Server
- Lease Time

---

# DHCP Architecture

```text
Client

↓

DHCP Server

↓

Network Configuration
```

---

# DHCP Ports

| Protocol | Port |
|----------|------|
| Client | UDP 68 |
| Server | UDP 67 |

DHCP uses **UDP** because it is lightweight and connectionless.

---

# The DORA Process

DHCP follows a four-step process often remembered by the acronym **DORA**.

- Discover
- Offer
- Request
- Acknowledge

---

# Step 1 – DHCP Discover

The client does not yet have an IP address.

It broadcasts:

```text
DHCP Discover
```

asking if any DHCP server is available.

---

# Step 2 – DHCP Offer

The DHCP server responds with:

```text
DHCP Offer
```

containing:

- Available IP address
- Subnet mask
- Gateway
- DNS server
- Lease time

---

# Step 3 – DHCP Request

The client requests the offered address by sending:

```text
DHCP Request
```

---

# Step 4 – DHCP ACK

The server confirms the allocation.

```text
DHCP ACK
```

The client is now ready to communicate on the network.

---

# DHCP DORA Flow

```text
Client

↓

DHCP Discover

↓

DHCP Server

↓

DHCP Offer

↓

Client

↓

DHCP Request

↓

DHCP Server

↓

DHCP ACK

↓

Client Receives IP Address
```

---

# Lease Time

An IP address is assigned for a limited period known as the **lease**.

Example:

```text
Lease Time

↓

24 Hours
```

Before the lease expires, the client attempts to renew it.

---

# DHCP Renewal

```text
Client

↓

Lease Half Expired

↓

DHCP Request

↓

DHCP ACK

↓

Lease Renewed
```

---

# Static vs Dynamic IP

| Feature | Static IP | Dynamic IP |
|----------|-----------|------------|
| Assigned Manually | Yes | No |
| Changes Over Time | No | Yes |
| Uses DHCP | No | Yes |
| Typical Use | Servers | Client Devices |

---

# DHCP Message Types

| Message | Purpose |
|----------|---------|
| Discover | Locate DHCP servers |
| Offer | Offer configuration |
| Request | Request offered configuration |
| ACK | Confirm configuration |
| NAK | Reject request |
| Release | Return IP address |
| Inform | Request additional configuration |

---

# Advantages

- Automatic configuration
- Reduces manual errors
- Efficient IP address management
- Simplifies administration
- Supports large networks

---

# Limitations

- Requires a DHCP server
- If the server fails, new devices may not obtain addresses
- Dynamic addresses may change over time

---

# DHCP in Home Networks

```text
Laptop

↓

Wi-Fi Router

↓

DHCP Server

↓

192.168.1.101
```

Most home routers act as DHCP servers.

---

# Summary

| Component | Purpose |
|-----------|---------|
| DHCP Client | Requests configuration |
| DHCP Server | Assigns configuration |
| Discover | Finds a DHCP server |
| Offer | Offers an IP address |
| Request | Requests the offered address |
| ACK | Confirms the assignment |
| Lease | Time the address remains valid |

---

# Key Takeaways

- DHCP stands for **Dynamic Host Configuration Protocol**.
- It automatically assigns IP addresses and other network settings.
- DHCP uses **UDP ports 67 and 68**.
- The four-step process is **Discover → Offer → Request → ACK (DORA)**.
- IP addresses are leased for a configurable period and can be renewed before expiration.
- DHCP greatly simplifies network administration by eliminating manual IP configuration.

---

# Conclusion

DHCP is a fundamental networking protocol that automates IP address assignment and network configuration. By using the DORA process, it allows devices to join networks quickly and efficiently without manual intervention, making it an essential component of modern home, enterprise, and campus networks.
