# TryHackMe: Wireshark: The Basics

## Room Metadata
| Platform | Type | Difficulty | Date |
|----------|------|------------|------|
| TryHackMe | Network | Easy | 2023-10-01 |

## Task 1: Introduction
No answer needed

## Task 2: Tool Overview
### Questions
- **Use the "Exercise.pcapng" file to answer the questions.**
- **Read the "capture file comments". What is the flag?**
  - **Answer**: TryHackMe_Wireshark_Demo
- **What is the total number of packets?**
  - **Answer**: 58620
- **What is the SHA256 hash value of the capture file?**
  - **Answer**: f446de335565fb0b0ee5e5a3266703c778b2f3dfad7efeaeccb2da5641a6d6eb

## Task 3: Packet Dissection
### Questions
- **Use the "Exercise.pcapng" file to answer the questions.**
- **View packet number 38. Which markup language is used under the HTTP protocol?**
  - **Answer**: eXtensible Markup Language (XML)
- **What is the arrival date of the packet? (Answer format: Month/Day/Year)**
  - **Answer**: 05/13/2004
- **What is the TTL value?**
  - **Answer**: 47
- **What is the TCP payload size?**
  - **Answer**: 424
- **What is the e-tag value?**
  - **Answer**: 9a01a-4696-7e354b00

## Task 4: Packet Navigation
### Questions
- **Use the "Exercise.pcapng" file to answer the questions.**
- **Search the "r4w" string in packet details. What is the name of artist 1?**
  - **Answer**: r4w8173
- **Go to packet 12 and read the packet comments. What is the answer?**
  - **Answer**: Use `md5sum <filename>` terminal command to get MD5 hash
- **There is a ".txt" file inside the capture file. Find the file and read it; what is the alien's name?**
  - **Answer**: PACKETMASTER
- **Look at the expert info section. What is the number of warnings?**
  - **Answer**: 1636

## Task 5: Packet Filtering
### Questions
- **Use the "Exercise.pcapng" file to answer the questions.**
- **Go to packet number 4. Right-click on the "Hypertext Transfer Protocol" and apply it as a filter.**
  - **Answer**: The filter query is `http`
- **Now, look at the filter pane. What is the number of displayed packets?**
  - **Answer**: 1089
- **Go to packet number 33790, follow the HTTP stream, and look carefully at the responses.**
  - **Answer**: The total number of artists is 3.
- **What is the name of the second artist?**
  - **Answer**: Blad3

## Task 6: Packet Dissection Details
### Packet Details
- **Frame (Layer 1)**: Shows the frame/packet details and physical layer information.
- **Source [MAC] (Layer 2)**: Shows the source and destination MAC addresses.
- **Source [IP] (Layer 3)**: Shows the source and destination IPv4 addresses.
- **Protocol (Layer 4)**: Shows the protocol used (UDP/TCP) and source and destination ports.
- **Protocol Errors**: Shows specific segments from TCP that needed to be reassembled.
- **Application Protocol (Layer 5)**: Shows details specific to the protocol used, such as HTTP, FTP, and SMB.
- **Application Data**: Shows the application-specific data.

## Task 7: Packet Navigation
### Packet Navigation
- **Packet Numbers**: Wireshark assigns a unique number to each packet for easy reference.
- **Go to Packet**: Allows navigation between packets and in-frame packet tracking.
- **Find Packets**: Allows searching for specific packets by content.
- **Mark Packets**: Helps analysts point to specific packets for further investigation.
- **Packet Comments**: Allows adding comments to specific packets for further investigation.
- **Export Packets**: Allows exporting specific packets for further analysis.
- **Export Objects (Files)**: Allows extracting files transferred through the wire.
- **Time Display Format**: Allows changing the time display format for better visibility.

## Task 8: Packet Filtering
### Packet Filtering
- **Display Filters**: Used for viewing packets valid for the used filter.
- **Capture Filters**: Used for capturing only the packets valid for the used filter.
- **Apply as Filter**: Filters traffic based on specific values.
- **Conversation Filter**: Filters packets based on IP addresses and port numbers.
- **Colourise Conversation**: Highlights linked packets without applying a display filter.
- **Prepare as Filter**: Adds the required query to the pane for execution.
- **Apply as Column**: Adds columns to the packet list pane for specific values.
- **Follow Stream**: Reconstructs streams to view raw traffic at the application level.

## Task 9: Simple Display Filter Queries
### Simple Display Filter Queries
- **Filter By Protocol Name or Port**: Filters based on protocol name or port number.
- **Filter By IP**: Filters for a specific IP address.
- **Filter By HTTP**: Filters for HTTP traffic using `http` as the filter query.
- **Filter By TCP Port**: Filters for TCP port traffic using `tcp.port == <port number>`.

## Task 10: Summary
- **Summary**: Wireshark is a powerful tool for packet analysis, providing detailed insights into network traffic and helping in troubleshooting and security analysis.
- **Recommendations**: Use Wireshark to dissect packets, navigate through captures, and apply filters to focus on specific events.

## Task 11: Flag
- **Flag**: THM{TryHackMe_Wireshark_Demo}
