
# Project 02 - OSPF Routing Troubleshooting Lab

## Objective
Configure and troubleshoot OSPF routing between three Cisco routers using EVE-NG.

## Technologies Used
- OSPF
- IPv4 addressing
- /30 point-to-point links
- Cisco IOS CLI
- EVE-NG
- VPCS

## Topology
Three routers connected in a triangle topology with LAN networks on R1 and R2.

## Troubleshooting Performed
- Found shutdown interface using `show ip interface brief`
- Fixed interface using `no shutdown`
- Verified OSPF adjacency using `show ip ospf neighbor`
- Checked OSPF-learned routes using `show ip route ospf`
- Fixed PC gateway/link issue
- Verified end-to-end connectivity using ping

## Verification Commands
```bash
show ip interface brief
show ip ospf neighbor
show ip route ospf
ping
