# Multi-Client Chat Server

## Overview

The **Multi-Client Chat Server** is a concurrent TCP chat application developed in **C** using **POSIX sockets**, **POSIX threads (pthreads)**, and **mutex synchronization**. Unlike a basic socket server that handles only one client, this server supports multiple clients communicating simultaneously.

Each connected client is handled by its own thread, allowing multiple users to send and receive messages concurrently. Shared resources such as the list of connected clients are protected using mutex locks to prevent race conditions and ensure thread-safe operations.

This project marked my introduction to concurrent programming in Linux and provided practical experience with thread management and synchronization.

---

# Project Objectives

The primary goals of this project were to:

- Learn concurrent programming using POSIX Threads.
- Build a TCP server capable of handling multiple clients.
- Understand thread synchronization using mutexes.
- Prevent race conditions while accessing shared resources.
- Implement real-time message broadcasting.

---

# Features

- Multiple clients connected simultaneously
- TCP-based communication
- IPv4 networking
- Dedicated thread for each client
- Real-time message broadcasting
- Username support
- Join and leave notifications
- Thread-safe client management
- Graceful client disconnection
- Error handling

---

# Technologies Used

- C Programming
- POSIX Sockets
- POSIX Threads (pthread)
- pthread Mutexes
- TCP/IP
- IPv4
- GCC
- Linux
- Makefile

---

# Concepts Implemented

This project demonstrates:

- Client-Server Architecture
- TCP Networking
- Multi-threading
- Concurrent Programming
- Thread Synchronization
- Mutex Locks
- Shared Memory
- Broadcast Communication
- Socket Programming
- Thread Lifecycle Management

---

# Project Architecture

```text
                  +----------------------+
                  |       Server         |
                  +----------------------+
                            |
        ---------------------------------------------
        |            |            |                 |
        ▼            ▼            ▼                 ▼
    Thread 1     Thread 2     Thread 3        Thread N
        |            |            |                 |
     Client A     Client B     Client C       Client N
```

Each client connection is assigned its own worker thread.

---

# Communication Flow

```text
Server Starts

↓

Create Socket

↓

Bind

↓

Listen

↓

Accept Client

↓

Create Thread

↓

Handle Client

↓

Broadcast Messages

↓

Client Disconnects

↓

Destroy Thread
```

---

# Thread Lifecycle

```text
Client Connects

↓

accept()

↓

pthread_create()

↓

Handle Client

↓

recv()

↓

Broadcast Message

↓

Client Leaves

↓

pthread_exit()
```

---

# Broadcasting Messages

When one client sends a message:

```text
Client A

↓

Server

↓

Broadcast

↓

Client B

↓

Client C

↓

Client D
```

Every connected client receives the message except the sender.

---

# Thread Synchronization

Since multiple threads access the client list simultaneously, synchronization is required.

The project uses:

```text
pthread_mutex_t
```

to protect shared resources.

---

# Why Mutex Locks?

Without synchronization:

```text
Thread A

↓

Modify Client List

↑

↓

Thread B
```

Both threads may access the same data simultaneously, causing a race condition.

Using a mutex:

```text
Thread A

↓

Lock Mutex

↓

Modify Client List

↓

Unlock Mutex

↓

Thread B
```

Only one thread accesses the shared resource at a time.

---

# pthread Functions Used

| Function | Purpose |
|----------|---------|
| pthread_create() | Create a new thread |
| pthread_join() | Wait for a thread to finish |
| pthread_detach() | Automatically clean up finished threads |
| pthread_exit() | Terminate a thread |
| pthread_mutex_init() | Initialize mutex |
| pthread_mutex_lock() | Lock shared resource |
| pthread_mutex_unlock() | Unlock shared resource |
| pthread_mutex_destroy() | Destroy mutex |

---

# Socket System Calls Used

| Function | Purpose |
|----------|---------|
| socket() | Create socket |
| bind() | Bind socket |
| listen() | Listen for connections |
| accept() | Accept clients |
| send() | Send messages |
| recv() | Receive messages |
| close() | Close socket |

---

# Server Workflow

```text
Start Server

↓

Create Socket

↓

Bind

↓

Listen

↓

Accept Client

↓

Create Thread

↓

Receive Messages

↓

Broadcast

↓

Client Disconnects

↓

Remove Client

↓

Continue Listening
```

---

# Client Workflow

```text
Create Socket

↓

Connect

↓

Enter Username

↓

Send Messages

↓

Receive Broadcasts

↓

Disconnect
```

---

# Client Management

The server maintains a shared list of connected clients.

Each client stores information such as:

- Socket Descriptor
- Username
- Thread ID

This shared list is protected using mutex locks.

---

# Skills Learned

Through this project, I learned:

- Creating concurrent applications
- POSIX Thread Programming
- Thread synchronization
- Mutex locking
- Shared resource management
- Broadcast communication
- Concurrent socket programming
- Thread-safe server design
- Debugging multi-threaded programs

---

# Challenges Faced

Some challenges encountered while building this project included:

- Understanding POSIX Threads
- Synchronizing shared data
- Avoiding race conditions
- Managing client disconnections
- Preventing resource leaks
- Broadcasting messages efficiently
- Debugging multiple threads running simultaneously

Overcoming these challenges significantly improved my understanding of concurrent programming.

---

# Improvements Over Previous Project

Compared to the **Linux Socket Chat** project, this implementation adds:

- Multi-client support
- Concurrent execution
- Thread-per-client model
- Username management
- Broadcast messaging
- Mutex synchronization
- Better server scalability

---

# Possible Future Improvements

Future enhancements include:

- Event-driven architecture using `poll()`
- `epoll()` support
- TLS/SSL encryption
- SQLite chat history
- Private messaging
- User authentication
- File transfer
- Commands
- Logging system
- Thread pool implementation

Several of these improvements were later explored in my **Event-Driven Chat Server** project.

---

# Learning Progression

```text
Linux Socket Chat

↓

Multi-Client Chat Server (Threads)

↓

Event-Driven Chat Server (poll())

```

Each project builds upon the concepts introduced in the previous one.

---

# Repository

GitHub Repository:

**https://github.com/Guru-codes07/multi---client---chat---server-**

---

# Related Documentation

This project applies concepts covered in:

- Client-Server Architecture
- Socket Programming Basics
- Socket System Calls
- TCP Three-Way Handshake
- Blocking vs Non-Blocking Sockets
- Processes vs Threads
- POSIX Threads
- Mutex Locks
- Thread Synchronization

---

# Key Takeaways

- Built a concurrent TCP chat server using POSIX Threads.
- Learned thread creation and lifecycle management.
- Implemented thread-safe shared resource access using mutexes.
- Designed a broadcast messaging system.
- Improved understanding of concurrent programming and Linux networking.
- Established a strong foundation for scalable server development.

---

# Conclusion

The **Multi-Client Chat Server** represents an important milestone in my systems programming journey. By combining POSIX sockets with POSIX threads and mutex synchronization, I learned how to build concurrent network applications capable of serving multiple clients simultaneously. This project strengthened my understanding of Linux networking, multithreading, synchronization, and scalable server architecture, paving the way for my next project: an event-driven chat server using `poll()`.
