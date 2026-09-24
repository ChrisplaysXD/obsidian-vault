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
| **🧠 Memory** | System session logs, active configuration states, daily timeline checkpoints, and failure postmortems. | [[Memory]] |

---

## ⚡ Quick Access & High-Yield Notes

```dataview
TABLE file.folder AS "Folder", tags AS "Tags"
FROM ""
WHERE file.name != "Home" AND !contains(file.name, "MOC") AND file.name != "Memory" AND file.name != "Living" AND file.name != "Daily" AND file.name != "Archive" AND !contains(file.folder, "Attachments") AND !contains(file.folder, "Templates")
SORT file.mtime DESC
LIMIT 12
```

---

## 🏷️ Global Domain Routing
- `#cybersecurity`, `#fido2`, `#cryptography` — [[Cybersecurity MOC]]
- `#networking`, `#comptia` — [[Computer Networks MOC]]
- `#academic`, `#sysadmin`, `#machinelearning` — [[Academic MOC]]
- `#japanese` — [[Japanese Language MOC]]
- `#memory`, `#living`, `#daily`, `#archive`, `#mistakes` — [[Memory]]
