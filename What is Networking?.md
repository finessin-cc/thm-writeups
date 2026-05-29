# TryHackMe: What is Networking?

## Room Metadata

| Field         | Value                       |
|---------------|-----------------------------|
| Platform      | TryHackMe                   |
| Type          | Networking Fundamentals     |
| Difficulty    | Beginner                    |
| Date          | July 10, 2021               |

## Task 1: What is Networking?

Networking refers to devices connected together. In computing, networks consist of devices like laptops, phones, security cameras, traffic lights, and farming equipment that communicate with each other.

**Question:** What is the key term for devices that are connected together?
- **Answer:** Network

## Task 2: What is the Internet?

The Internet is a massive network composed of many smaller networks. It originated from the ARPANET project in the late 1960s, funded by the US Defense Department. Tim Berners-Lee invented the World Wide Web in 1989, transforming the Internet into a repository for storing and sharing information.

Networks can be categorized as:
- **Private networks**: Local networks within organizations
- **Public networks**: The Internet connecting private networks

**Question:** Who invented the World Wide Web?
- **Answer:** Tim Berners-Lee

## Task 3: Identifying Devices on a Network

### IP Addresses
- Identify devices on a network using IP addresses
- IPv4 addresses consist of four octets (sections) separated by periods
- Each octet ranges from 0-255
- Private IP addresses (used internally) vs Public IP addresses (used on Internet)
- IPv4 has limited addresses (2^32 = 4.29 billion)
- IPv6 addresses support 2^128 addresses (340 trillion+) for better scalability

### MAC Addresses
- Physical network interface address assigned at manufacturing
- 12-character hexadecimal number (e.g., a4:c3:f0:85:ac:2d)
- First 6 characters identify manufacturer, last 6 are unique identifier
- Can be spoofed for security bypass attempts

**Questions:**
- What does the term "IP" stand for?
  - **Answer:** Internet Protocol
- What is each section of an IP address called?
  - **Answer:** Octet
- How many sections (in digits) does an IPv4 address have?
  - **Answer:** 4
- What does the term "MAC" stand for?
  - **Answer:** Media Access Control
- Deploy the interactive lab using the "View Site" button and spoof your MAC address to access the site. What is the flag?
  - **Answer:** `THM{YOU_GOT_ON_TRYHACKME}`

## Task 4: Ping (ICMP)

Ping is a fundamental network tool that uses ICMP (Internet Control Message Protocol) packets to test connectivity between devices.

### How Ping Works
- Uses ICMP echo packets and echo replies
- Measures round-trip time for packets
- Works with both IP addresses and website URLs
- Available on Linux and Windows operating systems

**Questions:**
- What protocol does ping use?
  - **Answer:** ICMP
- What is the syntax to ping 10.10.10.10?
  - **Answer:** `ping 10.10.10.10`
- What flag do you get when you ping 8.8.8.8?
  - **Answer:** `THM{I_PINGED_THE_SERVER}`

## Task 5: Continue Your Learning: Intro to LAN

The room recommends continuing with the "Intro to LAN" room for further networking education.

**Question:** Join the "Intro to LAN" room.
- **Answer:** No answer needed

## Summary

This room introduced fundamental networking concepts including:
- Definition of networks and the Internet
- Device identification through IP and MAC addresses
- IPv4 vs IPv6 addressing schemes
- Basic network testing with ping and ICMP
- The importance of networking in cybersecurity

The interactive labs demonstrated MAC address spoofing and basic network connectivity testing, providing hands-on experience with networking fundamentals.
