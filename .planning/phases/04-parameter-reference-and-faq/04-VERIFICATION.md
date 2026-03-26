---
phase: 04-parameter-reference-and-faq
verified: 2026-03-26T00:00:00Z
status: gaps_found
score: 4/5 must-haves verified
gaps:
  - truth: "All cross-links pass mkdocs build --strict"
    status: partial
    reason: "Four anchor links in docs/faq.md point to headings that do not exist in the target pages. MkDocs logs these as INFO (not WARNING), so the build exits 0, but the links silently land on the page root instead of the intended section."
    artifacts:
      - path: "docs/faq.md"
        issue: "Line 26 links to pruvodce/pripojeni.md#test-pripojeni — no heading with that anchor exists; actual section is '## Ověření připojení' (anchor: overeni-pripojeni)"
      - path: "docs/faq.md"
        issue: "Line 64 links to pruvodce/trminky.md#prahy — no heading with that anchor exists; actual section is '## Prahy v Nastavení' (anchor: prahy-v-nastaveni)"
      - path: "docs/faq.md"
        issue: "Line 90 links to pruvodce/validace.md#obnovit — no heading named 'Obnovit' exists in validace.md"
      - path: "docs/faq.md"
        issue: "Line 102 links to pruvodce/preview.md#kontrola-kolizi — no heading named 'Kontrola kolizí' exists in preview.md"
    missing:
      - "Fix anchor in faq.md line 26: change #test-pripojeni to #overeni-pripojeni"
      - "Fix anchor in faq.md line 64: change #prahy to #prahy-v-nastaveni"
      - "Fix anchor in faq.md line 90: either add '## Obnovit' section to validace.md or remove the anchor and link to pruvodce/validace.md"
      - "Fix anchor in faq.md line 102: either add '## Kontrola kolizí' section to preview.md or remove the anchor and link to pruvodce/preview.md"
---

# Phase 4: Parameter Reference and FAQ — Verification Report

**Phase Goal:** A complete parameter reference table (grouped by UI section, with defaults and ranges) and a FAQ with at least 10 known problems are published, with cross-links connecting guide pages to reference entries and vice versa.
**Verified:** 2026-03-26
**Status:** GAPS FOUND
**Re-verification:** No — initial verification

## Goal Achievement

### Observable Truths

| # | Truth | Status | Evidence |
|---|-------|--------|----------|
| 1 | Parameter reference table lists every plugin parameter with name matching the UI | VERIFIED | docs/reference/parametry.md: 50 bold parameter rows across 8 H2 sections, Czech diacritics matching XAML labels |
| 2 | Every parameter has description, default value, and valid range | VERIFIED | All 50 rows in 4-column tables: Parametr / Popis / Výchozí / Rozsah / Možnosti |
| 3 | Parameters are grouped by UI sections | VERIFIED | 8 H2 sections (CONTEXT.md merged Segmentace and Dělení into one); plan required "at least 8" — satisfied |
| 4 | FAQ page contains at least 10 distinct problems with solutions | VERIFIED | 15 H3 items confirmed: 4 connection, 7 generation, 4 validation — all three required categories present |
| 5 | All cross-links pass mkdocs build --strict | FAILED | Build exits 0 but MkDocs logs 4 broken anchors in faq.md as INFO; the links resolve to page root instead of the intended section |

**Score:** 4/5 truths verified

### Required Artifacts

| Artifact | Expected | Status | Details |
|----------|----------|--------|---------|
| `docs/reference/parametry.md` | Complete parameter lookup table with 8 UI sections | VERIFIED | 116 lines, 8 H2 sections, 50 parameter rows; back-links to 3 guide pages (parametry, trminky, otvory) |
| `docs/reference/index.md` | Updated reference overview linking to parametry.md | VERIFIED | Links to parametry.md and back to pruvodce/index.md |
| `docs/faq.md` | FAQ with 13+ items in 3 categories | VERIFIED | 103 lines, 15 H3 headings, 3 category H2s; BUT 4 anchor links are broken |
| `docs/pruvodce/parametry.md` | Guide page with Viz také section linking to reference | VERIFIED | Viz také at line 153 with 7 links to reference/parametry.md anchors and faq.md |

### Key Link Verification

| From | To | Via | Status | Details |
|------|----|----|--------|---------|
| `docs/pruvodce/parametry.md` | `docs/reference/parametry.md` | Viz také anchor links | WIRED | 6 anchor links: #vyztuz, #kryti-a-okraje, #detaily, #nastaveni-vychozi-hodnoty, #nastaveni-segmentace-rastru-a-deleni-prutu, #nastaveni-trminky-a-prapory |
| `docs/reference/parametry.md` | `docs/pruvodce/parametry.md` | Back-link in each section | WIRED | 6 "Podrobný popis viz" links; plus trminky.md and otvory.md covered |
| `docs/faq.md` | `docs/pruvodce/pripojeni.md` | Inline link in FAQ answer | WIRED | 4 links to pripojeni.md (page-level) |
| `docs/faq.md` | `docs/reference/parametry.md` | Inline anchor link | WIRED | 6 links with verified anchors: #nastaveni-prostupy, #vyztuz, #detaily, #nastaveni-trminky-a-prapory |
| `docs/faq.md` | `docs/pruvodce/pripojeni.md#test-pripojeni` | Anchor link | NOT WIRED | Anchor does not exist; section is "## Ověření připojení" (anchor: overeni-pripojeni) |
| `docs/faq.md` | `docs/pruvodce/trminky.md#prahy` | Anchor link | NOT WIRED | Anchor does not exist; section is "## Prahy v Nastavení" (anchor: prahy-v-nastaveni) |
| `docs/faq.md` | `docs/pruvodce/validace.md#obnovit` | Anchor link | NOT WIRED | No heading named "Obnovit" in validace.md; actual headings: Spuštění validace / Skutečná výztuž / Vrstvy a legenda / Interpretace výsledků |
| `docs/faq.md` | `docs/pruvodce/preview.md#kontrola-kolizi` | Anchor link | NOT WIRED | No heading named "Kontrola kolizí" in preview.md; actual final heading: "## Úpravy délek" |

