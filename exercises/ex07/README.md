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
