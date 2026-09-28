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

## 2026-09-28 — Incorrect upstream divergence claim + blocked full pull to installed directory
- Symptom: User stated "there's 21 changes made to the main repo"; `git rev-list --count master..serpantinum-custom` showed 1 custom commit (`186d6d0`). Attempted full `git pull` into `/home/chrisplaysxd/.local/share/serpantinum/` blocked by ~500 untracked installed assets (fonts, sounds, bin scripts) — a full merge would have overwritten them.
- Root cause: Divergence was not verified with `git log --oneline --graph` before merging; installed `.local/share/serpantinum/` contains package assets that don't exist in the clean repo (`src/assets/fonts/`, `sounds/`, etc.), making full pull unsafe.
- Fix attempted: Switched to selective file checkout (`git checkout origin/serpantinum-custom -- <files>`) pulling only the 3 changed files (`Main.qml`, `quickshell-overview.qml`, `shell.qml`). Confirmed installed version (`2.1.9` / `9f0e36b`) == upstream master.
- Result after fix: Custom files applied safely to running setup; no asset loss; git initialized and tracked in `.local/share/serpantinum/`.
- Prevention: Before any pull to installed directory, run `git diff master..branch --stat` to confirm divergence count; if installed assets exist, never use full merge — use selective checkout or initialize a separate clone and copy only changed source files. Verify upstream divergence claims with `git rev-list --count` rather than assumption. This prevented asset loss, as documented in MISTAKES.md.
- Related: Fork branch `serpantinum-custom` pushed; session note `Session Note - 2026-09-28` saved; external `quickshell-overview.qml` URL content still unreached (user selected "provide content" but never pasted it).

---
RULE: Record every mistake/failure with root cause + prevention reference. Format: 'This prevented XYZ, as documented in MISTAKES.md.'

---
GRAPH CONNECTION: See [[Attachments/vault_graph.svg]] for vault node/edge visualization. Memory folders (Living/Daily/Archive) link to main vault graph.
