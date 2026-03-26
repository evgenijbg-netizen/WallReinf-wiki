---
phase: 03-user-guide-content
plan: 01
subsystem: documentation
tags: [mkdocs, czech, admonitions, tekla, getting-started]

# Dependency graph
requires:
  - phase: 02-navigation-skeleton
    provides: Stub files for all 12 pruvodce pages with correct H1/H2 structure
provides:
  - Three complete "Getting Started" pages with Czech prose, version badges, admonitions, and screenshot placeholders
  - Screenshots directory with placeholder PNGs and .gitkeep
  - pozadavky.md: Tekla 2025, Windows 10 64-bit, .NET Framework 4.8 requirements
  - instalace.md: File copy install steps + Applications & Components launch workflow
  - pripojeni.md: Test pripojeni verification, Nactani sten workflow, wall navigation and status
affects:
  - 03-02-zakladni-workflow (cross-link target from pripojeni.md)
  - 05-screenshots (placeholder PNGs to be replaced)

# Tech tracking
tech-stack:
  added: []
  patterns:
    - Version badge admonition pattern: !!! info "Verze pluginu: [VERZE]" at top of every page
    - Screenshot placeholder pattern: image syntax + italic caption with capture instructions
    - Bold Czech UI element names matching XAML labels verbatim

key-files:
  created:
    - docs/assets/screenshots/.gitkeep
    - docs/assets/screenshots/pozadavky-tekla-verze.png (1x1 placeholder)
    - docs/assets/screenshots/instalace-slozka.png (1x1 placeholder)
    - docs/assets/screenshots/instalace-spusteni.png (1x1 placeholder)
    - docs/assets/screenshots/pripojeni-nastaveni.png (1x1 placeholder)
    - docs/assets/screenshots/pripojeni-nacist-steny.png (1x1 placeholder)
  modified:
    - docs/pruvodce/pozadavky.md
    - docs/pruvodce/instalace.md
    - docs/pruvodce/pripojeni.md

key-decisions:
  - "Tekla Structures version set to 2025 based on gRPC Tekla Open API reference in csproj PackageReference"
  - ".NET Framework 4.8 confirmed from TargetFramework net48 in WallReinf.csproj"
  - "Placeholder PNGs (1x1 white pixel) created for all screenshot references to allow mkdocs --strict to pass before Phase 5 screenshots exist"
  - "pripojeni.md uses 'Overeni pripojeni' as first H2 (renamed from stub 'Otevreni modelu') to match Settings dialog flow"

patterns-established:
  - "Page template: version badge admonition -> one-line orientation -> H2 sections with numbered workflow steps"
  - "Screenshot caption format: *[VERZE] — [window description]. Zachytit: [what to capture]*"
  - "Admonitions placed at risk/dependency points in workflow, not as generic intros"

requirements-completed: [START-01, START-02, START-03, UX-01, UX-02]

# Metrics
duration: 20min
completed: 2026-03-26
---

# Phase 3 Plan 01: Getting Started Pages Summary

**Three Czech-language "Getting Started" pages with Tekla 2025 + .NET 4.8 requirements, install/launch workflow, connection verification, wall loading, and navigation — all with version badges, admonitions at risk points, and screenshot placeholders.**

## Performance

- **Duration:** ~20 min
- **Started:** 2026-03-26T11:36:07Z
- **Completed:** 2026-03-26T11:56:00Z
- **Tasks:** 1
- **Files modified:** 4 (3 guide pages + .gitkeep + 5 placeholder PNGs)

## Accomplishments

- pozadavky.md: Full page covering Tekla Structures 2025, Windows 10 64-bit, .NET Framework 4.8 — confirmed from csproj TargetFramework net48
- instalace.md: Step-by-step install (copy to applications folder) and launch (Applications & Components panel) workflow with screenshots
- pripojeni.md: Test pripojeni verification flow, Nactani sten with Prefix field, wall navigation (prev/next/select from Tekla), wall status (Hotovo/Ke kontrole/Bez vyztuzne), cross-link to zakladni-workflow.md
- All pages have version badge admonition, at least 2 admonitions each, and bold UI element names matching XAML labels
- mkdocs build --strict passes (placeholder PNGs created for all image references)

## Task Commits

1. **Task 1: Write pozadavky.md, instalace.md, pripojeni.md** - `d071f34` (feat)

## Files Created/Modified

- `docs/pruvodce/pozadavky.md` - System requirements: Tekla 2025, Win 10 64-bit, .NET 4.8
- `docs/pruvodce/instalace.md` - Installation and first launch guide
- `docs/pruvodce/pripojeni.md` - Model connection, wall loading, navigation, and status
- `docs/assets/screenshots/.gitkeep` - Empty marker file for screenshots directory
- `docs/assets/screenshots/pozadavky-tekla-verze.png` - 1x1 placeholder PNG
- `docs/assets/screenshots/instalace-slozka.png` - 1x1 placeholder PNG
- `docs/assets/screenshots/instalace-spusteni.png` - 1x1 placeholder PNG
- `docs/assets/screenshots/pripojeni-nastaveni.png` - 1x1 placeholder PNG
- `docs/assets/screenshots/pripojeni-nacist-steny.png` - 1x1 placeholder PNG

## Decisions Made

- Tekla Structures 2025 specified as minimum version (gRPC Tekla Open API used per csproj PackageReference references)
- .NET Framework 4.8 confirmed from TargetFramework `net48` in WallReinf.csproj
- 1x1 white pixel placeholder PNGs created for all screenshot references — mkdocs --strict treats missing images as warnings that abort the build
- pripojeni.md H2 structure restructured from stub (Otevreni modelu / Vyber steny) to (Overeni pripojeni / Nacteni sten) to match actual plugin Settings workflow

## Deviations from Plan

### Auto-fixed Issues

**1. [Rule 3 - Blocking] Created placeholder PNG images for all screenshot references**
- **Found during:** Task 1 (verification step)
- **Issue:** mkdocs build --strict fails with 9 warnings when PNG files referenced in markdown do not exist on disk. The screenshots directory existed but was empty.
- **Fix:** Created 1x1 white pixel PNG files for all 9 screenshot references across all pruvodce pages (including 4 from zakladni-workflow.md that pre-existed from an earlier commit)
- **Files modified:** docs/assets/screenshots/*.png (5 new files for this plan, 4 already committed from plan 03-02)
- **Verification:** `python -m mkdocs build --strict` exits 0 with no warnings
- **Committed in:** Previously committed by 47e391c; new files for this plan not needing separate commit (tracked already)

---

**Total deviations:** 1 auto-fixed (Rule 3 - blocking)
**Impact on plan:** Required for build verification gate. No scope creep — placeholder PNGs are intentional phase 3 output.

## Issues Encountered

- zakladni-workflow.md (committed in 47e391c) already referenced screenshot PNGs that did not exist. This caused mkdocs --strict to fail. Fixed by creating all placeholder PNGs in one pass.

## User Setup Required

None - no external service configuration required.

## Next Phase Readiness

- Three "Getting Started" pages complete and linkable
- pripojeni.md cross-links to zakladni-workflow.md (plan 03-02, already committed)
- Screenshots directory populated with placeholder PNGs — Phase 5 will replace them
- Ready to proceed to plan 03-03 (parametry.md and feature pages)

---
*Phase: 03-user-guide-content*
*Completed: 2026-03-26*
