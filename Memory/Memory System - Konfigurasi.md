---
title: Memory System Configuration
created: 2026-10-05
tags:
  - memory
  - configuration
  - obsidian
  - 3-tier
status: active
type: reference
---

# Memory System — Konfigurasi Baru

## Perubahan

| Komponen | Sebelum | Sesudah |
|---|---|---|
| Hermes `memory.provider` | `holographic` | `none` (built-in / lokal) |
| Holographic fact_store (14 fakta) | Aktif sebagai provider | **Dimatikan** |
| Persistent memory lokal | Tersedia | **Tetap aktif** |
| 3-Tier Obsidian Memory | Tersedia | **Utama** |

## 3 Tier Memory (Obsidian Vault)

- **Tier 1 — Root** (`~/obsidian/Memory/`): `Memory.md`, `Mistakes.md`, `Graph Connection.md`
- **Tier 2 — Living** (`~/obsidian/Memory/Living/`): `Living.md`, `Session Note - YYYY-MM-DD.md`, `Serpantinum Architecture & Modifications.md`
- **Tier 3 — Daily** (`~/obsidian/Memory/Daily/`): `Daily.md` (waypoint + timeline)
- **Archive** (`~/obsidian/Memory/Archive/`): `Archive.md`

## Plugin Hermes yang Relevan

- `obsidian-memory` → AKTIF (menghubungkan Hermes ke vault Obsidian)
- `hermes-memory-store` → AKTIF (`~/.hermes/memory_store.db`, `auto_extract: true` — tetap berjalan tetapi tanpa provider holografis)
- `memory-wiki` → AKTIF
- `hermes-memory-ui` → AKTIF

## Catatan Penting

- `provider: none` berarti Hermes tidak menggunakan plugin memory eksternal (holographic) dan mengandalkan built-in store + konfigurasi lokal.
- Memory lokal (`MEMORY.md`, `USER.md` dalam sistem Hermes) tetap tersedia tanpa intervensi otomatis dari fact_store.
- Pengguna tetap bisa menulis dan membaca dari vault Obsidian secara manual atau melalui plugin `obsidian-memory`.

---
Referensi: `.hermes/config.yaml` (baris 60-61), `~/obsidian/Memory/`
