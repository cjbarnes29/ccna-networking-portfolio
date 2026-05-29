# Project 02 - OSPF Routing Troubleshooting Lab

## Objective
Configure and troubleshoot OSPF routing between three Cisco routers using EVE-NG.

## Technologies Used
- OSPF
- IPv4 Addressing
- Cisco IOS CLI
- EVE-NG
- VPCS
- Troubleshooting

---

# Network Topology

![Topology](screenshots/topology.png)

---

# Initial Issue - Interface Down

One router interface was administratively down causing OSPF adjacency failure.

![Interface Down](screenshots/interface-down-issue.png)

### Verification Command

```bash
show ip interface brief
