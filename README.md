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

The project implements:

```c
convert_to_netascii()
convert_from_netascii()
```

for these conversions.

---

## 📤 Put File – Upload

The file upload process works as follows:

```text
Client
  │
  │ File Request
  ▼
Server
  │
  │ Check File
  ▼
File Available
  │
  │ Acknowledgement
  ▼
Read File
  │
  │ Divide into packets
  ▼
Send UDP Packet
  │
  ▼
Wait for ACK
  │
  ├── Packet received → Send next packet
  │
  └── Packet not received → Retransmit packet
```

The file is read in chunks and transmitted through UDP packets.

---

## 📥 Get File – Download

The download process works as follows:

```text
Client
  │
  │ File Request
  ▼
Server
  │
  │ Check File
  ▼
File Available
  │
  │ ACK
  ▼
Send File Data
  │
  ▼
Client Receives Packet
  │
  ├── Write Data
  │
  └── Send ACK
  │
  ▼
Receive Next Packet
```

The transfer continues until the final packet is received.

---

## 🔁 Acknowledgement & Retransmission

Since UDP does not provide built-in acknowledgement or retransmission, the project implements its own acknowledgement mechanism.

After sending a data packet, the sender waits for an acknowledgement.

If the receiver reports:

```text
data packet not reached
```

the sender retransmits the packet.

This provides a basic mechanism for improving reliability over UDP.

---

## 🌐 Network Configuration

The server uses:

```text
Protocol : UDP
Port     : 8000
Address  : 127.0.0.1
```

For downloading files, the client accepts the server's IPv4 address.

Example:

```text
127.0.0.1
```

---

## ⚙️ Compilation

### Compile the Server

Navigate to the server directory:

```bash
cd server
gcc server.c -o server
```

### Compile the Client

Navigate to the client directory:

```bash
cd client
gcc client.c -o client
```

---

## ▶️ Running the Project

### Step 1: Start the Server

Open a terminal and run:

```bash
cd server
./server
```

### Step 2: Start the Client

Open another terminal and run:

```bash
cd client
./client
```

Both applications can then communicate through UDP.

---

## 🧪 Example Operations

### Upload a File

Select:

```text
1. Put file
```

Then provide the required file information and transfer mode.

### Download a File

Select:

```text
2. Get file
```

Enter:

```text
Server IP address
Transfer mode
File name
```

The client then requests the file from the server.

---

## 🧠 Key Concepts Learned

- UDP socket programming
- Client-server architecture
- IPv4 addressing
- Socket creation and binding
- `sendto()` and `recvfrom()`
- File descriptors and file handling
- Network byte order
- Packet-based data transfer
- Acknowledgement mechanisms
- Packet retransmission
- Octet and Netascii data handling
- Error handling
- Linux/POSIX networking APIs

---

## 💡 Key Challenges & Learnings

- Implemented client-server communication using **UDP sockets** and managed socket creation, binding, sending, and receiving operations.
- Implemented **Octet and Netascii transfer modes**, including newline conversion between local and network representations.
- Designed an **acknowledgement and retransmission mechanism** to handle packets reported as not received during UDP-based file transfer.
- Managed file reading, writing, creation, and transfer in fixed-size data chunks while maintaining synchronization between client and server.

---

## 🎯 Project Objective

The main objective of this project is to understand the fundamentals of **UDP-based network communication and file transfer** by implementing a TFTP-style client-server application from scratch in C.

The project provides practical experience with **socket programming, networking APIs, file handling, data conversion, and reliable communication over an unreliable transport protocol**.

---

## 👨‍💻 Author

**Sangamesh Dalavayi**

**Branch:** Electronics and Communication Engineering

**Skills:** C | Linux | Computer Networks | Socket Programming | System Programming
