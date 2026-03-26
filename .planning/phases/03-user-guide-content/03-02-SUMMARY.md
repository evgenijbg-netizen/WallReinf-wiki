---
phase: 03-user-guide-content
plan: 02
subsystem: ui
tags: [mkdocs, czech, documentation, content-authoring]

# Dependency graph
requires:
  - phase: 02-navigation-skeleton
    provides: stub files with H1/H2 skeletons for all 12 pruvodce pages
  - phase: 03-user-guide-content plan 01
    provides: getting-started pages (pozadavky, instalace, pripojeni) and screenshots directory
provides:
  - zakladni-workflow.md — end-to-end wall reinforcement demo page (68 lines)
  - parametry.md — comprehensive parameter hub page for all 3 MainWindow expanders (151 lines)
  - docs/assets/screenshots/ populated with placeholder PNGs for all referenced images
affects:
  - 03-user-guide-content plan 03 (otvory, trminky, diagonaly — these cross-link to parametry.md)
  - 03-user-guide-content plan 04 (preview, validace, pdf-export — these cross-link to zakladni-workflow.md)

# Tech tracking
tech-stack:
  added: []
  patterns:
    - Version badge admonition at top of every page (locked in CONTEXT.md)
    - Screenshot placeholders with Phase 5 capture instructions in italic caption
    - Workflow-oriented prose (explain WHEN and HOW, not just WHAT)
    - Minimal placeholder PNGs in docs/assets/screenshots/ to satisfy mkdocs --strict image validation

key-files:
  created:
    - docs/pruvodce/zakladni-workflow.md
    - docs/pruvodce/parametry.md
    - docs/assets/screenshots/top-bar-nacist-stena.png (placeholder)
    - docs/assets/screenshots/hlavni-dialog-expandery.png (placeholder)
    - docs/assets/screenshots/generovat-stav-steny.png (placeholder)
    - docs/assets/screenshots/poznamka-ke-stene.png (placeholder)
    - docs/assets/screenshots/vyztu-orientace-s1.png (placeholder)
    - docs/assets/screenshots/vyztu-svisle-vodorovna.png (placeholder)
    - docs/assets/screenshots/kryti-a-okraje.png (placeholder)
    - docs/assets/screenshots/detaily-t-spoj.png (placeholder)
    - docs/assets/screenshots/settings-vychozi-hodnoty.png (placeholder)
  modified: []

key-decisions:
  - "Placeholder PNG files (1x1 white pixel) created in docs/assets/screenshots/ — mkdocs --strict validates image paths and aborts with missing files; this is the only way to pass strict mode before Phase 5 screenshots exist"
  - "parametry.md uses workflow-oriented structure (Orientace S1 → Svislá výztuž → Vodorovná výztuž → Lemování → Krytí a okraje → Detaily → Settings) matching the logical setup order, not the raw UI top-to-bottom order"
  - "T-spoj dependency (requires Lemování) documented with !!! warning admonition — critical for user discoverability (Pitfall 6 from RESEARCH.md)"
  - "Settings window coverage on parametry.md only (no own page) — Výchozí hodnoty, Segmentace rastru, Dělení prutu, Normy all documented contextually"

patterns-established:
  - "Screenshot placeholder pattern: ![Alt text](../assets/screenshots/name.png) followed by *[VERZE] — Description. Zachytit: what to capture.*"
  - "Cross-link format: [Prostupy](otvory.md) — relative path within pruvodce/ section"
  - "Collapsible advanced sections: ??? note block for secondary content (Tabulka přesahů)"

requirements-completed: [START-04, GUIDE-01, UX-01, UX-02, UX-03]

# Metrics
duration: 25min
completed: 2026-03-26
---

# Phase 3 Plan 02: zakladni-workflow.md + parametry.md Summary

**End-to-end workflow demo page and comprehensive parameter hub covering all 3 MainWindow expanders with T-spoj dependency warning, Settings defaults tip, and cross-links to all feature pages**

## Performance

