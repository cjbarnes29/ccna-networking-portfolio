# Project 04 - ACL Security Configuration and Troubleshooting

## Project Overview

This project demonstrates the configuration, verification, and troubleshooting of Cisco Extended Access Control Lists (ACLs).

The objective was to control traffic between two separate LAN networks while learning how ACL placement, direction, and rule configuration affect packet forwarding.

Several intentional configuration mistakes were introduced and later corrected to simulate real-world network troubleshooting scenarios.

---

## Topology

![Topology](01-topology.png)

---

## Network Diagram

```text
PC1 ---- SW1 ---- R1 -------- R2 ---- PC2
                 |            |
          192.168.10.0   192.168.20.0
```

---

## IP Addressing

| Device | Interface | IP Address |
|----------|----------|----------|
| PC1 | Eth0 | 192.168.10.10/24 |
| R1 | G0/0 | 192.168.10.1/24 |
| R1 | G0/2 | 10.0.12.1/30 |
| R2 | G0/0 | 10.0.12.2/30 |
| R2 | G0/1 | 192.168.20.1/24 |
| PC2 | Eth0 | 192.168.20.10/24 |

---

## Technologies Used

- Cisco IOSv Routers
- Ethernet Switching
- Static Routing
- Extended ACLs
- ICMP Filtering
- EVE-NG
- VPCS

---

## Skills Demonstrated

- Extended ACL Configuration
- ACL Placement Best Practices
- ACL Direction (Inbound vs Outbound)
- Traffic Filtering
- ICMP Control
- Troubleshooting ACL Errors
- Verification and Testing

---

# Step 1 - Verify Base Connectivity

Before implementing ACLs, connectivity between PC1 and PC2 was verified.

### Successful Ping Test

![Successful Ping](02-base-successful-ping.png)

### Explanation

At this stage, routing was fully operational.

PC1 successfully reached PC2 through R1 and R2, confirming:

- Correct IP addressing
- Proper static routing
- Functional Layer 3 connectivity

---

# Step 2 - ACL Applied in Wrong Direction

An Extended ACL was created and applied in the wrong direction.

### Configuration Error

![Wrong ACL Direction](03-wrong-acl-direction.png)

### Verification

![Wrong Direction Verification](04-show-run-wrong-direction.png)

### Result

![Ping Still Works](05-ping-still-works.png)

### Explanation

Although the ACL contained the correct deny statement, it was applied in the wrong direction.

Because of the incorrect placement, packets were not filtered as intended and communication continued successfully.

This is one of the most common ACL mistakes made by beginners.

---

# Step 3 - Correct ACL Direction

The ACL was removed and reapplied in the proper direction.

### Correct Configuration

![Correct ACL Direction](06-correct-acl-direction.png)

### Result

![Ping Blocked](07-ping-blocked-by-acl.png)

### Explanation

After correcting the ACL direction, ICMP traffic from PC1 to PC2 was successfully blocked.

The ACL now processed packets at the correct point in the traffic flow.

---

# Step 4 - Missing Permit Statement

The ACL was modified to remove the permit statement.

### Configuration Error

![Missing Permit Statement](08-acl-missing-permit-any.png)

### Explanation

Every ACL contains an implicit:

```cisco
deny ip any any
```

at the end.

When the permit statement was removed, traffic that was not explicitly permitted was automatically denied.

This demonstrates the importance of understanding the implicit deny rule.

---

# Step 5 - ACL Corrected

The ACL was updated with a permit statement.

### Correct ACL

![ACL With Permit](09-acl-with-permit-any.png)

### Explanation

The ACL now contained:

```cisco
access-list 100 permit ip any any
```

allowing all traffic not explicitly denied.

This restored expected network behavior.

---

# Step 6 - Incorrect Source Address

An ACL entry was created using an incorrect source IP address.

### Configuration Error

![Wrong Source IP](10-wrong-source-ip-acl.png)

### Result

![Ping Still Works](11-ping-still-works-wrong-source.png)

### Explanation

The ACL referenced an IP address that did not belong to PC1.

Because the ACL never matched the actual traffic, packets continued to pass through the router.

This demonstrates why accurate source and destination addresses are critical in ACL design.

---

# Step 7 - Correct Source Address

The ACL was corrected using the actual PC1 address.

### Correct Configuration

![Correct Source Address](12-correct-source-ip-fix.png)

### Result

![Final ACL Block](13-final-acl-block-ping.png)

### Explanation

After correcting the source address, the ACL successfully matched the traffic and blocked ICMP packets between PC1 and PC2.

---

# Final Verification

The final configuration was verified using Cisco IOS commands.

### Verification Commands

```cisco
show access-lists
show run interface g0/0
show ip route
```

### Output

![Verification](14-verification-commands.png)

### Verification Results

The final checks confirmed:

- ACL 100 was configured correctly
- ACL 100 was applied inbound on G0/0
- Static routes were present
- ACL match counters increased during testing
- ICMP traffic was successfully filtered

---

# Key Lessons Learned

- Extended ACLs should be placed close to the source.
- ACL direction is critical for proper traffic filtering.
- Every ACL contains an implicit deny statement.
- Incorrect source or destination addresses can prevent ACLs from matching traffic.
- Verification commands are essential for troubleshooting.
- Testing before and after changes helps validate ACL operation.

---

# Conclusion

This project successfully demonstrated the implementation and troubleshooting of Cisco Extended ACLs.

Through multiple troubleshooting scenarios, I gained practical experience with ACL placement, direction, traffic filtering, verification commands, and real-world troubleshooting techniques commonly used by network engineers.
