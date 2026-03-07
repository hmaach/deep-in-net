# Deep in Net

# Exercice 01

## Overview

This exercise demonstrates basic Ethernet cabling concepts and IP communication between devices using RJ-45 cables in Packet Tracer.

---

## What is an RJ-45 Cable?

An RJ-45 cable is an Ethernet cable used to connect network devices in a Local Area Network (LAN).
It uses an 8-pin connector and twisted-pair wiring to transmit data based on Ethernet standards.

RJ-45 cables are commonly used to connect:

- Computers
- Switches
- Routers
- Network devices

---

## Straight-Through RJ-45 Cable

A straight-through cable uses the **same wiring standard on both ends** (T568A–T568A or T568B–T568B).

### Usage

It is used to connect **different types of devices**, such as:

- PC to Switch
- PC to Router
- Switch to Router

---

## Crossover RJ-45 Cable

A crossover cable uses **different wiring standards on each end** (T568A on one end and T568B on the other).

### Usage

It is used to connect **similar devices directly**, such as:

- PC to PC
- Switch to Switch
- Router to Router

---

## How to Calculate Available Subnets

### Step 1: Identify the Subnet Mask

The subnet mask (CIDR notation) defines how many bits are used for the network portion of the IP address.

Examples:

- `/24` → 255.255.255.0
- `/29` → 255.255.255.248

---

### Step 2: Calculate the Block Size

The block size determines how many IP addresses each subnet contains.

Formula:

```
Block Size = 256 − last octet of subnet mask
```

Examples:

- `/24` → 256 − 0 = 256 addresses
- `/29` → 256 − 248 = 8 addresses

---

### Step 3: Identify Subnet Ranges

Subnets increase by the block size in the last octet.

Example for `/29`:

```
192.168.13.0
192.168.13.8
192.168.13.16
192.168.13.24
...
192.168.13.248
```

Each of these is a separate subnet.

---

### Step 4: Determine Usable Host Addresses

In each subnet:

- First address → Network address (not usable)
- Last address → Broadcast address (not usable)
- All addresses in between → Usable host IPs

Example:

```
192.168.13.248/29
Network:   192.168.13.248
Usable:    192.168.13.249 – 192.168.13.254
Broadcast: 192.168.13.255
```

---

## Application in This Exercise

- Each PC pair is connected using a **crossover RJ-45 cable**.
- PCs communicate only if they are in the **same subnet**.
- Subnet calculation ensures correct IP address assignment.
- No default gateway is required because communication occurs within the same network.

---

## Key Concept

The subnet mask defines the network boundaries.
Devices with the same subnet mask are not necessarily in the same network unless their IP addresses fall within the same subnet range.



# Exercice 02

## Objective

This exercise demonstrates how a **switch** and a **hub** operate in a network, how computers communicate when connected to each device, and how traffic behavior differs under simultaneous transmissions.

---

## Topology Description

* One group of PCs is connected to a **Switch**
* One group of PCs is connected to a **Hub**
* Each group uses its own IP subnet
* No router is used

---

## IP Addressing

### Switch Network

* Subnet: `192.168.1.0/29`
* Subnet mask: `255.255.255.248`
* All PCs connected to the switch are assigned IPs within this range
* All switch-connected PCs can communicate successfully at the same time

### Hub Network

* Subnet: `192.168.1.192/27`
* Subnet mask: `255.255.255.224`
* All PCs connected to the hub are assigned IPs within this range
* PCs can communicate one at a time, but simultaneous transmissions fail due to collisions

---

## Device Operation

### Switch

* Operates at **OSI Layer 2 (Data Link)**
* Uses MAC addresses to forward frames
* Each port is a separate collision domain
* Supports full-duplex communication
* Allows multiple simultaneous transmissions without collisions

### Hub

* Operates at **OSI Layer 1 (Physical)**
* Does not analyze MAC or IP addresses
* Broadcasts incoming signals to all ports
* All devices share a single collision domain
* Operates in half-duplex mode, causing collisions during simultaneous transmissions

