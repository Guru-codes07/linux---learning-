# HTTP (Hypertext Transfer Protocol)

The **Hypertext Transfer Protocol (HTTP)** is an application-layer protocol used for communication between web clients (such as browsers) and web servers.

HTTP defines how requests are sent by clients and how responses are returned by servers.

Every time you visit a website, your browser uses HTTP or HTTPS to communicate with the server.

---

# What is HTTP?

HTTP is a **request-response protocol**.

A client sends a request.

The server processes the request and sends back a response.

```text
Client

↓

HTTP Request

↓

Server

↓

HTTP Response

↓

Client
```

---

# Why Do We Need HTTP?

Suppose you open:

```text
https://www.example.com
```

Your browser must tell the server:

- Which webpage you want
- Which data you need
- Which format you accept

HTTP defines a standard way to exchange this information.

---

# HTTP Architecture

```text
Browser

↓

HTTP Request

↓

Web Server

↓

HTTP Response

↓

Browser
```

---

# HTTP in the OSI Model

```text
Application Layer
        │
       HTTP
        │
Transport Layer
        │
       TCP
        │
Internet Layer
        │
        IP
        │
Network Access Layer
```

HTTP works on top of TCP.

---

# Default Ports

| Protocol | Port |
|----------|------|
| HTTP | 80 |
| HTTPS | 443 |

---

# HTTP Request

An HTTP request is sent from the client to the server.

It consists of:

- Request Line
- Headers
- Blank Line
- Optional Body

---

## HTTP Request Format

```text
GET /index.html HTTP/1.1
Host: example.com
User-Agent: Firefox
Accept: text/html

```

---

# Request Line

Example:

```text
GET /index.html HTTP/1.1
```

It contains:

- HTTP Method
- Resource
- HTTP Version

---

# HTTP Methods

HTTP defines several methods that indicate what action the client wants to perform.

---

## GET

Retrieves data from the server.

Example:

```http
GET /products HTTP/1.1
```

Used for:

- Opening web pages
- Reading data
- Searching

---

## POST

Sends data to the server.

Example:

```http
POST /login HTTP/1.1
```

Used for:

- Login forms
- Registration
- Uploading data

---

## PUT

Creates or replaces an existing resource.

Example:

```http
PUT /users/10 HTTP/1.1
```

---

## PATCH

Updates part of an existing resource.

Example:

```http
PATCH /users/10 HTTP/1.1
```

---

## DELETE

Deletes a resource.

Example:

```http
DELETE /users/10 HTTP/1.1
```

---

## HEAD

Similar to GET, but returns only the headers.

Useful for checking whether a resource exists.

---

## OPTIONS

Returns the HTTP methods supported by the server.

---

# HTTP Headers

Headers provide additional information about the request or response.

Example:

```http
Host: example.com

User-Agent: Firefox

Accept: text/html
```

---

# Common Request Headers

| Header | Purpose |
|---------|----------|
| Host | Domain name |
| User-Agent | Browser information |
| Accept | Accepted content types |
| Authorization | Authentication credentials |
| Cookie | Sends cookies |
| Content-Type | Type of request body |
| Content-Length | Size of request body |

---

# HTTP Request Body

Some requests contain a body.

Example:

```http
POST /login HTTP/1.1
Content-Type: application/json

{
    "username":"guru",
    "password":"1234"
}
```

GET requests usually do not contain a body.

---

# HTTP Response

The server sends an HTTP response after processing the request.

A response contains:

- Status Line
- Headers
- Blank Line
- Response Body

---

## Response Format

```http
HTTP/1.1 200 OK
Content-Type: text/html
Content-Length: 145

<html>
...
</html>
```

---

# Status Line

Example:

```text
HTTP/1.1 200 OK
```

Contains:

- HTTP Version
- Status Code
- Status Message

---

# HTTP Status Codes

Status codes indicate the result of the request.

---

## 1xx – Informational

Example:

```text
100 Continue
```

---

## 2xx – Success

| Code | Meaning |
|------|---------|
| 200 | OK |
| 201 | Created |
| 204 | No Content |

