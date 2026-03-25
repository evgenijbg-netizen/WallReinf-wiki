# Project Research Summary

**Project:** WallReinf Wiki — User Manual for Wall Reinforcement Wizard (WRW) Tekla Structures Plugin
**Domain:** Static documentation wiki / user manual site for a desktop application plugin
**Researched:** 2026-03-25
**Confidence:** HIGH

## Executive Summary

The Wall Reinforcement Wizard wiki is a Czech-language, single-version, screenshot-heavy user manual for a C#/WPF Tekla Structures plugin. The correct way to build this is with MkDocs Material 9.7.6 on GitHub Pages, deployed via GitHub Actions CI. This combination is the de-facto industry standard for technical documentation at this scale: it provides built-in Czech UI localization, client-side full-text search, hierarchical navigation, admonition callouts, and image lightbox — all without a custom build pipeline, Node.js, or a backend. The stack has zero meaningful competitors for a Czech-only, single-version, screenshot-heavy user manual with this audience size.

The recommended approach is a six-phase build: start by standing up the infrastructure and proving the CI pipeline works before writing a single word of content, then build the page skeleton (navigation structure), then fill in user guide content, then the parameter reference and FAQ, then screenshots, and finally polish. This order is dictated by the dependency graph: infrastructure must work before content matters; navigation structure must be stable before cross-links can be written; screenshots require a running Tekla instance and should not block text content. Every phase has clear deliverables, and each phase can be reviewed independently.

The key risk is not technical — the stack is mature and well-documented. The primary risks are content-architecture risks: structuring the wiki around the plugin's UI tree rather than user workflows (the most common mistake in technical documentation), letting screenshots go stale after plugin UI updates, and failing to pin dependency versions (causing a silent MkDocs 2.x incompatibility break). All three are preventable with upfront conventions established in Phase 1.

---

## Key Findings

### Recommended Stack

MkDocs Material 9.7.6 with MkDocs 1.6.1, Python 3.10+, and GitHub Actions CI is the recommended stack. It is verified against PyPI as of March 2026 and all features required for this project are present in the public release (the Insiders program was retired November 2025; all features are now free). The stack entered maintenance mode in November 2025 — meaning no new features — but this has zero impact on this project since all required features are fully present and stable. The successor tool (Zensical, same team) is at v0.0.29 pre-release and is not ready for production; use Material for MkDocs now and plan a migration assessment in late 2026.

**Core technologies:**
- MkDocs 1.6.1: Static site build engine — Markdown-in, HTML-out; purpose-built for documentation
- Material for MkDocs 9.7.6: Theme + feature layer — built-in Czech UI, search, navigation, admonitions, lightbox hooks
- mkdocs-glightbox 0.5.2: Image lightbox — mandatory for a screenshot-heavy manual; zero-config
- GitHub Actions: CI/CD deploy — official recommended path; `mkdocs gh-deploy --force` on every push to `main`
- Python 3.10+: Runtime — required by MkDocs toolchain

**Critical version note:** Pin all dependencies in `requirements.txt` from day one. MkDocs 2.0 is incompatible with Material for MkDocs 9.x — unpinned installs will silently or loudly break the build.

### Expected Features

**Must have (table stakes — P1 for launch):**
- Hierarchical sidebar navigation with explicit `nav:` configuration in `mkdocs.yml`
- Full-text search with Czech (`cs`) language stemming — configured in both `theme.language` and `plugins.search.lang`
- Getting Started section — install, connect to Tekla, open the plugin dialog
- Feature reference pages — one page per major plugin feature (openings, stirrups, U-bars, preview, validation, PDF export)
- Parameter reference tables — valid ranges, defaults, boundary behavior
- FAQ / Troubleshooting — minimum 5-10 known problems with solutions
- Admonitions (warning, tip, note callouts) — engineers read fast; visual stops prevent mistakes
- Screenshots at critical steps — plugin dialog, preview panel, validation window (placeholder text acceptable at launch if Tekla not yet available)
- On-page table of contents, breadcrumbs, light/dark mode toggle — all free via MkDocs Material

**Should have (differentiators — P2, add after validation):**
- Annotated screenshots with numbered callouts
- Content tabs for variant workflows (e.g., "With openings / Without openings")
- "Edit this page" GitHub link — lowers friction for fixing errors
- Search result highlighting (`search.highlight` config)
- Version badge / plugin version callout on each page

