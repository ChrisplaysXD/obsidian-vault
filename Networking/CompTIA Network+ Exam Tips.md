---
title: CompTIA Network+ Exam Tips & High-Yield Concepts
created: 2026-09-09
tags:
  - networking
  - comptia
  - exam-prep
  - certification
  - cheat-sheet
aliases:
  - Network+ Exam Tips
  - Network+ Cheat Sheet
type: cheatsheet
status: complete
---

# CompTIA Network+ Exam Tips & High-Yield Concepts

Consolidated exam survival guide organizing core networking principles, hardware diagnostic standards, routing algorithms, and enterprise security policies.

---

## 1. Physical Layer & Cabling Standards

### Cable Testing Tools
- **OTDR (Optical Time-Domain Reflectometer)**: Fiber optic fault location, attenuation measurement, and splice defect identification.
- **TDR (Time-Domain Reflectometer)**: Copper cable break location, impedance mismatches, and distance-to-fault measurements.
- **Wiremap Tester**: Validates copper continuity, pair pairing, shorts, reversals, and split pairs.

### Crossover vs Straight-Through Wiring
- **Crossover Cable**: Swaps transmit and receive pairs (pins 1 & 2 to pins 3 & 6) to connect identical MDI/MDI interfaces (e.g., PC-to-PC, switch-to-switch) prior to Auto-MDIX.
- **Straight-Through Cable**: Identical T568A or T568B pin ordering on both terminations.
- **Rollover Cable**: Flips all pin assignments for direct terminal console access.

### Frame Anomaly Terminology
- **Giants (Jabbers)**: Ethernet frames exceeding standard MTU limits (>1518 bytes or >1522 bytes for 802.1Q tagged frames). Often triggered by incorrect MTU configurations, unsynchronized jumbo frames, or malfunctioning NIC drivers.
- **Runts**: Collision fragments or undersized frames (<64 bytes) dropped immediately by switch hardware.

### Power over Ethernet (PoE) Standards
| Standard | IEEE Spec | PSE Output Power | PD Available Power | Typical Devices |
| :--- | :--- | :--- | :--- | :--- |
| **PoE** | 802.3af | Up to 15.4 W | 12.95 W | Basic VoIP phones, entry-level IoT |
| **PoE+** | 802.3at | Up to 30 W | 25.5 W | Dual-radio APs, pan-tilt cameras |
| **PoE++ (Type 3)**| 802.3bt | Up to 60 W | 51 W | High-throughput Wi-Fi 6/7 APs |
| **PoE++ (Type 4)**| 802.3bt | Up to 100 W | 71.3 W | Digital signage, smart building hubs |

> [!tip] Energy Efficient Ethernet
> IEEE **802.3az** denotes Energy Efficient Ethernet (EEE), reducing power consumption when link channels idle. It is unrelated to device power delivery.

---

## 2. Enterprise & Cloud Architecture

### SASE (Secure Access Service Edge)
Cloud-native architectural model converging software-defined WAN (SD-WAN) with edge security microservices into a unified cloud-delivered stack:
$$\text{SASE} = \text{SD-WAN} + \text{CASB} + \text{SWG} + \text{ZTNA} + \text{FWaaS}$$

### Enterprise WAN: Leased Lines vs. VPN
- **Dedicated Leased Lines (T3/DS3, Metro Ethernet, Dark Fiber)**: Provide guaranteed throughput, deterministic low latency, and binding ISP Service Level Agreements (SLAs).
- **Site-to-Site VPN Over Public Internet**: Cost-effective best-effort transmission subject to public routing congestion, packet jitter, and ISP peering bottlenecks.

### AWS Direct Connect & Cloud Peering
Direct Connect provisions private physical cross-connects between on-premises data centers and cloud VPCs via colocation facilities. It completely circumvents the public internet, delivering predictable throughput and diminished egress data pricing (comparable to Azure ExpressRoute and Google Cloud Interconnect).

### Full-Mesh Topologies
Every node maintains a dedicated point-to-point link with every other participant:
$$\text{Number of Physical Links} = \frac{n(n-1)}{2}$$
For a 5-node cluster: $\frac{5 \times 4}{2} = 10\text{ connections}$. While resilient against multiple concurrent link disruptions, full-mesh implementations scale exponentially in capital expenditure.

### Infrastructure as Code (IaC)
Declarative definitions (Terraform, Ansible, CloudFormation) enforce consistency, reproducibility, Git version control auditability, and automated pipeline deployment across multi-vendor network estates.

---

## 3. Routing, Switching & Protocols

### Longest Prefix Match Rule
Routers select routes based on the highest CIDR prefix length (most specific subnet mask):
- `192.168.5.0/24` supersedes `192.168.0.0/16`
- `192.168.0.0/16` supersedes Default Route `0.0.0.0/0`

### Default Gateway & ARP Resolution
When sending traffic outside the local subnet (determined by bitwise comparison of destination IP and local subnet mask), a host uses ARP to discover the MAC address of its **Default Gateway**, not the final destination. The gateway then strips Layer 2 framing and routes across Layer 3 hops.

### Exterior Gateway Routing (BGP)
Border Gateway Protocol is the global path-vector routing protocol operating between autonomous systems (AS). It applies policy metrics (AS path length, local preference, multi-exit discriminators). All interior routing protocols (OSPF, EIGRP, RIP) operate strictly within an internal AS domain.

### Subnetting Fundamentals: /8 to /12
- Allocated subnet bits: $12 - 8 = 4\text{ bits}$
- Resulting subnets: $2^4 = 16\text{ subnets}$ (e.g., `10.0.0.0/12`, `10.16.0.0/12` ... `10.240.0.0/12`)
- Host addresses per subnet: $2^{32-12} = 2^{20} = 1,048,576\text{ addresses}$

### Device Monitoring (SNMP)
Simple Network Management Protocol queries device agents for CPU utilization, link saturation, and hardware temperatures, while asynchronous **SNMP Traps** dispatch immediate alerts to the Network Management System (NMS) upon threshold crossings.

---

## 4. Network Security & Access Control

### Next-Generation Firewalls (NGFW)
Operate at OSI Layer 7 (Application Layer) performing Deep Packet Inspection (DPI), application signature recognition, TLS/SSL stream interception, and identity-aware threat mitigation, transcending stateless Layer 3/4 port/IP access control lists.

### Port Security & 802.1X Defense
When unauthorized hubs or rogue switches attempt to multiplex multiple MAC addresses onto a single physical switchport, port security restricts the maximum learned MAC table entries. Limiting a port to 1 MAC prevents address spoofing and MITM eavesdropping.

### Demilitarized Zone (DMZ)
An isolated transit perimeter buffered by dual-homed or back-to-back firewalls. Hosts public-facing endpoints (DNS, reverse proxies, web endpoints) while containing external compromises from pivoting into the internal operational network.

### Business Continuity Metrics: RTO vs RPO
- **RTO (Recovery Time Objective)**: The maximum tolerable downtime duration before operations must be restored.
- **RPO (Recovery Point Objective)**: The maximum allowable data loss window measured backwards from an incident.

---

## Related Notes
- [[Computer Networks MOC]]
- [[CompTIA Network+ Practice Questions]]
- [[Network Transmission Media & Cabling]]
- [[Wi-Fi Security - Deauth & Handshake Capture]]
- [[Cloud Architecture & Delivery Models]]
