# EIGRP Configuration and Metric Analysis Lab (NET 365)

## Overview

This lab demonstrates the configuration, verification, and analysis of the **Enhanced Interior Gateway Routing Protocol (EIGRP)** in a four-router Cisco network. The objective was to establish end-to-end connectivity, configure dynamic routing using **EIGRP Autonomous System (AS) 5205**, and examine how EIGRP selects routes based on its composite metric by modifying interface bandwidth and delay.

## Objectives

- Configure IP addressing on four Cisco routers and two end hosts.
- Verify Layer 3 connectivity between all directly connected devices.
- Configure EIGRP AS 5205 across the network.
- Advertise connected networks using EIGRP.
- Configure passive interfaces to suppress unnecessary routing updates.
- Disable automatic route summarization.
- Analyze EIGRP path selection by modifying bandwidth and delay metrics.
- Verify routing behavior using Cisco IOS verification commands.

---

# Network Topology

> *Insert network topology diagram here.*

---

# Initial Configuration

## IP Addressing

Each router interface was configured according to the provided addressing scheme.

Configuration included:

- Hostnames
- IPv4 addressing
- Interface activation (`no shutdown`)
- Clock rates on DCE serial interfaces

### Example Configuration (R1)

```cisco
enable
configure terminal

hostname R1

interface Fa0/0
 ip address 44.44.X.1 255.255.255.0
 no shutdown

interface Fa0/1
 ip address 66.66.5.1 255.255.255.252
 no shutdown

interface S0/2/0
 ip address 200.0.0.6 255.255.255.252
 clock rate 1000000
 no shutdown
```

---

# Connectivity Verification

After configuring all routers and hosts, connectivity was validated using the following commands:

```cisco
show ip interface brief
show ip route
ping
```

## Verification Results

- All interfaces reached **UP/UP** status.
- Successful ping tests between:
  - Hosts and their default gateways
  - All directly connected routers
- Routing tables contained all directly connected networks.

---

# EIGRP Configuration

## Autonomous System

```
AS Number: 5205
```

EIGRP was enabled on every router using the appropriate network statements.

### Example (R1)

```cisco
router eigrp 5205

network 44.44.X.0 0.0.0.255
network 66.66.5.0 0.0.0.3
network 200.0.0.4 0.0.0.3

no auto-summary
```

---

# Passive Interfaces

Passive interfaces were configured on LAN-facing interfaces to prevent unnecessary EIGRP hello packets while still advertising those connected networks.

| Router | Passive Interface | Purpose |
|---------|-------------------|----------|
| R1 | Fa0/0 | Host 1 LAN |
| R2 | Loopback0 | Loopback Network |
| R3 | Fa0/0 | Host 2 LAN |

Example:

```cisco
router eigrp 5205
 passive-interface Fa0/0
```

---

# EIGRP Verification

The following commands were used to verify the EIGRP configuration:

```cisco
show ip protocols
show ip eigrp neighbors
show ip route
```

## Results

- EIGRP AS 5205 was running successfully.
- Auto-summary was disabled.
- Every router established two EIGRP neighbor adjacencies.
- Routes were dynamically exchanged across the network.
- EIGRP initially selected the path with the lowest default metric.

---

# EIGRP Metric Analysis

One of the primary objectives of this lab was to demonstrate how EIGRP selects routes using its composite metric.

The default EIGRP metric is primarily calculated using:

- Bandwidth
- Delay

---

## Step 1 — Configure Bandwidth

The serial interfaces were configured to match the link speeds shown in the topology.

| Link | Bandwidth |
|-------|-----------|
| Link 1 | 1 Mbps |
| Link 2 | 2 Mbps |

Configuration:

```cisco
bandwidth 1000
```

or

```cisco
bandwidth 2000
```

depending on the interface.

---

## Step 2 — Modify Delay

To influence route selection, the delay on the direct R1–R2 link was increased.

### R1

```cisco
interface S0/2/0
 delay 500
```

### R2

```cisco
interface S0/2/0
 delay 500
```

Increasing delay raised the EIGRP metric for the direct path, making the alternate route more attractive.

---

# Route Verification

The updated routing behavior was verified using:

```cisco
show interface S0/2/0
show ip route
tracert 172.11.5.1
```

## Results

The routing table changed after the metric adjustment.

### Initial Preferred Path

```
R1 → R2
```

### New Preferred Path

```
R1 → R4 → R3 → R2
```

The traceroute from Host 1 confirmed that traffic followed the longer physical path because it had the lower EIGRP composite metric.

---

# Key Cisco IOS Commands

## Configuration

```cisco
router eigrp 5205
network
passive-interface
no auto-summary
bandwidth
delay
```

## Verification

```cisco
show ip protocols
show ip eigrp neighbors
show ip route
show interface
show ip interface brief
ping
tracert
```

---

# Key Concepts Demonstrated

- EIGRP Neighbor Formation
- Dynamic Route Advertisement
- Passive Interfaces
- Disabling Auto-Summarization
- Composite Metric Calculation
- Bandwidth Metric
- Delay Metric
- Feasible Distance
- Successor Route Selection
- Dynamic Path Optimization

---

# Conclusion

This lab demonstrated the complete deployment of EIGRP in a multi-router Cisco network. After establishing dynamic routing and verifying neighbor relationships, interface bandwidth and delay metrics were intentionally modified to influence EIGRP's route selection process. Increasing the delay on the direct R1–R2 link caused EIGRP to calculate a higher composite metric for that path, resulting in traffic being redirected through the alternate R1 → R4 → R3 → R2 route. This exercise illustrates how EIGRP uses bandwidth and delay—not simply hop count—to determine the most efficient forwarding path.
