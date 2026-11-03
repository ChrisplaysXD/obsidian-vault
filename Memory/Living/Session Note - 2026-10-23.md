# Session Note — 2026-10-23 & 10-29 — Erosion & Dilation Notebook

## Task
Image processing assignment (S5 Cyber_unika): create `Tugas_Erosion_Dilation.ipynb` in
`~/Documents/Cyber_unika/S5/image_processing/erosion-dilation/` applying:
- Binarization (Otsu threshold, inverse polarity: object = white on black)
- Erosion with ellipse / cross / rectangle SE (3x3 & 5x5) -> 6 variants
- Dilation of each erosion result with the same 6 SE variants (erosion->dilation = opening)
- Per-image markdown sections + kesimpulan

## 2026-10-29 Rebuild (current state)
- User asked to rebuild the notebook using ALL 6 images in `gambar-tugas/`
  (3 apples: Glossy/Hollowed/Speckled + squares grid + letter A + letter L).
- Regenerated via `/tmp/kilo/gen_notebook.py` -> `Tugas_Erosion_Dilation.ipynb`
  (12 cells, 14 figures, 0 errors; IMG_DIR = "gambar-tugas"; images also saved to `hasil/`).
- Grid layout: per-image rows (2 x N) to support 6 images (the earlier 2x3 grid broke
  with IndexError when >3 images — recount subplot dims when image count changes).
- Numeric verification: for all 6 images x 6 SE, erosion sum < orig < dilation sum (PASS).
  Confirmed ellipse3 kernel == cross3 kernel (OpenCV identity) — matches kesimpulan note.
- Loose PNGs were removed by user from `material+gambar-20261023/` (zip remains); all
  images now live in `gambar-tugas/`. Do not reference the material folder again.

## Key Decisions
- Used OpenCV `cv2.erode`/`cv2.dilate` with `cv2.getStructuringElement` — stdlib-first per user prefs.
- Otsu auto-threshold with polarity check (`mean > 127` logic flipped) so apples (bright fg on white bg)
  and darker images both segment correctly without manual tuning.
- Per-image markdown sections (5.1–5.3) matching the tugas.odt table layout exactly.
- Verified via `jupyter nbconvert --execute --inplace` + nbformat validation (0 errors, 9 figures).

## Mistake
- Summary grid indexing bug (col 5 out of bounds) — fixed, documented in Mistakes.md.

## Files
- `Tugas_Erosion_Dilation.ipynb` (recreated 2026-10-29, executed, ~3.6MB, 14 figures)
- Images: `gambar-tugas/*.png` (6 photos — the single source of truth)
- `hasil/*.png` (14 exported figures)
- Task spec extracted from `tugas.odt` (OOXML zip + regex text pull)
