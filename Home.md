---
title: Knowledge Base Dashboard
created: 2026-09-09
tags:
  - dashboard
  - home
  - index
type: dashboard
status: active
---

# 🌌 Central Knowledge Base

Welcome to your central personal vault. All notes are indexed into cohesive topic clusters, interconnected via bi-directional wikilinks, and tagged for multi-dimensional graph exploration.

---

## 🗺️ Maps of Content (MOCs)

| Domain | Description | Primary Hub Link |
| :--- | :--- | :--- |
| **🛡️ Cybersecurity** | Penetration testing, wireless attacks, cryptography, FIDO2 hardware tokens, and security audits. | [[Cybersecurity MOC]] |
| **🌐 Networking** | CompTIA Network+ certification prep, physical cabling standards, routing protocols, and cloud WANs. | [[Computer Networks MOC]] |
| **🎓 Academics** | University curriculum spanning foundational computer science (Semester 3) and specialized engineering tracks (Semester 5). | [[Academic MOC]] |
| **🎌 Japanese** | Conversational fluency, The Moe Way immersion tracking, JLPT N5-N3 benchmarks, and Renshuu/Anki sync. | [[Japanese Language MOC]] |

---

## ⚡ Quick Access & High-Yield Notes

### Hardware & Security Engineering
- [[Hardware Security Keys - FIDO2 & WebAuthn]] — CTAP2 protocols, DIY RP2040 Pico-FIDO build, Linux `pam_u2f` setup, and physical vs. software threat modeling.
- [[Wi-Fi Security - Deauth & Handshake Capture]] — 802.11 monitor mode, frame deauth injection, 4-way handshake capture, and Hashcat/Aircrack analysis.
- [[Compfest CTF Writeup - Crypto & Forensics]] — Custom totient RSA exploitation via Wiener's continued fractions and packet-time steganography.
- [[SkillSpector AI Security Audit]] — AI agent execution permissions, MCP risks, and prompt injection mitigation.

### Enterprise Infrastructure & Theory
- [[CompTIA Network+ Exam Tips]] — Consolidated cheat sheet spanning OTDR/TDR, PoE standards, BGP, longest prefix match, SASE, and subnetting.
- [[CompTIA Network+ Practice Questions]] — Practice questions covering IPS, OSI layers, troubleshooting methodology, and APIPA.
- [[Network Transmission Media & Cabling]] — Copper standards (UTP/STP), single-mode vs multi-mode fiber propagation, and wireless links.

### University Coursework
- **Semester 3**:
  - [[Data Structures & Algorithms - Fundamentals]] — Linear and non-linear memory taxonomy, algorithm time-space efficiency, and Big-O concepts.
  - [[Computer Architecture & CPU Fetch Cycle]] — Hardware register pipelines (PC, IR, MAR) and instruction fetch-decode-execute phases.
- **Semester 5**:
  - [[Cloud Architecture & Delivery Models]] — IaaS/PaaS/SaaS architectures, scalability vs elasticity, and multi-tenant security principles (includes ![[PRAKTIKUM CHAPTER 2.pdf]]).
  - [[Cloud Computing Overview]] — Course roadmap, virtualization layers, and distributed computing models.
  - [[Data Management & Social Sentiment Analysis]] — Social media sentiment extraction and municipal communication research.
  - [[Digital Image Processing Fundamentals]] — 2D spatial signal sampling, quantization, spatial filtering kernels, and edge detection.
  - [[Enterprise Data Systems Architecture]] — OLTP vs OLAP, data warehousing schemas, and distributed ETL/ELT pipelines.
  - [[Linux System Administration & Automation]] — Systemd service units, PAM security architecture, and POSIX/CoW storage management.
  - [[Machine Learning Foundations & Supervised Learning]] — Supervised vs unsupervised taxonomy, loss function optimization, and validation metrics.

---

## 📊 Dynamic Note Index (Dataview)

```dataview
TABLE type AS "Note Type", status AS "Status", tags AS "Tags"
FROM ""
WHERE file.name != "Home" AND !contains(file.folder, "Attachments")
SORT file.mtime DESC
LIMIT 12
```

---

## 🏷️ Global Tag Index
- `#cybersecurity` — [[Cybersecurity MOC]]
- `#networking` — [[Computer Networks MOC]]
- `#academic` — [[Academic MOC]]
- `#comptia` — [[CompTIA Network+ Exam Tips]]
- `#fido2` — [[Hardware Security Keys - FIDO2 & WebAuthn]]
- `#cryptography` — [[Compfest CTF Writeup - Crypto & Forensics]]
- `#sysadmin` — [[Linux System Administration & Automation]]
- `#machinelearning` — [[Machine Learning Foundations & Supervised Learning]]
- `#japanese` — [[Japanese Language MOC]]
- `#memory` — [[Memory/Graph Connection]]
- `#mistakes` — [[Memory/Mistakes]]
- `#living` — [[Memory/Living]]
- `#daily` — [[Memory/Daily]]
- `#archive` — [[Memory/Archive]]
