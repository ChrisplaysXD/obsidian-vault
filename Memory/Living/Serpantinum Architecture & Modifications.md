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

## Complete Widget & Component Catalog

The visual shell in Serpantinum divides its interface elements across bar containers, floating desktop canvases, popouts, and transient overlays. Every visual module is implemented in QML under `~/.local/share/serpantinum/src/quickshell/`.

### 1. Bar Modules (`bar/modules/`)
Horizontal top bar controls located at `~/.local/share/serpantinum/src/quickshell/bar/modules/`:
- **Media & Audio**:
  - `MediaWidget.qml`: Playback controls, title/artist display, dynamic pill formatting.
  - `VisWidget.qml`: 16-bar audio spectrum visualizer interpolated with Matugen palette colors.
- **Status & Navigation**:
  - `FocusWidget.qml`: Active window title and process tracking.
  - `InfoWidget.qml`: General status info pill.
  - `LeftWidget.qml`: Left bar anchor container.
  - `TrayWidget.qml`: System tray icon host and status notifier item embedder.
  - `WeatherWidget.qml`: Current weather status and temperature badge.
- **Hardware & System Status (`bar/modules/system/`)**:
  - `BatWidget.qml`: Battery state of charge and power profile.
  - `BtWidget.qml`: Bluetooth device pairing and RF status.
  - `KbWidget.qml`: Keyboard layout indicator and switch trigger.
  - `SysMonWidget.qml`: Aggregated CPU, memory, and thermal status pill.
  - `VolWidget.qml`: PipeWire / WirePlumber audio volume and mute state.
  - `WifiWidget.qml`: Wireless connection state and SSID indicator.
- **Time & Date (`bar/modules/timedate/`)**:
  - `TimeDateWidget.qml`: Time/date container supporting interchangeable faces:
    - `faces/BadgeFace.qml`: Compact pill badge display.
    - `faces/ClassicFace.qml`: Traditional digital clock and date readout.
    - `faces/MaterialFace.qml`: Material-inspired multi-tier clock presentation.
- **Workspaces (`bar/modules/workspaces/`)**:
  - `WorkspacesWidget.qml`: Hyprland workspace switcher with dynamic visual modes:
    - `faces/NumbersFace.qml`: Numeric index workspace badges.
    - `faces/PacmanFace.qml`: Pacman-styled animated workspace indicators.
    - `faces/PillsFace.qml`: Pill-shaped active/inactive workspace capsules.

### 2. Sidebar Modules (`bar/sidemodules/`)
Vertical sidebar equivalents located at `~/.local/share/serpantinum/src/quickshell/bar/sidemodules/`:
- `SideBar.qml`: Master vertical shell panel layout.
- `SideMediaWidget.qml`: Vertical media player widget.
- `SideVisWidget.qml`: Vertical 16-bar audio visualizer with dynamic color syncing.
- `SideFocusWidget.qml`: Vertical active window focus badge.
- `SideInfoWidget.qml`: Vertical system info indicator.
- `SideTopWidget.qml`: Sidebar header container.
- `SideTrayWidget.qml`: Vertical system tray.
- `SideWeatherWidget.qml`: Vertical weather indicator.
- **System Submodules (`bar/sidemodules/system/`)**:
  - `SideBatWidget.qml`, `SideBtWidget.qml`, `SideKbWidget.qml`, `SideSysMonWidget.qml`, `SideVolWidget.qml`, `SideWifiWidget.qml`.
- **Vertical TimeDate & Workspaces**:
  - `timedate/SideTimeDateWidget.qml` with faces: `faces/SideBadgeFace.qml`, `faces/SideClassicFace.qml`, `faces/SideMaterialFace.qml`.
  - `workspaces/SideWorkspacesWidget.qml` with faces: `faces/SideNumbersFace.qml`, `faces/SidePacmanFace.qml`, `faces/SidePillsFace.qml`.

### 3. Desktop Canvas Widgets & Faces (`widgets/` & `widgets/faces/`)
Freely positionable desktop widgets and modular face components located at `~/.local/share/serpantinum/src/quickshell/widgets/`:
- **Widget Engine & Lifecycle (`widgets/`)**:
  - `Widget.qml`: Base container handling position, geometry, and layer properties.
  - `WidgetLoader.qml`: Dynamic QML loader instantiating registered desktop widgets.
  - `WidgetRedactor.qml`: On-screen editor for interactive widget dragging, resizing, and styling.
  - `WidgetRegistry.qml`: Catalog mapping widget names to their underlying Face components.
