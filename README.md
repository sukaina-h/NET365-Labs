# NET 365 – Enterprise Routing and Network Infrastructure

## Overview

This repository contains my coursework, lab implementations, and networking projects completed in **NET 365 – Enterprise Routing and Network Infrastructure** at **DePaul University**.

Throughout this course, I gained hands-on experience configuring and troubleshooting enterprise networks using Cisco IOS and Cisco Packet Tracer. The labs focused on dynamic routing protocols, IPv4 and IPv6 routing, route optimization, redundancy, and network troubleshooting using industry-standard verification commands.

Each lab is documented with configuration files, topology diagrams, verification outputs, and technical explanations demonstrating practical networking concepts used in enterprise environments.

---

# Course Learning Outcomes

Throughout this course, I learned how to:

- Design enterprise network topologies
- Configure Cisco routers and switches
- Configure IPv4 and IPv6 addressing
- Implement static and dynamic routing
- Deploy enterprise routing protocols
- Configure multi-area routing architectures
- Analyze routing tables
- Troubleshoot routing issues
- Verify network connectivity using Cisco IOS
- Optimize routing through routing metrics and path selection
- Document enterprise networking projects

---

# Networking Technologies Covered

## IPv4 Networking

- IPv4 Addressing
- Subnetting
- Variable Length Subnet Masking (VLSM)
- Loopback Interfaces
- Default Gateways
- Point-to-Point Links

---

## IPv6 Networking

- IPv6 Addressing
- IPv6 Routing
- IPv6 Neighbor Discovery
- OSPFv3
- IPv6 Interface Configuration
- IPv6 Route Verification

---

## Routing Protocols

### Static Routing

- Static Routes
- Default Routes
- Administrative Distance

### RIP Version 2

- Dynamic Route Advertisement
- Route Propagation
- Route Verification

### Enhanced Interior Gateway Routing Protocol (EIGRP)

- Neighbor Relationships
- Composite Metric Calculation
- Bandwidth and Delay Metrics
- Feasible Distance
- Successor Routes
- Passive Interfaces
- Route Optimization

### Open Shortest Path First (OSPF)

- Link-State Routing
- SPF (Dijkstra) Algorithm
- Router IDs
- Multi-Area OSPF
- Area Border Routers (ABRs)
- Route Summarization
- OSPF Cost Manipulation
- Passive Interfaces

### OSPFv3

- IPv6 Dynamic Routing
- Interface-Based Configuration
- Neighbor Discovery
- Link-State Advertisements (LSAs)

### Border Gateway Protocol (BGP)

- Autonomous Systems (AS)
- External BGP (eBGP)
- Route Advertisement
- Best Path Selection
- WAN Failover
- Internet Routing Concepts

---

# Cisco IOS Skills

Throughout these labs, I became proficient with Cisco IOS configuration and troubleshooting commands, including:

```cisco
show ip interface brief
show ip route
show ip protocols
show ip ospf neighbor
show ip ospf database
show ip eigrp neighbors
show ip bgp
show ip bgp summary
show ipv6 route
show ipv6 ospf neighbor
show running-config
ping
traceroute
```

---

# Enterprise Networking Skills

This course strengthened my understanding of:

- Enterprise Routing
- Dynamic Routing Protocols
- Route Convergence
- Routing Metrics
- Link-State vs Distance-Vector Routing
- Path Selection
- Network Redundancy
- WAN Connectivity
- Cisco CLI Administration
- Network Troubleshooting
- Routing Table Analysis
- Layer 3 Network Design

---

# Repository Structure

```
NET365/

├── README.md
│
├── Static-Routing/
├── RIPv2/
├── EIGRP/
├── OSPF/
├── IPv6-OSPFv3/
├── BGP/
│
├── Topology-Diagrams/
└── Packet-Tracer-Files/
```

---

# Featured Labs

## EIGRP Configuration and Metric Analysis

**Topics Covered**

- EIGRP Neighbor Formation
- Passive Interfaces
- Composite Metrics
- Bandwidth
- Delay
- Route Optimization

**Repository**

```
NET365/EIGRP
```

---

## Multi-Area OSPF Routing

**Topics Covered**

- Multi-Area OSPF
- Router IDs
- Route Summarization
- OSPF Cost Manipulation
- SPF Algorithm

**Repository**

```
NET365/OSPF
```

---

## IPv6 Routing with OSPFv3

**Topics Covered**

- IPv6 Addressing
- OSPFv3
- Neighbor Discovery
- Dynamic IPv6 Routing

**Repository**

```
NET365/IPv6-OSPFv3
```

---

## Border Gateway Protocol (BGP)

**Topics Covered**

- Multiple Autonomous Systems
- External BGP
- OSPF Integration
- BGP Route Advertisement
- WAN Failover

**Repository**

```
NET365/BGP
```

---

# Tools Used

- Cisco Packet Tracer
- Cisco IOS
- Command Line Interface (CLI)
- Git
- GitHub

---

# Key Skills Demonstrated

- Enterprise Networking
- Cisco Routing
- IPv4
- IPv6
- Dynamic Routing
- Static Routing
- OSPF
- OSPFv3
- EIGRP
- BGP
- Routing Optimization
- Route Summarization
- Cisco IOS
- Network Troubleshooting
- Packet Tracer
- Network Documentation

---

# What I Learned

This course significantly strengthened my understanding of enterprise networking and routing technologies. Through hands-on Cisco labs, I learned how to design, configure, verify, and troubleshoot routed networks using industry-standard protocols such as EIGRP, OSPF, OSPFv3, and BGP.

Beyond simply configuring routers, I developed the ability to analyze routing decisions, interpret routing tables, optimize traffic flow through routing metrics, and understand how dynamic routing protocols adapt to network changes. I also gained practical experience with IPv6 deployment, multi-area OSPF design, inter-domain routing with BGP, and systematic network troubleshooting using Cisco IOS verification commands.

These projects reflect practical networking skills that serve as a strong foundation for careers in cybersecurity, network engineering, cloud networking, and infrastructure administration.
