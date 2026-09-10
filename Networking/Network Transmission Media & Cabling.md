---
title: Network Transmission Media & Cabling Standards
created: 2026-09-09
tags:
  - networking
  - physical-layer
  - cabling
  - fiber-optics
  - copper
aliases:
  - Transmission Media
  - Cable Standards
type: note
status: complete
---

# Network Transmission Media & Cabling Standards

A structural breakdown of OSI Layer 1 physical mediums: copper cabling, optical fiber wave propagation, and wireless transmission channels.

---

## 1. Copper Media (Electrical Signaling)

Supported Ethernet bandwidth standards span 10 Mbps (10BASE-T), 100 Mbps (Fast Ethernet), 1 Gbps (1000BASE-T), and 10 Gbps (10GBASE-T).

| Cable Category | Description | Primary Pros | Primary Cons |
| :--- | :--- | :--- | :--- |
| **Coaxial** | Copper core with dielectric insulator and woven braided shield (RG-6, RG-59). Largely deprecated for local LANs; retained in DOCSIS broadband. | Higher native shielding than basic wire. | Bulkier, harder to terminate, obsolete for structured switch fabrics. |
| **UTP (Unshielded Twisted Pair)** | 4 twisted pairs relying on differential signaling and twist cancellation to reject crosstalk (Cat5e, Cat6, Cat6a). | Highly flexible, inexpensive, rapid termination (RJ-45). | Vulnerable to external electromagnetic interference (EMI) and radio frequency interference (RFI). |
| **STP (Shielded Twisted Pair)** | Foil or braided metal shielding wrapped around individual pairs and/or the outer sheath. | Exceptional noise rejection in industrial environments. | More rigid, higher unit cost, requires proper equipment grounding to prevent ground loops. |

> [!tip] 100-Meter Distance Limitation
> Standard twisted-pair copper Ethernet is strictly bounded by IEEE standards to a maximum horizontal run of **100 meters** (90 m solid-core horizontal cabling + 10 m total stranded patch leads).

---

## 2. Fiber Optic Media (Lightwave Signaling)

Light pulses travel through silica glass cores via Total Internal Reflection. 

| Spec | Core Diameter | Light Source | Distance Range | Primary Application |
| :--- | :--- | :--- | :--- | :--- |
| **Single-Mode (SMF)** | ~9 µm | Laser Diode (1310 nm / 1550 nm) | Up to 10 km – 40+ km | Telecommunications backbones, long-haul WAN, campus interconnects |
| **Multi-Mode (MMF)** | 50 µm or 62.5 µm | LED / VCSEL (850 nm / 1300 nm) | Up to 300 m – 550 m | Data center switches, SAN arrays, intra-building riser backbones |

> [!abstract] Engineering Tradeoffs
> - **Advantages**: Complete immunity to electromagnetic interference (EMI/RFI), zero electrical ground potential differences, massive bandwidth capacity, and physical security (difficult to passively tap without detection).
> - **Disadvantages**: Fragile bending radii (microbending/macrobending signal loss), higher termination tooling cost, specialized inspection scopes (OTDR).

---

## 3. Wireless Transmission (Electromagnetic Spectrum)

- **Terrestrial Wireless**: Direct microwave or radio frequency propagation (Wi-Fi 802.11, cellular 4G/5G, point-to-point microwave). Offers low latency and dense local bandwidth over short-to-medium line-of-sight paths.
- **Satellite Systems**: High-altitude orbital relays (LEO like Starlink ~550 km, GEO ~35,786 km). Provides global ubiquitous coverage for maritime and remote environments at the cost of higher orbital transit latency and weather-induced attenuation (rain fade).

---

## Related Notes
- [[Computer Networks MOC]]
- [[CompTIA Network+ Exam Tips#Physical Layer & Cabling Standards]]
- [[Wi-Fi Security - Deauth & Handshake Capture]]
- [[Cloud Architecture & Delivery Models]]