---

## Observations

* Communication between PCs connected to the switch is always successful
* Communication between PCs connected to the hub succeeds only when one device transmits at a time
* Simultaneous transmissions on the hub result in collisions and failed communication

---

## Conclusion

This exercise shows that switches are more efficient and reliable than hubs. By separating collision domains and operating at Layer 2, switches allow concurrent communication, while hubs suffer from collisions due to shared bandwidth and Layer 1 operation.


# Exercise 03

## Overview

This project demonstrates the design and configuration of a small local network using **Cisco Packet Tracer**, focusing on core network services: **DHCP, DNS, HTTPS, and FTP**.

---

## Network Topology

* One local network: `192.168.1.0/24`
* One switch
* Multiple servers, each dedicated to a single service
* Client PCs connected to the same LAN

---

## IP Addressing Plan

### Servers (Static IP Addresses)

| Server       | Service         | IP Address      |
| ------------ | --------------- | --------------- |
| HTTPS Server | Secure Web      | `192.168.1.99`  |
| FTP Server   | File Transfer   | `192.168.1.100` |
| DNS Server   | Name Resolution | `192.168.1.101` |
| DHCP Server  | IP Assignment   | `192.168.1.102` |

Subnet Mask: `255.255.255.0`

---

## DHCP Configuration

The DHCP server is responsible for assigning IP configuration to all PCs.

### DHCP Pool Settings

* Network: `192.168.1.0/24`
* Start IP: `192.168.1.10`
* Maximum users: 50
* DNS Server: `192.168.1.101`

Only the **DHCP service** is enabled on this server. All other services are disabled.

Client PCs are configured to obtain their IP settings automatically using DHCP.

---

## DNS Configuration

The DNS server resolves domain names to IP addresses.

### DNS Records

**A Record**

* `deep-in-net.local` → `192.168.1.99`

**CNAME Record**

* `deep-in-net.com` → `deep-in-net.local`

This configuration allows both domain names to resolve to the HTTPS server.

---

## HTTPS Server Configuration

The HTTPS server provides secure web access.

* HTTP service: **Disabled**
* HTTPS service: **Enabled**

### Web Page

The HTTPS server displays a simple page containing a hello message.

Access method:

```
https://192.168.1.99
https://deep-in-net.com
```

---

## FTP Server Configuration

The FTP server is dedicated to file transfer services.

* FTP service: **Enabled**
* All other services: **Disabled**

### User Account

| Username  | Permissions |
| --------- | ----------- |
| deepinnet | R W D N L   |

Permissions:

* Read
* Write
* Delete
* Rename
* List

Clients can authenticate and transfer files using standard FTP commands.

---

## Validation & Testing

### DNS Resolution

From a client PC:

```
ping deep-in-net.local
ping deep-in-net.com
```

Both commands resolve to `192.168.1.99`, confirming correct DNS configuration.

### HTTPS

Accessing the HTTPS server by IP or domain displays the secure web page.

### FTP

Clients can successfully:

* Authenticate as `deepinnet`
* Upload and download files
* List server directories

---

## Key Networking Concepts
* Server and service roles in a network
* DHCP operation (DORA process)
* DNS purpose and resolution process
* HTTP vs HTTPS
* FTP operation
* TCP vs UDP
* OSI model layers
* Ports and their role in networking
* DNS record types (A, CNAME)


# Exercise 04

## Overview

This exercise demonstrates how a **router enables communication between two different IP networks**. Two PCs are placed in separate subnets and connected through a single router. Successful communication between the PCs proves correct IP addressing, default gateway configuration, and routing behavior.

---

## Network Topology

* One router (Cisco 1841)
* Two PCs
* Each PC is connected directly to a different router interface
* Two distinct /30 networks

This setup highlights the routing role of the router.

---

## IP Addressing Plan

### PC0

* IP Address: `192.168.1.2`
* Subnet Mask: `255.255.255.252` (/30)
* Default Gateway: `192.168.1.1`

