
# Project 02 - OSPF Routing Troubleshooting

## Project Overview

This project demonstrates OSPF (Open Shortest Path First) routing configuration and troubleshooting using three Cisco routers connected in a triangle topology.

The lab focuses on identifying and fixing common OSPF issues such as:

- Interface shutdown problems
- OSPF area mismatches
- Missing OSPF network advertisements
- Incorrect subnet masks
- Wrong PC default gateway configuration

After troubleshooting, full end-to-end connectivity between PCs was successfully restored.

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

- R1 LAN: 192.168.1.0/24
- R2 LAN: 192.168.2.0/24

Point-to-Point Links:

- 10.0.12.0/30
- 10.0.13.0/30
- 10.0.23.0/30

## Topology Diagram

![Topology](topology.png)

---

# Issues Introduced

The following problems were intentionally configured for troubleshooting practice:

1. R1 G0/1 interface was shutdown
2. R2 had OSPF area mismatch
3. R2 LAN network missing from OSPF
4. PC2 configured with wrong default gateway

---

# Troubleshooting Process

## R1 Interface Shutdown Issue

R1 G0/1 was administratively down which prevented OSPF neighbor adjacency.

### Verification Command

```bash
show ip int br
```

![R1 Shutdown](r1-g0-1-shutdown.png)

Solution applied:

```bash
conf t
interface g0/1
no shutdown
```

---

# OSPF Area Mismatch

R2 was configured with the wrong OSPF area which caused adjacency failure.

### Error Message

![Area Mismatch](ospf-area-mismatch.png)

### Fix Applied

```bash
router ospf 1
no network 10.0.12.0 0.0.0.3 area 1
network 10.0.12.0 0.0.0.3 area 0
```

---

# OSPF Neighbor Verification

After correcting the configuration, OSPF neighbors successfully reached FULL state.

![OSPF Neighbor](ospf-neighbor-restored.png)

---

# Routing Table Verification

OSPF learned routes were verified using:

```bash
show ip route ospf
```

![Routing Table](routing-table.png)

The routing table confirmed that routers successfully learned remote networks dynamically through OSPF.

---

# Wrong Gateway Issue

PC2 initially had the wrong default gateway configured.

![Wrong Gateway](wrong-gateway.png)

Correct gateway configured:

```bash
192.168.2.1
```

---

# End-to-End Connectivity Test

After troubleshooting and verification, successful communication between PCs was restored.

![Successful Ping](successful-ping.png)

Ping test used:

```bash
ping 192.168.1.10
```

This verified successful routing between different LAN networks.

---

# Skills Practiced

- OSPF configuration
- OSPF troubleshooting
- Interface troubleshooting
- Routing verification
- Neighbor adjacency troubleshooting
- Gateway troubleshooting
- Cisco CLI verification commands

---

# Verification Commands Used

```bash
show ip ospf neighbor
show ip interface brief
show ip route ospf
show running-config
ping
```
