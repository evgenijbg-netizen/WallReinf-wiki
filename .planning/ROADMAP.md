# Roadmap: WallReinf Wiki

## Overview

This roadmap delivers a Czech-language user manual for the Wall Reinforcement Wizard Tekla Structures plugin, built on MkDocs Material and hosted on GitHub Pages. The six phases follow the dependency graph: infrastructure must work before content matters, navigation must be stable before cross-links can be written, guide content must exist before reference can link to it, and screenshots depend on a running Tekla instance and must not block text content. The result is a deployable, searchable wiki that a structural engineer can use to learn the plugin from first launch through PDF export.

## Phases

**Phase Numbering:**
- Integer phases (1, 2, 3): Planned milestone work
- Decimal phases (2.1, 2.2): Urgent insertions (marked with INSERTED)

Decimal phases appear between their surrounding integers in numeric order.

- [ ] **Phase 1: Infrastructure and Deploy Pipeline** - MkDocs Material site with working CI/CD deploy to GitHub Pages
- [ ] **Phase 2: Navigation Skeleton** - Complete page structure with stub files and explicit nav configuration
- [x] **Phase 3: User Guide Content** - All workflow-based guide pages written with prose, admonitions, and screenshot placeholders (completed 2026-03-26)
- [ ] **Phase 4: Parameter Reference and FAQ** - Parameter tables, FAQ with 10+ known problems, and cross-links between guide and reference
- [ ] **Phase 5: Screenshots** - All screenshots captured, placed, and captioned with plugin version
- [ ] **Phase 6: Polish and Launch** - Final audit, theme tuning, strict build check, launch-ready site

## Phase Details

### Phase 1: Infrastructure and Deploy Pipeline

**Goal:** A live skeleton site is deployed to GitHub Pages with working search, light/dark mode, and pinned dependencies -- proving the entire CI/CD pipeline works before any content investment.

**Why this order:** Deploy problems discovered with one stub page cost nothing to fix. Deploy problems discovered after 20 pages of content cost rework. Pinning dependencies here prevents the MkDocs 2.x incompatibility trap permanently. The CI pipeline is the highest-leverage unknown to resolve first.

**Requirements:** INFRA-01, INFRA-02, INFRA-03, INFRA-04, INFRA-05, INFRA-06, INFRA-07

**Success Criteria:**
- [ ] `mkdocs serve` runs locally and renders the index page with Material theme
- [ ] Pushing to `main` triggers GitHub Actions and deploys to `gh-pages` branch without manual intervention
- [ ] The site is accessible at the GitHub Pages URL with correct CSS, navigation, and search
- [ ] Full-text search returns results for Czech text entered on the index page
- [ ] Light/dark mode toggle is visible and functional in the theme header

**UAT:**
- [ ] Visit the GitHub Pages URL in a browser -- the site loads with Material theme styling
- [ ] Type a Czech word from the index page into the search bar -- a result appears
- [ ] Click the light/dark mode toggle -- the theme switches
- [ ] Check the GitHub Actions tab -- the latest workflow run is green with `contents: write` permission
- [ ] Verify `site/` is not committed to the repository

**Plans:** 1/2 plans executed

Plans:
- [ ] 01-01-PLAN.md &mdash; Create all MkDocs config files, dependencies, CI workflow, index page, and logo
- [ ] 01-02-PLAN.md &mdash; Initialize git, push to GitHub, verify live deployment

### Phase 2: Navigation Skeleton

**Goal:** The complete page structure is defined in `mkdocs.yml` with all stub files created, establishing the information architecture (guide vs. reference split) before any content is written.

**Why this order:** Renaming or moving pages after cross-links exist breaks all internal references. The navigation structure must be agreed and stable before content investment. This phase locks the file naming convention (ASCII slugs) and two-section split so that all subsequent content work builds on a stable foundation.

**Requirements:** NAV-01, NAV-02, NAV-03, NAV-04, NAV-05, NAV-06

**Success Criteria:**
- [ ] `mkdocs.yml` has an explicit `nav:` configuration listing every page (no auto-discovery)
- [ ] Sidebar shows two top-level sections (Pruvodce and Reference) with all subsections visible
- [ ] Every stub page renders with on-page table of contents and breadcrumbs
- [ ] All filenames use ASCII-only slugs (no Czech diacritics in paths)
- [ ] Navigating through the full sidebar visits every planned page without 404 errors

