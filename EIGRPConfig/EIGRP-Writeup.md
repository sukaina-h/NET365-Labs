EIGRP Configuration and Metric Analysis Lab (NET 365)
Overview
This document details the configuration and testing of a four-router network utilizing the Enhanced Interior Gateway Routing Protocol (EIGRP). The primary goals of this lab were to:

Configure basic IP addressing, hostnames, and connectivity on four Cisco routers (R1, R2, R3, R4) and two end hosts (Host 1, Host 2).

Implement EIGRP Autonomous System (AS) 5205, including network advertisement, passive interfaces, and disabling auto-summarization.

Analyze EIGRP's path selection mechanism by manipulating the bandwidth and delay metrics on serial links.

Network Topology:
1. Initial Setup and Connectivity
1.1 IP Addressing and Interface Configuration
All interfaces were configured according to the IP Addressing Requirements, using a placeholder Student Number (<SN>). Clock rates were set on the DCE (Data Communications Equipment) ends of the serial links to match the specified link speeds (Link 1: 1 Mbps, Link 2: 2 Mbps).

Key Commands (Example on R1):

R1> enable
R1# configure terminal
R1(config)# hostname R1-<Initials>
R1(config)# interface Fa0/0
R1(config-if)# ip address 44.44.<SN>.1 255.255.255.0
R1(config-if)# no shutdown
R1(config-if)# exit

R1(config)# interface Fa0/1
R1(config-if)# ip address 66.66.5.1 255.255.255.252
R1(config-if)# no shutdown
R1(config-if)# exit

R1(config)# interface S0/2/0
R1(config-if)# ip address 200.0.0.6 255.255.255.252
R1(config-if)# clock rate 1000000  <-- DCE side for Link 1 (1 Mbps)
R1(config-if)# no shutdown
R1(config-if)# exit

1.2 Verification
After configuring all devices (including default gateways on Host 1 and Host 2):

show ip int brief was used on all routers to verify correct IP addresses and UP/UP status.

Successful Pings were achieved between each host and its default gateway, and between all 1-hop neighbor routers (R1 ↔ R2, R1 ↔ R4, R4 ↔ R3, R2 ↔ R3).

show ip route confirmed all directly connected subnets were in the routing tables.

2. EIGRP Configuration (AS 5205)
2.1 EIGRP Activation and Network Statements
EIGRP was initiated on all four routers using Autonomous System 5205. network statements were used to activate the protocol on all connected interfaces, including the Loopback0 interface on R2.

Key Commands (Example on R1):

R1(config)# router eigrp 5205
R1(config-router)# network 44.44.<SN>.0 0.0.0.255  <-- Subnet A
R1(config-router)# network 66.66.5.0 0.0.0.3      <-- Subnet E
R1(config-router)# network 200.0.0.4 0.0.0.3      <-- Link 1
R1(config-router)# no auto-summary

2.2 Passive Interfaces
To prevent unnecessary EIGRP neighbor formation and updates on LAN segments, specific interfaces were configured as passive.

Passive Interface Configuration:

Router
Interface
Purpose
R1
Fa0/0
Subnet A (Host 1)
R2
Loopback0
Subnet B
R3
Fa0/0
Subnet D (Host 2)

Key Command (Example on R1):
R1(config-router)# passive-interface Fa0/0

2.3 Verification of EIGRP Adjacency (Part 1.1 Initial State)
show ip protocol confirmed EIGRP AS 5205 was running and auto-summary was disabled.

show ip eigrp neighbor confirmed the two required EIGRP neighbor adjacencies on each router were established (e.g., R1 showed R2 and R4 as neighbors).
Before metric manipulation, show ip route showed the shortest paths were chosen based on default EIGRP metrics (bandwidth and delay). Typically, the path with the higher serial link bandwidth (Link 2: 2 Mbps) would be preferred if all other metrics were equal.

3. EIGRP Metric Manipulation (Bandwidth and Delay)
To force path selection over a specific route, the Bandwidth and Delay values—the primary components of the EIGRP metric—were manually adjusted.

3.1 Step 4: Setting Bandwidth
The bandwidth command was used on all four serial interfaces to match the diagram's link speeds in Kbps.

Router
Interface
Link
Command (bandwidth in Kbps)
R1/R2
S0/2/0
Link 1 (1 Mbps)
bandwidth 1000
R3/R4
S0/2/0
Link 2 (2 Mbps)
bandwidth 2000

3.2 Step 5: Setting Delay (Metric Control)
The Delay metric was specifically raised on Link 1 to make the R1-R2 path appear less desirable than the longer R1-R4-R3-R2 path, which utilizes Link 2.

On R1, interface S0/2/0: delay 500 (5000 microseconds)

On R2, interface S0/2/0: delay 500 (5000 microseconds)

The path R1 → R4 → R3 → R2 maintained the default low delay, effectively reducing its overall EIGRP metric relative to the now-penalized R1 → R2 path.

3.3 Path Verification (Part 1.2 Final State)
After applying the metric adjustments:

show interface S0/2/0 on R1 confirmed the new BW (1000 Kbit) and DLY (5000 usec) values.

The R1 Routing Table (show ip route) was updated, showing that the route to Subnet B (172.11.5.0/28) was now learned via R4/Fa0/1 instead of R2/S0/2/0.

tracert 172.11.5.1 from Host 1 confirmed the path shifted: the traffic now flowed through the longer route (R1 → R4 → R3 → R2).

Conclusion: By manually configuring a higher Delay on the direct Link 1, the EIGRP metric calculation was altered, causing the routers to prefer the longer path (R1-R4-R3-R2) which had 
a lower overall calculated metric (Feasible Distance) to reach the destination Subnet B. This demonstrates how EIGRP uses composite metrics to make forwarding decision.