- **Modular Widget Faces (`widgets/faces/`)**:
  - **Clock Faces**:
    - `ClockFaceAnalog.qml`: Classical analog clock with moving hour, minute, and second hands.
    - `ClockFaceDigital.qml`: Big digital time display.
    - `ClockFaceMaterial.qml`: Material You layout clock with stacked hours and minutes.
    - `ClockFaceMaterialAnalog.qml`: Material-styled analog dial.
    - `ClockFaceMaterialLumen.qml`: Lumen luminous styling clock.
    - `ClockFaceMinimal.qml`: Stripped-down minimalist clock face.
  - **Media & Visualizer Faces**:
    - `MusicFace.qml`: Full desktop media card with cover art, progress bar, and metadata.
    - `MusicFaceRound.qml`: Circular album art turntable player.
    - `VisualizerFace.qml`: Standalone desktop audio spectrum visualizer.
    - `VisualizerFaceContinuous.qml`: Continuous wave visualizer for desktop audio rendering.
  - **Hardware Utilization Faces (`widgets/faces/usage/`)**:
    - `CpuFace.qml`: Processor load meter and frequency gauges.
    - `RamFace.qml`: Physical RAM and swap space utilization ring.
    - `DiskFace.qml`: Filesystem storage capacity breakdown.
    - `TempFace.qml`: Thermal sensor monitoring for CPU/GPU.
  - **User & Environment Faces**:
    - `BatteryFace.qml`: Dedicated desktop battery monitor and charging rate gauge.
    - `UserFace.qml`: User profile avatar and hostname presentation.
    - `WeatherFaceCompact.qml`: Small-footprint desktop weather overview.
    - `WeatherFaceFull.qml`: Multi-day desktop weather forecast widget.
    - `WeatherFaceRound.qml`: Circular gauge weather widget.
    - `ImageFaceRect.qml`, `ImageFaceRound.qml`, `ImageFaceRounded.qml`: Custom wallpaper/photo frames for desktop decoration.

### 4. Overlays, Popups, and Floating Shell Panes
Floating panels and transient popouts triggered via bar clicks, keybindings, or IPC:
- **Popouts & Menus**:
  - `calendar/CalendarPopup.qml`: Interactive calendar modal triggered from the date widget.
  - `media/MusicPopup.qml`: Detailed MPRIS media player popout.
  - `network/NetworkPopup.qml`: Wi-Fi scanning, connection selector, and VPN manager.
  - `volume/VolumePopup.qml`: Per-application audio mixer and PipeWire output sink router.
  - `popouts/Osd.qml`: On-screen display for volume, brightness, and mute changes.
  - `popouts/PopoutManager.qml`: Central manager coordinating popout positions and auto-dismissal.
  - `popouts/SideMusicPopout.qml`: Dedicated side-anchored music popout.
  - `popouts/TrayBase.qml`: Generic flyout frame for system tray context items.
- **Full Shell Panels & Overlays**:
  - `launcher/Launcher.qml`: Full application launcher and command prompt.
  - `clipboard/Clipboard.qml`: Clipboard history manager and quick-paste picker.
  - `dock/Dock.qml`: Floating application dock.
  - `lock/Lock.qml` & `lock/VideoLock.qml`: Lock screen implementations with live video background support.
  - `idle/Idle.qml`: Screen dimmer and inactivity lock trigger.
  - `polkit/Polkit.qml` & `polkit/PolkitService.qml`: Privilege escalation authentication dialog.
  - `screenshot/ScreenshotOverlay.qml`: Region and window screenshot selection overlay.
  - `syspanel/SystemPanel.qml`: Central control center quick-settings panel.
- **Quickactions Floating Utilities (`quickactions/` & `quickactions/actions/`)**:
  - `quickactions/Floating.qml`: Window frame hosting floating utility widgets.
  - `actions/Dock.qml`: Quickaction dock switch.
  - `actions/DrawAction.qml`: Screen annotation and whiteboard drawing canvas.
  - `actions/SystemUsage.qml`: Detailed live resource usage inspector.
  - `actions/Timer.qml`: Floating stopwatch and countdown timer.
- **Notification Daemon (`notifications/`)**:
  - `notifications/NotificationManager.qml`: Global notification listener and priority dispatch.
  - `notifications/NotificationPopups.qml`: Toast popup container rendered on screen.
  - `notifications/NotificationCenter.qml`: Historic notification tray and action center.
  - `notifications/Notification.qml`: Individual notification card delegate.
  - `notifications/types/`: Specialized notification delegates (`Default.qml`, `Screenshot.qml`, `Update.qml`, `Weather.qml`).
- **Wallpaper System (`wallpaper/`)**:
  - `wallpaper/WallpaperEngine.qml`: Desktop background renderer supporting static images and live shaders.
  - `wallpaper/WallpaperPicker.qml`: Visual wallpaper selector and theme trigger.

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

### 7. Idle Lockscreen Floating Media Card (`src/quickshell/lock/Lock.qml`)
- **Context & Design**: Restored the Android 14/15-styled floating media pill card anchored below `clockModule` during the idle lockscreen state.
- **Dynamic Offset**: When `isMediaActive` is true, `clockModule.anchors.verticalCenterOffset` smoothly animates from centered (`-40 * s`) upward to `-130 * s` to make room for `mediaModule`. When password input opens (`screenRoot.inputActive = true`), both the clock and media card animate out to reveal `mainDashboardShell`.
- **Visuals & CAVA Synchronization**:
  - Outlined with dynamic beat-pulsing ambient glow driven by `Cava.barLevels`.
  - Background container features heavily blurred album art masked with `MultiEffect` to eliminate corner bleeding beyond the 26px rounded border.
  - Interactive squiggly waveform canvas oscillating on active playback with seek-scrubbing support.
  - 4-bar mini CAVA equalizer and responsive playback controls (`Previous`, `Play/Pause`, `Next`).
  - Automatically activates and tears down `Cava.registerConsumer()` / `Cava.unregisterConsumer()` based on lock state and active playback.

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
