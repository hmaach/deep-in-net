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
