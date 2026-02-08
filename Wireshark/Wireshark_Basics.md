## What is Wireshark?
Wireshark is an open-source, cross-platform network packet analyser tool capable of sniffing and investigating live traffic and inspecting packet captures (PCAP).
- There are multiple purposes for its use:-
    - Detecting and troubleshooting network problems, such as network load failure points and congestion.
    - Detecting security anomalies, such as rogue hosts, abnormal port usage, and suspicious traffic.
    - Investigating and learning protocol details, such as response codes and payload data.

> Note: Wireshark is not an Intrusion Detection System (IDS). It only allows analysts to discover and investigate the packets in depth. It also doesn't modify packets; it reads them. Hence, detecting any anomaly or network problem highly relies on the analyst's knowledge and investigation skills.

---
## GUI and Data
Wireshark GUI opens with a single all-in-one page, which helps users investigate the traffic in multiple ways. At first glance, five sections stand out.

- **Toolbar**	The main toolbar contains multiple menus and shortcuts for packet sniffing and processing, including filtering, sorting, summarising, exporting and merging. 
- **Display Filter Bar**	The main query and filtering section.
- **Recent Files**	List of the recently investigated files. You can recall listed files with a double-click. 
- **Capture Filter and Interfaces**	Capture filters and available sniffing points (network interfaces).  The network interface is the connection point between a computer and a network. The software connection (e.g., lo, eth0 and ens33) enables networking hardware.
- **Status Bar**	Tool status, profile and numeric packet information.

<img width="1665" height="792" alt="Wireshark window" src="https://github.com/user-attachments/assets/7ba13ded-df09-4116-b3e1-5161a70898cf" />

### Loading PCAP Files
Let's load that file `http1.pcap` and see Wireshark's detailed packet presentation.

<img width="1856" height="712" alt="http1 pcap file in wireshark" src="https://github.com/user-attachments/assets/e3dacad7-dba0-475d-9250-955e3cb2fe57" />

Packet details are shown in three different panes:-
- **Packet List Pane**	Summary of each packet (source and destination addresses, protocol, and packet info). You can click on the list to choose a packet for further investigation. Once you select a packet, the details will appear in the other panels.
- **Packet Details Panel**	Detailed protocol breakdown of the selected packet.
- **Packet Bytes Pane**	Hex and decoded ASCII representation of the selected packet. It highlights the packet field depending on the clicked section in the details pane.

### Colouring Packets
Wireshark also colour packets in order of different conditions and the protocol to spot anomalies and protocols in captures quickly.This glance at packet information can help track down exactly what you're looking for during analysis.
- Wireshark has two types of packet colouring methods:
    - Temporary rules that are only available during a program session and permanent rules that are saved under the preference file (profile) and available for the next program session. 
- Use the "right-click menu" or "View --> Coloring Rules" menu to create permanent colouring rules.
- The "Colourise Packet List" menu activates/deactivates the colouring rules.
- The default permanent colouring:
  <img width="1590" height="710" alt="default color setting in wireshark" src="https://github.com/user-attachments/assets/d0d33426-8846-471d-ad3b-44f5be45a645" />

### Traffic Sniffing
You can use the blue "shark button" to start network sniffing (capturing traffic), the red button will stop the sniffing, and the green button will restart the sniffing process. The status bar will also provide the used sniffing interface and the number of collected packets.
<img width="1809" height="813" alt="packet sniffing" src="https://github.com/user-attachments/assets/31a1f883-569b-4cb4-ad8b-60a8483b4329" />

### Merge PCAP Files

Wireshark can combine two pcap files into one single file. You can use the "File --> Merge" menu path to merge a pcap with the processed one. When you choose the second file, Wireshark will show the total number of packets in the selected file. Once you click "open", it will merge the existing pcap file with the chosen one and create a new pcap file. Note that you need to save the "merged" pcap file before working on it.
![Merge to pcap](https://github.com/user-attachments/assets/8e9fbad6-8e95-4600-be52-15e512ccb373)


### View File Details
Knowing the file details is helpful. Especially when working with multiple pcap files, sometimes you will need to know and recall the file details (File hash, capture time, capture file comments, interface and statistics) to identify the file, classify and prioritise it. You can view the details by following "Statistics --> Capture File Properties" or by clicking the "pcap icon located on the left bottom".
![view deatils of capture file](https://github.com/user-attachments/assets/adddafcb-3e3f-4d48-9115-04c2b4630c95)

---
## Packet Dissection
Packet dissection is also known as protocol dissection, which investigates packet details by decoding available protocols and fields. Wireshark supports a long list of protocols for dissection, and you can also write your dissection scripts. You can find more details on dissection [here](https://github.com/boundary/wireshark/blob/master/doc/README.dissector)

### Packet Details
Click on a packet in the packet list pane to open its details (double-click will open details in a new window). Packets consist of 5 to 7 layers based on the OSI model.The picture below shows viewing packet number 27.

<img width="1953" height="1058" alt="packet details" src="https://github.com/user-attachments/assets/0b58f143-7d78-4869-a9c8-72df181d5bbe" />

- Closer view of the details pane:
  <img width="898" height="161" alt="closer view of the details pane" src="https://github.com/user-attachments/assets/ef87de02-182f-46eb-9718-bc2b4a4b8140" />

- Seven distinct layers to the packet: `frame/packet`,`source [MAC]`,`source [IP]`,`protocol`,`protocol errors`, `application protocol`, and `application data`.
- **The Frame (Layer 1)**:This will show you what frame/packet you are looking at and details specific to the Physical layer of the OSI model.
- **Source [MAC] (Layer 2)**:This will show you the source and destination MAC Addresses; from the Data Link layer of the OSI model.
- **Source [IP] (Layer 3)**:This will show you the source and destination IPv4 Addresses; from the Network layer of the OSI model.
- **Protocol (Layer 4)**:This will show you details of the protocol used (UDP/TCP) and source and destination ports; from the Transport layer of the OSI model.
- **Protocol Errors**:This continuation of the 4th layer shows specific segments from TCP that needed to be reassembled.
- **Application Protocol (Layer 5)**:This will show details specific to the protocol used, such as HTTP, FTP,  and SMB. From the Application layer of the OSI model.
- **Application Data**: This extension of the 5th layer can show the application-specific data.
   
