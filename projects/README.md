# Projects

This directory contains documentation for the practical projects I've built while learning Linux systems programming, networking, and concurrent programming.

Each project has its own dedicated GitHub repository and its own documentation page within this directory. These projects demonstrate the practical application of the concepts covered throughout this repository.

---

# Purpose

The goal of this directory is to:

- Document each project and its architecture
- Explain the concepts implemented in the project
- Showcase the progression of my systems programming skills
- Provide quick access to the project's source code

---

# Projects

| Project | Documentation | GitHub Repository |
|----------|---------------|-------------------|
| Linux Socket Chat | [Linux-Socket-Chat.md](Linux-Socket-Chat.md) | https://github.com/Guru-codes07/linux-socket-chat |
| Multi-Client Chat Server | [Multi-Client-Chat-Server.md](Multi-Client-Chat-Server.md) | https://github.com/Guru-codes07/multi---client---chat---server- |
| Event-Driven Chat Server (`poll()`) | [Event-Poll-Chat-Server.md](Event-Poll-Chat-Server.md) | https://github.com/Guru-codes07/c-event-loop-chat |

---

# Learning Progression

```text
Linux Socket Programming
        │
        ▼
Linux Socket Chat
        │
        ▼
Multi-Client Chat Server (Threads)
        │
        ▼
Event-Driven Chat Server (poll())
        │
        ▼
epoll()-based Server (Planned)
```

Each project builds upon the concepts learned in the previous one, gradually introducing more advanced Linux and networking techniques.

---

# Technologies

The projects in this directory make use of:

- C Programming
- POSIX Sockets
- TCP/IP Networking
- POSIX Threads (`pthread`)
- `poll()`
- Linux System Calls
- GCC
- GNU/Linux

---

# Repository Structure

```text
Projects/
├── README.md
├── Linux-Socket-Chat.md
├── Multi-Client-Chat-Server.md
└── Event-Poll-Chat-Server.md
```

Each documentation file explains the project's architecture, implementation, concepts, and includes a link to its standalone GitHub repository.

---

# License

All projects are open source and intended for learning, experimentation, and demonstrating Linux systems programming concepts.
