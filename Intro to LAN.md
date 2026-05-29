# TryHackMe: Intro to LAN

| Field | Details |
|---|---|
| **Platform** | TryHackMe |
| **Room** | Intro to LAN |
| **Difficulty** | Easy |
| **Estimated Time** | 15 minutes |
| **Category** | Fundamentals / Networking / LAN |

---

## Table of Contents

1. [LAN Topologies](#task-1-introducing-lan-topologies)
2. [Subnetting](#task-2-a-primer-on-subnetting)
3. [ARP](#task-3-arp)
4. [DHCP](#task-4-dhcp)

---

## Task 1: Introducing LAN Topologies

A **network topology** refers to the physical or logical design/layout of a network — how devices are interconnected and how data flows between them.

### Star Topology

All devices connect individually to a **central networking device** (switch or hub).

```
      [Device A]
          |
[Device B]--[Switch/Hub]--[Device C]
          |
      [Device D]
```

| Attribute | Detail |
|---|---|
| **Cost** | High — requires dedicated hardware and extensive cabling |
| **Scalability** | Excellent — easy to add new devices |
| **Reliability** | Good — single device failure doesn't bring down the network |
| **Single Point of Failure** | Yes — central device failure disables all connected nodes |
| **Maintenance** | Increases with scale; troubleshooting can be complex |

---

### Bus Topology

All devices connect along a single **backbone cable**. Data travels along the shared medium to reach its destination.

```
[Device A]--[Device B]--[Device C]--[Device D]
|_____________Backbone Cable_________________|
```

| Attribute | Detail |
|---|---|
| **Cost** | Low — minimal cabling and no dedicated switching hardware |
| **Scalability** | Poor — performance degrades rapidly as devices are added |
| **Bottleneck** | High risk — all traffic shares a single cable |
| **Troubleshooting** | Difficult — all data travels the same route |
| **Redundancy** | None — a single cable break disables the entire network |

---

### Ring Topology

Also known as **token topology**. Devices are connected in a closed loop, forwarding data around the ring until it reaches the destination.

```
[Device A] → [Device B] → [Device C]
     ↑                          ↓
[Device D] ← ─────────────────←
```

| Attribute | Detail |
|---|---|
| **Cost** | Low — minimal cabling, less hardware dependency |
| **Data Direction** | Unidirectional — travels one way around the loop |
| **Troubleshooting** | Easier than bus due to single data direction |
| **Efficiency** | Low — data may traverse many devices before reaching destination |
| **Bottleneck** | Low risk |
| **Single Point of Failure** | Yes — a broken cable or failed device breaks the entire loop |

---

### Topology Comparison Table

| Feature | Star | Bus | Ring |
|---|---|---|---|
| **Setup Cost** | High | Low | Low |
| **Scalability** | High | Low | Medium |
| **Fault Tolerance** | Medium | Low | Low |
| **Troubleshooting** | Medium | Hard | Easy |
| **Bottleneck Risk** | Low | High | Low |
| **Single Point of Failure** | Central device | Backbone cable | Any node/cable |

---

### Switches vs. Hubs/Repeaters

| Device | Behaviour |
|---|---|
| **Hub / Repeater** | Broadcasts every received packet to **all** ports — inefficient, generates excessive traffic |
| **Switch** | Maintains a **MAC address table** per port; sends packets only to the **intended destination port** |

Switches are standard in modern networks (businesses, schools, enterprises). They support 4, 8, 16, 24, 32, or 64 port configurations.

### Routers

A **router** connects separate networks and passes data between them via **routing** — the process of determining the optimal path for data to travel across networks.

- Routers and switches can be interconnected to create **redundant paths**
- If one path fails, data can take an alternate route — eliminating downtime at the cost of slightly increased latency

### Task Answers

| Question | Answer |
|---|---|
| What does LAN stand for? | `Local Area Network` |
| What is the verb given to the job Routers perform? | `Routing` |
| What device centrally connects multiple devices and transmits data to the correct location? | `Switch` |
| What topology is cost-efficient to set up? | `Bus Topology` |
| What topology is expensive to set up and maintain? | `Star Topology` |
| Flag from the interactive lab? | `THM{REDACTED}` |

---

## Task 2: A Primer on Subnetting

**Subnetting** is the process of dividing a larger network into smaller, logical sub-networks. This allows network administrators to segment traffic, improve security, and allocate IP space efficiently.

### Subnet Mask

A subnet mask is a **32-bit (4-octet)** number used to define the boundary between the network portion and host portion of an IP address. Each octet ranges from `0` to `255`.

**Example:**

```
IP Address:    192.168.1.100
Subnet Mask:   255.255.255.0
```

### Subnet Address Types

| Type | Purpose | Example |
|---|---|---|
| **Network Address** | Identifies the start of the network — not assignable to a host | `192.168.1.0` |
| **Host Address** | Assigned to individual devices on the subnet | `192.168.1.100` |
| **Default Gateway** | Special host address; forwards traffic destined for other networks. Typically `.1` or `.254` | `192.168.1.254` |

### Practical Example

A device at `192.168.1.100` with subnet mask `255.255.255.0`:

```
Network:         192.168.1.0
Usable Hosts:    192.168.1.1  –  192.168.1.253
Default Gateway: 192.168.1.254
Broadcast:       192.168.1.255
```

### Benefits of Subnetting

| Benefit | Description |
|---|---|
| **Efficiency** | Reduces unnecessary broadcast traffic within large networks |
| **Security** | Isolates sensitive network segments (e.g., staff vs. public Wi-Fi in a café) |
| **Control** | Granular management of which devices can communicate with which |

### Real-World Use Case — Café Network

```
Network
├── Staff Subnet    → Cash registers, POS systems, internal devices
└── Public Subnet   → Customer hotspot, internet-only access
```

Both subnets share upstream internet connectivity but are isolated from each other.

### Task Answers

| Question | Answer |
|---|---|
| Technical term for dividing a network into smaller pieces? | `Subnetting` |
| How many bits are in a subnet mask? | `32` |
| Range of a subnet mask octet? | `0-255` |
| Address used to identify the start of a network? | `Network Address` |
| Address used to identify devices within a network? | `Host Address` |
| Device responsible for sending data to another network? | `Default Gateway` |

---

## Task 3: ARP

### What is ARP?

**ARP (Address Resolution Protocol)** is a Layer 2 protocol responsible for mapping **IP addresses** (logical identifiers) to **MAC addresses** (physical identifiers) on a local network.

Every device on a network maintains an **ARP cache** — a local table storing known IP-to-MAC address mappings.

### How ARP Works

ARP uses two message types to resolve addresses:

| Message Type | Direction | Purpose |
|---|---|---|
| **ARP Request** | Broadcast → all devices | "Who has IP `x.x.x.x`? Tell me your MAC address." |
| **ARP Reply** | Unicast → requesting device | "I have that IP. My MAC address is `XX:XX:XX:XX:XX:XX`." |

### ARP Resolution Process

```
Device A wants to communicate with 192.168.1.50

1. Device A checks its ARP cache → no entry found
2. Device A broadcasts ARP Request:
   "Who has 192.168.1.50? Tell 192.168.1.10"

3. All devices receive the broadcast
4. Device at 192.168.1.50 sends ARP Reply (unicast):
   "192.168.1.50 is at AA:BB:CC:DD:EE:FF"

5. Device A stores the mapping in its ARP cache:
   192.168.1.50  →  AA:BB:CC:DD:EE:FF

6. Communication proceeds using the resolved MAC address
```

### ARP Cache

- Stored locally on each device
- Reduces repeated ARP broadcasts for known hosts
- Entries expire after a timeout period

> **Security Note:** ARP has no authentication mechanism, making it vulnerable to **ARP Spoofing / ARP Poisoning** attacks, where a malicious device sends fake ARP replies to associate its MAC address with a legitimate IP — enabling man-in-the-middle attacks.

### Task Answers

| Question | Answer |
|---|---|
| What does ARP stand for? | `Address Resolution Protocol` |
| What ARP packet type asks a device if it has a specific IP? | `Request` |
| What address is used as a physical identifier for a device? | `MAC Address` |
| What address is used as a logical identifier for a device? | `IP Address` |

---

## Task 4: DHCP

### What is DHCP?

**DHCP (Dynamic Host Configuration Protocol)** automates the assignment of IP addresses to devices joining a network, eliminating the need for manual (static) configuration.

IP addresses can be assigned in two ways:

| Method | Description |
|---|---|
| **Static** | Manually configured on the device — used for servers, printers, gateways |
| **Dynamic (DHCP)** | Automatically assigned by a DHCP server — standard for end-user devices |

### DHCP 4-Way Handshake (DORA)

```
Client                              DHCP Server
  |                                      |
  |──[1. DHCP Discover]─────────────────►|   Broadcast: "Is there a DHCP server?"
  |                                      |
  |◄─[2. DHCP Offer]────────────────────|   "You can use IP 192.168.1.100"
  |                                      |
  |──[3. DHCP Request]──────────────────►|   "I'll take that IP address"
  |                                      |
  |◄─[4. DHCP ACK]─────────────────────|   "Confirmed. IP is yours."
  |                                      |
```

### DHCP Packet Types

| Packet | Sender | Description |
|---|---|---|
| **DHCP Discover** | Client | Broadcast sent to locate available DHCP servers on the network |
| **DHCP Offer** | Server | Server proposes an available IP address to the client |
| **DHCP Request** | Client | Client formally requests the offered IP address |
| **DHCP ACK** | Server | Server confirms the assignment; client begins using the IP |

### Task Answers

| Question | Answer |
|---|---|
| DHCP packet used by a device to retrieve an IP address? | `DHCP Discover` |
| Packet a device sends once it has been offered an IP? | `DHCP Request` |
| Last DHCP packet sent from server to device? | `DHCP ACK` |

---

## Summary of Key Concepts

| Concept | Key Takeaway |
|---|---|
| **Star Topology** | Centralised switch; scalable but expensive; central device is a single point of failure |
| **Bus Topology** | Single backbone cable; cheap to deploy; prone to bottleneck and total failure on cable break |
| **Ring Topology** | Devices form a loop; easy to troubleshoot; entire network fails if loop breaks |
| **Switch** | Directs traffic to specific ports via MAC table; more efficient than a hub |
| **Router** | Connects separate networks; routes traffic between them |
| **Subnetting** | Divides networks into segments; improves efficiency, security, and control |
| **Subnet Mask** | 32-bit value defining network vs. host boundaries in an IP address |
| **Default Gateway** | Device (usually a router) that forwards traffic to external networks |
| **ARP** | Resolves IP addresses to MAC addresses via broadcast request / unicast reply |
| **ARP Cache** | Local store of IP-to-MAC mappings to reduce repeated broadcasts |
| **DHCP** | Automates IP assignment via Discover → Offer → Request → ACK (DORA) |
ENDOFFILE
