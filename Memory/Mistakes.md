# MISTAKES.md — Mistake Log

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
RULE: Record every mistake/failure with root cause + prevention reference. Format: 'This prevented XYZ, as documented in MISTAKES.md.'

---
GRAPH CONNECTION: See [[Attachments/vault_graph.svg]] for vault node/edge visualization. Memory folders (Living/Daily/Archive) link to main vault graph.
