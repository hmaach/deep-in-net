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