### PC1

* IP Address: `192.168.2.2`
* Subnet Mask: `255.255.255.252` (/30)
* Default Gateway: `192.168.2.1`

### Router Interfaces

| Interface       | IP Address    | Subnet Mask       |
| --------------- | ------------- | ----------------- |
| FastEthernet0/0 | `192.168.1.1` | `255.255.255.252` |
| FastEthernet0/1 | `192.168.2.1` | `255.255.255.252` |

All router interfaces are enabled using `no shutdown`.

---

## Configuration Summary

* Each PC is placed in a different subnet
* The router connects both subnets using Layer 3 routing
* Each PC uses the router as its default gateway
* No static or dynamic routing protocols are required because the router is directly connected to both networks

---

## Verification and Testing

### Connectivity Test

ICMP (ping) is used to verify communication:

* PC0 → PC1
* PC1 → PC0

Successful ICMP replies confirm:

* Correct IP addressing
* Correct default gateway configuration
* Proper router operation

---

## Key Networking Concepts
* Router and its role in networking
* Difference between switch and router
* OSI model layers
* Network Layer (Layer 3)
* Default gateway
* Subnetting with /30 networks
* ICMP protocol


# Exercise 05

## Overview

This exercise demonstrates communication within local networks connected to switches and communication between different subnets through a router.

The objectives are:

* All devices connected to the same switch must communicate with each other.
* All devices in Subnet 1 must communicate with all devices in Subnet 2.
* All devices in Subnet 2 must communicate with all devices in Subnet 1.

---

## Network Topology

* 1 Router (Cisco 2911)
* 2 Switches
* Multiple PCs per switch
* 2 distinct IP subnets

Each switch connects devices inside the same LAN. The router connects both LANs and enables inter-subnet routing.

---

## Subnet Design

### Subnet 1 (Left Side)

Network: `192.168.1.0/29`
Subnet Mask: `255.255.255.248`

* Example host range: `192.168.1.1 – 192.168.1.6`
* Broadcast: `192.168.1.7`

Router interface (connected to Switch 1):

* `192.168.1.1/29`

PCs in this subnet use:

* Default Gateway: `192.168.1.1`

---

### Subnet 2 (Right Side)

Network: `192.168.1.64/27` *(adjust according to your exact addressing scheme)*
Subnet Mask: `255.255.255.224`

* Example host range: `192.168.1.65 – 192.168.1.94`
* Broadcast: `192.168.1.95`

Router interface (connected to Switch 2):

* `192.168.1.65/27`

PCs in this subnet use:

* Default Gateway: `192.168.1.65`

---

## Router Configuration

Each router interface is configured with an IP address belonging to its respective subnet and enabled using:

```
no shutdown
```

No static routing is required because both networks are directly connected to the router.

---

## Communication Logic

### Intra-Switch Communication

Devices connected to the same switch communicate using:

* MAC addresses
* ARP resolution
* Layer 2 switching

No router involvement is required for same-subnet communication.

---

### Inter-Subnet Communication

When a device in Subnet 1 sends traffic to Subnet 2:

1. It checks whether the destination is inside its subnet.
2. If not, it forwards the packet to its default gateway.
3. The router consults its routing table.
4. The router forwards the packet to the correct outgoing interface.
5. The destination device receives the packet.

The same process occurs in reverse for return traffic.

---

## Verification

Connectivity is verified using ICMP (ping):

* PC ↔ PC within Subnet 1
* PC ↔ PC within Subnet 2
* PC from Subnet 1 → PC from Subnet 2
* PC from Subnet 2 → PC from Subnet 1

Successful replies confirm:

* Correct subnetting
* Proper default gateway configuration
* Functional Layer 2 switching
* Correct Layer 3 routing

---

## Key Networking Concepts

* Subnetting (/29 and /27)
* Switch operation (Layer 2)
* Router operation (Layer 3)
* Default gateway
* ARP protocol
* Routing table
* ICMP protocol
* Broadcast and network addresses