**Defer (v2+ only):**
- English translation — only if the plugin UI is translated to English
- Versioned docs via `mike` plugin — only if multiple plugin versions are simultaneously maintained
- Comment/feedback system (Disqus, giscus) — audience is small and known; a support email or GitHub Issues link suffices
- AI chatbot / LLM Q&A — full-text search is sufficient at this audience size
- Interactive parameter calculator — the plugin itself serves this purpose

### Architecture Approach

The architecture is a three-layer system: an authoring layer (`docs/*.md` + `mkdocs.yml` + assets), a build layer (MkDocs Material running in CI), and a delivery layer (GitHub Pages CDN serving the `gh-pages` branch). All state lives in the URL; the site is entirely static with no server-side logic. Content is organized into two distinct sections per the Diátaxis framework: a linear user guide (`docs/pruvodce/`) covering workflows, and a parameter reference (`docs/reference/`) covering field-by-field descriptions. These two content types must be separated — mixing them produces pages that serve neither audience well.

**Major components:**
1. `mkdocs.yml` — master configuration: site URL, navigation tree, theme settings, plugin declarations; changes here affect the entire site
2. `docs/pruvodce/` — workflow-based user guide (10 pages covering first launch through PDF export); linear reading order
3. `docs/reference/` — parameter reference; users return here frequently to look up a single value
4. `docs/assets/screenshots/` — static image assets; screenshots are placed here and MkDocs copies them to the built site unchanged
5. `.github/workflows/ci.yml` — GitHub Actions pipeline; triggers on push to `main`, runs `mkdocs gh-deploy --force`; never deploy manually from a local machine

**Key patterns:**
- Explicit `nav:` config in `mkdocs.yml` — always; auto-discovery sorts alphabetically and breaks reading order
- Admonitions throughout the user guide — zero setup cost, high user value
- ASCII slugs in filenames, Czech content in Markdown — avoids URL encoding issues with Czech characters
- `site/` in `.gitignore` — the `gh-pages` branch is managed exclusively by CI

### Critical Pitfalls

1. **Feature-based instead of task-based structure** — organize content around user workflows ("how do I add openings?"), not UI panel names. Warning sign: section titles that match dialog names exactly. Address this in the navigation structure before writing any content.

2. **Missing or incorrect `site_url`** — set `site_url: https://<username>.github.io/WallReinf-wiki/` (with trailing slash) in `mkdocs.yml` from the first commit. Without it, navigation, CSS, and search break when landing on a 404 page or deep-linked URL on GitHub Pages.

3. **MkDocs 2.x incompatibility via unpinned dependencies** — pin `mkdocs==1.6.1` and `mkdocs-material==9.7.6` in `requirements.txt`. Running `pip install --upgrade mkdocs` will install MkDocs 2.x, which is incompatible with Material 9.x. Recovery without pinning is HIGH cost.

4. **GitHub Actions deploy fails silently** — add `permissions: contents: write` explicitly to the workflow. Without it, `gh-pages` branch is never created and GitHub Pages returns 404 with no error in the Actions log. Verify the `gh-pages` branch exists after the first CI run.

5. **Screenshots become stale and erode trust** — use screenshots strategically (high-value steps only, target < 20 for v1), name files descriptively by dialog name (not `screenshot01.png`), caption with plugin version, and include "update screenshots" in the release checklist for each plugin version bump.

---

## Implications for Roadmap

Based on research, the following six-phase structure is recommended. The ordering is dictated by dependency constraints: CI must work before content matters; navigation structure must be stable before cross-links are valid; screenshots have an external dependency on Tekla Structures and must not block text content.

### Phase 1: Infrastructure and Deploy Pipeline

**Rationale:** The CI/CD pipeline is the most critical unknown. A broken deploy discovered after all content is written is expensive. A broken deploy discovered with one page of content is cheap to fix. Several pitfalls (missing `site_url`, missing `contents: write` permission, wrong GitHub Pages branch source) can only be caught by an actual deploy to GitHub Pages. Establishing this in Phase 1 also pins dependencies, preventing the MkDocs 2.x upgrade trap permanently.
**Delivers:** A live, deployable skeleton site at the GitHub Pages URL — one page, full CSS, working search, `gh-pages` branch active
**Addresses pitfalls:** Missing `site_url` (Pitfall 2), MkDocs 2.x incompatibility (Pitfall 3/4), GitHub Actions silent fail (Pitfall 5)
**Must include:** `mkdocs.yml` with pinned `site_url`, `requirements.txt` with pinned versions, `.github/workflows/ci.yml` with `contents: write`, `.gitignore` excluding `site/`, `docs/index.md` stub, GitHub Pages configured to serve `gh-pages` branch

### Phase 2: Navigation Skeleton

