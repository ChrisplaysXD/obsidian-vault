---
tags: [session, serpantinum, quickshell, git, memory]
date: 2026-09-28
parent: "[[Living]]"
---

# Session Note — 2026-09-28

- Up: [[Living]]

## Date & Context
Monday, 28 September 2026 (WIB, UTC+07:00). Session conducted on CachyOS KDE + Hyprland (MSI GF63, i7-9750H, GTX 1650 Ti).

## What We Wanted To Do
- Confirm the recent serpantinum custom changes were pushed to the user's fork (`ChrisplaysXD/serpantinum-modded`).
- Build a new branch (`serpantinum-custom`) and push backed-up custom files (`quickshell-overview.qml`, `shell.qml`, `Main.qml`).
- Apply the same updates to the running local setup (`/home/chrisplaysxd/.local/share/serpantinum/`).
- Update the fork's README.md install URL and the `install/install.sh` default `REPO_SLUG` to point to the fork.
- Save today's session note in the Obsidian vault following the three-tier memory structure (Memory/Living/, Memory/Daily/, Memory/Archive/).

## What We Did To Make It
1. Cloned fork to `/home/chrisplaysxd/Projects/Web/serpantinum-fork/`.
2. Created branch `serpantinum-custom`; pushed custom files (`quickshell-overview.qml`, `shell.qml`, `Main.qml`) as commit `186d6d0`.
3. Updated README.md install URL to `https://raw.githubusercontent.com/ChrisplaysXD/serpantinum-modded/serpantinum-custom/install/install.sh` (commit `b05214c`).
4. Updated `install/install.sh` default `REPO_SLUG` from `ilyamiro/serpantinum` to `ChrisplaysXD/serpantinum-modded` (commit `3f1528d`).
5. Merged upstream `master` (`9f0e36b`, v2.1.9) into `serpantinum-custom` — clean, zero conflicts.
6. Initialized git in `.local/share/serpantinum/`, linked to the fork branch (`serpantinum-custom`), and applied the 3 custom files safely (full pull blocked by ~500 untracked installed assets; selective checkout used instead). Committed (`da25ae7`).
7. Created this session note in `Memory/Living/` and updated `Memory/Daily/Daily.md` timeline.

## Constraints & Rules Followed
- `.hypr` / `hyprland-dots` not accessed (user constraint from persistent memory).
- Changes to shell made only in `/home/chrisplaysxd/.local/share/serpantinum/` (per standing instruction).
- Planning session protocol: show final PRD, wait for user response before starting any project (per memory).
- Web project default directory: `/home/chrisplaysxd/Projects/Web/` (per memory).
- Token-saver model rules: manual triggers preferred; chat/free = longer engaging responses; coding/paid = ponytail full + caveman lite ON.

## What To Do To Prevent Future Recurrence
- Always check upstream divergence before claiming "21 changes"; confirm with `git log --oneline` against installed version.
- Separate upstream updates from local custom files by tracking them explicitly in the clone branch, not mixing them with installed assets.
- When pulling to `.local/share/serpantinum/`, use selective file checkout (`git checkout origin/branch -- <files>`) rather than full merge to avoid overwriting installed fonts/assets.
- Before applying the external `quickshell-overview.qml` URL content (`https://github.com/Shanu-Kumawat/quickshell-overview/blob/main/quickshell-overview.qml`), verify the fetched content against the local backup before replacing.

## Unresolved / Pending
- The external `quickshell-overview.qml` content from the unreachable GitHub URL was never pasted/provided by the user; the pushed and local versions remain the local backup (Sep 25 02:58, 1804 bytes).
