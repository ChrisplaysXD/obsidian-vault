---
tags: [session, usb, ventoy, multi-boot]
---
# Session Note — 2026-09-19

## USB Setup (Terminal-First)
- Device: `/dev/sdc` (29.5G, USB, Alcor `058f:6387`, Generic Flash Disk, serial `E312F9D9`)
- Detection method: `lsblk` + `udevadm` + `blkid` (terminal only, no Python script)
- User preference: terminal commands over Python scripts

## Multi-Boot Setup (Ventoy CLI)
- Tool installed: Ventoy 1.1.17 (`/opt/ventoy/Ventoy2Disk.sh`)
- Method: CLI (`-i /dev/sdc`) with interactive `y` confirmation (via `yes` pipeline, completed asynchronously)
- Partitions created:
  - `/dev/sdc1`: exfat, LABEL=Ventoy (29.5G) — ISO storage
  - `/dev/sdc2`: 32M — Ventoy boot/reserved
- Auto-mounted at: `/run/media/chrisplaysxd/Ventoy`
- Modern interface available: `VentoyGUI.x86_64` / `VentoyWeb.sh`
- No persistent partition (rescue ISOs only: Arch, Ubuntu, Fedora — not yet copied)

## Issues / Notes
- `dmesg` blocked (no permissions)
- Web search blocked (`Firecrawl` 403 — no `FIRECRAWL_API_KEY`)
- Original `flash_detect.py` removed per terminal-first preference
- `VentoyWorker.sh` hang cleaned up after timeout