**UAT:**
- [ ] Open the deployed site -- sidebar shows Pruvodce and Reference sections with all expected subsections
- [ ] Click every link in the sidebar -- each page loads (stub content is fine, no 404s)
- [ ] On any page, verify breadcrumbs are visible above the content
- [ ] On any page with headings, verify the right-side TOC appears
- [ ] Inspect URLs in the browser -- no encoded Czech characters in paths

**Plans:** 1 plan

Plans:
- [x] 02-01-PLAN.md &mdash; Create full nav config in mkdocs.yml and all 15 stub files with visual verification

### Phase 3: User Guide Content

**Goal:** All workflow-based guide pages are written with full prose content, admonitions for warnings/tips, version badges, correct terminology matching the plugin UI, and `[SCREENSHOT]` placeholders where images will be inserted later.

**Why this order:** Writing task-based guide content before reference forces the author to think in user workflows, reinforcing the correct information architecture. Guide pages must exist before reference pages can cross-link to them. Screenshot placeholders preserve page structure without blocking on the Tekla dependency.

**Requirements:** START-01, START-02, START-03, START-04, GUIDE-01, GUIDE-02, GUIDE-03, GUIDE-04, GUIDE-05, GUIDE-06, GUIDE-07, UX-01, UX-02, UX-03

**Success Criteria:**
- [ ] Each guide page covers its topic with substantive prose (not just headings or bullet lists)
- [ ] Admonitions (warning, tip, note) are used on pages where the user could make a mistake or benefit from a shortcut
- [ ] Every guide page displays a badge or admonition indicating the plugin version
- [ ] Terminology on wiki pages matches the labels visible in the plugin UI
- [ ] Screenshot placeholders are present at every step where a visual would help the user

**UAT:**
- [ ] Read the "Zaciname" (Getting Started) pages in order -- a new user can understand requirements, installation, connection to Tekla, and the basic workflow
- [ ] Read each feature guide page -- the content explains when and how to use the feature, not just what the UI fields are
- [ ] Spot-check 3 admonitions -- each contains a genuine warning, tip, or note (not filler)
- [ ] Compare 5 parameter names on wiki pages against the plugin UI -- they match exactly
- [ ] Confirm `[SCREENSHOT]` placeholders exist where visuals are needed

**Plans:** 4/4 plans complete

Plans:
- [x] 03-01-PLAN.md &mdash; Create screenshots directory and write Getting Started pages (pozadavky, instalace, pripojeni)
- [ ] 03-02-PLAN.md &mdash; Write foundational pages (zakladni-workflow end-to-end demo, parametry hub page)
- [ ] 03-03-PLAN.md &mdash; Write feature pages (otvory, trminky, diagonaly) with Settings coverage
- [ ] 03-04-PLAN.md &mdash; Write output pages (preview with heatmap, validace, pdf-export)

### Phase 4: Parameter Reference and FAQ

**Goal:** A complete parameter reference table (grouped by UI section, with defaults and ranges) and a FAQ with at least 10 known problems are published, with cross-links connecting guide pages to reference entries and vice versa.

**Why this order:** Reference content gains full value once guide pages exist to link from. FAQ content emerges naturally after writing the guide -- you know what confuses users once you have written the steps. Cross-links require both ends to exist, so this phase follows the guide.

**Requirements:** REF-01, REF-02, REF-03, FAQ-01, FAQ-02, FAQ-03, FAQ-04, UX-04

**Success Criteria:**
- [ ] Parameter reference table lists every plugin parameter with name matching the UI, description, default value, and valid range
- [ ] Parameters are grouped by UI section (same grouping as the plugin dialog)
- [ ] FAQ page contains at least 10 distinct problems with solutions, covering Tekla connection, reinforcement generation, and validation issues
- [ ] Guide pages link to relevant parameter reference entries; reference entries link back to the guide sections that use them
- [ ] Cross-links between guide and reference are functional (no broken links)

**UAT:**
- [ ] Open the parameter reference -- find a parameter by name, verify it has description, default, and range
- [ ] Compare the parameter grouping against the plugin UI sections -- they match
- [ ] Count FAQ entries -- at least 10 are present
- [ ] Verify FAQ covers all three required areas: Tekla connection (FAQ-02), generation (FAQ-03), validation (FAQ-04)
- [ ] Click 3 cross-links from guide to reference and 3 from reference to guide -- all resolve correctly

