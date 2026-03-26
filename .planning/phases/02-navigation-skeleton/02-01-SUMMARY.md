---
phase: 02-navigation-skeleton
plan: 01
subsystem: ui
tags: [mkdocs, mkdocs-material, navigation, markdown]

# Dependency graph
requires:
  - phase: 01-infrastructure-and-deploy-pipeline
    provides: mkdocs.yml with theme config and navigation.tabs already enabled
provides:
  - Explicit nav: tree in mkdocs.yml covering all 16 entries (home + 12 guide + 2 reference + FAQ)
  - 12 stub pages in docs/pruvodce/ with Czech H1 headings and H2 section placeholders
  - 2 stub pages in docs/reference/ with Czech H1 headings and H2 section placeholders
  - docs/faq.md stub page
  - mkdocs build --strict passing with exit code 0
affects:
  - 03-content-guide
  - 04-reference-content
  - 05-screenshots

# Tech tracking
tech-stack:
  added: []
  patterns: [Czech prose in Markdown files with ASCII-only filenames, stub pages with H1 + 2+ H2 headings for TOC generation, explicit nav: tree (no auto-discovery)]

key-files:
  created:
    - docs/pruvodce/index.md
    - docs/pruvodce/pozadavky.md
    - docs/pruvodce/instalace.md
    - docs/pruvodce/pripojeni.md
    - docs/pruvodce/zakladni-workflow.md
    - docs/pruvodce/parametry.md
    - docs/pruvodce/otvory.md
    - docs/pruvodce/trminky.md
    - docs/pruvodce/diagonaly.md
    - docs/pruvodce/preview.md
    - docs/pruvodce/validace.md
    - docs/pruvodce/pdf-export.md
    - docs/reference/index.md
    - docs/reference/parametry.md
    - docs/faq.md
  modified:
    - mkdocs.yml

key-decisions:
  - "Section index pages (pruvodce/index.md, reference/index.md) listed in nav without a label so MkDocs Material infers the tab label from the H1 heading"
  - "No internal cross-links in stubs to avoid --strict failures before content phases fill in targets"
  - "ASCII-only filenames (trminky.md not trminky-with-diacritics) with Czech content inside files"

patterns-established:
  - "Stub pattern: Czech H1 heading + 1-2 sentence description + 2+ H2 section placeholders for TOC"
  - "Nav pattern: explicit nav: block required, no MkDocs auto-discovery"
  - "Quality gate: mkdocs build --strict must exit 0 before committing"

requirements-completed: [NAV-01, NAV-02, NAV-03, NAV-04, NAV-05, NAV-06]

# Metrics
duration: 2min
completed: 2026-03-26
---

# Phase 02 Plan 01: Navigation Skeleton Summary

**Full MkDocs nav tree with 16 explicit entries, 15 Czech stub pages with H2-based TOC, and mkdocs build --strict passing at exit code 0**

## Performance

- **Duration:** 2 min
- **Started:** 2026-03-26T09:34:38Z
- **Completed:** 2026-03-26T09:36:30Z
- **Tasks:** 2 (1 auto + 1 checkpoint auto-approved)
- **Files modified:** 16

## Accomplishments

- Updated mkdocs.yml nav from single `- Domu: index.md` entry to a 4-tab tree covering 16 pages
- Created 12 stub files in docs/pruvodce/ and 2 in docs/reference/ plus docs/faq.md (15 total)
- All stubs follow Czech H1 + 1-2 sentence description + 2+ H2 placeholders pattern for TOC generation
- mkdocs build --strict exits 0 with zero errors; all filenames are ASCII-only

## Task Commits

Each task was committed atomically:

1. **Task 1: Create nav config and all stub files** - `ac39006` (feat)
2. **Task 2: Verify navigation renders correctly in browser** - checkpoint auto-approved (--auto mode)

**Plan metadata:** pending (docs commit below)

## Files Created/Modified

- `mkdocs.yml` - Updated nav: block from 1 entry to full 4-tab tree with 16 entries
- `docs/pruvodce/index.md` - Pruvodce section overview stub
- `docs/pruvodce/pozadavky.md` - System requirements stub (NAV-01, START-01)
- `docs/pruvodce/instalace.md` - Installation stub (START-02)
- `docs/pruvodce/pripojeni.md` - Model connection stub (START-03)
- `docs/pruvodce/zakladni-workflow.md` - Basic workflow stub (START-04)
- `docs/pruvodce/parametry.md` - Main parameters stub (GUIDE-01)
- `docs/pruvodce/otvory.md` - Openings stub (GUIDE-02)
- `docs/pruvodce/trminky.md` - Stirrups stub (GUIDE-03)
- `docs/pruvodce/diagonaly.md` - Diagonal bars stub (GUIDE-04)
- `docs/pruvodce/preview.md` - Preview panel stub (GUIDE-05)
- `docs/pruvodce/validace.md` - Validation window stub (GUIDE-06)
- `docs/pruvodce/pdf-export.md` - PDF export stub (GUIDE-07)
- `docs/reference/index.md` - Reference section overview stub
- `docs/reference/parametry.md` - Parameters reference stub (REF-01, REF-02, REF-03)
- `docs/faq.md` - FAQ stub (FAQ-01..04)

## Decisions Made

- Section index pages listed in nav without label so MkDocs Material infers the label from the H1 heading
- No internal cross-links in stubs to prevent --strict failures before content phases exist
- ASCII-only filenames with Czech prose inside files (established in Phase 2 context)

## Deviations from Plan

None - plan executed exactly as written.

## Issues Encountered

None. The `mkdocs` binary is not on PATH on this Windows machine; build is invoked via `python -m mkdocs`. The Material for MkDocs informational banner about MkDocs 2.0 is printed to stderr before the build but does not affect the exit code. Build exits 0.

## User Setup Required

None - no external service configuration required.

## Next Phase Readiness

- Information architecture is locked: all file paths, nav order, and section hierarchy are stable
- Phase 3 (content - guide) can begin writing content into docs/pruvodce/ stubs
- Phase 4 (reference content) can begin filling docs/reference/parametry.md tables
- No blockers for content phases

---
*Phase: 02-navigation-skeleton*
*Completed: 2026-03-26*
