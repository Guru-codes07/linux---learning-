# DNS (Domain Name System)

The **Domain Name System (DNS)** is a distributed naming system that translates human-readable domain names (such as `google.com`) into IP addresses that computers use to communicate over a network.

Without DNS, users would have to remember numerical IP addresses instead of easy-to-read domain names.

DNS is often referred to as the **Phone Book of the Internet**.

---

# Why Do We Need DNS?

Humans prefer names:

```text
google.com

github.com

openai.com
```

Computers communicate using IP addresses:

```text
142.250.183.14

140.82.121.4

104.18.33.45
```

DNS converts domain names into IP addresses automatically.

---

# Example

Suppose you type:

```text
https://www.google.com
```

Your computer cannot communicate using the name.

Instead, it asks a DNS server:

```text
"What is the IP address of www.google.com?"
```

The DNS server replies:

```text
142.250.xxx.xxx
```

Your browser then connects to that IP address.

---

# How DNS Works

```text
User

↓

Browser

↓

Operating System DNS Cache

↓

Recursive DNS Resolver

↓

Root DNS Server

↓

TLD Server

↓

Authoritative DNS Server

↓

IP Address

↓

Browser Connects
```

---

# DNS Resolution Process

## Step 1

User enters:

```text
www.google.com
```

---

## Step 2

The browser checks its DNS cache.

If found:

```text
Connect Immediately
```

Otherwise:

```text
Query DNS Server
```

---

## Step 3

The recursive resolver receives the request.

---

## Step 4

The resolver asks a Root DNS Server.

```text
Where is ".com"?
```

---

## Step 5

The Root Server replies:

```text
Ask the .com TLD server.
```

---

## Step 6

The resolver contacts the TLD server.

```text
Where is google.com?
```

---

## Step 7

The TLD server replies:

```text
Ask Google's Authoritative DNS Server.
```

---

## Step 8

The resolver contacts Google's authoritative server.

```text
What is the IP address of www.google.com?
```

---

## Step 9

The authoritative server replies:

```text
142.xxx.xxx.xxx
```

---

## Step 10

The resolver returns the IP address to your computer.

Your browser establishes a TCP connection.

---

# Visual Representation

```text
Browser

↓

Recursive Resolver

↓

Root Server

↓

TLD Server

↓

Authoritative DNS Server

↓

IP Address

↓

Browser Connects
```

---

# DNS Components

## Domain Name

Example:

```text
www.google.com
```

---

## Root Domain

```text
.
```

Usually hidden.

---

## Top-Level Domain (TLD)

Examples:

```text
.com

.org

.net

.edu

.gov

.io
```

---

## Second-Level Domain

Example:

```text
google
```

---

## Subdomain

Example:

```text
www
```

---

# DNS Servers

There are four major DNS server types.

| Server | Purpose |
|---------|---------|
| Recursive Resolver | Performs DNS lookup for the client |
| Root Server | Directs queries to TLD servers |
| TLD Server | Directs queries to authoritative servers |
| Authoritative Server | Stores actual DNS records |

---

# DNS Records

DNS servers store various record types.

---

## A Record

Maps a domain name to an IPv4 address.

Example:

```text
google.com

↓

142.xxx.xxx.xxx
```

---

## AAAA Record

Maps a domain name to an IPv6 address.

---

## CNAME Record

Creates an alias.

Example:

```text
www.example.com

↓

example.com
```

---

## MX Record

Specifies the mail server for a domain.

Used for email delivery.

---

## NS Record

Specifies the authoritative DNS servers for a domain.

---

## TXT Record

Stores arbitrary text.

Often used for:

- SPF
- DKIM
- Domain verification

---

# DNS Cache

To reduce lookup time, DNS responses are cached.

Caches exist in:

- Browser
- Operating System
- Router
- ISP Resolver

Cached responses avoid repeated DNS lookups.

---

# TTL (Time To Live)

Each DNS record has a TTL value.

Example:

```text
TTL = 3600 seconds
```

After the TTL expires, the resolver performs another lookup.

---

# Public DNS Servers

Popular public DNS providers include:

| Provider | IPv4 Address |
|-----------|--------------|
| Google DNS | 8.8.8.8 |
| Google DNS | 8.8.4.4 |
| Cloudflare DNS | 1.1.1.1 |
| Cloudflare DNS | 1.0.0.1 |
| OpenDNS | 208.67.222.222 |

---

# DNS Ports

DNS primarily uses:

| Protocol | Port |
|-----------|------|
| UDP | 53 |
| TCP | 53 |

UDP is used for most DNS queries because it is fast.

TCP is used for:

- Zone transfers
- Large DNS responses
- DNSSEC

---

# DNS Lookup Example

Linux command:

```bash
nslookup google.com
```

Output:

```text
Name: google.com

Address: 142.xxx.xxx.xxx
```

---

Using `dig`:

```bash
dig google.com
```

---

Using `host`:

```bash
host google.com
```

---

# DNS in Socket Programming

When using:

```c
getaddrinfo()
```

the operating system automatically performs DNS resolution.

Example:

```c
getaddrinfo("google.com",
            "80",
            NULL,
            &result);
```

The programmer does not manually query DNS servers.

---

# Advantages

- Easy-to-remember domain names
- Distributed architecture
- Fast due to caching
- Highly scalable
- Supports load balancing

---

# Common Problems

- Incorrect DNS records
- Expired cache
- DNS server unavailable
- Slow DNS resolution
- Incorrect resolver configuration

---

# Summary

| Component | Purpose |
|-----------|---------|
| Domain Name | Human-readable website name |
| Resolver | Performs DNS lookup |
| Root Server | Points to TLD server |
| TLD Server | Points to authoritative server |
| Authoritative Server | Returns the IP address |
| A Record | IPv4 mapping |
| AAAA Record | IPv6 mapping |
| CNAME | Alias |
| MX | Mail server |

---

# Key Takeaways

- DNS stands for **Domain Name System**.
- It translates domain names into IP addresses.
- DNS follows a hierarchical lookup process involving Root, TLD, and Authoritative servers.
- Most DNS queries use **UDP port 53**, while TCP is used for specific cases.
- Common DNS records include **A**, **AAAA**, **CNAME**, **MX**, **NS**, and **TXT**.
- Applications typically rely on system functions such as `getaddrinfo()` to perform DNS lookups automatically.

---

# Conclusion

The Domain Name System is one of the core services of the Internet. It allows users to access websites using easy-to-remember names while computers communicate using IP addresses. Understanding DNS is essential for network programming, system administration, and troubleshooting connectivity issues.