---

## 3xx – Redirection

| Code | Meaning |
|------|---------|
| 301 | Moved Permanently |
| 302 | Found |
| 304 | Not Modified |

---

## 4xx – Client Errors

| Code | Meaning |
|------|---------|
| 400 | Bad Request |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |
| 405 | Method Not Allowed |

---

## 5xx – Server Errors

| Code | Meaning |
|------|---------|
| 500 | Internal Server Error |
| 502 | Bad Gateway |
| 503 | Service Unavailable |
| 504 | Gateway Timeout |

---

# Common Response Headers

| Header | Purpose |
|---------|----------|
| Content-Type | Type of returned data |
| Content-Length | Response size |
| Server | Web server information |
| Date | Response time |
| Set-Cookie | Sends cookies |
| Cache-Control | Cache settings |

---

# HTTP Response Body

The response body contains the requested resource.

Example:

```html
<html>

<head>
<title>Home</title>
</head>

<body>

<h1>Hello World</h1>

</body>

</html>
```

---

# HTTP Request-Response Cycle

```text
Browser

↓

DNS Lookup

↓

TCP Connection

↓

HTTP Request

↓

Web Server

↓

HTTP Response

↓

Browser Displays Page
```

---

# HTTP is Stateless

HTTP does not remember previous requests.

Example:

```text
Request 1

↓

Server Responds

↓

Connection Ends
```

The next request is treated as completely new.

To maintain user sessions, websites use:

- Cookies
- Sessions
- Tokens

---

# HTTP Versions

| Version | Features |
|----------|----------|
| HTTP/1.0 | One request per connection |
| HTTP/1.1 | Persistent connections |
| HTTP/2 | Multiplexing, Header Compression |
| HTTP/3 | Runs over QUIC (UDP) |

---

# HTTP vs HTTPS

| Feature | HTTP | HTTPS |
|----------|-------|--------|
| Encryption | No | Yes |
| Default Port | 80 | 443 |
| Security | Low | High |
| Uses TLS | No | Yes |

---

# HTTP in Socket Programming

When writing an HTTP server using sockets, the client sends a request like:

```text
GET / HTTP/1.1
Host: localhost
```

The server responds:

```text
HTTP/1.1 200 OK

Content-Type: text/plain

Hello World
```

This is simply text sent over a TCP connection.

---

# Example HTTP Request

```http
GET /index.html HTTP/1.1
Host: example.com
User-Agent: Firefox
Accept: text/html
```

---

# Example HTTP Response

```http
HTTP/1.1 200 OK
Content-Type: text/html

<html>

<body>

<h1>Hello World</h1>

</body>

</html>
```

---

# Advantages

- Simple protocol
- Human-readable messages
- Platform-independent
- Widely supported
- Easy to implement

---

# Limitations

- Stateless by default
- HTTP traffic is unencrypted
- Requires HTTPS for secure communication

---

# Summary

| Component | Purpose |
|-----------|---------|
| Request | Sent by the client |
| Response | Returned by the server |
| Method | Action to perform |
| Header | Metadata |
| Body | Data being transmitted |
| Status Code | Indicates request result |

---

# Key Takeaways

- HTTP stands for **Hypertext Transfer Protocol**.
- It is an application-layer protocol that follows the **request-response** model.
- HTTP typically uses **TCP port 80**, while HTTPS uses **TCP port 443**.
- Common HTTP methods include **GET**, **POST**, **PUT**, **PATCH**, and **DELETE**.
- Requests and responses consist of a start line, headers, and an optional body.
- Status codes indicate the outcome of a request, such as **200 OK**, **404 Not Found**, and **500 Internal Server Error**.
- HTTP is **stateless**, so mechanisms like cookies and sessions are used to maintain user state.

---

# Conclusion

HTTP is the foundation of communication on the World Wide Web. It enables browsers, servers, APIs, and web applications to exchange information using a standardized request-response model. Understanding HTTP is essential for web development, network programming, REST API design, and building applications such as web servers and browsers.
