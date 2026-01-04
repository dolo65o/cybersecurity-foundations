## TCP(Transmission Control Protocol)

Transmission Control Protocol (TCP) is a connection-oriented protocol requiring a TCP three-way-handshake to establish a connection. TCP provides reliable data transfer, flow control and congestion control. Higher-level protocols such as HTTP, POP3, IMAP and SMTP use TCP.

## The TCP/IP protocol consists of four layers:-

- Application
- Transport
- Internet
- Network Interface

### Packets & Frames

* Packets and frames are small pieces of data that, when forming together, make a larger piece of information or message.
* A packet is a piece of data from Layer 3 (Network Layer) of the OSI model, containing information such as an IP header and payload. A frame, however, is used at Layer 2 (Data Link) of the OSI model.

# Headers

TCP packets contain various sections of information known as headers that are added from encapsulation.

* Source Port:-This value is the port opened by the sender to send the TCP packet from.
* Destination Port:-This value is the port number that an application or service is running on the remote host (the one receiving data).
* Source IP:-IP address of the device that is sending the packet.
* Destination IP:- IP address of the device that the packet is destined for.
* Sequence Number:-When a connection occurs, the first piece of data transmitted is given a random number.
* Acknowledgement Number:-the number for the next piece of data will have the sequence number + 1.
* Checksum:-A checksum is a value used to ensure data integrity in network communications, particularly in TCP.
* Data:-This header is where the data.
* Flag:-how the packet should be handled by either device during the handshake process.

> Information is added to each layer of the TCP model as the piece of data (or packet) traverses it.This process is known as encapsulation - where the reverse of this process is decapsulation.

## Three-way handshake

TCP guarantees that any data sent will be recieved on the other end. This process is named the Three-way handshake.

Some are speical messages used in Three-way handshake.
1. `SYN` : This packet is used to initiate a connection and synchronise the two devices together.
2. `SYN/ACK` : This packet is sent by the receiving device (server) to acknowledge the synchronisation attempt from the client.
3. `ACK` : The acknowledgement packet can be used by either the client or server to acknowledge that a series of messages/packets have been successfully received.
4. `DATA` : Once a connection has been established, data is sent via the "DATA" message.
5. `FIN` :  used to cleanly (properly) close the connection.
> `RST` : This packet abruptly ends all communication.

### Process
1. SYN - Client: Here's my Initial Sequence Number(ISN) to SYNchronise with (0)
2. SYN/ACK - Server: Here's my Initial Sequence Number (ISN) to SYNchronise with (5,000), and I ACKnowledge your initial number sequence (0)
3. ACK - Client: I ACKnowledge your Initial Sequence Number (ISN) of (5,000), here is some data that is my ISN+1 (0 + 1)

## TCP Closing a Connection:

TCP will close a connection once a device has determined that the other device has successfully received all of the data.To initiate the closure of a TCP connection, the device will send a `FIN` packet to the other device.with TCP, the other device will also have to acknowledge this packet.

## UDP(User Datagram Program)
- UDP is a stateless protocol that doesn't require a constant connection between the two devices for data to be sent. For example, the Three-way handshake does not occur
- UDP is used in situations where applications can tolerate data being lost (such as video streaming or voice chat) or in scenarios where an unstable connection is not the end-all.
- UDP packets are much simpler than TCP packets and have fewer headers. However, both protocols share some standard headers
  * Time to Live (TTL) :- This field sets an expiry timer for the packet, so it doesn't clog up your network.
  * Source Address:- The IP address of the device that the packet is being sent from.
  * Destination Address :- The device's IP address the packet is being sent to so that data knows where to travel next.

## Ports 101

Networking devices also use ports to enforce strict rules when communicating with one another. When a connection has been established (recalling from the OSI model's room), any data sent or received by a device will be sent through these ports. In computing, ports are a numerical value between 0 and 65535 (65,535).

> The standard rule for web data is port 80, a few other protocols have been allocated a standard rule. Any port that is within 0 and 1024 (1,024) is known as a common port.

Some ptotocols:- 

| Protocol                                   | Port Number | Description                                                                                                              |
|--------------------------------------------|-------------|--------------------------------------------------------------------------------------------------------------------------|
| File Transfer Protocol (FTP)               |     21      | Used by a file-sharing application built on a client-server model.                                                       |
| Secure Shell (SSH)                         |     22      | Used to securely login to systems via a text-based interface.                                                            |
| HyperText Transfer Protocol (HTTP)         |     80      | This protocol powers the World Wide Web (WWW)!                                                                           |
| HyperText Transfer Protocol Secure (HTTPS) |     443     | This protocol does the exact same as above; however, securely using encryption.                                          |
| Server Message Block (SMB)                 |     445     | Similar to the File Transfer Protocol (FTP); however, as well as files, SMB allows you to share devices like printers.   |
| Remote Desktop Protocol (RDP)              |     3389    | logging in to a system using a visual desktop interface                                                                  |

 [table of the 1024 common ports listed]([https://pages.github.com/](http://www.vmaxx.net/techinfo/ports.htm))