# Exercise 06

## Overview

This exercise demonstrates communication between two separate local networks connected through two routers. Since each router only knows its directly connected networks by default, static routes are configured to enable end-to-end connectivity.

The objective is to allow:

* PC in Subnet 1 to communicate with PC in Subnet 2
* PC in Subnet 2 to communicate with PC in Subnet 1

---

## Network Topology

* 2 Routers
* 2 PCs
* 3 Networks:

  * LAN 1: `192.168.1.0/24`
  * WAN link: `10.10.0.0/30`
  * LAN 2: `192.168.2.0/24`

---

## IP Addressing Plan

### PC1 (Subnet 1)

* IP Address: `192.168.1.2`
* Subnet Mask: `255.255.255.0`
* Default Gateway: `192.168.1.1`

### Router1

* LAN Interface: `192.168.1.1/24`
* WAN Interface: `10.10.0.1/30`

### Router2

* WAN Interface: `10.10.0.2/30`
* LAN Interface: `192.168.2.1/24`

### PC2 (Subnet 2)

* IP Address: `192.168.2.2`
* Subnet Mask: `255.255.255.0`
* Default Gateway: `192.168.2.1`

All router interfaces are enabled using `no shutdown`.

---

## Static Routing Configuration

Since each router only knows its directly connected networks, static routes are required.

### On Router1

To reach Subnet 2:

```
ip route 192.168.2.0 255.255.255.0 10.10.0.2
```

### On Router2

To reach Subnet 1:

```
ip route 192.168.1.0 255.255.255.0 10.10.0.1
```

These routes inform each router where to forward traffic destined for the remote network.

---

## Verification

Connectivity is verified using ICMP (ping):

* PC1 → PC2
* PC2 → PC1

Successful replies confirm:

* Correct IP configuration
* Proper default gateways
* Accurate static routing entries
* Functional inter-router communication

---

## Knowledge Section

### What is a Routing Table?

A routing table is a data structure stored in a router that contains information about available networks and the paths used to reach them.

It includes:

* Destination network
* Subnet mask
* Next-hop IP address or outgoing interface
* Route source (connected, static, dynamic)

### Role in Network Traffic

When a router receives a packet:

1. It reads the destination IP address.
2. It compares it against entries in the routing table.
3. It selects the best matching route.
4. It forwards the packet to the specified next hop.

Without a routing table, routers cannot determine where to send packets destined for remote networks.


# Exercice 07

## Objective

Create the network shown in **ex07-scenario** using Cisco Packet Tracer.

### Requirements

* All devices connected to the same switch must communicate with each other.
* All devices in **Subnet 1** must communicate with devices in **Subnet 2**.
* All devices in **Subnet 2** must communicate with devices in **Subnet 1**.

---

# Network Topology

## Subnet 1 (Left Side)

* Network: `192.168.1.0/24`
* Switch1 connected to:

  * PC1
  * PC2
  * PC3
  * PC4
  * PC5
* Router1 connected to Switch1

## Subnet 2 (Right Side)

* Network: `192.168.2.0/24`
* Switch2 connected to:

  * Laptop0
  * PC6
  * PC7
  * PC8
* Router2 connected to Switch2

## Router-to-Router Link

* Network: `10.10.0.0/30`
* Used for inter-router communication

---

# IP Addressing Plan

## Subnet 1

| Device  | IP Address  | Subnet Mask   | Gateway     |
| ------- | ----------- | ------------- | ----------- |
| Router1 | 192.168.1.1 | 255.255.255.0 | —           |
| PC1     | 192.168.1.2 | 255.255.255.0 | 192.168.1.1 |
| PC2     | 192.168.1.3 | 255.255.255.0 | 192.168.1.1 |
| PC3     | 192.168.1.4 | 255.255.255.0 | 192.168.1.1 |
| PC4     | 192.168.1.5 | 255.255.255.0 | 192.168.1.1 |
| PC5     | 192.168.1.6 | 255.255.255.0 | 192.168.1.1 |