- **Duration:** ~25 min
- **Started:** 2026-03-26T10:00:00Z
- **Completed:** 2026-03-26T10:25:00Z
- **Tasks:** 2
- **Files modified:** 11 (2 guide pages + 9 placeholder PNGs)

## Accomplishments

- zakladni-workflow.md: full 68-line end-to-end walkthrough from wall selection through generation to NoteWindow section, with cross-links to pripojeni/parametry/feature pages and 4 screenshot placeholders
- parametry.md: 151-line comprehensive hub covering all 3 expanders (Výztuž, Krytí a okraje, Detaily) and Settings context (Výchozí hodnoty, Segmentace rastru, Dělení prutu, Normy) with T-spoj dependency warning and Výchozí hodnoty tip
- All 9 screenshot placeholder PNGs created in docs/assets/screenshots/ to maintain mkdocs --strict compliance

## Task Commits

Each task was committed atomically:

1. **Task 1: Write zakladni-workflow.md** - `47e391c` (feat)
2. **Task 2: Write parametry.md** - `235762f` (feat)

## Files Created/Modified

- `docs/pruvodce/zakladni-workflow.md` — End-to-end wall reinforcement demo (68 lines)
- `docs/pruvodce/parametry.md` — Comprehensive parameter guide for all 3 expanders + Settings (151 lines)
- `docs/assets/screenshots/*.png` — 9 minimal placeholder PNGs (1x1 pixel, satisfies --strict image validation)

## Decisions Made

- Placeholder PNGs required: mkdocs --strict treats missing image targets as errors (not warnings as RESEARCH.md suggested). Created minimal 1x1 white pixel PNGs for all referenced screenshots.
- parametry.md structure follows logical workflow order rather than raw UI top-to-bottom, starting with Orientace S1 (which affects all subsequent settings) per CONTEXT.md workflow-oriented guidance.
- T-spoj section placed after Okrajové podmínky within Detaily, with prominent !!! warning explaining the Lemování dependency (RESEARCH.md Pitfall 6).

## Deviations from Plan

### Auto-fixed Issues

**1. [Rule 3 - Blocking] Created docs/assets/screenshots/ with minimal placeholder PNG files**
- **Found during:** Task 1 (zakladni-workflow.md verification)
- **Issue:** mkdocs build --strict fails with "target not found among documentation files" for all image references — the screenshots directory was empty and mkdocs validates image paths in strict mode
- **Fix:** Created docs/assets/screenshots/ directory with minimal 1x1 PNG placeholder files for all screenshots referenced across plan 03-01 and 03-02 pages (9 total: 4 from zakladni-workflow.md, 5 from parametry.md)
- **Files modified:** docs/assets/screenshots/*.png (9 files created)
- **Verification:** python -m mkdocs build --strict exits 0
- **Committed in:** 47e391c (Task 1 commit)

---

**Total deviations:** 1 auto-fixed (Rule 3 - blocking build issue)
**Impact on plan:** Auto-fix essential for mkdocs --strict compliance. Placeholder PNGs are intentional design — they will be replaced by real screenshots in Phase 5. No scope creep.

## Issues Encountered

None — both pages written in a single pass, build passed after placeholder PNG creation.

## User Setup Required

None - no external service configuration required.

## Next Phase Readiness

- parametry.md is now the hub page that all feature pages (otvory, trminky, diagonaly) can cross-link to
- zakladni-workflow.md is ready to receive cross-links from index and other pages
- docs/assets/screenshots/ directory exists and pattern is established — plan 03-03 and 03-04 can follow the same placeholder PNG approach
- mkdocs --strict passes cleanly — ready for plan 03-03

---
*Phase: 03-user-guide-content*
*Completed: 2026-03-26*

## Self-Check: PASSED

- [x] docs/pruvodce/zakladni-workflow.md exists (68 lines)
- [x] docs/pruvodce/parametry.md exists (151 lines)
- [x] Commit 47e391c exists (Task 1)
- [x] Commit 235762f exists (Task 2)
- [x] mkdocs build --strict exits 0
