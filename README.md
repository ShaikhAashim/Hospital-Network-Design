# Hospital Network Design – Cisco Packet Tracer

A simulated hospital network connecting six departments through VLANs, inter-VLAN routing, and extended ACLs.

## Topology

Hierarchical star topology:

- **Router0 (Cisco 2911)** connects to the central switch through an 802.1Q trunk on `G0/0`.
- **Central switch (Cisco 2960)** connects to six departmental switches.
- Each departmental switch connects its department's wired devices. The Nurse switch connects to a wireless Access Point for the tablets.

### Device Roles

| Device | Role |
|---|---|
| 1 × Cisco 2911 router | Provides default gateways and inter-VLAN routing using router-on-a-stick. |
| 1 × central Cisco 2960 switch | Aggregates departmental switches and carries VLAN traffic to the router. |
| 6 × departmental Cisco 2960 switches | Connect and isolate devices in their respective department VLANs. |
| 1 × Wireless Access Point | Connects Nurse tablets wirelessly to VLAN 30. |
| End devices | Admin: 2 PCs; Doctor: 1 laptop and 1 printer; Nurses: 2 tablets; ICU: 2 PCs; Laboratory: 2 PCs; Pharmacy: 2 PCs and 1 printer. |

## Departments & VLANs

| Department | VLAN | Network | Gateway |
|---|---:|---|---|
| Admin | 10 | `192.168.10.0/24` | `192.168.10.1` |
| Doctor | 20 | `192.168.20.0/24` | `192.168.20.1` |
| Nurses | 30 | `192.168.30.0/24` | `192.168.30.1` |
| ICU | 40 | `192.168.40.0/24` | `192.168.40.1` |
| Laboratory | 50 | `192.168.50.0/24` | `192.168.50.1` |
| Pharmacy | 60 | `192.168.60.0/24` | `192.168.60.1` |

## Technologies Used

- Cisco Packet Tracer
- VLANs and IEEE 802.1Q trunking
- Router-on-a-stick inter-VLAN routing
- Wireless Access Point
- Extended IPv4 ACLs

## ACL Security Policy

- Block Admin → ICU and Admin → Laboratory.
- Block ICU → Admin.
- Block Laboratory → Admin.
- Permit other IP traffic unless matched by a deny rule.

## Verification

- `ping` — test inter-department connectivity.
- `show vlan brief` — verify VLAN assignments.
- `show interfaces trunk` — verify trunking.
- `show ip interface brief` and `show ip route` — verify router interfaces and routes.
- `show access-lists` — verify ACL rules and match counters.

## ACL Demo

1. From Admin PC, ping the ICU PC (`192.168.40.11`) before applying ACLs.
2. Apply the ACL policies on the router subinterfaces.
3. Repeat the ping to demonstrate that Admin → ICU traffic is blocked.
4. From the Doctor laptop, ping the ICU PC to demonstrate that permitted clinical traffic still works.

## Project File

Open the `.pkt` file in Cisco Packet Tracer to inspect the topology and run the simulation.
