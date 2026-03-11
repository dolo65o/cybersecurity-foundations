## What is a Network?

A network is a collection of connected items. 
A friendship circle, for example, brings people together because they share common interests, hobbies, or abilities.

Networks exist in many spheres of life.
* A city's public transit system
* Infrastructure like the national power grid for electricity.
  
But, more specifically, in computing, networking is the same concept, albeit dispersed among various gadgets.
In computing, a network might consist of two or billions of units. 
These devices range from your laptop and phone to security cameras, traffic lights, and even farming!


## What is the Internet?

The Internet is a single, massive network made up of numerous smaller networks.
In the late 1960s, the ARPANET project included the original version of the Internet.But it wasn't until 1989 that Tim Berners-Lee invented the World Wide Web (WWW), which gave rise to the Internet as we know it today. It wasn't until this time that the Internet began to function as a storehouse for information sharing and storage, as it does now.

<img width="852" height="579" alt="internet2" src="https://github.com/user-attachments/assets/074b8066-5435-4aba-80d2-dd8675c03b98" />

Numerous tiny networks connected to one another make up the Internet.  These tiny networks are known as private networks, and the networks that link them are known as public networks, or the Internet!


## IP Address (IPv4 Basics)

An IP address (Internet Protocol address) is used to identify a device on a network.
Depending on the network setup, an IP address can be static (fixed) or dynamic (changes over time).
<img width="1140" height="487" alt="ip address" src="https://github.com/user-attachments/assets/a58db696-a015-4103-bd9c-49b012cc297c" />

The value of each octet will summarise to be the IP address of the device on the network. This number is calculated through a technique known as IP addressing & subnetting.
IP Addresses follow a set of standards known as protocols. These protocols are the backbone of networking and force many devices to communicate in the same language.


## MAC Address

Devices on a network will all have a physical network interface, which is a microchip board found on the device's motherboard. This network interface is assigned a unique address at the factory it was built at, called a MAC (Media Access Control ) address. The MAC address is a twelve-character hexadecimal number (a base sixteen numbering system used in computing to represent numbers) split into two's and separated by a colon. These colons are considered separators. For example, a4:c3:f0:85:ac:2d. The first six characters represent the company that made the network interface, and the last six is a unique number.

<img width="1140" height="669" alt="mac address" src="https://github.com/user-attachments/assets/0749076f-352b-4c2c-8b64-da30dd5242a8" />

However, an interesting thing with MAC addresses is that they can be faked or "spoofed" in a process known as spoofing. This spoofing occurs when a networked device pretends to identify as another using its MAC address.


## Internet Control Message Protocol (ICMP)

- Mainly used for network diagnostics and error reporting. Two popular commands rely on ICMP, and they are instrumental in network troubleshooting and network security. 
    - `Ping` This command uses ICMP to test connectivity to a target system and measures the round-trip time (RTT). In other words, it can be used to learn that the target is alive and that its reply can reach our system.
        - The `ping` command sends an ICMP Echo Request (ICMP Type 8).
        - The computer on the receiving end responds with an ICMP Echo Reply (ICMP Type 0).
    - `traceroute`  It uses ICMP to discover the route from your host to the target.The Internet protocol has a field called Time-to-Live (TTL) that indicates the maximum number of routers a packet can travel through before it is dropped. The router decrements the packet’s TTL by one before it sends it across. When the TTL reaches zero, the router drops the packet and sends an ICMP Time Exceeded message (ICMP Type 11). (In this context, “time” is measured in the number of routers, not seconds.)