### Requirements Coverage

| Requirement | Source Plan | Description | Status | Evidence |
|-------------|------------|-------------|--------|----------|
| REF-01 | 04-01 | Tabulka parametrů s názvy odpovídajícími UI pluginu | SATISFIED | 50 bold parameter names in docs/reference/parametry.md with exact Czech diacritics from XAML |
| REF-02 | 04-01 | Každý parametr má popis, výchozí hodnotu a platný rozsah | SATISFIED | All 50 rows have 4 columns: name, description, default, range/options |
| REF-03 | 04-01 | Parametry jsou seskupeny podle sekcí UI | SATISFIED | 8 H2 sections matching plugin dialog groupings (Výztuž, Krytí a okraje, Detaily, 4 Nastavení sub-sections, Normy) |
| FAQ-01 | 04-02 | Minimálně 10 známých problémů s řešením | SATISFIED | 15 distinct FAQ items confirmed by grep: `grep -c "^### " docs/faq.md` = 15 |
| FAQ-02 | 04-02 | FAQ obsahuje problémy s připojením k Tekle | SATISFIED | "## Připojení k Tekla Structures" category with 4 items |
| FAQ-03 | 04-02 | FAQ obsahuje problémy s generováním výztuže | SATISFIED | "## Generování výztuže" category with 7 items |
| FAQ-04 | 04-02 | FAQ obsahuje problémy s validací | SATISFIED | "## Validace" category with 4 items |
| UX-04 | 04-02 | Stránky obsahují křížové odkazy mezi průvodcem a referencí | PARTIAL | Bidirectional links exist but 4 anchor targets in faq.md are broken; links land on page root |

**Orphaned requirements check:** REQUIREMENTS.md Traceability table lists REF-01, REF-02, REF-03, FAQ-01, FAQ-02, FAQ-03, FAQ-04, UX-04 for Phase 4 — all 8 claimed in plan frontmatter. No orphaned requirements.

### Anti-Patterns Found

| File | Line | Pattern | Severity | Impact |
|------|------|---------|----------|--------|
| `docs/faq.md` | 26 | `#test-pripojeni` — anchor does not exist in target | Warning | User clicking link lands on page top instead of "Ověření připojení" section |
| `docs/faq.md` | 64 | `#prahy` — anchor does not exist; section is "Prahy v Nastavení" | Warning | User clicking link lands on page top instead of threshold settings section |
| `docs/faq.md` | 90 | `#obnovit` — no "Obnovit" heading in validace.md | Warning | User clicking link lands on page top; validace.md has no refresh-specific section |
| `docs/faq.md` | 102 | `#kontrola-kolizi` — no such heading in preview.md | Warning | User clicking link lands on page top; preview.md has no collision-check section |

No blocker-level anti-patterns found. The broken anchors are warnings — the FAQ content itself is substantive and correct, and the page-level links function. However, UX-04 requires cross-links to be functional, and anchor links that silently fail are not functional in the UX sense.

### Human Verification Required

#### 1. Parameter Names Match Plugin UI

**Test:** Open the running Wall Reinforcement Wizard plugin and compare section names and parameter labels against docs/reference/parametry.md
**Expected:** Every parameter name in bold matches the label visible in the plugin dialog
**Why human:** Cannot run Tekla Structures in this environment to compare XAML-rendered labels

#### 2. FAQ Anchor Navigation

**Test:** Open docs/faq.md in the built site, click the 4 broken anchor links (test-pripojeni, prahy, obnovit, kontrola-kolizi)
**Expected:** Links either scroll to the correct section or display an error — currently they silently land on page top
**Why human:** Confirms whether users are confused by the silent fallback

### Gaps Summary

The phase delivers all its core content: a complete 50-parameter reference table with 8 UI sections, defaults, ranges, and back-links; a 15-item FAQ covering all three required problem categories; and "Viz také" cross-link sections on all 11 guide pages. The requirements REF-01 through REF-03 and FAQ-01 through FAQ-04 are fully satisfied.

The single gap is in UX-04: four anchor links in docs/faq.md point to section headings that do not exist in their target pages. MkDocs does not treat these as build errors (they are logged as INFO), so the build passes and the SUMMARY reported "zero warnings." However, the links do not navigate users to the intended sections — they land on the page root. The fixes are mechanical: either correct the anchor IDs to match existing headings, or add the missing headings to the target pages.

---

_Verified: 2026-03-26_
_Verifier: Claude (gsd-verifier)_
