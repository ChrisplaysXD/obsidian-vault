---
title: Serpantinum Architecture & Modifications
created: 2026-09-25
tags:
  - serpantinum
  - quickshell
  - architecture
  - living
  - memory
  - cava
  - hyprland
parent: "[[Living]]"
type: reference
status: active
---

# 🐍 Serpantinum Architecture & Modifications

- Up: [[Living]]

## Overview & Directory Topology
Serpantinum operates as the desktop shell environment on top of Hyprland and CachyOS. It is built primarily on Quickshell (Qt6/QML) and orchestrated through bash helper daemons. 

```
~/.local/share/serpantinum/         # Upstream source & core logic
├── bin/
│   ├── serpantinum                # Primary CLI wrapper (serpantinum launch/msg/ipc/reload/kill)
│   └── serpantinumd               # Background daemon manager
└── src/
    ├── scripts/
    │   ├── caching.sh             # Runtime directory resolution (/run/user/1000/serpantinum)
    │   ├── reload.sh              # Dispatches Quickshell IPC forceReload
    │   └── qs_manager.sh          # Workspace & window IPC manager
    └── quickshell/
        ├── Shell.qml              # Root entry point loaded by Quickshell process
        ├── Main.qml               # Root IPC handler ("main" target: forceReload)
        ├── singletons/
        │   ├── audio/
        │   │   ├── MprisController.qml  # [MODIFIED] Active MPRIS player bridge & album palette
        │   │   └── Cava.qml             # Raw stdout CAVA process for bar levels
        │   └── theme/
        │       └── ThemeBackend.qml     # Global color fallback & geometry tokens
        ├── bar/
        │   ├── modules/
        │   │   ├── VisWidget.qml        # [MODIFIED] Top bar CAVA visualizer
        │   │   └── MediaWidget.qml      # Top bar playback info & transport controls
        │   └── sidemodules/
        │       ├── SideVisWidget.qml    # [MODIFIED] Sidebar vertical CAVA visualizer
        │       └── SideMediaWidget.qml  # Sidebar media controls
        └── media/
            └── art_fetch.sh             # [MODIFIED] Album art, Matugen palette, CAVA bridge

~/.config/serpantinum/             # User settings & layout overrides
/run/user/1000/serpantinum/        # Runtime volatile cache (RAM tmpfs)
└── music/
    ├── covers/                    # Hash-keyed artwork and gradient dumps
    │   ├── <hash>_art.jpg
    │   ├── <hash>_blur.png
    │   ├── <hash>_grad.txt        # 3-stop linear-gradient string
    │   └── <hash>_text.txt        # Calculated contrast text color
    ├── last_cava_hash             # Prevents redundant CAVA config rewrites
    └── device_cache.json          # Cached wpctl sink metadata
```

---

## Detailed Modifications

### 1. Cover Art Processing & Gradient Extraction (`src/quickshell/media/art_fetch.sh`)
- **Problem**: Upstream used basic ImageMagick histogram quantization (`convert ... -colors 3`). For dark or muted album art, this dumped near-black hex codes (`#050606`, `#161516`). Cache hits skipped color extraction entirely, locking tracks into old muddy palettes.
- **Modification**:
  - Implemented `get_vibrant_grad()`: Runs `matugen image "$art" -t scheme-vibrant --prefer saturation --source-color-index 0 -j hex --dry-run` to extract high-saturation primary, tertiary, and container tones (`$c1`, `$c2`, `$c3`). Falls back to ImageMagick only if Matugen fails.
  - Added cache validation: When an image exists in `/run/user/1000/serpantinum/music/covers/`, the script checks if `_grad.txt` exists and is non-empty. If missing, it immediately runs `get_vibrant_grad()` instead of bypassing color generation.
  - Generates the gradient format expected by Quickshell: `linear-gradient(45deg, $c1, $c2, $c3, $c1)`.