---

## Subnet 2

| Device  | IP Address  | Subnet Mask   | Gateway     |
| ------- | ----------- | ------------- | ----------- |
| Router2 | 192.168.2.1 | 255.255.255.0 | —           |
| Laptop0 | 192.168.2.2 | 255.255.255.0 | 192.168.2.1 |
| PC6     | 192.168.2.3 | 255.255.255.0 | 192.168.2.1 |
| PC7     | 192.168.2.4 | 255.255.255.0 | 192.168.2.1 |
| PC8     | 192.168.2.5 | 255.255.255.0 | 192.168.2.1 |

---

## Router Interconnection

| Device  | Interface | IP Address | Mask            |
| ------- | --------- | ---------- | --------------- |
| Router1 | Serial    | 10.10.0.1  | 255.255.255.252 |
| Router2 | Serial    | 10.10.0.2  | 255.255.255.252 |

---

# ⚙️ Router Configuration

## Router1

```bash
enable
configure terminal

interface g0/0
ip address 192.168.1.1 255.255.255.0
no shutdown

interface s0/0/0
ip address 10.10.0.1 255.255.255.252
no shutdown

ip route 192.168.2.0 255.255.255.0 10.10.0.2

end
write memory
```

---

## Router2

```bash
enable
configure terminal

interface g0/0
ip address 192.168.2.1 255.255.255.0
no shutdown

interface s0/0/0
ip address 10.10.0.2 255.255.255.252
no shutdown

ip route 192.168.1.0 255.255.255.0 10.10.0.1

end
write memory
```

---

# How Communication Works

### Same Switch Communication

Devices in the same subnet:

* Use ARP to resolve MAC addresses.
* Communicate directly at Layer 2 via the switch.

No router involvement is required.

---

### Inter-Subnet Communication

1. PC sends packet to its **default gateway**.
2. Router checks its **routing table**.
3. If destination is remote:

   * Packet is forwarded via serial link.
4. Receiving router forwards packet to its local subnet.

Static routes allow routers to know how to reach the remote network.

---

# Verification

## Test 1 – Same Subnet

From PC1:

```bash
ping 192.168.1.6
```

Expected: Successful replies.

From PC6:

```bash
ping 192.168.2.5
```

Expected: Successful replies.

---

## Test 2 – Between Subnets

From PC1:

```bash
ping 192.168.2.3
```

From PC7:

```bash
ping 192.168.1.4
```

Expected: Successful replies.

---

## Check Routing Table

On routers:

```bash
show ip route
```

You should see:

* Connected routes (C)
* Static routes (S)

---

#  Knowledge: Routing Table

## Definition

A routing table is a data table stored in a router that contains:

* Destination networks
* Subnet masks
* Next-hop addresses
* Outgoing interfaces

## Role

When a router receives a packet:

1. It reads the destination IP.
2. Searches the routing table.
3. Chooses the best matching route.
4. Forwards the packet accordingly.

Without proper routes, inter-network communication fails.

---

## Expected Result

* All devices on the same switch communicate successfully.
* Subnet 1 and Subnet 2 communicate bidirectionally.
* Static routing enables inter-router communication.


# Exercice 07

## Objective

Create the network shown in **ex07-scenario** using Cisco Packet Tracer.

### Requirements

* All devices connected to the same switch must communicate with each other.
* All devices in **Subnet 1** must communicate with devices in **Subnet 2**.
* All devices in **Subnet 2** must communicate with devices in **Subnet 1**.

---

# Network Topology

## Subnet 1 (Left Side)

* Network: `192.168.1.0/24`
* Switch1 connected to:

  * PC1
  * PC2
  * PC3
  * PC4
  * PC5
* Router1 connected to Switch1

## Subnet 2 (Right Side)

* Network: `192.168.2.0/24`
* Switch2 connected to:

  * Laptop0
  * PC6
  * PC7
  * PC8
* Router2 connected to Switch2

