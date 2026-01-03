# OSI Model

The OSI model (or Open Systems Interconnection Model) is an essential model used in networking.  This critical model provides a framework dictating how all networked devices will send, receive and interpret data.One of the main benefits of the OSI model is that devices can have different functions and designs on a network while communicating with other devices. Data sent across a network that follows the uniformity of the OSI model can be understood by other devices.

The OSI model consists of seven layers. Each layer has a different set of responsibilities and is arranged from Layer 7 to Layer 1.

<img width="1127" height="786" alt="osi model" src="https://github.com/user-attachments/assets/64ecdb6f-daa5-4d28-88a1-b57f0dff39da" />

##
Let Explore each Network Layer one by one:-

## Physical layers

Transmitting data over a physical medium,such as a cable or over the air.Devices use electrical signals to transfer data between each other in a binary numbering system (1's and 0's).For example, ethernet cables connecting devices.

## Data Link layer

Transmits data between network nodes using MAC address-based switching.
It receives a packet from the network layer (including the IP address for the remote computer) and adds in the physical MAC (Media Access Control) address of the receiving endpoint. Inside every network-enabled computer is a Network Interface Card (NIC) which comes with a unique MAC address to identify it.

## Network layer

where the magic of routing & re-assembly of data takes place (from these small chunks to the larger chunk). Some protocols at this layer determine exactly what is the "optimal" path that data should take to reach a device, we should only know about their existence at this stage of the networking module. Briefly, these protocols include OSPF (Open Shortest Path First) and RIP (Routing Information Protocol). The factors that decide what route is taken is decided like :

- What path is the shortest? I.e. has the least amount of devices that the packet needs to travel across.
- What path is the most reliable? I.e. have packets been lost on that path before?
- Which path has the faster physical connection? I.e. is one path using a copper connection (slower) or a fibre (considerably faster)?

## Transport layer 

Transfering data b/w hosts.

When data is sent between devices, it follows one of two different protocols that are decided based upon several factors:
- TCP:- Transmission Control Protocol (TCP) is a connection-oriented protocol requiring a TCP three-way-handshake to establish a connection. TCP provides reliable data transfer, flow control and congestion control. Higher-level protocols such as HTTP, POP3, IMAP and SMTP use TCP.
- UDP:- User Datagram Protocol (UDP) is a connectionless protocol; UDP does not require a connection to be established. UDP is suitable for protocols that rely on fast queries, such as DNS, and for protocols that prioritise real-time communications, such as audio/video conferencing and broadcast.

## Session Layer

The Session Layer (Layer 5 of the OSI Model) acts as a "dialog controller." It manages the conversation between applications on different devices, ensuring they can establish, maintain, and synchronize their interaction.

### Core Responsibilities

- Session Management: Establishes, maintains, and terminates connections (sessions) between local and remote applications.
- Synchronization: Adds checkpoints to a data stream. If a transfer is interrupted, it can resume from the last checkpoint rather than starting over.
- Dialog Control: Decides whose turn it is to talk (Simplex, Half-duplex, or Full-duplex).
 
## Presentation Layer

The Presentation Layer (Layer 6 of the OSI Model) acts as the network's "Translator." It ensures that the data sent from the application layer of one system can be read by the application layer of another system.

### Core Responsibilities

- Translation: Converts data from machine-dependent formats (e.g., EBCDIC) into a generic format (e.g., ASCII) and back.
- Encryption/Decryption: Handles data security (like SSL/TLS) to ensure privacy during transmission.
- Compression: Reduces the file size to speed up data transfer.

## Application layer

The application layer of the OSI model is the layer that you will be most familiar with. This familiarity is because the application layer is the layer in which protocols and rules are in place to determine how the user should interact with data sent or received.
Everyday applications such as email clients, browsers, or file server browsing software such as FileZilla provide a friendly, Graphical User Interface (GUI) for users to interact with data sent or received. 

## OSI Model Mnemonic

A common way to remember the OSI layers is:

**P**lease  
**D**o  
**N**ot  
**T**ouch  
**S**am’s  
**P**et  
**A**lligator
