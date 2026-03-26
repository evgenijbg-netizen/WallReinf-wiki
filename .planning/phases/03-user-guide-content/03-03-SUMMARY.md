---
phase: 03-user-guide-content
plan: 03
subsystem: docs/pruvodce
tags: [content, guide, openings, stirrups, diagonal-rebar, czech]
dependency_graph:
  requires: [03-02]
  provides: [otvory.md, trminky.md, diagonaly.md]
  affects: [docs/pruvodce/]
tech_stack:
  added: []
  patterns: [MkDocs Material admonitions, pymdownx.details collapsible sections, screenshot placeholders, Czech prose with bold XAML UI labels]
key_files:
  created: []
  modified:
    - docs/pruvodce/otvory.md
    - docs/pruvodce/trminky.md
    - docs/pruvodce/diagonaly.md
    - docs/assets/screenshots/otvory-lemovaci-u-pruty.png
    - docs/assets/screenshots/settings-prostupy.png
    - docs/assets/screenshots/settings-trminky-prapory.png
    - docs/assets/screenshots/trminky-prapory-segmenty.png
    - docs/assets/screenshots/diagonaly-rohy-prostupu.png
decisions:
  - "otvory.md covers all three Settings sections (Prostupy filtry, Generace otvorů, Fiktivní zvětšení otvorů) per CONTEXT.md assignment"
  - "trminky.md documents Třmínky a prapory Settings section with threshold defaults sourced from RebarParameters.cs (StirrupThreshold=300, FlagThreshold=1500)"
  - "diagonaly.md is compact — diagonal feature is controlled by a single CheckBox; diameter is shared with U-bars (no separate field)"
  - "Cross-link from diagonaly.md uses parametry.md#nastaveni-a-vychozi-hodnoty and parametry.md (non-anchored) for shared concepts"
metrics:
  duration_minutes: 5
  completed_date: "2026-03-26"
  tasks_completed: 2
  files_modified: 8
---

# Phase 3 Plan 03: Feature Guide Pages (Otvory, Třmínky, Diagonály) Summary

Three feature guide pages replacing stubs with full Czech prose content, XAML-matched UI terminology, cross-links to parametry.md, admonitions, and screenshot placeholders. Settings window controls are documented on their respective feature pages per CONTEXT.md.

## Tasks Completed

| Task | Name | Commit | Files |
|------|------|--------|-------|
| 1 | Write otvory.md | c42e56c | docs/pruvodce/otvory.md, 2 placeholder PNGs |
| 2 | Write trminky.md and diagonaly.md | 3a8ee62 | docs/pruvodce/trminky.md, docs/pruvodce/diagonaly.md, 3 placeholder PNGs |

## What Was Built

**otvory.md (82 lines):** Full guide for opening detection and reinforcement.
- Opening types: dveřní/okenní otvory, kapsy (neprostupující), výřezy (Beam/slab cutouty)
- Prostupy section in main dialog: Průměr combobox, links to Šikmá výztuž and Třmínky nad dveřmi
- Lemovací U-pruty: dependency on Lemování (U-čka) with warning admonition
- Settings Prostupy: Ignorovat kapsy/výřezy/všechny prostupy with targeted warning
- Settings Generace otvorů: Limit protažení noh U-ček and Odsazení ohybu kotevních prutů
- Settings Fiktivní zvětšení otvorů: H/V sliders with collapsible advanced note

**trminky.md (61 lines):** Guide for stirrups, flags, threshold logic, and segment interaction.
- Třmínky (closed loops) vs. Prapory (L-shaped, Class 9) explained
- Settings Třmínky a prapory: prah třmínku (default 300mm), prah praporu (default 1500mm) from RebarParameters.cs
- Threshold logic documented in !!! note admonition
- Třmínky nad dveřmi CheckBox: overrides threshold logic above door openings
- Warning about inverted thresholds (plugin does not auto-validate)
- Cross-link to parametry.md#segmentace-rastru for segment settings

**diagonaly.md (42 lines):** Compact guide for 45-degree corner diagonal rebar.
- Šikmá výztuž v rozích (45°) CheckBox in Prostupy section
- Placement: all 4 corners, both S1 and S2 layers, 45° angle
- Diameter shared with U-bars from Průměr: field (no separate control)
- Collapsible note: Fiktivní zvětšení does not affect diagonal placement

## Deviations from Plan

### Auto-fixed Issues

**1. [Rule 3 - Missing assets] Created 5 placeholder PNGs for new screenshot references**
- **Found during:** Task 1 and Task 2 — mkdocs build --strict aborted on missing image files
- **Fix:** Created 1x1 pixel white PNG placeholders using Python struct/zlib (same approach as Phase 3 plan 01)
- **Files:** otvory-lemovaci-u-pruty.png, settings-prostupy.png, settings-trminky-prapory.png, trminky-prapory-segmenty.png, diagonaly-rohy-prostupu.png
- **Commit:** Included in task commits c42e56c and 3a8ee62

## Self-Check: PASSED

- FOUND: docs/pruvodce/otvory.md
- FOUND: docs/pruvodce/trminky.md
- FOUND: docs/pruvodce/diagonaly.md
- FOUND: commit c42e56c (feat(03-03): write otvory.md)
- FOUND: commit 3a8ee62 (feat(03-03): write trminky.md and diagonaly.md)