## Router-to-Router Link

* Network: `10.10.0.0/30`
* Used for inter-router communication

---

# IP Addressing Plan

## Subnet 1

| Device  | IP Address  | Subnet Mask   | Gateway     |
| ------- | ----------- | ------------- | ----------- |
| Router1 | 192.168.1.1 | 255.255.255.0 | —           |
| PC1     | 192.168.1.2 | 255.255.255.0 | 192.168.1.1 |
| PC2     | 192.168.1.3 | 255.255.255.0 | 192.168.1.1 |
| PC3     | 192.168.1.4 | 255.255.255.0 | 192.168.1.1 |
| PC4     | 192.168.1.5 | 255.255.255.0 | 192.168.1.1 |
| PC5     | 192.168.1.6 | 255.255.255.0 | 192.168.1.1 |

---

## Subnet 2

| Device  | IP Address  | Subnet Mask   | Gateway     |
| ------- | ----------- | ------------- | ----------- |
| Router2 | 192.168.2.1 | 255.255.255.0 | —           |
| Laptop0 | 192.168.2.2 | 255.255.255.0 | 192.168.2.1 |
| PC6     | 192.168.2.3 | 255.255.255.0 | 192.168.2.1 |
| PC7     | 192.168.2.4 | 255.255.255.0 | 192.168.2.1 |
| PC8     | 192.168.2.5 | 255.255.255.0 | 192.168.2.1 |

---

## Router Interconnection

| Device  | Interface | IP Address | Mask            |
| ------- | --------- | ---------- | --------------- |
| Router1 | Serial    | 10.10.0.1  | 255.255.255.252 |
| Router2 | Serial    | 10.10.0.2  | 255.255.255.252 |

---

# ⚙️ Router Configuration

## Router1

```bash
enable
configure terminal

interface g0/0
ip address 192.168.1.1 255.255.255.0
no shutdown

interface s0/0/0
ip address 10.10.0.1 255.255.255.252
no shutdown

ip route 192.168.2.0 255.255.255.0 10.10.0.2

end
write memory
```

---

## Router2

```bash
enable
configure terminal

interface g0/0
ip address 192.168.2.1 255.255.255.0
no shutdown

interface s0/0/0
ip address 10.10.0.2 255.255.255.252
no shutdown

ip route 192.168.1.0 255.255.255.0 10.10.0.1

end
write memory
```

---

# How Communication Works

### Same Switch Communication

Devices in the same subnet:

* Use ARP to resolve MAC addresses.
* Communicate directly at Layer 2 via the switch.

No router involvement is required.

---

### Inter-Subnet Communication

1. PC sends packet to its **default gateway**.
2. Router checks its **routing table**.
3. If destination is remote:

   * Packet is forwarded via serial link.
4. Receiving router forwards packet to its local subnet.

Static routes allow routers to know how to reach the remote network.

---

# Verification

## Test 1 – Same Subnet

From PC1:

```bash
ping 192.168.1.6
```

Expected: Successful replies.

From PC6:

```bash
ping 192.168.2.5
```

Expected: Successful replies.

---

## Test 2 – Between Subnets

From PC1:

```bash
ping 192.168.2.3
```

From PC7:

```bash
ping 192.168.1.4
```

Expected: Successful replies.

---

## Check Routing Table

On routers:

```bash
show ip route
```

You should see:

* Connected routes (C)
* Static routes (S)

---

#  Knowledge: Routing Table

## Definition

A routing table is a data table stored in a router that contains:

* Destination networks
* Subnet masks
* Next-hop addresses
* Outgoing interfaces

## Role

When a router receives a packet:

1. It reads the destination IP.
2. Searches the routing table.
3. Chooses the best matching route.
4. Forwards the packet accordingly.

Without proper routes, inter-network communication fails.

---

## Expected Result

* All devices on the same switch communicate successfully.
* Subnet 1 and Subnet 2 communicate bidirectionally.
* Static routing enables inter-router communication.
