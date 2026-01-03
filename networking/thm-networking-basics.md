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
The value of each octet will summarise to be the IP address of the device on the network. This number is calculated through a technique known as IP addressing & subnetting
IP Addresses follow a set of standards known as protocols. These protocols are the backbone of networking and force many devices to communicate in the same language.


## MAC Address

Devices on a network will all have a physical network interface, which is a microchip board found on the device's motherboard. This network interface is assigned a unique address at the factory it was built at, called a MAC (Media Access Control ) address. The MAC address is a twelve-character hexadecimal number (a base sixteen numbering system used in computing to represent numbers) split into two's and separated by a colon. These colons are considered separators. For example, a4:c3:f0:85:ac:2d. The first six characters represent the company that made the network interface, and the last six is a unique number.

<img width="1140" height="669" alt="mac address" src="https://github.com/user-attachments/assets/0749076f-352b-4c2c-8b64-da30dd5242a8" />
However, an interesting thing with MAC addresses is that they can be faked or "spoofed" in a process known as spoofing. This spoofing occurs when a networked device pretends to identify as another using its MAC address.


## Ping & ICMP

Ping is one of the most fundamental network tools available to us. Ping uses ICMP (Internet Control Message Protocol) packets to determine the performance of a connection between devices, for example, if the connection exists or is reliable.
The time taken for ICMP packets travelling between devices is measured by ping.This measuring is done using ICMP's echo packet and then ICMP's echo reply from the target device.

What I learned from this room:
I understood how devices communicate on a network using IP and MAC addresses, and how tools like ping help verify connectivity using ICMP.
