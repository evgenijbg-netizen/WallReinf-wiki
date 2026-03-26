# Phase 2: Navigation Skeleton - Context

**Gathered:** 2026-03-26
**Status:** Ready for planning

<domain>
## Phase Boundary

Define the complete page structure in `mkdocs.yml` with explicit `nav:` config and all stub files created. Establishes the information architecture (guide vs. reference split) before any content is written. No substantive content — only stubs with headings and short descriptions.

</domain>

<decisions>
## Implementation Decisions

### Section Structure
- Top-level navigation uses `navigation.tabs` (already enabled in mkdocs.yml)
- Three main sections via tabs:
  1. **Průvodce** — task-based user guide (linear reading order)
  2. **Reference** — parameter lookup tables
  3. **FAQ** — troubleshooting and common problems
- Home (index.md) stays as landing page outside the tabs

### Guide Pages (docs/pruvodce/)
- `index.md` — Začínáme overview
- `pozadavky.md` — Požadavky (Tekla verze, .NET, OS) [START-01]
- `instalace.md` — Instalace a spuštění pluginu [START-02]
- `pripojeni.md` — Připojení k modelu v Tekle [START-03]
- `zakladni-workflow.md` — Základní workflow (výběr stěny → nastavení → generování) [START-04]
- `parametry.md` — Hlavní parametry (průměry, krytí, rozteče, okrajové pruty) [GUIDE-01]
- `otvory.md` — Otvory a U-pruty kolem otvorů [GUIDE-02]
- `trminky.md` — Třmínky a interakce segmentů [GUIDE-03]
- `diagonaly.md` — Diagonální pruty [GUIDE-04]
- `preview.md` — Preview panel [GUIDE-05]
- `validace.md` — Validační okno [GUIDE-06]
- `pdf-export.md` — PDF export [GUIDE-07]

### Reference Pages (docs/reference/)
- `index.md` — Reference overview
- `parametry.md` — Kompletní tabulka parametrů [REF-01, REF-02, REF-03]

### FAQ Page (docs/)
- `faq.md` — FAQ / Troubleshooting [FAQ-01..04]

### File Naming Convention
- ASCII-only slugs (no diacritics): `trminky.md` not `třmínky.md`
- Lowercase with hyphens for multi-word: `zakladni-workflow.md`
- Czech content inside, ASCII filenames outside

### Stub Content Pattern
- Each stub page has: Czech heading (H1), 1-2 sentence description of what will go there, placeholder sections with H2 headings
- No internal cross-links in stubs (would break `--strict` if targets don't exist yet within the same phase)
- `mkdocs build --strict` must pass after all stubs are created

### Claude's Discretion
- Exact wording of stub descriptions
- Whether to add `toc` depth overrides per page
- Ordering of pages within sections (follow the order listed above)

</decisions>

<canonical_refs>
## Canonical References

**Downstream agents MUST read these before planning or implementing.**

### Navigation Setup
- `.planning/research/ARCHITECTURE.md` — Recommended project structure, nav patterns, Diataxis framework
- `.planning/research/PITFALLS.md` — Feature-based vs task-based structure pitfall
- `mkdocs.yml` — Current nav config (only `- Domů: index.md`), theme features already enabled

### Requirements
- `.planning/REQUIREMENTS.md` — NAV-01 through NAV-06 define acceptance criteria

### Prior Phase
- `.planning/phases/01-infrastructure-and-deploy-pipeline/01-CONTEXT.md` — Site identity, theme settings

</canonical_refs>

<code_context>
## Existing Code Insights

### Reusable Assets
- `mkdocs.yml` — Already has `navigation.tabs`, `navigation.sections`, `navigation.top` features enabled
- `docs/index.md` — Homepage stub exists with Czech content
- `docs/assets/logo.png` — Logo already in place

### Established Patterns
- Czech prose in Markdown files, ASCII slugs in filenames
- `mkdocs build --strict` as quality gate (zero warnings required)
- Bold text references (not hyperlinks) to avoid broken links in `--strict` mode

### Integration Points
- `mkdocs.yml` `nav:` section must be expanded from single entry to full tree
- `docs/index.md` links should be updated to point to actual pages once stubs exist

</code_context>

<specifics>
## Specific Ideas

No specific requirements — open to standard approaches. Page structure follows directly from REQUIREMENTS.md (GUIDE-01..07, START-01..04, REF-01..03, FAQ-01..04).

</specifics>

<deferred>
## Deferred Ideas

None — discussion stayed within phase scope

</deferred>

---

*Phase: 02-navigation-skeleton*
*Context gathered: 2026-03-26 via auto mode*
