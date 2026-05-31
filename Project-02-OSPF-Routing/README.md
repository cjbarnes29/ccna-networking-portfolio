# Project 02 - OSPF Routing Configuration and Troubleshooting

## Project Overview

This project demonstrates the implementation of OSPF (Open Shortest Path First) routing between three Cisco routers using EVE-NG and Cisco IOS.

The network was designed using a triangle topology with multiple point-to-point connections and separate LAN networks. OSPF was configured to dynamically exchange routing information between routers and provide end-to-end connectivity between PCs.

In addition to the initial implementation, multiple routing and connectivity issues were intentionally introduced to practice troubleshooting and network verification techniques commonly used in enterprise environments.

The project includes:
- OSPF configuration
- Dynamic route learning
- Neighbor adjacency verification
- Interface troubleshooting
- OSPF area troubleshooting
- Gateway troubleshooting
- End-to-end connectivity testing

---

# Project Objectives

- Configure OSPF routing between three routers
- Establish OSPF neighbor relationships
- Verify dynamic route learning
- Troubleshoot interface and routing problems
- Restore end-to-end PC connectivity
- Practice Cisco IOS verification commands

---

# Technologies Used

- Cisco IOS CLI
- OSPF Routing Protocol
- EVE-NG
- VPCS

---

# Network Topology

The network consists of three routers connected using /30 point-to-point links.

LAN Networks:

| Device | Network |
|---|---|
| R1 LAN | 192.168.1.0/24 |
| R2 LAN | 192.168.2.0/24 |

Point-to-Point Networks:

| Link | Network |
|---|---|
| R1 ↔ R2 | 10.0.12.0/30 |
| R1 ↔ R3 | 10.0.13.0/30 |
| R2 ↔ R3 | 10.0.23.0/30 |

## Topology Diagram

![Topology](topology.png)

---

# Troubleshooting Scenarios

The following problems were intentionally introduced into the lab:

- R1 G0/1 interface shutdown
- OSPF area mismatch
- Missing OSPF advertisements
- Wrong PC default gateway
- Neighbor adjacency failure

![Mistake List](mistake-list.png)

---

# R1 Interface Shutdown Issue

R1 GigabitEthernet0/1 was administratively down, preventing OSPF neighbor adjacency formation.

Verification command used:

```bash
show ip interface brief
```

![Interface Down](interface-down.png)

### Fix Applied

```bash
conf t
interface g0/1
no shutdown
```

After enabling the interface, router communication was restored.

![No Shutdown](no-shutdown.png)

---

# OSPF Area Mismatch

R2 was configured with the wrong OSPF area which prevented adjacency formation.

![Area Mismatch](area-mismatch.png)

### Incorrect Configuration

```bash
network 10.0.12.0 0.0.0.3 area 1
```

### Corrected Configuration

```bash
no network 10.0.12.0 0.0.0.3 area 1
network 10.0.12.0 0.0.0.3 area 0
```

---

# Initial OSPF Neighbor Failure

Before troubleshooting, routers failed to establish FULL OSPF neighbor relationships.

Verification command used:

```bash
show ip ospf neighbor
```

![No Neighbor](no-neighbor.png)

---

# Router 3 Routing Verification Before Fix

Router 3 initially showed incomplete routing information due to OSPF issues.

Verification command used:

```bash
show ip route ospf
```

![Router3 Before Fix](router3-before-fix.png)

---

# OSPF Neighbor Recovery

After correcting the configuration issues, all routers successfully established FULL neighbor relationships.

Verification command used:

```bash
show ip ospf neighbor
```

![Neighbor Fix 1](neighbor-after-fix.png)

![Neighbor Fix 2](neighbor-after-fix-2.png)

![Neighbor Fix 3](neighbor-after-fix-3.png)

---

# Wrong Gateway Issue

PC2 initially had an incorrect default gateway configured, preventing communication with remote networks.

![Wrong Gateway](wrong-gateway.png)

### Correct Gateway

```bash
192.168.2.1
```

---

# Final Connectivity Verification

After troubleshooting and applying corrections, successful end-to-end communication between PCs was verified.

Ping test used:

```bash
ping 192.168.1.10
```

![Successful Ping](successful-ping.png)

Successful replies confirmed that OSPF routing and LAN communication were fully restored.

---

# Skills Practiced

- OSPF configuration
- OSPF troubleshooting
- Interface troubleshooting
- Neighbor adjacency troubleshooting
- Dynamic route verification
- Gateway troubleshooting
- Cisco IOS verification commands

---

# Verification Commands Used

```bash
show ip interface brief
show ip ospf neighbor
show ip route ospf
show running-config
ping
```
