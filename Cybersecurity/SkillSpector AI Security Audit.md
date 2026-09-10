---
title: "SkillSpector AI Security Audit"
created: 2026-09-09
tags:
  - cybersecurity
  - ai-security
  - audit
  - supply-chain
  - agent-security
aliases:
  - SkillSpector Audit
  - AI Agent Vulnerability Audit
type: note
status: complete
---

# SkillSpector AI Security Audit

Comprehensive security analysis and risk categorization of AI agent skills, plugins, and execution permissions across local development environments.

> [!abstract] Threat Landscape
> Autonomous agent workflows grant language models direct tool execution capabilities (filesystem writes, command execution, and MCP server communication). Unvetted or compromised skills expose critical vectors for memory poisoning, prompt injection, and excessive agency.

---

## 1. Audit Summary Statistics

| Metric | Hermes Environment | Antigravity Environment | Cumulative Total |
| :--- | :--- | :--- | :--- |
| **Total Skills Scanned** | 89 | 216 | 305 |
| **Critical Severity** | 13 | 11 | 24 |
| **High Severity** | 11 | 8 | 19 |
| **Medium Severity** | 12 | 27 | 39 |
| **Clean / Low Risk** | 51 | 168 | 219 |

---

## 2. Primary Vulnerability Vectors Identified

### A. MCP Rug Pulls & Least Privilege Violations
Skills requesting broad Model Context Protocol (MCP) tool access allow malicious servers to redefine available endpoints post-handshake, bypassing static configuration controls.

### B. Memory Poisoning & Agent Snooping
Subagents and shared session memory stores lack strict process isolation boundaries, enabling persistent instruction overrides across unrelated user workflows.

### C. Analysis Evasion & Prompt Injection
Unsanitized external inputs (such as scraped web pages or repository metadata) inject hidden system instructions that manipulate autonomous execution loops.

---

## 3. Hardening Guidelines

1. **Explicit Permission Scoping**: Restrict shell and disk write capabilities to designated workspace paths only.
2. **Deterministic Sandboxing**: Enforce sandbox containers for unverified third-party tools.
3. **Session Memory Validation**: Periodically purge and audit persistent cross-session memory files.

---

## Related Notes
- [[Cybersecurity MOC]]
- [[Hardware Security Keys - FIDO2 & WebAuthn]]
- [[Cloud Architecture & Delivery Models]]
