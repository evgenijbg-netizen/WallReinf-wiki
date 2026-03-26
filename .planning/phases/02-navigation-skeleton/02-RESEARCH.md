# Phase 2: Navigation Skeleton - Research

**Researched:** 2026-03-26
**Domain:** MkDocs Material navigation configuration — explicit nav tree, stub file creation, --strict build
**Confidence:** HIGH

<user_constraints>
## User Constraints (from CONTEXT.md)

### Locked Decisions

**Section Structure**
- Top-level navigation uses `navigation.tabs` (already enabled in mkdocs.yml)
- Three main sections via tabs: Průvodce, Reference, FAQ
- Home (index.md) stays as landing page outside the tabs

**Guide Pages (docs/pruvodce/)**
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

**Reference Pages (docs/reference/)**
- `index.md` — Reference overview
- `parametry.md` — Kompletní tabulka parametrů [REF-01, REF-02, REF-03]

**FAQ Page (docs/)**
- `faq.md` — FAQ / Troubleshooting [FAQ-01..04]

**File Naming Convention**
- ASCII-only slugs (no diacritics): `trminky.md` not `třmínky.md`
- Lowercase with hyphens for multi-word: `zakladni-workflow.md`
- Czech content inside, ASCII filenames outside

**Stub Content Pattern**
- Each stub page has: Czech heading (H1), 1-2 sentence description of what will go there, placeholder sections with H2 headings
- No internal cross-links in stubs (would break `--strict` if targets don't exist yet within the same phase)
- `mkdocs build --strict` must pass after all stubs are created

### Claude's Discretion
- Exact wording of stub descriptions
- Whether to add `toc` depth overrides per page
- Ordering of pages within sections (follow the order listed above)

### Deferred Ideas (OUT OF SCOPE)
None — discussion stayed within phase scope
</user_constraints>

<phase_requirements>
## Phase Requirements

| ID | Description | Research Support |
|----|-------------|-----------------|
| NAV-01 | Site má explicitní nav: konfiguraci v mkdocs.yml (ne auto-discovery) | `nav:` key syntax verified; explicit tree prevents alphabetical auto-sort |
| NAV-02 | Navigace je rozdělena na dvě sekce: Průvodce (task-based) a Reference | Tab-per-section pattern with `navigation.tabs` already enabled in mkdocs.yml |
| NAV-03 | Sidebar navigace zobrazuje všechny sekce a podsekce | `navigation.sections` already enabled; sub-pages under section index auto-expand |
| NAV-04 | Každá stránka má on-page TOC (table of contents) | TOC is on by default in Material; H2 headings in each stub create TOC entries |
| NAV-05 | Breadcrumbs jsou viditelné na každé stránce | Enabled implicitly by `navigation.tabs` + `navigation.sections`; no extra config needed |
| NAV-06 | Soubory používají ASCII slugy (žádné české znaky v názvech souborů) | All stub filenames are ASCII-only per locked decisions |
</phase_requirements>

---

## Summary

Phase 2 is purely a structural operation: expand `mkdocs.yml` `nav:` from one entry to a full three-tab tree and create all 16 stub files. No library installation or tooling decisions are needed — the infrastructure from Phase 1 is complete and verified. The current `mkdocs.yml` already has `navigation.tabs`, `navigation.sections`, and `navigation.top` enabled, which satisfies NAV-03 and NAV-05 without additional config changes.

The critical constraint is `mkdocs build --strict`. This flag promotes warnings to errors, meaning every file listed in `nav:` must exist on disk, and no internal cross-links can point to pages that don't exist yet. Stubs therefore must not contain Markdown links — bold text references are the safe alternative established in Phase 1.

The tab-based navigation with `navigation.tabs` means each top-level `nav:` entry that contains sub-pages renders as a tab in the header. The landing page (`index.md`) listed as a flat top-level entry will render as a tab too unless handled carefully — it should be listed first without sub-pages.

**Primary recommendation:** Write `nav:` in mkdocs.yml first, then create stub files in the order they appear in `nav:`. Run `mkdocs build --strict` after all files exist to validate.

---

## Standard Stack

### Core

| Component | Version | Purpose | Why Standard |
|-----------|---------|---------|--------------|
| mkdocs.yml `nav:` | MkDocs 1.6.1 | Explicit navigation tree controlling sidebar and tab order | Auto-discovery sorts alphabetically and cannot be relied on for linear user guides |
| MkDocs Material `navigation.tabs` | 9.7.6 | Renders top-level `nav:` sections as header tabs | Already enabled in Phase 1; creates the three-tab layout |
| MkDocs Material `navigation.sections` | 9.7.6 | Renders sub-sections as collapsible groups in sidebar | Already enabled in Phase 1; no change needed |
| `mkdocs build --strict` | MkDocs 1.6.1 | Treats warnings as errors; validates all `nav:` file paths exist | Quality gate that makes broken structure impossible to ship |

### How `navigation.tabs` Works with the Nav Tree

When `navigation.tabs` is enabled, MkDocs Material renders each top-level `nav:` entry that contains child pages as a tab. Top-level entries that are single pages (like `Domů: index.md`) render as standalone tabs without dropdowns.

The three-tab layout requires the nav tree to be structured as:

```yaml
nav:
  - Domů: index.md          # standalone tab → landing page
  - Průvodce:               # tab with sidebar sub-items
    - pruvodce/index.md
    - ...sub-pages...
  - Reference:              # tab with sidebar sub-items
    - reference/index.md
    - ...sub-pages...
  - FAQ: faq.md             # standalone tab → single page
```

"Domů" and "FAQ" will appear as tabs in the header. Clicking "Domů" loads index.md. Clicking "Průvodce" loads pruvodce/index.md and activates the guide sidebar. This matches the locked three-tab decision (Průvodce, Reference, FAQ) with the homepage outside the tabs.

---

## Architecture Patterns

### Recommended File Structure After Phase 2

```
docs/
├── index.md                  # Homepage (Phase 1, unchanged)
├── faq.md                    # FAQ stub (new in Phase 2)
├── pruvodce/
│   ├── index.md              # "Začínáme" overview stub
│   ├── pozadavky.md          # Stub
│   ├── instalace.md          # Stub
│   ├── pripojeni.md          # Stub
│   ├── zakladni-workflow.md  # Stub
│   ├── parametry.md          # Stub
│   ├── otvory.md             # Stub
│   ├── trminky.md            # Stub
│   ├── diagonaly.md          # Stub
│   ├── preview.md            # Stub
│   ├── validace.md           # Stub
│   └── pdf-export.md         # Stub
└── reference/
    ├── index.md              # Reference overview stub
    └── parametry.md          # Reference stub
```

Total new files: 15 (14 stubs + 1 existing `docs/index.md` which may need a link update)

### Pattern 1: Complete nav: Tree

**What:** Every page must appear in `nav:`. MkDocs Material with `navigation.sections` uses the section index file (e.g., `pruvodce/index.md`) as the click target for the tab itself.

**When to use:** Always when using explicit nav; required for `--strict` to pass if pages exist on disk.

**Example:**
```yaml
# Source: https://squidfunk.github.io/mkdocs-material/setup/setting-up-navigation/
nav:
  - Domů: index.md
  - Průvodce:
    - pruvodce/index.md
    - Požadavky: pruvodce/pozadavky.md
    - Instalace: pruvodce/instalace.md
    - Připojení k modelu: pruvodce/pripojeni.md
    - Základní workflow: pruvodce/zakladni-workflow.md
    - Hlavní parametry: pruvodce/parametry.md
    - Otvory: pruvodce/otvory.md
    - Třmínky: pruvodce/trminky.md
    - Diagonální pruty: pruvodce/diagonaly.md
    - Preview panel: pruvodce/preview.md
    - Validační okno: pruvodce/validace.md
    - PDF export: pruvodce/pdf-export.md
  - Reference:
    - reference/index.md
    - Parametry: reference/parametry.md
  - FAQ: faq.md
```

Note: The section index pages (`pruvodce/index.md`, `reference/index.md`) are listed WITHOUT a label — MkDocs infers the label from the H1 heading of the file. This is standard Material practice.

### Pattern 2: Stub File Structure

**What:** Each stub has exactly: H1 title (Czech), one or two sentences describing what the page will contain, and H2 headings as section placeholders.

**When to use:** Every new page in this phase.

**Why no cross-links:** `mkdocs build --strict` fails on broken Markdown links. Stubs for pages that will be written in Phase 3/4 must not link to each other. Bold text references are safe (Phase 1 established pattern).

**Example stub — pruvodce/pozadavky.md:**
```markdown
# Požadavky

Tato stránka popisuje systémové požadavky pro spuštění pluginu Wall Reinforcement Wizard.

## Tekla Structures

## Operační systém

## .NET Framework
```

**Example stub — reference/index.md:**
```markdown
# Reference

Referenční část obsahuje kompletní přehled všech parametrů pluginu s jejich výchozími hodnotami a platnými rozsahy.

## Obsah reference
```

### Pattern 3: Section Index Pages

**What:** `pruvodce/index.md` and `reference/index.md` serve as the "landing page" for each tab. When a user clicks the tab, they see this overview page.

**When to use:** Whenever a nav section has multiple sub-pages (as both Průvodce and Reference do).

**Content for section index stubs:** H1 name, 1-2 sentence overview, brief list of what pages are in the section (as plain text, not hyperlinks).

### Anti-Patterns to Avoid

- **Adding cross-links in stubs:** Any `[text](../other-page.md)` in a stub will cause `mkdocs build --strict` to fail if that page has a typo in the path or was not created yet. Use bold text only: `**Průvodce funkcemi**`.
- **Omitting a page from nav:** If a `.md` file exists in `docs/` but is not listed in `nav:`, MkDocs Material will warn about it. With `--strict`, this becomes an error. Create stubs and add them to nav in the same commit.
- **Using Czech characters in filenames:** `třmínky.md` would produce URLs with percent-encoded characters. `trminky.md` is the correct slug.
- **Duplicate nav labels:** If two entries share the same display label within a section, the sidebar renders both but it looks confusing. Keep labels unique within each section.

---

## Don't Hand-Roll

| Problem | Don't Build | Use Instead | Why |
|---------|-------------|-------------|-----|
| Breadcrumbs on every page | Custom Jinja2 partial | `navigation.tabs` + `navigation.sections` (already enabled) | Material renders breadcrumbs automatically from nav tree depth |
| Table of contents | Custom HTML or JS | Material's built-in TOC (H2/H3 in Markdown) | TOC is auto-generated from heading hierarchy; no config needed |
| Page-ordering logic | Custom sort script | Explicit `nav:` in mkdocs.yml | The nav order IS the page order; no runtime logic required |
| Strict link validation | Custom linter | `mkdocs build --strict` | Built-in; treats broken links as build errors |

**Key insight:** Every navigation feature required by NAV-01 through NAV-06 is already provided by the MkDocs Material features enabled in Phase 1. Phase 2 is purely content-structure work, not configuration work.

---

## Common Pitfalls

### Pitfall 1: File Created But Not in Nav

**What goes wrong:** A `.md` file exists in `docs/` but is absent from the `nav:` key. MkDocs emits a warning ("Documentation file 'X' is not in the 'nav' configuration"). With `--strict`, this is a build error.

**Why it happens:** Files are created in the wrong order — file first, nav entry forgotten.

**How to avoid:** Write the complete `nav:` tree in `mkdocs.yml` first, then create the files to match. The build will fail with "file not found" until the stub exists, which is the correct failure mode — it tells you which files still need to be created.

**Warning signs:** Build passes locally but `--strict` fails in CI.

### Pitfall 2: Section Index Listed WITH a Label

**What goes wrong:** Writing `- Průvodce: pruvodce/index.md` (flat entry) instead of a section block causes the section to appear as a flat tab with no sub-pages visible in the sidebar.

**Why it happens:** Confusing the syntax for a flat entry vs. a section entry.

**How to avoid:** A section that has sub-pages must be written as:
```yaml
- Průvodce:
  - pruvodce/index.md        # no label — uses H1 from file
  - Label: pruvodce/page.md  # sub-pages have labels
```
NOT as:
```yaml
- Průvodce: pruvodce/index.md  # this is a flat page, no sub-pages
```

### Pitfall 3: Cross-Links in Stubs Break --strict

**What goes wrong:** `docs/index.md` currently uses bold references to sections ("**Začínáme**", "**Průvodce funkcemi**") precisely to avoid this. If stubs use `[text](../page.md)` Markdown links and any path has a typo, `--strict` fails.

**Why it happens:** Natural to write "see [Instalace](instalace.md)" when thinking ahead to Phase 3 content.

**How to avoid:** No Markdown links in stub pages. Use bold text only. Links will be added in Phase 3/4 when content is written.

### Pitfall 4: Mismatched Nav Label vs. H1

**What goes wrong:** The nav label in `mkdocs.yml` says "Třmínky" but the H1 in `trminky.md` says "Třmínky a interakce segmentů". The browser tab title and the sidebar label are different, which looks inconsistent.

**Why it happens:** Nav labels are often shortened for space; page H1 is the full descriptive title.

**How to avoid:** This is acceptable and normal — nav labels should be short, H1 can be longer. But be intentional about it. Sidebar label = short navigation name. H1 = full descriptive title.

### Pitfall 5: docs/index.md Link Update

**What goes wrong:** The existing `docs/index.md` uses bold text references ("**Začínáme**", etc.) because the target pages did not exist at Phase 1. After Phase 2 creates all stub files, those references could be converted to proper links. However, converting them in Phase 2 is optional and possibly premature — the content pages (Phase 3) may rename H2 sections.

**How to avoid:** Leave `docs/index.md` bold-text references as-is in Phase 2. Update to proper links in Phase 3 once page structure is stable.

---

## Code Examples

### Complete nav: Configuration

```yaml
# Source: locked decisions from 02-CONTEXT.md + MkDocs Material nav docs
nav:
  - Domů: index.md
  - Průvodce:
    - pruvodce/index.md
    - Požadavky: pruvodce/pozadavky.md
    - Instalace: pruvodce/instalace.md
    - Připojení k modelu: pruvodce/pripojeni.md
    - Základní workflow: pruvodce/zakladni-workflow.md
    - Hlavní parametry: pruvodce/parametry.md
    - Otvory: pruvodce/otvory.md
    - Třmínky: pruvodce/trminky.md
    - Diagonální pruty: pruvodce/diagonaly.md
    - Preview panel: pruvodce/preview.md
    - Validační okno: pruvodce/validace.md
    - PDF export: pruvodce/pdf-export.md
  - Reference:
    - reference/index.md
    - Parametry: reference/parametry.md
  - FAQ: faq.md
```

### Stub Template (generic)

```markdown
# [Czech Title]

[1-2 sentence description of what this page will contain when written in Phase 3/4.]

## [Section Heading 1]

## [Section Heading 2]

## [Section Heading 3]
```

### Build Verification Command

```bash
# Run from repo root after all stubs are created
mkdocs build --strict

# Expected: "INFO - Documentation built successfully." with zero warnings
# Failure modes: "ERROR - Config value: 'nav'. Error: The following pages exist in the docs
#   directory, but are not included in the 'nav' configuration" — means a file was created
#   but not added to nav, or a nav entry references a file that doesn't exist yet.
```

---

## State of the Art

| Old Approach | Current Approach | Impact for Phase 2 |
|--------------|------------------|--------------------|
| Auto-discovery (no `nav:` key) | Explicit `nav:` key | Must define every page; correct approach per NAV-01 |
| Flat docs/ directory | Subdirectories by section | pruvodce/ and reference/ subdirectories already decided |
| `mkdocs build` without --strict | `mkdocs build --strict` | Zero-warning requirement; broken file paths are build errors |

---

## Open Questions

1. **"Domů" tab visibility with navigation.tabs**
   - What we know: `navigation.tabs` renders top-level nav entries as tabs. A flat entry (`- Domů: index.md`) renders as a tab. Clicking it loads index.md.
   - What's unclear: Whether a "Domů" tab next to "Průvodce", "Reference", "FAQ" is the desired visual. Some sites omit the home page from tabs and rely on the logo click.
   - Recommendation: Include it as `- Domů: index.md` per the locked decision ("Home stays outside the tabs" may mean it should NOT be a tab). If the intent is that "Domů" is accessible only via logo click, remove it from `nav:` — but this would make index.md an orphan page that `--strict` would warn about unless it is still listed. Safe default: include it as the first nav entry.

2. **toc depth overrides**
   - What we know: MkDocs Material supports `toc_depth` per page via page-level metadata.
   - What's unclear: Whether any stub pages need custom TOC depth. The discretion is given to Claude.
   - Recommendation: No per-page toc overrides in stubs. All stubs have ≤3 H2 headings; default TOC depth (H2+H3) is appropriate.

---

## Validation Architecture

### Test Framework

| Property | Value |
|----------|-------|
| Framework | mkdocs build --strict (no unit test framework — static site) |
| Config file | mkdocs.yml |
| Quick run command | `mkdocs build --strict 2>&1 \| tail -5` |
| Full suite command | `mkdocs build --strict` |

This is a static documentation project with no Python/JS unit tests. The sole automated validation is the MkDocs build itself. `--strict` mode is the test harness: it validates all nav entries resolve to existing files, no orphan pages exist, and no broken internal links are present.

### Phase Requirements → Test Map

| Req ID | Behavior | Test Type | Automated Command | File Exists? |
|--------|----------|-----------|-------------------|-------------|
| NAV-01 | `nav:` key present and explicit in mkdocs.yml | smoke | `mkdocs build --strict` | ✅ mkdocs.yml exists |
| NAV-02 | Průvodce and Reference sections exist as nav sections | smoke | `mkdocs build --strict` | ❌ Wave 0 — stub files needed |
| NAV-03 | Sidebar shows all sections and sub-sections | manual-only | Visual inspection in browser | N/A |
| NAV-04 | On-page TOC present on every page | manual-only | Visual inspection — H2 headings generate TOC entries automatically | N/A |
| NAV-05 | Breadcrumbs visible on every page | manual-only | Visual inspection in browser after deploy | N/A |
| NAV-06 | All filenames are ASCII-only slugs | smoke | `find docs/ -name "*.md" \| grep -P "[^\x00-\x7F]"` — zero output = pass | ❌ Wave 0 — stub files needed |

NAV-03, NAV-04, NAV-05 are structural features provided entirely by MkDocs Material theme configuration (already enabled in Phase 1). They cannot be tested by a build command — they require browser verification after the first `mkdocs serve` or deploy. The build succeeding is a necessary but not sufficient condition.

### Sampling Rate

- **Per task commit:** `mkdocs build --strict`
- **Per wave merge:** `mkdocs build --strict`
- **Phase gate:** Full build passes with zero warnings before `/gsd:verify-work`

### Wave 0 Gaps

- [ ] `docs/pruvodce/index.md` — section index for Průvodce tab
- [ ] `docs/pruvodce/pozadavky.md` — covers NAV-02, NAV-06
- [ ] `docs/pruvodce/instalace.md` — covers NAV-02, NAV-06
- [ ] `docs/pruvodce/pripojeni.md` — covers NAV-02, NAV-06
- [ ] `docs/pruvodce/zakladni-workflow.md` — covers NAV-02, NAV-06
- [ ] `docs/pruvodce/parametry.md` — covers NAV-02, NAV-06
- [ ] `docs/pruvodce/otvory.md` — covers NAV-02, NAV-06
- [ ] `docs/pruvodce/trminky.md` — covers NAV-02, NAV-06
- [ ] `docs/pruvodce/diagonaly.md` — covers NAV-02, NAV-06
- [ ] `docs/pruvodce/preview.md` — covers NAV-02, NAV-06
- [ ] `docs/pruvodce/validace.md` — covers NAV-02, NAV-06
- [ ] `docs/pruvodce/pdf-export.md` — covers NAV-02, NAV-06
- [ ] `docs/reference/index.md` — section index for Reference tab
- [ ] `docs/reference/parametry.md` — covers NAV-02, NAV-06
- [ ] `docs/faq.md` — covers NAV-02
- [ ] `nav:` expansion in mkdocs.yml — covers NAV-01

All 16 items are the entire deliverable of Phase 2.

---

## Sources

### Primary (HIGH confidence)
- `.planning/research/ARCHITECTURE.md` — Project structure, nav patterns, Content-as-Config Navigation pattern, tab layout examples
- `.planning/research/PITFALLS.md` — Orphan pages pitfall, feature-based vs task-based structure, --strict validation requirement
- `mkdocs.yml` — Current config: navigation.tabs, navigation.sections, navigation.top already enabled
- `docs/index.md` — Bold-text reference pattern established in Phase 1
- `.planning/phases/02-navigation-skeleton/02-CONTEXT.md` — All locked decisions

### Secondary (MEDIUM confidence)
- [Material for MkDocs — Setting up navigation](https://squidfunk.github.io/mkdocs-material/setup/setting-up-navigation/) — Tab rendering, section index, navigation.tabs behavior

### Tertiary (LOW confidence)
None.

---

## Metadata

**Confidence breakdown:**
- nav: syntax: HIGH — verified against current mkdocs.yml and ARCHITECTURE.md examples
- Stub file pattern: HIGH — established by Phase 1 decisions (bold text, no cross-links, --strict gate)
- Tab rendering with navigation.tabs: HIGH — ARCHITECTURE.md documents this pattern from official Material docs
- Wave 0 file list: HIGH — directly derived from locked decisions in CONTEXT.md

**Research date:** 2026-03-26
**Valid until:** 2026-04-26 (MkDocs 1.6.1 + Material 9.7.6 pinned; no version drift expected)
