# Office VLAN Network — Router-on-a-Stick Design

**Status: In progress.** Topology is built and cabled; VLAN, trunk, and inter-VLAN routing configuration is in progress.

A small-office network design in Cisco Packet Tracer, applying VLSM subnetting to a router-on-a-stick topology — one router handling inter-VLAN routing for four departments through a single trunked link, instead of a dedicated physical interface per department.

## Topology

- 1x Router (2911) — `GigabitEthernet0/0`, split into four sub-interfaces (one per VLAN)
- 1x Switch (2960-24TT) — `FastEthernet0/1` as the 802.1Q trunk to the router
- 4x PC, one per department, each on its own VLAN and access port

## Addressing Plan

Base network `192.168.10.0/24`, sized by VLSM to each department's host count:

| Department | VLAN | Subnet | Mask | Gateway |
|---|---|---|---|---|
| Sales | 10 | 192.168.10.0/26 | 255.255.255.192 | 192.168.10.1 |
| HR | 20 | 192.168.10.64/27 | 255.255.255.224 | 192.168.10.65 |
| IT | 30 | 192.168.10.96/28 | 255.255.255.240 | 192.168.10.97 |
| Finance | 40 | 192.168.10.112/29 | 255.255.255.248 | 192.168.10.113 |

## Progress So Far

- [x] Devices placed and cabled (router, switch, 4 PCs)
- [x] VLANs created and named on the switch
- [x] Access ports assigned to each VLAN
- [x] Trunk port configured between switch and router
- [x] Router sub-interfaces configured (encapsulation + IP addressing)
- [x] PC IP configuration (static or DHCP) set per department
- [ ] Inter-VLAN connectivity verified (ping between departments)
## Why Router-on-a-Stick

Rather than giving the router one physical interface per department (expensive and doesn't scale), this design uses 802.1Q VLAN tagging over a single trunk link, with the router's sub-interfaces each handling one VLAN's traffic and acting as that VLAN's gateway.

## Author

Built by Nassif — CompTIA Network+ (N10-009) and Cisco CCNA-style hands-on practice project.