**Plans:** 1/2 plans executed

Plans:
- [ ] 04-01-PLAN.md &mdash; Write complete parameter reference table (10 UI sections) and update reference index
- [ ] 04-02-PLAN.md &mdash; Write FAQ page (13+ items) and add bidirectional cross-links to all guide pages

### Phase 5: Screenshots

**Goal:** All screenshot placeholders are replaced with actual annotated screenshots captured from the running plugin, with descriptive filenames and version captions.

**Why this order:** Screenshots require a running Tekla Structures instance with a model -- an external dependency outside the wiki author's control. By this phase, every needed screenshot is identified from placeholders in the guide pages, and the content structure is stable so screenshots will not need to be retaken due to reorganization.

**Requirements:** IMG-01, IMG-02, IMG-03, IMG-04, IMG-05, IMG-06

**Success Criteria:**
- [ ] The main plugin dialog, preview panel, and validation window each have a dedicated screenshot on their respective pages
- [ ] Key steps in the guide pages have accompanying screenshots (placeholders fully replaced)
- [ ] Every screenshot file uses a descriptive name reflecting the dialog or step shown (not generic names like screenshot01.png)
- [ ] Every screenshot caption includes the plugin version number
- [ ] All screenshots render correctly on the deployed site

**UAT:**
- [ ] Browse every guide page -- no `[SCREENSHOT]` placeholder text remains
- [ ] Check 5 screenshot filenames in `docs/assets/screenshots/` -- each name describes the content (e.g., `hlavni-dialog-parametry.png`)
- [ ] Check 3 screenshot captions -- each mentions the plugin version
- [ ] On the deployed site, click/view 3 screenshots -- they load and are legible

**Plans**: TBD

### Phase 6: Polish and Launch

**Goal:** The site passes a strict build check with no warnings, all cross-links are verified, and the wiki is ready for end users.

**Why this order:** Polishing before content and screenshots exist wastes effort. All polish items are fast and low-risk. This phase is the final quality gate before announcing the wiki to users.

**Requirements:** (no unmapped requirements -- this phase covers final integration and quality)

**Success Criteria:**
- [ ] `mkdocs build --strict` completes with zero warnings (no broken links, no orphan pages)
- [ ] Every page in the navigation is reachable and renders correctly on the deployed site
- [ ] Search returns relevant results for common user queries (e.g., "otvory", "trminek", "instalace")
- [ ] The site loads correctly on both desktop and mobile browsers

**UAT:**
- [ ] Run `mkdocs build --strict` locally -- it exits with code 0 and no warnings
- [ ] Navigate the entire site following the sidebar -- every page loads, no 404s
- [ ] Search for 3 common terms -- results are relevant and link to the correct pages
- [ ] Open the site on a phone or narrow browser window -- layout is usable

**Plans**: TBD

## Milestone Summary

**Total v1 requirements:** 41
**Mapped to phases:** 41
**Unmapped:** 0

| Phase | Requirements | Count |
|-------|-------------|-------|
| 1. Infrastructure and Deploy Pipeline | 1/2 | In Progress|  | 2. Navigation Skeleton | NAV-01 .. NAV-06 | 6 |
| 3. User Guide Content | 4/4 | Complete    | 2026-03-26 | 4. Parameter Reference and FAQ | 1/2 | In Progress|  | 5. Screenshots | IMG-01 .. IMG-06 | 6 |
| 6. Polish and Launch | (integration/quality -- no new requirements) | 0 |
| **Total** | | **41** |

Phase 6 carries no dedicated requirements because it is a quality gate: it verifies that all prior phases integrate correctly and the site meets launch standards. All 41 functional requirements are delivered by Phases 1-5.

## Progress

**Execution Order:**
Phases execute in numeric order: 1 -> 2 -> 3 -> 4 -> 5 -> 6

| Phase | Plans Complete | Status | Completed |
|-------|----------------|--------|-----------|
| 1. Infrastructure and Deploy Pipeline | 0/2 | Planned | - |
| 2. Navigation Skeleton | 1/1 | Complete | 2026-03-26 |
| 3. User Guide Content | 4/4 | Complete | 2026-03-26 |
| 4. Parameter Reference and FAQ | 0/2 | Planned | - |
| 5. Screenshots | 0/TBD | Not started | - |
| 6. Polish and Launch | 0/TBD | Not started | - |
