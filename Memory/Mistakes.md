---
tags: [mistakes, memory, index]
parent: "[[Memory]]"
---
# MISTAKES.md — Mistake Log

- Up: [[Memory]]

Rule: Every mistake, failure, or unexpected result is recorded here with root cause and prevention.
Future fix reference format: "This prevented XYZ, as documented in MISTAKES.md."

---

## 2026-09-19 — Browser harness timeout on YouTube (first entry)
- Symptom: `TimeoutError` on `capture_screenshot` / `new_tab` with YouTube (`search_query=smii7yplus`).
- Root cause: `browser_harness/_ipc.py` recv blocked; timeout 5.0s too short for dynamic SPAs.
- Fix attempted: increased `timeout=5.0` → `30.0` in `helpers.py` (line 44).
- Result after fix: still fails (`TimeoutError` on recv). Deeper root cause: dynamic page load blocks CDP `Page.captureScreenshot` response.
- Prevention: for YouTube/media automation, avoid `capture_screenshot` on video pages; use static/extract approaches; or switch to cloud anti-bot backend (`browserbase`) instead of free harness.
- Related: web search configured (`searxng` + `tavily`); browser backend switched (`browser-use`, `camofox` tested); harness limitation confirmed.

---

## 2026-09-25 — Quickshell MPRIS property mismatch and stale art cache
- Symptom: Quickshell top bar visualizer (`VisWidget.qml`) stuck on fallback mauve color despite terminal CAVA dynamically switching colors.
- Root cause: `MprisController.qml` queried `p.isPlaying` on `Quickshell.Services.Mpris.MprisPlayer`. The service uses `p.playbackState === MprisPlaybackState.Playing`; `p.isPlaying` returned `undefined` (falsy) causing false playback state. Simultaneously, `art_fetch.sh` skipped color extraction on cache hits, preserving legacy dark ImageMagick histogram colors.
- Fix attempted: Rewrote `MprisController.qml` to evaluate `p.playbackState === MprisPlaybackState.Playing`, decoupled `albumColors` from play/pause state, added `get_vibrant_grad()` with cache fallback in `art_fetch.sh`, bound visualizers to reactive color properties, purged stale `_grad.txt` files, and reloaded via IPC.
- Result after fix: Bars immediately blend across vibrant Matugen-derived album art colors and update in real-time on track change.
- Prevention: Audit Quickshell C++/Qt service types before writing bindings; decouple thematic metadata from transport states; version cache assets so generator updates invalidate obsolete files automatically.

---
RULE: Record every mistake/failure with root cause + prevention reference. Format: 'This prevented XYZ, as documented in MISTAKES.md.'

---
GRAPH CONNECTION: See [[Attachments/vault_graph.svg]] for vault node/edge visualization. Memory folders (Living/Daily/Archive) link to main vault graph.
