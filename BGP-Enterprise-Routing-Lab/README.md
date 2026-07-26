# Border Gateway Protocol (BGP) Multi-Autonomous System Lab (NET 365)

## Overview

This project demonstrates the implementation of the **Border Gateway Protocol (BGP)** across multiple autonomous systems (AS) using Cisco routers. The lab combines **OSPF** for internal routing within each autonomous system and **External BGP (eBGP)** for exchanging routes between different autonomous systems.

The network was designed to simulate a simplified Internet environment where multiple autonomous systems exchange routing information while maintaining independent internal routing domains.

Throughout the lab, BGP neighbor relationships were established, routes were advertised between autonomous systems, end-to-end connectivity was verified, and failover behavior was analyzed after intentionally disabling a WAN connection.

---

# What is BGP?

**Border Gateway Protocol (BGP)** is the Internet's standard **Exterior Gateway Protocol (EGP)** used to exchange routing information between different **Autonomous Systems (ASes)**.

Unlike routing protocols such as OSPF or EIGRP that operate inside a single organization, BGP allows separate organizations, Internet Service Providers (ISPs), and enterprise networks to exchange routing information across administrative boundaries.

Today, nearly every route on the public Internet is learned through BGP.

---

# Why is BGP Important?

BGP enables:

- Internet-wide routing
- Communication between different organizations
- Highly scalable routing
- Route redundancy and failover
- Traffic engineering through routing policies
- Internet Service Provider (ISP) connectivity

Without BGP, the modern Internet would not function.

---

# BGP Concepts Demonstrated

This lab demonstrates several core BGP concepts:

- Multiple Autonomous Systems (AS)
- External BGP (eBGP)
- Dynamic route advertisement
- Neighbor relationships
- Route propagation
- Best path selection
- Failover and convergence
- OSPF as the Interior Gateway Protocol (IGP)
- End-to-end routing verification

---

# Learning Objectives

- Configure IPv4 addressing
- Configure multiple autonomous systems
- Configure OSPF within each AS
- Configure eBGP neighbor relationships
- Advertise local networks into BGP
- Verify BGP route exchange
- Analyze BGP routing tables
- Test WAN failover
- Verify end-to-end connectivity

---

# Network Design

The topology consists of five Cisco routers distributed across multiple autonomous systems.

Each autonomous system exchanges routes using **External BGP (eBGP)** while relying on **OSPF** for internal routing.

---

# Technologies Used

- Cisco IOS
- Border Gateway Protocol (BGP)
- External BGP (eBGP)
- OSPF
- Cisco Packet Tracer
- IPv4 Routing
- Cisco CLI

---

# BGP Configuration

Each border router was configured with:

- Local Autonomous System Number
- Neighbor relationships
- Advertised local networks
- OSPF redistribution where required

Example:

```cisco
router bgp <AS_NUMBER>

neighbor <Neighbor-IP> remote-as <Neighbor-AS>

network <Network> mask <Subnet-Mask>
```

---

# OSPF Configuration

Within each autonomous system, OSPF provided internal routing.

Responsibilities included:

- Learning internal routes
- Advertising LAN networks
- Connecting internal routers
- Providing reachability to BGP border routers

---

# Verification Commands

The following Cisco IOS commands were used during implementation.

## BGP

```cisco
show ip bgp
```

```cisco
show ip bgp summary
```

```cisco
show ip protocols
```

## Routing

```cisco
show ip route
```

## Connectivity

```cisco
ping
```

```cisco
tracert
```

---

# Failover Testing

One objective of the lab was to observe BGP convergence after a WAN failure.

The following action was performed:

- Shutdown of Router R2 Serial0/2/1 interface

After the failure:

- BGP recalculated the best available path.
- Routing tables were updated.
- End-to-end connectivity was maintained through an alternate route.
- Traceroute confirmed traffic successfully bypassed the failed link.

This demonstrated BGP's ability to adapt to network topology changes while maintaining connectivity. :contentReference[oaicite:1]{index=1}

---

# Verification Results

The completed network successfully demonstrated:

- Stable eBGP neighbor relationships
- Dynamic route advertisement
- Reachability across multiple autonomous systems
- Successful route propagation
- End-to-end host connectivity
- Successful failover after WAN link failure
- Dynamic routing table updates

Verification included:

- `show ip bgp`
- `show ip bgp summary`
- `show ip route`
- `show ip protocols`
- `ping`
- `tracert`

---

# Skills Demonstrated

- Border Gateway Protocol (BGP)
- External BGP (eBGP)
- OSPF
- Dynamic Routing
- Autonomous Systems
- Route Advertisement
- Route Selection
- WAN Routing
- Network Redundancy
- Failover Testing
- Cisco IOS
- Cisco CLI
- Enterprise Networking
- Network Troubleshooting
- Packet Tracer

---

# Repository Structure

```
BGP-Enterprise-Routing-Lab/

│
├── README.md
├── topology.png
├── packet-tracer/
│     └── bgp-lab.pkt
├── configs/
│     ├── R1.txt
│     ├── R2.txt
│     ├── R3.txt
│     ├── R4.txt
│     └── R5.txt
```

---

# Conclusion

This project demonstrates the deployment of a multi-autonomous system network using Cisco routers, combining **OSPF** for internal routing and **External BGP (eBGP)** for inter-domain routing. BGP neighbor relationships were established to exchange routes between autonomous systems, while OSPF provided efficient routing within each domain. The lab concluded with failover testing, where a WAN link failure triggered BGP to recalculate 
the best available path, illustrating BGP's dynamic convergence and resilience in enterprise and service provider networks.
