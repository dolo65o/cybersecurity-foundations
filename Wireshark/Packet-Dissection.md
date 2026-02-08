## Packet Dissection
Packet dissection is also known as protocol dissection, which investigates packet details by decoding available protocols and fields. Wireshark supports a long list of protocols for dissection, and you can also write your dissection scripts. You can find more details on dissection [here](https://github.com/boundary/wireshark/blob/master/doc/README.dissector)

### Packet Details
Click on a packet in the packet list pane to open its details (double-click will open details in a new window). Packets consist of 5 to 7 layers based on the OSI model.The picture below shows viewing packet number 27.

<img width="1953" height="1058" alt="packet details" src="https://github.com/user-attachments/assets/0b58f143-7d78-4869-a9c8-72df181d5bbe" />

- Closer view of the details pane:
  <img width="898" height="161" alt="closer view of the details pane" src="https://github.com/user-attachments/assets/ef87de02-182f-46eb-9718-bc2b4a4b8140" />

- Seven distinct layers to the packet: `frame/packet`,`source [MAC]`,`source [IP]`,`protocol`,`protocol errors`, `application protocol`, and `application data`.
  - **The Frame (Layer 1)**:This will show you what frame/packet you are looking at and details specific to the Physical layer of the OSI model.

    <img width="827" height="418" alt="The Frame (Layer 1)" src="https://github.com/user-attachments/assets/c814aece-ee7d-4e4e-8c5e-20d7cd30fde0" />


  - **Source [MAC] (Layer 2)**:This will show you the source and destination MAC Addresses; from the Data Link layer of the OSI model.
  - 
    <img width="1134" height="112" alt="Source  MAC  (Layer 2)" src="https://github.com/user-attachments/assets/71117360-e817-40bd-a317-37ed98f5d0d9" />

  - **Source [IP] (Layer 3)**:This will show you the source and destination IPv4 Addresses; from the Network layer of the OSI model.

    <img width="829" height="331" alt="Source  IP  (Layer 3)" src="https://github.com/user-attachments/assets/f78150f8-289e-49e7-95f9-b3a675b7958a" />

  - **Protocol (Layer 4)**:This will show you details of the protocol used (UDP/TCP) and source and destination ports; from the Transport layer of the OSI model.

    <img width="1054" height="532" alt="Protocol (Layer 4)" src="https://github.com/user-attachments/assets/ee5fd278-0607-46f9-87e1-1193a414ff5a" />

  - **Application Protocol (Layer 5)**:This will show details specific to the protocol used, such as HTTP, FTP,  and SMB. From the Application layer of the OSI model.

    <img width="1261" height="352" alt="Application Protocol (Layer 5)" src="https://github.com/user-attachments/assets/f70cb5af-61c4-4b37-8771-5ffea9cdd148" />

  - **Application Data**: This extension of the 5th layer can show the application-specific data.
 
    <img width="1159" height="102" alt="Application Data" src="https://github.com/user-attachments/assets/ce6932f3-ecbd-48b5-bb35-dc5dfba091e8" />
  
> **Protocol Errors**:This continuation of the 4th layer shows specific segments from TCP that needed to be reassembled.
