---
phase: 03-user-guide-content
plan: 04
subsystem: ui
tags: [mkdocs, czech, documentation, preview, validation, pdf-export, rebar]

# Dependency graph
requires:
  - phase: 03-02
    provides: parametry.md with anchor slugs for cross-linking
  - phase: 03-03
    provides: otvory.md, trminky.md, diagonaly.md (sibling pages in same section)
provides:
  - docs/pruvodce/preview.md — inline dock and standalone Preview výztuže window guide
  - docs/pruvodce/validace.md — Grafická validace výztuže window guide with reality mode
  - docs/pruvodce/pdf-export.md — PDF/PNG/Print export from validation window
affects: [phase-04-reference-content, phase-05-screenshots, phase-06-integration-qa]

# Tech tracking
tech-stack:
  added: []
  patterns:
    - "Preview vs validation distinction: preview=planned rebar (before generate), validation=actual Tekla model rebar (after generate)"
    - "Layer legend with Tekla class numbers (Class 3/6/7/8/9/11) used in validace.md"
    - "Export workflow always preceded by layer visibility adjustment tip"

key-files:
  created:
    - docs/pruvodce/preview.md
    - docs/pruvodce/validace.md
    - docs/pruvodce/pdf-export.md
    - docs/assets/screenshots/preview-inline-dok.png
    - docs/assets/screenshots/preview-samostatne-okno.png
    - docs/assets/screenshots/preview-panel-heatmapa.png
    - docs/assets/screenshots/validace-okno.png
    - docs/assets/screenshots/validace-vrstvy-legenda.png
    - docs/assets/screenshots/validace-export-tlacitka.png
    - docs/assets/screenshots/pdf-export-vystup.png
  modified: []

key-decisions:
  - "Preview page covers BOTH inline dock (MainWindow right column) and standalone RebarPreviewWindow — per CONTEXT.md locked decision"
  - "Heatmapa (O x delka matice) documented on preview.md, not as separate page — per CONTEXT.md peripheral features decision"
  - "validace.md !!! note admonition explicitly distinguishes validation (real Tekla model) from preview (planned) to prevent user confusion"
  - "pdf-export.md format comparison table added (PDF/PNG/Tisk use cases) — improves scannability for export decision"

patterns-established:
  - "Pattern: !!! note Validation vs Preview admonition — placed immediately after window title explanation"
  - "Pattern: Screenshot placeholder filenames follow content-description format: validace-vrstvy-legenda.png"

requirements-completed: [GUIDE-05, GUIDE-06, GUIDE-07, UX-01, UX-02, UX-03]

# Metrics
duration: 20min
completed: 2026-03-26
---

# Phase 3 Plan 04: Preview, Validace, PDF Export Summary

**Czech wiki guide pages for preview panel (inline dock + standalone window + heatmap), validation window (reality mode, layer legend with Tekla classes), and PDF/PNG/Print export from validation**

## Performance

- **Duration:** ~20 min
- **Started:** 2026-03-26T11:26:00Z
- **Completed:** 2026-03-26T11:46:00Z
- **Tasks:** 2
- **Files modified:** 13 (3 guide pages + 10 screenshot placeholders)

## Accomplishments

- preview.md (98 lines): covers inline dock controls (Vrstvy, Heatmapa, Uprazy delek, Kolize, Sjednotit), standalone Preview výztuže window, layer table, heatmap matrix interaction, length adjustment workflow with collision warning, cross-link to parametry.md
- validace.md (65 lines): covers Grafická validace výztuže window, Skutecna výztuž z Tekla modelu reality mode, layer legend with all 6 Tekla class numbers, Průhlednost slider, Legenda barev expander, interpretation guide, cross-link to preview.md
- pdf-export.md (47 lines): covers Export PDF / Export PNG / Tisk workflow, layer visibility tip, export content description, format comparison table, cross-links to validace.md

## Task Commits

Each task was committed atomically:

1. **Task 1: Write preview.md** - `092da97` (feat)
2. **Task 2: Write validace.md and pdf-export.md** - `c54d0de` (feat)

**Plan metadata:** (docs commit — see below)

## Files Created/Modified

- `docs/pruvodce/preview.md` — inline dock + standalone preview window guide with heatmap section
- `docs/pruvodce/validace.md` — validation window with reality mode, layer legend, class numbers
- `docs/pruvodce/pdf-export.md` — export workflow from validation window
- `docs/assets/screenshots/preview-inline-dok.png` — 1x1 placeholder
- `docs/assets/screenshots/preview-samostatne-okno.png` — 1x1 placeholder
- `docs/assets/screenshots/preview-panel-heatmapa.png` — 1x1 placeholder
- `docs/assets/screenshots/validace-okno.png` — 1x1 placeholder
- `docs/assets/screenshots/validace-vrstvy-legenda.png` — 1x1 placeholder
- `docs/assets/screenshots/validace-export-tlacitka.png` — 1x1 placeholder
- `docs/assets/screenshots/pdf-export-vystup.png` — 1x1 placeholder
- `docs/assets/screenshots/trminky-prapory-segmenty.png` — 1x1 placeholder (Rule 3 fix)
- `docs/assets/screenshots/settings-trminky-prapory.png` — 1x1 placeholder (Rule 3 fix)
- `docs/assets/screenshots/diagonaly-rohy-prostupu.png` — 1x1 placeholder (Rule 3 fix)

## Decisions Made

- Preview page covers both inline dock and standalone window on one page (per CONTEXT.md locked decision — no separate pages)
- Heatmapa documented as a section within preview.md (not its own page)
- Validation !!! note admonition added to explicitly distinguish it from preview at the top of the page
- pdf-export.md format comparison table (PDF/PNG/Tisk) added at discretion for better scannability

## Deviations from Plan

### Auto-fixed Issues

**1. [Rule 3 - Blocking] Created missing screenshot placeholders for trminky.md and diagonaly.md**
- **Found during:** Task 2 verification (mkdocs build --strict)
- **Issue:** trminky.md and diagonaly.md (written in plan 03-03) referenced 3 screenshot files that were never created as placeholders, causing mkdocs --strict to abort with warnings
- **Fix:** Created 1x1 PNG placeholders: `trminky-prapory-segmenty.png`, `settings-trminky-prapory.png`, `diagonaly-rohy-prostupu.png`
- **Files modified:** 3 new PNG files in docs/assets/screenshots/
- **Verification:** mkdocs build --strict passes with 0 warnings
- **Committed in:** `c54d0de` (Task 2 commit)

---

**Total deviations:** 1 auto-fixed (Rule 3 — blocking build issue from prior plan)
**Impact on plan:** Fix was necessary for mkdocs --strict gate to pass. No scope creep — just missing placeholder PNGs from plan 03-03.

## Issues Encountered

None beyond the auto-fixed blocking issue above.

## User Setup Required

None - no external service configuration required.

## Next Phase Readiness

- All 12 pruvodce/ pages now have substantive content (plans 03-01 through 03-04 complete)
- Phase 4 (reference content) can proceed independently
- Phase 5 (screenshots) has complete placeholder infrastructure — all screenshot references exist as 1x1 PNGs; Phase 5 just replaces them with real screenshots
- Blocker remains: Phase 5 requires access to running Tekla Structures instance with a model

---
*Phase: 03-user-guide-content*
*Completed: 2026-03-26*
