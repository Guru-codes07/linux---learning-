# Client-Server Architecture

**Client-Server Architecture** is one of the most widely used networking models in modern computing. It is a communication model in which one computer (**the client**) requests services or resources, while another computer (**the server**) processes the request and sends back a response.

Almost every application on the Internet follows this architecture, including websites, email services, cloud storage, online games, and chat applications.

---

# What is Client-Server Architecture?

Client-Server Architecture is a distributed computing model where multiple clients communicate with a centralized server over a network.

Instead of every computer communicating directly with each other, clients send requests to a server, and the server responds accordingly.

---

# Why Do We Need Client-Server Architecture?

Without a centralized server:

* Data would be difficult to manage.
* Every computer would need to communicate with every other computer.
* Security would be harder to enforce.
* Resource sharing would become inefficient.

With Client-Server Architecture:

* Resources are centralized.
* Multiple clients can access the same service.
* Easier administration.
* Better security.
* Easier scalability.

---

# Basic Architecture

```text
                +------------------+
                |      Server      |
                +------------------+
                  ▲      ▲      ▲
                  │      │      │
          ┌───────┘      │      └───────┐
          │              │              │
+----------------+ +----------------+ +----------------+
|    Client 1    | |    Client 2    | |    Client 3    |
+----------------+ +----------------+ +----------------+
```

The server waits for requests, while clients initiate communication.

---

# What is a Client?

A **client** is a device or application that requests a service from a server.

Examples:

* Web browser
* Mobile application
* Chat client
* FTP client
* Email client
* SSH client

Responsibilities of a client:

* Initiate communication
* Send requests
* Receive responses
* Display results to the user

---

# What is a Server?

A **server** is a computer or application that provides services to clients.

Examples:

* Web server
* Database server
* File server
* DNS server
* Mail server
* Chat server

Responsibilities of a server:

* Wait for incoming connections
* Process requests
* Access resources
* Send responses
* Handle multiple clients

---

# Request-Response Model

Communication generally follows this pattern:

```text
Client
   │
   │ Request
   ▼
Server
   │
   │ Process Request
   ▼
Response
   │
   ▼
Client
```

The client always starts the communication.

---

# Real-World Example

Suppose you open your browser and visit:

```text
https://www.google.com
```

The sequence is:

1. Browser acts as the client.
2. Browser sends an HTTP request.
3. Google's server receives the request.
4. The server processes it.
5. The server sends back the web page.
6. The browser displays the page.

---

# Client-Server Communication Flow

```text
Client

↓

Create Socket

↓

Connect to Server

↓

Send Request

↓

Receive Response

↓

Close Connection
```

Server:

```text
Server

↓

Create Socket

↓

Bind Port

↓

Listen

↓

Accept Connection

↓

Receive Request

↓

Process Request

↓

Send Response

↓

Close Connection
```

---

# Client-Server Example Using a Chat Application

Imagine a chat server running on:

```text
IP Address : 192.168.1.100
Port       : 8080
```

Three users connect:

```text
Alice

↓

Server

↑

Bob

↓

Server

↑

Charlie
```

Each client communicates only with the server.

The server is responsible for forwarding messages to the appropriate clients.

---

# One Server, Multiple Clients

A single server can handle many clients simultaneously.

```text
                 Server
                    │
     ┌──────────────┼──────────────┐
     │              │              │
 Client A       Client B       Client C
```

Servers achieve this using techniques such as:

* Threads
* Processes
* I/O Multiplexing (`select()`, `poll()`, `epoll()`)

---

# Advantages

* Centralized management
* Easy maintenance
* Better security
* Resource sharing
* Supports multiple clients
* Easier backups
* Scalable

---

# Disadvantages

* Server failure affects all clients.
* High server load can reduce performance.
* Requires a reliable network connection.
* Can become a bottleneck if not properly designed.

---

# Types of Servers

| Server          | Purpose                           |
| --------------- | --------------------------------- |
| Web Server      | Hosts websites                    |
| File Server     | Stores and shares files           |
| Database Server | Stores databases                  |
| Mail Server     | Sends and receives email          |
| DNS Server      | Resolves domain names             |
| FTP Server      | Transfers files                   |
| Chat Server     | Handles messaging between clients |

---

# Client-Server vs Peer-to-Peer (P2P)

| Client-Server            | Peer-to-Peer                    |
| ------------------------ | ------------------------------- |
| Central server           | No central server               |
| Easy management          | Harder to manage                |
| Better security          | Lower centralized security      |
| Easier backups           | Distributed data                |
| Server provides services | Every node can provide services |

Example:

Client-Server:

```text
Client → Server → Client
```

Peer-to-Peer:

```text
Computer ↔ Computer ↔ Computer
```

---

# Client-Server in Socket Programming

### Server Side

Typical sequence:

```c
socket();

bind();

listen();

accept();

recv();

send();

close();
```

---

### Client Side

Typical sequence:

```c
socket();

connect();

send();

recv();

close();
```

---

# Real-World Services

| Service      | Client          | Server          |
| ------------ | --------------- | --------------- |
| Web Browsing | Browser         | Web Server      |
| SSH          | SSH Client      | SSH Server      |
| Email        | Mail Client     | Mail Server     |
| Chat         | Chat Client     | Chat Server     |
| Database     | Database Client | Database Server |
| FTP          | FTP Client      | FTP Server      |

---

# Where is Client-Server Used?

Client-Server Architecture powers countless everyday applications, including:

* Websites
* Mobile applications
* Cloud storage
* Online banking
* Social media platforms
* Video conferencing
* Multiplayer games
* Email systems
* Streaming services
* Messaging applications

---

# Relation with TCP/IP

Client-Server Architecture relies heavily on the TCP/IP protocol suite.

Typical communication stack:

```text
Application
│
TCP
│
IP
│
Ethernet / Wi-Fi
```

TCP ensures reliable communication, while IP ensures packets reach the correct destination.

---

# Your Chat Server Example

Your multi-client chat server follows the Client-Server model.

### Server

* Waits for client connections.
* Accepts multiple clients.
* Receives messages.
* Broadcasts messages to other clients.

### Client

* Connects to the server.
* Sends messages.
* Receives messages.
* Displays chat output.

This is a classic Client-Server application.

---

# Key Terms

| Term       | Meaning                                         |
| ---------- | ----------------------------------------------- |
| Client     | Requests a service                              |
| Server     | Provides a service                              |
| Request    | Message sent by a client                        |
| Response   | Message returned by a server                    |
| Socket     | Communication endpoint                          |
| Port       | Identifies an application on a device           |
| Connection | Communication channel between client and server |

---

# Key Takeaways

* Client-Server Architecture is a centralized communication model.
* Clients initiate communication, while servers respond.
* A server can handle multiple clients simultaneously.
* Most Internet applications follow this architecture.
* Socket programming in C is commonly used to implement Client-Server applications.
* Your TCP echo server and multi-client chat server are practical examples of the Client-Server model.

---

# Conclusion

Client-Server Architecture is the backbone of modern networking and distributed computing. It enables efficient communication between applications by separating service providers (servers) from service consumers (clients). Understanding this architecture is essential before diving into advanced socket programming, concurrent servers, web servers, and network protocol implementation. It also provides the foundation for building scalable applications such as chat systems, file servers, APIs, and cloud-based services.