**Rationale:** The navigation structure must be agreed and stable before content is written. Renaming or moving pages after cross-links exist breaks all internal references. This phase defines the information architecture (the task-based vs. feature-based decision) before any content investment has been made. Restructuring after content exists is rated MEDIUM recovery cost in the pitfalls research.
**Delivers:** Complete `nav:` tree in `mkdocs.yml`, all page files created as stubs, navigation visible and correct in the live site
**Addresses pitfalls:** Feature-based structure instead of task-based (Pitfall 1), orphan pages unreachable from nav
**Must establish:** ASCII-slug file naming convention, two-section split (guide vs. reference), explicit `nav:` config — never auto-discovery

### Phase 3: User Guide Content

**Delivers:** `docs/pruvodce/*.md` — all 10 workflow pages written with prose content, admonitions (warnings, tips), parameter descriptions, and `[SCREENSHOT: dialog X]` placeholders where screenshots will go
**Rationale:** Writing task-based guide content before reference forces the author to think in user workflows, reinforcing the correct information architecture established in Phase 2. Screenshot placeholders preserve the page structure for later substitution without blocking content completion.
**Implements:** Diátaxis how-to section, admonition pattern, Content-as-Config Navigation pattern

### Phase 4: Parameter Reference and FAQ

**Rationale:** Reference content and FAQ both depend on guide pages existing (to cross-link from). The parameter reference gains its full value once the guide pages link to it for look-up. The FAQ content emerges naturally after writing the guide (you know what confuses users once you have written the steps).
**Delivers:** `docs/reference/parametry.md` with complete parameter table (ranges, defaults, boundary behavior), `docs/faq.md` with minimum 10 known problems and solutions, cross-links in both directions between guide and reference

### Phase 5: Screenshots

**Rationale:** Screenshots require an external dependency — a running Tekla Structures installation with a real model. This is outside the wiki author's control during earlier phases. By Phase 5, every screenshot needed is known (from the placeholders in Phase 3 pages), and the content structure is stable so screenshots won't need to be retaken due to page reorganization.
**Delivers:** Screenshots captured and placed in `docs/assets/screenshots/`, placeholder text in Markdown replaced with actual image references, glightbox zoom functional
**Must establish:** Naming convention (dialog name in filename), version annotation in image captions, compression target (< 200 KB per image), "update screenshots" added to plugin release checklist

### Phase 6: Polish and Launch

**Delivers:** Theme customization (logo, colors if desired), `site_description` for SEO and social cards, `repo_url` + `edit_uri` for "Edit this page" links, final navigation and cross-link audit, `mkdocs build --strict` CI check to catch broken links and orphan pages, launch-readiness verification checklist
**Rationale:** Polishing before content and screenshots exist wastes effort. All polish items are fast and low-risk; they belong at the end.

### Phase Ordering Rationale

- Infrastructure before content: pitfalls research explicitly rates this as the highest-leverage investment — deploy problems discovered early cost nothing; discovered late cost rework
- Navigation before content writing: renaming files after cross-links exist is rated MEDIUM recovery cost; establishing structure first eliminates this risk entirely
- Screenshots after text content: the Tekla external dependency means screenshots cannot be on the critical path; text-only pages are deployable and useful on their own
- Reference and FAQ after guide: cross-links between sections require both ends to exist; guide pages must exist before reference can link back to them

### Research Flags

Phases with well-documented patterns (skip research-phase during planning):
- **Phase 1:** Standard MkDocs Material + GitHub Actions pattern; official docs are authoritative and complete; no unknown decisions
- **Phase 2:** Navigation configuration is fully documented; decision is which structure fits the user's workflow, not how to implement it
- **Phase 3:** Content writing; no technical research needed; conventions are established
- **Phase 4:** Reference table and FAQ; content work; no technical unknowns
- **Phase 6:** Material for MkDocs customization is comprehensively documented

Phases that may benefit from targeted research during planning:
- **Phase 5:** Screenshot tooling choice (Greenshot vs. Snagit vs. Windows Snipping Tool), annotation approach, and compression workflow are not covered in existing research. If annotated screenshots are desired at launch (vs. plain screenshots), a brief tool evaluation is warranted.

---

## Confidence Assessment

| Area | Confidence | Notes |
|------|------------|-------|
| Stack | HIGH | All versions verified against PyPI (March 2026); official MkDocs Material docs confirm Czech support, GitHub Actions pattern, and MkDocs 2.x incompatibility warning |
| Features | HIGH | MkDocs Material feature set is mature and stable; user manual conventions are well-established; feature list is conservative and grounded in audience size |
| Architecture | HIGH | Patterns verified against official MkDocs Material documentation; file structure is straightforward and has no novel decisions |
| Pitfalls | HIGH | Most pitfalls are documented in official sources (MkDocs 2.x issue, GitHub Actions permissions, site_url behavior); screenshot staleness is supported by multiple secondary sources |

