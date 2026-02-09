
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
