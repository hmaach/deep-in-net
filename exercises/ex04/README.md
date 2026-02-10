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
