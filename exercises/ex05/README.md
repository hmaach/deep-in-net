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
