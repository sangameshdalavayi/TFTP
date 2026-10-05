# TFTP – File Transfer Application

## 📌 Overview

This project implements a **TFTP (Trivial File Transfer Protocol) style file transfer application in C** using **UDP socket programming**.

The application consists of a **client and server** that communicate over a network to upload and download files. It supports two transfer modes: **Octet** and **Netascii**.

The project demonstrates practical concepts of **computer networking, socket programming, file handling, data conversion, acknowledgements, and reliable data transfer over UDP**.

---

## 🚀 Features

- Client-server file transfer using **UDP**
- Upload files using **Put File**
- Download files using **Get File**
- Supports **Octet transfer mode**
- Supports **Netascii transfer mode**
- File availability checking
- Acknowledgement-based data transfer
- Packet retransmission when a packet is reported as not received
- IPv4 address validation
- File creation and overwriting
- Data transfer using fixed-size packets
- Menu-driven interface
- Separate client and server implementations

---

## 🛠️ Technologies Used

- **C Programming**
- **Linux / Unix**
- **UDP Socket Programming**
- **Computer Networking**
- **File Handling**
- **POSIX System Calls**
- **IPv4**

---

## 🔧 System Calls & Functions Used

| Function | Purpose |
|---|---|
| `socket()` | Creates a UDP socket |
| `bind()` | Binds the socket to an IP address and port |
| `sendto()` | Sends data through the UDP socket |
| `recvfrom()` | Receives data from the UDP socket |
| `htons()` | Converts port number to network byte order |
| `inet_addr()` | Converts IPv4 address to network format |
| `open()` | Opens or creates a file |
| `read()` | Reads file data |
| `write()` | Writes received data to a file |
| `close()` | Closes files and sockets |
| `memcpy()` | Copies file data into packets |
| `strcmp()` | Compares transfer modes and acknowledgements |
| `strlen()` | Determines string length |
| `snprintf()` | Constructs file transfer requests |

---

## 📂 Project Structure

```text
TFTP/
│
├── client/
│   ├── client.c
│   ├── main.h
│   └── a.out
│
└── server/
    ├── server.c
    ├── main.h
    └── a.out
```

### Client

The client provides options to:

1. Put a file
2. Get a file
3. Exit

### Server

The server handles file upload and download requests received from the client.

---

## 🔄 File Transfer Modes

### 1. Octet Mode

In **Octet mode**, file data is transferred without modification.

```text
File → Read → UDP Packet → Network → UDP Packet → Write → File
```

This mode transfers the original bytes directly.

### 2. Netascii Mode

In **Netascii mode**, newline characters are converted before transmission.

```text
\n  →  \r\n
```

At the receiving side, the conversion is reversed:

```text
\r\n  →  \n
```

The
