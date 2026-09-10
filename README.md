# 🌌 Personal Knowledge Vault & Second Brain

Personal knowledge repository synchronized across desktop and mobile. Built with Obsidian, structured with Maps of Content (MOCs), and tracked under Git version control.

---

## 🕸️ Interactive Knowledge Graph

The graph below visualizes the vault's topological layout rendered via GitHub Mermaid. Solid links represent primary domain hierarchies, while dashed connectors represent active cross-domain bridges between low-level hardware, defensive networking, and computational theory.

```mermaid
flowchart TD
  subgraph Hub ["🌌 Central Nexus"]
    Home["Home Dashboard"]
  end

  subgraph Cyber ["🛡️ Cybersecurity Domain"]
    CMOC["Cybersecurity MOC"]
    HWKey["Hardware Security Keys (FIDO2)"]
    WiFi["Wi-Fi Security (Deauth)"]
    CTF["Compfest CTF (Crypto/Forensics)"]
    Audit["SkillSpector AI Security Audit"]
  end

  subgraph Net ["🌐 Networking Domain"]
    NMOC["Computer Networks MOC"]
    NetTips["CompTIA Network+ Exam Tips"]
    NetQuiz["CompTIA Diagnostic Test"]
    Media["Transmission Media & Cabling"]
  end

  subgraph Acad ["🎓 Academic Coursework"]
    AMOC["Academic MOC"]
    
    subgraph Sem3 ["Semester 3: Core Foundations"]
      DSA["Data Structures & Algorithms"]
      CPU["Computer Architecture & CPU"]
    end
    
    subgraph Sem5 ["Semester 5: Engineering Tracks"]
      Cloud["Cloud Architecture & Overview"]
      DataM["Data Management & Analytics"]
      ImageP["Digital Image Processing"]
      EDS["Enterprise Data Systems"]
      SysAdmin["Linux SysAdmin & Ubuntu Server"]
      ML["Machine Learning Foundations"]
    end
  end

  %% Hierarchical Hub Links
  Home --> CMOC
  Home --> NMOC
  Home --> AMOC

  CMOC --> HWKey
  CMOC --> WiFi
  CMOC --> CTF
  CMOC --> Audit

  NMOC --> NetTips
  NMOC --> NetQuiz
  NMOC --> Media

  AMOC --> DSA
  AMOC --> CPU
  AMOC --> Cloud
  AMOC --> DataM
  AMOC --> ImageP
  AMOC --> EDS
  AMOC --> SysAdmin
  AMOC --> ML

  %% Bi-Directional Cross-Domain Graph Bridges
  HWKey -.->|PAM Auth| SysAdmin
  HWKey -.->|Silicon Registers| CPU
  WiFi -.->|Physical RF| Media
  WiFi -.->|"802.1X Defense"| NetTips
  Cloud -.->|Cloud Peering| NetTips
  CTF -.->|Continued Fractions| DSA
  ImageP -.->|Matrix Tensors| ML
  ImageP -.->|Memory Efficiency| DSA
  DataM -.->|Analytical Warehouses| EDS
  DataM -.->|Classification Models| ML
  Audit -.->|Multi-Tenancy Risk| Cloud

  classDef hub fill:#f59e0b,stroke:#d97706,stroke-width:2px,color:#000;
  classDef cyber fill:#dc2626,stroke:#991b1b,stroke-width:2px,color:#fff;
  classDef net fill:#2563eb,stroke:#1e40af,stroke-width:2px,color:#fff;
  classDef acad fill:#059669,stroke:#065f46,stroke-width:2px,color:#fff;
  classDef sem fill:#7c3aed,stroke:#5b21b6,stroke-width:2px,color:#fff;

  class Home hub;
  class CMOC,HWKey,WiFi,CTF,Audit cyber;
  class NMOC,NetTips,NetQuiz,Media net;
  class AMOC,DSA,CPU acad;
  class Cloud,DataM,ImageP,EDS,SysAdmin,ML sem;
```

---

## 📂 Vault Hierarchy

```text
.
├── Academics/
│   ├── Academic MOC.md
│   ├── Semester 3/
│   │   ├── Computer Architecture & CPU Fetch Cycle.md
│   │   └── Data Structures & Algorithms - Fundamentals.md
│   └── Semester 5/
│       ├── Cloud Computing/
│       ├── Data Management/
│       ├── Enterprise Data System/
│       ├── Image Processing/
│       ├── Machine Learning/
│       └── System Administrator/
├── Attachments/
├── Cybersecurity/
│   ├── Compfest CTF Writeup - Crypto & Forensics.md
│   ├── Cybersecurity MOC.md
│   ├── Hardware Security Keys - FIDO2 & WebAuthn.md
│   ├── SkillSpector AI Security Audit.md
│   └── Wi-Fi Security - Deauth & Handshake Capture.md
├── Home.md
├── Networking/
│   ├── CompTIA Network+ Exam Tips.md
│   ├── CompTIA Network+ Practice Questions.md
│   ├── Computer Networks MOC.md
│   └── Network Transmission Media & Cabling.md
└── Templates/
```

---

## 🔄 Sync Architecture
- **Desktop (CachyOS Linux)**: Native Git engine interfacing with the `obsidian-git` community plugin. Configured to auto-pull on boot and commit changes every 10 minutes.
- **Mobile (Android/iOS)**: `obsidian-git` using isomorphic-git over HTTPS, authenticated via a scoped GitHub Personal Access Token (PAT).
- **Workspace Protection**: `.obsidian/workspace*.json` and local temporary caches are excluded via `.gitignore` to prevent multi-device merge conflicts.
