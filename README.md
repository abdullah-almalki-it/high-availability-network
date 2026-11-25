# High Availability Enterprise Network

Graduation project, Computer Networks Diploma, College of Telecom & Information, Riyadh (11/2026).

A 3-branch enterprise network built on a 3-layer hierarchy (Core / Distribution / Access), with redundant devices and links so traffic keeps flowing when a device or cable fails.

![Network topology](HA_Network_Topology.png)

## Overview

- **Branches:** HQ (Branch A) and two remote branches (R and J), connected through an ISP router
- **Devices:** 10 routers (Cisco 2911), 6 Layer 3 switches (3560-24PS), 6 Layer 2 switches (2960-24TT), 2 access points, 4 servers, 15 end devices
- **Goal:** remove single points of failure and fail over automatically

## Technologies

| Technology | Purpose |
|---|---|
| HSRP | Redundant default gateway per VLAN |
| OSPF | Dynamic internal routing with automatic re-convergence |
| EBGP | Routing exchange with the ISP |
| EtherChannel (PAgP) | Link aggregation between distribution switches |
| PVST+ / Rapid-PVST | Loop prevention, Root Bridge per VLAN |
| 802.1Q Trunking, PortFast | VLAN transport, faster access ports |
| DHCP, NAT | Automatic addressing, Internet access |

## Testing and results

- Ping between branches: 4/4 packets received, 0% loss
- Traceroute: destination reached in 8 hops
- Verified with `show standby brief`, `show etherchannel summary`, `show ip bgp summary`
- Failover tests: cables disconnected and core devices powered off, traffic moved to backup paths automatically

## Problems solved

1. **DHCP not reaching clients** (server on a separate network): fixed with `ip helper-address` on the Layer 3 switch VLAN interfaces
2. **Slow, unstable network** (too many discovery packets): enabled PortFast, tuned OSPF timers, shut down unused ports
3. **Switching loops** from cross-connected links: configured STP and set a Root Bridge per VLAN

## Tools

Cisco Packet Tracer (main build), Huawei eNSP (rebuilt version)

## Future work

Firewalls, IBGP inside the ISP network, AAA and SNMP servers for authentication and monitoring.

## Files

- `Abdullah_Almalki_HA_Network_Project.pdf`: full project summary
- `HA_Network_Topology.png`: network diagram

## Author

Abdullah Almalki, Computer Networks student, Riyadh. HCIA-Datacom certified, CCNA candidate.
