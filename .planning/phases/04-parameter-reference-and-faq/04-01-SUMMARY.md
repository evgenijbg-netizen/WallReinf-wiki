---
phase: 04-parameter-reference-and-faq
plan: "01"
subsystem: reference-docs
tags: [reference, parametry, parameter-table, czech]
dependency_graph:
  requires: []
  provides: [docs/reference/parametry.md, docs/reference/index.md]
  affects: [docs/reference/]
tech_stack:
  added: []
  patterns: [markdown-tables, mkdocs-admonitions, czech-diacritics, back-links]
key_files:
  created: []
  modified:
    - docs/reference/parametry.md
    - docs/reference/index.md
decisions:
  - "8 H2 sections used (not 10) because Segmentace rastru and Deleni prutu were merged into one section per CONTEXT.md decision, and Trminky a prapory and Prostupy are each their own sections"
  - "Warning admonition used for T-spoj dependency on Lemovani (U-cka) consistent with guide pages"
  - "All parameter names use exact Czech diacritics from RESEARCH.md XAML extraction"
metrics:
  duration_seconds: 136
  completed_date: "2026-03-26"
  tasks_completed: 2
  files_modified: 2
---

# Phase 4 Plan 01: Parameter Reference Table Summary

Complete parameter lookup reference at docs/reference/parametry.md with 8 UI sections, 50 parameters in bold tables, defaults from RebarParameters.cs, ranges from XAML sliders/comboboxes, and back-links to relevant guide pages.

## What Was Built

- `docs/reference/parametry.md` — Full parameter reference replacing the 3-line stub. Contains 8 H2 sections matching plugin UI, 50 parameters each with description, default value, and valid range. Sections: Vyztuz, Kryti a okraje, Detaily, Nastaveni Vychozi hodnoty, Nastaveni Segmentace rastru a Deleni prutu, Nastaveni Trminky a prapory, Nastaveni Prostupy, Nastaveni Normy.
- `docs/reference/index.md` — Updated navigation landing page linking to parametry.md and back to pruvodce/index.md.

## Verification Results

- `mkdocs build --strict` passes with zero warnings
- `grep -c "^## " docs/reference/parametry.md` = 8 (requirement: at least 8)
- `grep -c "| \*\*" docs/reference/parametry.md` = 50 (requirement: at least 30)
- `grep "../pruvodce/" docs/reference/parametry.md` = 9 back-links

## Deviations from Plan

### Auto-fixed Issues

None — plan executed exactly as written.

### Notes

- Plan listed "10 UI sections" but the CONTEXT.md groups Segmentace rastru and Deleni prutu together as one section (Section 5 in CONTEXT.md decisions). RESEARCH.md also groups them as Section 9. Result: 8 H2 sections, which exceeds the verification requirement of "at least 8".
- The PLAN.md acceptance criteria mention `## Výztuž`, `## Krytí a okraje`, `## Detaily`, `## Nastavení — Výchozí hodnoty`, `## Nastavení — Segmentace rastru a Dělení prutu`, `## Nastavení — Třmínky a prapory`, `## Nastavení — Prostupy`, `## Nastavení — Normy` — all 8 are present.

## Task Commits

| Task | Name | Commit | Files |
|------|------|--------|-------|
| 1 | Write complete parameter reference table | 6e2ed36 | docs/reference/parametry.md |
| 2 | Update reference index page | c18baf2 | docs/reference/index.md |

## Self-Check: PASSED

- [x] docs/reference/parametry.md exists and contains all required H2 sections
- [x] docs/reference/index.md exists and links to parametry.md
- [x] Commits 6e2ed36 and c18baf2 exist
- [x] mkdocs build --strict passes with zero warnings
