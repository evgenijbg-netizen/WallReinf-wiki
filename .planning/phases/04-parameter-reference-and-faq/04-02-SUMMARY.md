---
phase: 04-parameter-reference-and-faq
plan: "02"
subsystem: documentation
tags: [faq, cross-links, viz-take, mkdocs]
dependency_graph:
  requires: [04-01]
  provides: [FAQ-01, FAQ-02, FAQ-03, FAQ-04, UX-04]
  affects: [docs/faq.md, docs/pruvodce/*.md]
tech_stack:
  added: []
  patterns: [bidirectional-cross-links, viz-take-sections, verified-anchor-ids]
key_files:
  created:
    - docs/faq.md
  modified:
    - docs/pruvodce/parametry.md
    - docs/pruvodce/otvory.md
    - docs/pruvodce/trminky.md
    - docs/pruvodce/diagonaly.md
    - docs/pruvodce/pripojeni.md
    - docs/pruvodce/zakladni-workflow.md
    - docs/pruvodce/preview.md
    - docs/pruvodce/validace.md
    - docs/pruvodce/pdf-export.md
    - docs/pruvodce/pozadavky.md
    - docs/pruvodce/instalace.md
decisions:
  - "FAQ anchors verified from generated HTML before writing cross-links — Czech diacritics stripped predictably: Připojení → pripojeni-k-tekla-structures, Generování → generovani-vyztuze, Validace → validace"
  - "Reference anchors also verified from HTML: Výztuž → vyztuz, Krytí a okraje → kryti-a-okraje, Detaily → detaily, Nastavení-Třmínky → nastaveni-trminky-a-prapory, Nastavení-Prostupy → nastaveni-prostupy"
  - "pozadavky.md and instalace.md added to Viz take scope (not in original cross-link map) — relevant to FAQ connection issues, improves discoverability"
metrics:
  duration: 10
  completed_date: "2026-03-26"
  tasks_completed: 2
  files_modified: 12
---

# Phase 4 Plan 02: FAQ and Cross-Links Summary

**One-liner:** FAQ with 15 items in 3 categories plus verified bidirectional Viz také sections on all 11 guide pages, zero build warnings.

## Tasks Completed

| Task | Name | Commit | Files |
|------|------|--------|-------|
| 1 | Write FAQ page with 15 problems and solutions | 62b5a0c | docs/faq.md |
| 2 | Add Viz také cross-link sections to all guide pages | c2655fb | 11 guide pages in docs/pruvodce/ |

## Verification Results

- `grep -c "^### " docs/faq.md` → **15** (exceeds 13 minimum)
- `grep -c "## Viz tak" docs/pruvodce/*.md` → **11 guide pages** (exceeds 9 minimum)
- `grep -l "reference/parametry.md" docs/pruvodce/*.md` → **5 guide pages** with parameter reference links
- `grep -c "pruvodce/" docs/faq.md` → **15** links from FAQ to guide pages
- `grep -c "pruvodce/" docs/reference/parametry.md` → **9** links from reference to guide pages
- `mkdocs build --strict` → **0 warnings, 0 errors**

## FAQ Structure

**Připojení k Tekla Structures (4 items — FAQ-02):**
- Plugin hlásí "Tekla není spuštěna"
- "Nelze připojit k Tekle" při testu připojení
- Status po "Test připojení" zůstává "Neověřeno"
- Dropdown Stěna je po kliknutí Načíst prázdný

**Generování výztuže (7 items — FAQ-03):**
- Generovat přepíše existující výztuž
- U-pruty kolem prostupů se negenerují
- T-spoj (závlače) je zašedlý
- Plugin generuje příliš mnoho třmínků nebo praporů
- Prah praporu nastavený níže než Prah třmínku
- Orientace S1 — průměry přiřazeny k opačné vrstvě
- Diagonální pruty a U-pruty mají stejný průměr

**Validace (4 items — FAQ-04):**
- Validační okno je prázdné
- Validační okno neodpovídá aktuálnímu stavu modelu
- PDF export selhal s chybou
- Po úpravě délek v preview se pruty kříží s okraji nebo otvory

## Deviations from Plan

### Auto-added items

**1. [Rule 2 - Missing coverage] Added pozadavky.md and instalace.md to Viz také scope**
- **Found during:** Task 2
- **Issue:** Cross-Link Map in RESEARCH.md did not include pozadavky.md and instalace.md, but both pages directly discuss Tekla connection requirements where connection FAQ is relevant
- **Fix:** Added `## Viz také` section to both pages linking to `faq.md#pripojeni-k-tekla-structures`
- **Files modified:** docs/pruvodce/pozadavky.md, docs/pruvodce/instalace.md
- **Result:** Total 11 guide pages with Viz také (up from 9 in the cross-link map)

## Self-Check: PASSED

- `docs/faq.md` exists and contains 15 H3 headings
- `62b5a0c` commit found in git log
- `c2655fb` commit found in git log
- All 11 guide pages contain `## Viz také`
- `mkdocs build --strict` passes with zero warnings
