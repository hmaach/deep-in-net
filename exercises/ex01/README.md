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