**Overall confidence:** HIGH

The technology stack is unusually well-suited to this project — there are no meaningful trade-offs or competing approaches for a Czech-only, single-version, screenshot-heavy user manual at this scale. Research conclusions are consistent across all four domains.

### Gaps to Address

- **Screenshot tooling:** Research identified the need for annotated screenshots as a P2 feature but did not evaluate specific tools. During content planning, decide on Greenshot, Snagit, or another annotation tool before Phase 5. This is a low-stakes decision with no lock-in.
- **Exact GitHub Pages URL:** The `site_url` in `mkdocs.yml` requires the actual GitHub organization/username and repository name. This must be set correctly before Phase 1 deploy. No research gap — just a configuration value that must be filled in.
- **Plugin version coverage:** The parameter reference (Phase 4) requires complete knowledge of all plugin parameters. This depends on the plugin's current state and is not a research gap in the wiki toolchain — it is a content dependency on the plugin author providing accurate parameter documentation.

---

## Sources

### Primary (HIGH confidence)
- [mkdocs-material on PyPI](https://pypi.org/project/mkdocs-material/) — version 9.7.6, March 19 2026
- [mkdocs on PyPI](https://pypi.org/project/mkdocs/) — version 1.6.1, August 30 2024
- [mkdocs-glightbox on PyPI](https://pypi.org/project/mkdocs-glightbox/) — version 0.5.2, October 23 2025
- [Material for MkDocs — Publishing your site](https://squidfunk.github.io/mkdocs-material/publishing-your-site/) — GitHub Actions workflow, permissions
- [Material for MkDocs — Setting up navigation](https://squidfunk.github.io/mkdocs-material/setup/setting-up-navigation/) — nav patterns
- [Material for MkDocs — Setting up site search](https://squidfunk.github.io/mkdocs-material/setup/setting-up-site-search/) — Czech search config
- [Material for MkDocs — Changing the language](https://squidfunk.github.io/mkdocs-material/setup/changing-the-language/) — Czech `cs` UI support
- [Material for MkDocs — Reference](https://squidfunk.github.io/mkdocs-material/reference/) — complete component list
- [Material for MkDocs blog — Zensical announcement, maintenance mode](https://squidfunk.github.io/mkdocs-material/blog/2025/11/05/zensical/)
- [Material for MkDocs blog — Insiders now free, MkDocs 2.0 warning](https://squidfunk.github.io/mkdocs-material/blog/2025/11/11/insiders-now-free-for-everyone/)
- [Material for MkDocs blog — MkDocs 2.0 implications](https://squidfunk.github.io/mkdocs-material/blog/2026/02/18/mkdocs-2.0/)
- [Zensical GitHub releases](https://github.com/zensical/zensical/releases) — v0.0.29 pre-release status, March 24 2026
- [MkDocs issue #2520 — site_url and 404 behavior](https://github.com/squidfunk/mkdocs-material/issues/2520)
- [Creating your site — Material for MkDocs](https://squidfunk.github.io/mkdocs-material/creating-your-site/)
- [Writing Your Docs — MkDocs](https://www.mkdocs.org/user-guide/writing-your-docs/)

### Secondary (MEDIUM confidence)
- [Documentation Generator Comparison 2025](https://okidoki.dev/documentation-generator-comparison) — Docusaurus/VitePress/MkDocs comparison
- [AltexSoft — User Manuals and Other Documentation](https://www.altexsoft.com/blog/user-manuals-documentation/) — user manual structure conventions
- [GitBook — Documentation structure best practices](https://gitbook.com/docs/guides/docs-best-practices/documentation-structure-tips) — information architecture
- [TechSmith — How to Build the Best User Manual](https://www.techsmith.com/blog/user-documentation/) — screenshots and visual elements
- [Should you add screenshots to documentation?](https://thisisimportant.net/posts/screenshots-in-documentation/) — screenshot strategy
- [Archbee — User Documentation best practices](https://www.archbee.com/blog/user-documentation-best-practices) — documentation conventions
- [Deploying MkDocs to GitHub Pages with GitHub Actions](https://thomasthornton.cloud/2024/05/01/deploying-mkdocs-to-github-pages-with-github-actions/) — CI/CD pattern validation

---

*Research completed: 2026-03-25*
*Ready for roadmap: yes*
