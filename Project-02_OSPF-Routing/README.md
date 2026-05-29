# Project 02 - OSPF Routing Troubleshooting Lab

## Objective
Configure and troubleshoot OSPF routing between three Cisco routers using EVE-NG and Cisco IOS.

## Technologies Used
- OSPF
- IPv4 Addressing
- Cisco IOS CLI
- EVE-NG
- VPCS
- Troubleshooting

---

# Network Topology

![Topology](topology.png)

Three routers were connected in a triangle topology with separate LAN networks connected to Router 1 and Router 2.

---

# Initial Issue - Interface Down

One router interface was administratively down causing OSPF adjacency failure.

![Interface Down](interface-down-issue.png)

### Verification Command

```bash
show ip interface brief