### 2. Standalone CAVA Color Sync (`src/quickshell/media/art_fetch.sh` & `~/.config/cava/`)
- **Problem**: The switch to Serpantinum reset terminal CAVA to default monochromatic theme colors.
- **Modification**:
  - Split CAVA configuration into a static base (`~/.config/cava/config_base`) and the live target (`~/.config/cava/config`).
  - Added `update_cava_album_colors()` inside `art_fetch.sh`: Whenever a track changes, it reads the vibrant hex codes extracted by Matugen, generates the `[color]` gradient block, merges it with `config_base`, updates `~/.config/cava/config`, and sends `killall -USR1 cava` to reload terminal visualizers on the fly.
  - Tracks `last_cava_hash` in RAM tmpfs to avoid unnecessary disk I/O while playing the same track.

### 3. MPRIS State & Palette Bridge (`src/quickshell/singletons/audio/MprisController.qml`)
- **Problem**: 
  1. `activePlayer` and `isPlaying` inspected `p.isPlaying`. Quickshell's native `Quickshell.Services.Mpris.MprisPlayer` service does not implement an `isPlaying` boolean; it uses `playbackState === MprisPlaybackState.Playing`. Accessing `p.isPlaying` evaluated to `undefined`, making the controller report playback as permanently stopped.
  2. `albumColors` was gated behind `if (!grad || !isPlaying) return def;`. Pausing or brief desyncs dumped the extracted palette back to default mauve.
- **Modification**:
  - Updated player resolution:
    ```qml
    let playing = players.find(p => p && (p.playbackState === MprisPlaybackState.Playing || p.isPlaying));
    ```
  - Updated playback status:
    ```qml
    readonly property bool isPlaying: activePlayer ? (activePlayer.playbackState === MprisPlaybackState.Playing || activePlayer.isPlaying === true) : false
    ```
  - Decoupled `albumColors` from `isPlaying`: As long as a valid track `grad` string exists, `albumColors` returns the 3 extracted palette colors.
  - Added `readonly property color activeAccentColor` for single-color accent consumers.

### 4. Top Bar Visualizer Widget (`src/quickshell/bar/modules/VisWidget.qml`)
- **Problem**: Every bar rectangle hardcoded `ThemeBackend.mauve`. The widget completely ignored playing album art.
- **Modification**:
  - Bound reactive properties:
    ```qml
    readonly property var albumColors: MprisController.albumColors
    readonly property string albumGrad: MprisController.grad
    readonly property bool hasActivePlayer: MprisController.hasActivePlayer
    ```
  - Implemented `getBarColor(idx, total)`: Interpolates smoothly across the 16 bars using a 3-stop gradient between `cols[0]`, `cols[1]`, and `cols[2]`. Falls back to `ThemeBackend.mauve` only when no track is loaded.
  - Wrapped bar color in `Behavior on color { ColorAnimation { duration: 350 } }` for smooth track transitions.

### 5. Sidebar Visualizer Widget (`src/quickshell/bar/sidemodules/SideVisWidget.qml`)
- **Modification**: Mirrored the exact reactive binding, `getBarColor()` interpolation logic, and 350ms color animation onto the vertical visualizer widget.

### 6. Fastfetch Config Recovery
- **Location**: Permanent backup preserved at `~/.local/share/caelestia/fastfetch/config.jsonc`, restored into `~/.config/fastfetch/config.jsonc`.

---

## Operational Commands & Debugging
- **Hot-Reload Quickshell**:
  ```bash
  serpantinum reload
  # Equivalent low-level IPC call:
  quickshell -p /home/chrisplaysxd/.local/share/serpantinum/src/quickshell/Shell.qml ipc call main forceReload
  ```
- **Inspect Live Quickshell Logs**:
  ```bash
  tail -f /run/user/1000/quickshell/by-id/*/log.qslog
  ```
- **Force Re-fetch Active Track Artwork**:
  ```bash
  bash ~/.local/share/serpantinum/src/quickshell/media/art_fetch.sh "$(playerctl metadata mpris:artUrl)" "$(playerctl metadata xesam:title)" "$(playerctl metadata xesam:artist)"
  ```
- **Purge Corrupted/Stale Gradient Cache**:
  ```bash
  rm -f /run/user/1000/serpantinum/music/covers/*_grad.txt
  rm -f /run/user/1000/serpantinum/music/last_cava_hash
  ```
