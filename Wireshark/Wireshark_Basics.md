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
   
---
## Packet Navigation
Wireshark calculates the number of investigated packets and assigns a unique number for each packet. This helps the analysis process for big captures and makes it easy to go back to a specific point of an event,This known as Packet Numbers.

<img width="1002" height="817" alt="image" src="https://github.com/user-attachments/assets/4a09956c-78b4-483f-a0f0-bdb080f3e88e" />

### Go to Packet
This feature not only navigates between packets up and down; it also provides in-frame packet tracking and finds the next packet in the particular part of the conversation.The "Go" menu and toolbar to view specific packets.

![Go to packet](https://github.com/user-attachments/assets/66c3ce25-919e-41a5-aaec-239f4cc03a2e)

### Find Packets
The "Edit --> Find Packet" menu to make a search inside the packets for a particular event of interest. This helps analysts and administrators to find specific intrusion patterns or failure traces.
- There are two crucial points in finding packets:
    - The first is knowing the input type. This functionality accepts four types of inputs (Display filter, Hex, String and Regex). String and regex searches are the most commonly used search types.
    - The second point is choosing the search field. You can conduct searches in the three panes (packet list, packet details, and packet bytes), and it is important to know the available information in each pane to find the event of interest.
      
  ![find packets](https://github.com/user-attachments/assets/53f15548-f255-43be-9ca2-1722d6e84caf)

### Mark Packets
The "Edit" or the "right-click" menu to mark/unmark packets.Marked packets will be shown in black regardless of the original colour representing the connection type.

![Mark packets](https://github.com/user-attachments/assets/fccdb02a-6337-4fe7-922c-20c7ffa9b448)

> Note that marked packet information is renewed every file session, so marked packets will be lost after closing the capture file.

### Packet Comments
Add comments for particular packets that will help the further investigation or remind and point out important/suspicious points for other layer analysts. Unlike packet marking, the comments can stay within the capture file until the operator removes them.

![Packet comment](https://github.com/user-attachments/assets/5aa26787-a8f3-49d6-906c-310ca2799e59)

### Export Packets
This functionality helps analysts share the only suspicious packages (decided scope). Thus redundant information is not included in the analysis process.The "File" menu to export packets.

![export packets](https://github.com/user-attachments/assets/bfd5493a-e02c-4855-bc6d-4aaf44118391)

### Export Objects (Files)
Exporting objects are available only for selected protocol's streams (DICOM, HTTP, IMF, SMB and TFTP).

![exports objects](https://github.com/user-attachments/assets/3041422e-9bfd-4235-a8b0-66ba348df5b2)

### Time Display Format 
Wireshark lists the packets as they are captured, so investigating the default flow is not always the best option. By default, Wireshark shows the time in "Seconds Since Beginning of Capture", the common usage is using the UTC Time Display Format for a better view.The "View --> Time Display Format" menu to change the time display format.

![Time display format](https://github.com/user-attachments/assets/f4212181-e356-4184-9900-f733a44f3ef4)

---
## Packet Filtering
* Wireshark has a powerful filter engine that helps analysts to narrow down the traffic and focus on the event of interest. Wireshark has two types of filtering approaches:
  - Capture filters are used for "capturing" only the packets valid for the used filter.
  - Display filters are used for "viewing" the packets valid for the used filter.
* There are two different ways to filter traffic and remove the noise from the capture file:
    - The first one uses queries, and the second uses the right-click menu.
*  Wireshark provides a powerful GUI, and there is a golden rule for analysts who don't want to write queries for basic tasks: ***If you can click on it, you can filter and copy it***.

### Apply as Filter
Click on the field you want to filter and use the "right-click menu" or "Analyse --> Apply as Filter" menu to filter the specific value.This option is a good way of investigating a particular value in packets. 

![Apply as filter](https://github.com/user-attachments/assets/99f108a4-cc30-47a4-a770-6803a7989a7f)

>  Note that the number of total and displayed packets are always shown on the status bar.

### Conversation Filter
To investigate a specific packet number and all linked packets by focusing on IP addresses and port numbers. In that case, the "Conversation Filter" option helps you view only the related packets and hide the rest of the packets easily.The"right-click menu" or "Analyse --> Conversation Filter" menu to filter conversations.

![conversation filter](https://github.com/user-attachments/assets/f40da541-83bc-40fd-be0e-1855775f469e)

### Colourise Conversation
It highlights the linked packets without applying a display filter and decreasing the number of viewed packets. This option works with the "Colouring Rules" option ad changes the packet colours without considering the previously applied colour rule. You can use the "right-click menu" or "View --> Colourise Conversation" menu to colourise a linked packet in a single click.

![Colour conversation](https://github.com/user-attachments/assets/a951ece8-45cd-49cc-ae12-d62aea0f3996)

> Note that you can use the "View --> Colourise Conversation --> Reset Colourisation" menu to undo this operation.

### Prepare as Filter
It adds the required query to the pane and waits for the execution command (enter) or another chosen filtering option by using the ".. and/or.." from the "right-click menu".

![Prepare as filter](https://github.com/user-attachments/assets/ccaf65d4-15e8-4ec8-a284-f28b8e5d4fe2)

### Apply as Column
By default, the packet list pane provides basic information about each packet.The "right-click menu" or "Analyse --> Apply as Column" menu to add columns to the packet list pane.This function helps analysts examine the appearance of a specific value/field across the available packets in the capture file.

![apply as column](https://github.com/user-attachments/assets/be861e5c-a04d-4547-9189-7189aa44de4a)


> You can enable/disable the columns shown in the packet list pane by clicking on the top of the packet list pane.

### Follow Stream

Wireshark displays everything in packet portion size. However, it is possible to reconstruct the streams and view the raw traffic as it is presented at the application level.the protocol, streams help analysts recreate the application-level data and understand the event of interest. It is also possible to view the unencrypted protocol data like usernames, passwords and other transferred data.the"right-click menu" or "Analyse --> Follow TCP/UDP/HTTP Stream" menu to follow traffic streams. Streams are shown in a separate dialogue box; packets originating from the server are highlighted with blue, and those originating from the client are highlighted with red.

![Follow stream](https://github.com/user-attachments/assets/cf475470-b449-4568-8998-d76da23504ac)

### Simple Display Filter Queries
The easiest way to filter quickly the huge amount of packets, is by applying a display filter using the "Apply a display filter" bar .There are many filter queries available and each of them can be extensively tweaked to show very specific results.

<img width="1665" height="530" alt="simple display filter" src="https://github.com/user-attachments/assets/0b489b80-13b0-4ef5-a101-679d125c8c7f" />

#### Filter By Protocol Name or Port
There are two basic ways to filter based on a specific protocol: by protocol name and by protocol port number.
- To filter by protocol name, simply type in the protocol name and hit enter or click on the arrow button at the right hand side of the display filter bar.

![Filter By HTTP ](https://github.com/user-attachments/assets/af76950a-0840-4522-96fa-6466272d5dff)

  
> similarly filter for other protocols using keywords like arp, dhcp, ftp, smtp, pop, imap, and more.

To filter by protocol port number, you can use the structure `tcp.port == <port number>` or `udp.port == <port number>`. For example, if you want to see only http packets, you would use the filter `tcp.port == 80` and then hit enter. 

![filter by tcp post](https://github.com/user-attachments/assets/cb353a54-8bfb-4aa8-8500-3b9d66e69b64)

#### Filter By IP
To filter for a specific IP, you can use the structure `ip.addr == <IP address>`. So if you need to search for the IP `192.168.1.2`, your filter would be `ip.addr == 192.168.1.2`. 

![Filter by ip](https://github.com/user-attachments/assets/7dffda56-0ca2-445b-8003-77ac2c7b9c35)
