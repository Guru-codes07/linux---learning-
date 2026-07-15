# HTTPS & TLS

**HTTPS (Hypertext Transfer Protocol Secure)** is the secure version of HTTP. It uses **TLS (Transport Layer Security)** to encrypt communication between a client and a server, ensuring confidentiality, integrity, and authentication.

Whenever you see a URL beginning with:

```text
https://
```

the communication is protected using TLS.

---

# Why Do We Need HTTPS?

Suppose you log into your bank using plain HTTP.

```text
Username

↓

Password

↓

Internet
```

Anyone monitoring the network could read your credentials.

With HTTPS:

```text
Username

↓

Encrypted Data

↓

Internet

↓

Server
```

Even if someone intercepts the traffic, they cannot read the encrypted information.

---

# HTTP vs HTTPS

| Feature | HTTP | HTTPS |
|----------|------|--------|
| Encryption | No | Yes |
| Default Port | 80 | 443 |
| Authentication | No | Yes |
| Data Integrity | No | Yes |
| Uses TLS | No | Yes |

---

# What is TLS?

**TLS (Transport Layer Security)** is a cryptographic protocol that provides secure communication over a network.

TLS is responsible for:

- Encryption
- Authentication
- Data Integrity

HTTP simply uses TLS underneath to become HTTPS.

---

# SSL vs TLS

SSL (Secure Sockets Layer) is the predecessor of TLS.

| SSL | TLS |
|------|-----|
| Older protocol | Modern protocol |
| Insecure | Secure |
| Deprecated | Currently used |

Although people still say **SSL Certificate**, modern websites actually use TLS.

---

# HTTPS Architecture

```text
Browser

↓

TLS Handshake

↓

Encrypted TCP Connection

↓

HTTP Messages

↓

Web Server
```

---

# How HTTPS Works

```text
Client

↓

TCP Three-Way Handshake

↓

TLS Handshake

↓

Encrypted Communication

↓

HTTP Requests & Responses
```

---

# Security Goals

TLS provides three important properties.

---

## Confidentiality

Only the sender and receiver can read the transmitted data.

---

## Integrity

Ensures that data is not modified during transmission.

---

## Authentication

Verifies that the client is communicating with the genuine server.

---

# Cryptography

TLS uses two kinds of encryption.

---

## Symmetric Encryption

Uses the same key for encryption and decryption.

```text
Shared Key

↓

Encrypt

↓

Decrypt
```

Examples:

- AES
- ChaCha20

Fast and efficient.

---

## Asymmetric Encryption

Uses two keys.

```text
Public Key

↓

Encrypt

↓

Private Key

↓

Decrypt
```

Examples:

- RSA
- ECC

Slower but ideal for securely exchanging keys.

---

# Public Key

The public key can be shared with anyone.

It is used to encrypt information.

---

# Private Key

The private key is secret.

Only the server possesses it.

It is used to decrypt information.

---

# Digital Certificates

A certificate proves the identity of a server.

It contains:

- Domain name
- Public key
- Expiration date
- Certificate Authority
- Digital signature

Example:

```text
example.com

↓

Public Key

↓

Certificate
```

---

# Certificate Authority (CA)

A Certificate Authority is a trusted organization that verifies server identities and signs certificates.

Examples include:

- Let's Encrypt
- DigiCert
- GlobalSign
- Sectigo

---

# TLS Handshake

Before encrypted communication begins, the client and server perform a handshake.

---

## Step 1

Client sends:

```text
Client Hello
```

Includes:

- Supported TLS versions
- Supported cipher suites
- Random number

---

## Step 2

Server replies:

```text
Server Hello
```

Includes:

- Selected cipher suite
- TLS version
- Server certificate

---

## Step 3

The client verifies the server's certificate.

If valid:

```text
Continue
```

Otherwise:

```text
Connection Failed
```

---

## Step 4

The client and server securely generate a shared session key.

---

## Step 5

Encrypted communication begins.

---

# TLS Handshake Flow

```text
Client

↓

Client Hello

↓

Server Hello

↓

Certificate

↓

Key Exchange

↓

Session Key

↓

Encrypted Communication
```

---

# Session Keys

After the handshake:

```text
Symmetric Encryption

↓

AES

↓

Fast Communication
```

The expensive asymmetric encryption is only used during key exchange.

---

# Cipher Suites

A cipher suite defines:

- Key exchange algorithm
- Encryption algorithm
- Authentication algorithm

Example:

```text
TLS_AES_128_GCM_SHA256
```

---

# HTTPS Request Flow

```text
Browser

↓

DNS Lookup

↓

TCP Connection

↓

TLS Handshake

↓

Encrypted HTTP Request

↓

Server

↓

Encrypted HTTP Response
```

---

# Common HTTPS Port

| Protocol | Port |
|----------|------|
| HTTPS | 443 |

---

# TLS in Socket Programming

When using OpenSSL:

```c
SSL_CTX_new()

↓

SSL_new()

↓

SSL_set_fd()

↓

SSL_accept()

↓

SSL_read()

↓

SSL_write()
```

These functions establish an encrypted connection over a normal TCP socket.

---

# Advantages

- Encrypts communication
- Prevents eavesdropping
- Verifies server identity
- Protects passwords
- Protects cookies
- Ensures message integrity

---

# Limitations

- Slightly higher CPU usage
- Certificate management required
- More complex than plain HTTP

---

# Summary

| Component | Purpose |
|-----------|---------|
| HTTP | Web protocol |
| HTTPS | Secure HTTP |
| TLS | Encryption protocol |
| Certificate | Server identity |
| Public Key | Encrypt data |
| Private Key | Decrypt data |
| CA | Signs certificates |

---

# Key Takeaways

- HTTPS is HTTP running over TLS.
- TLS provides encryption, authentication, and data integrity.
- HTTPS typically uses TCP port **443**.
- TLS uses asymmetric encryption during the handshake and symmetric encryption for data transfer.
- Digital certificates verify the server's identity.
- Modern secure websites rely on TLS rather than the older SSL protocol.

---

# Conclusion

HTTPS is the standard for secure communication on the modern Internet. By combining HTTP with TLS, it protects sensitive information such as passwords, payment details, and personal data from interception and tampering. Understanding HTTPS and TLS is essential for web development, network security, and secure socket programming.
