# What is OSPF?

**Open Shortest Path First (OSPF)** is a **link-state Interior Gateway Protocol (IGP)** used by enterprise networks to dynamically exchange routing information between routers within a single autonomous system (AS). Unlike distance-vector routing protocols, OSPF builds a complete map of the network topology and uses the **Shortest Path First (SPF)** algorithm, developed by Edsger Dijkstra, to determine the most efficient route to each destination.

OSPF is widely used in medium and large enterprise networks because it provides:

- Fast network convergence after topology changes
- Loop-free routing through the SPF algorithm
- Support for hierarchical network design using multiple areas
- Route summarization for improved scalability
- Equal-Cost Multi-Path (ECMP) load balancing
- Efficient bandwidth utilization through Link-State Advertisements (LSAs)

Unlike routing protocols that rely on hop count, OSPF selects routes based on **cost**, a metric primarily derived from interface bandwidth. Network administrators can manually modify interface costs to influence path selection and traffic flow.

---

## How OSPF Works

1. Routers discover neighboring OSPF routers by exchanging **Hello packets**.
2. Neighboring routers establish adjacencies.
3. Routers exchange **Link-State Advertisements (LSAs)** to describe their directly connected networks.
4. Each router builds an identical **Link-State Database (LSDB)** containing the complete network topology.
5. The **Shortest Path First (SPF)** algorithm calculates the lowest-cost path to every destination.
6. The resulting routes are installed in the routing table.

---

## OSPF Areas Used in This Lab

This project demonstrates a **multi-area OSPF** deployment.

| Area | Purpose |
|------|---------|
| **Area 0** | Backbone area that connects all other OSPF areas |
| **Area 2** | Internal area containing the left side of the topology |

Router **R3** functions as the **Area Border Router (ABR)** by connecting Area 0 and Area 2 while summarizing routes between them.

---

## OSPF Concepts Demonstrated

This lab includes several enterprise OSPF features:

- Multi-Area OSPF
- Area Border Router (ABR)
- Router IDs
- Link-State Advertisements (LSAs)
- Passive Interfaces
- Route Summarization
- Interface Cost Manipulation
- SPF (Dijkstra) Path Calculation
- Dynamic Route Convergence
