# IPv6 Configuration and OSPFv3 Routing Lab (NET 365)

## Overview

This lab demonstrates the implementation of **IPv6 networking** and **OSPFv3 (Open Shortest Path First Version 3)** in a four-router Cisco topology. The objective was to configure IPv6 addressing, establish OSPFv3 neighbor adjacencies, advertise IPv6 networks, configure passive interfaces, and verify end-to-end connectivity between multiple LANs.

Unlike OSPFv2, which is designed for IPv4 networks, **OSPFv3** is specifically designed to support IPv6 routing while maintaining the same link-state routing principles.

---

# What is IPv6?

**Internet Protocol Version 6 (IPv6)** is the successor to IPv4 and was developed to address the exhaustion of IPv4 addresses. IPv6 uses **128-bit addresses**, providing approximately **340 undecillion (3.4 × 10³⁸)** unique addresses, enabling virtually unlimited address space for modern networks.

IPv6 introduces several improvements over IPv4, including:

- Vastly larger address space
- Simplified packet header
- Built-in support for IPsec
- Stateless Address Autoconfiguration (SLAAC)
- Improved multicast communication
- Elimination of Network Address Translation (NAT) requirements in most deployments
- More efficient routing and packet processing

---

# What is OSPFv3?

**Open Shortest Path First Version 3 (OSPFv3)** is a **link-state Interior Gateway Protocol (IGP)** used to dynamically exchange IPv6 routing information within a single autonomous system.

OSPFv3 performs many of the same functions as OSPFv2, including:

- Neighbor discovery using Hello packets
- Exchange of Link-State Advertisements (LSAs)
- Construction of a Link-State Database (LSDB)
- Shortest Path First (SPF) calculations using Dijkstra's Algorithm
- Fast convergence after topology changes

Unlike OSPFv2, OSPFv3 is enabled directly on interfaces rather than through network statements.

---

# Learning Objectives

- Configure IPv6 addressing on Cisco routers
- Enable IPv6 routing
- Configure OSPFv3 Process ID 20
- Establish OSPFv3 neighbor adjacencies
- Configure passive interfaces
- Advertise IPv6 LAN and serial networks
- Verify dynamic IPv6 routing
- Analyze OSPFv3 operation
- Validate end-to-end IPv6 connectivity

---

# Network Topology

> *Insert topology diagram here.*

---

# IPv6 Addressing Scheme

The lab uses multiple IPv6 /64 networks for LAN and point-to-point serial links.

| Network | Purpose |
|----------|---------|
| 2001:A:C:E1::/64 | Host 1 LAN |
| 2001:A:C:E2::/64 | Loopback Network |
| 2001:A:C:E3::/64 | LAN between R2 and R3 |
| 2001:A:C:E4::/64 | Host 2 LAN |
| 2001:A:C:E5::/64 | LAN between R1 and R4 |
| 2001:A:C:FF::/126 | Point-to-Point Serial Links |

---

# Router Configuration

Each router was configured with:

- IPv6 unicast routing
- IPv6 interface addresses
- OSPFv3 Process ID 20
- Passive interfaces where appropriate
- Serial interface bandwidth configuration

Example (R1)

```cisco
ipv6 unicast-routing

interface FastEthernet0/0
 ipv6 address 2001:A:C:E1::1/64
 ipv6 ospf 20 area 0

interface Serial0/2/0
 ipv6 address 2001:A:C:FF::2/126
 ipv6 ospf 20 area 0

ipv6 router ospf 20
 passive-interface FastEthernet0/0
```

---

# OSPFv3 Configuration

OSPFv3 was enabled directly on the participating interfaces.

Example:

```cisco
interface FastEthernet0/0
 ipv6 ospf 20 area 0
```

Unlike OSPFv2, there are **no `network` statements**. Interfaces participate in OSPFv3 only after the `ipv6 ospf` command is applied.

---

# Passive Interfaces

Passive interfaces prevent unnecessary OSPF Hello packets while still advertising connected IPv6 networks.

| Router | Passive Interface |
|---------|-------------------|
| R1 | FastEthernet0/0 |
| R2 | Loopback1 |

---

# Verification Commands

The following Cisco IOS commands were used to verify the configuration.

## Neighbor Verification

```cisco
show ipv6 ospf neighbor
```

## Interface Verification

```cisco
show ipv6 ospf interface
```

## IPv6 Routing Table

```cisco
show ipv6 route
```

## OSPFv3 Database

```cisco
show ipv6 ospf database
```

## IPv6 Interfaces

```cisco
show ipv6 interface brief
```

## Connectivity Testing

```cisco
ping
traceroute
```

---

# Results

The network successfully achieved:

- Full IPv6 connectivity
- Stable OSPFv3 neighbor adjacencies
- Dynamic IPv6 route learning
- End-to-end communication between all LANs
- Automatic route propagation across the topology

All routers successfully exchanged IPv6 routing information through OSPFv3, allowing traffic to reach remote IPv6 networks without static routing.

---

# Key Concepts Demonstrated

- IPv6 Addressing
- IPv6 Routing
- OSPFv3
- Link-State Routing
- Neighbor Discovery
- Link-State Advertisements (LSAs)
- Link-State Database (LSDB)
- Dijkstra's Shortest Path First (SPF)
- Passive Interfaces
- Dynamic Routing
- Cisco IOS
- Enterprise Networking

---

# Repository Structure

```
NET365-IPv6-OSPFv3-Lab/

│
├── README.md
├── topology.png
├── packet-tracer/
│     └── ipv6-ospfv3-lab.pkt
├── configs/
│     ├── R1.txt
│     ├── R2.txt
│     ├── R3.txt
│     └── R4.txt

```

---

# Skills Demonstrated

- IPv6 Networking
- OSPFv3 Configuration
- Dynamic Routing
- Cisco IOS
- Enterprise Networking
- Network Troubleshooting
- IPv6 Address Planning
- Routing Verification
- Cisco CLI
- Packet Tracer

---

# Conclusion

This project demonstrates the deployment of an IPv6 enterprise network using Cisco routers and OSPFv3. IPv6 addressing was configured across LAN and serial interfaces, dynamic routing was established using OSPFv3, and passive interfaces were implemented to optimize routing behavior. The lab highlights the differences between OSPFv2 and OSPFv3 while reinforcing key 
networking concepts such as neighbor discovery, dynamic route exchange, and IPv6 routing in modern enterprise environments.
