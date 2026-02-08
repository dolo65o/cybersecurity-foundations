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
