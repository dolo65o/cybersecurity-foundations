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
