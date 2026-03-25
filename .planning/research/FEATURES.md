# Feature Research

**Domain:** Technical documentation / user manual wiki (static site, desktop application)
**Researched:** 2026-03-25
**Confidence:** HIGH (MkDocs Material is mature, well-documented; user manual conventions are well-established)

---

## Feature Landscape

### Table Stakes (Users Expect These)

Features users assume exist. Missing these = product feels incomplete or unprofessional.

| Feature | Why Expected | Complexity | Notes |
|---------|--------------|------------|-------|
| Hierarchical navigation (sidebar) | Users expect a persistent left-nav showing all sections and subsections | LOW | MkDocs Material nav built-in; requires only `mkdocs.yml` nav config |
| Full-text search | "I need to find X" is the #1 user action in any reference doc; engineers search rather than browse | LOW | MkDocs Material built-in, runs client-side, zero config |
| Table of contents (on-page TOC) | Long pages need an anchor outline on the right side so users can jump to a section | LOW | MkDocs Material built-in via `toc` plugin |
| Breadcrumbs | Show where the user is in the hierarchy — critical for deep page structures | LOW | MkDocs Material built-in |
| Getting Started / Quick Start section | Engineers want to verify they can launch the plugin in 5 minutes before reading all details | LOW | Content only; no special tooling |
| Feature reference pages | One page per major plugin feature (openings, stirrups, U-bars, preview, validation, PDF export) | LOW | Content + structure; one Markdown file per feature |
| Installation / setup instructions | How to install, connect to Tekla, which Tekla version is required | LOW | Content only |
| FAQ / Troubleshooting section | Engineers hit a wall, search for their error message — missing this = support tickets | MEDIUM | Content curation; requires domain knowledge of common errors |
| Screenshots at key steps | Visual confirmation that the user is doing the right thing in the right dialog | MEDIUM | Dependency: screenshots require running Tekla with a real model |
| Responsive layout (mobile-friendly) | Not the primary use case (engineers use desktop) but expected from any modern site | LOW | MkDocs Material is responsive by default |
| Keyboard-navigable search | Engineers are keyboard-heavy; `/` to open search is expected | LOW | MkDocs Material built-in |
| Page titles and headings | Scannable headings so users can orient themselves without reading every word | LOW | Markdown convention; enforced through authoring discipline |
| Internal cross-links between pages | Pages reference each other (e.g. "see also: Openings") for non-linear navigation | LOW | Standard Markdown links; require discipline to maintain |
| Light/dark mode toggle | Standard in 2026 for developer/technical audiences | LOW | MkDocs Material built-in; one line config |

### Differentiators (Competitive Advantage)

Features that make this wiki clearly better than a plain PDF manual or a barebones docs site.

| Feature | Value Proposition | Complexity | Notes |
|---------|-------------------|------------|-------|
| Admonitions (note/warning/tip callout boxes) | Engineers read fast — a colored "Warning" box with a caution icon stops their eye and prevents mistakes | LOW | MkDocs Material built-in (`!!! warning`, `!!! tip`, etc.); 12 types |
| Annotated screenshots (callouts/arrows) | A screenshot with numbered callouts explaining each UI element is 10x more useful than prose describing the same | MEDIUM | Requires image editing tool (e.g. Greenshot, Snagit); not a site feature per se |
| Content tabs for variant workflows | When two parameter combinations lead to different outcomes, tabs keep the page linear (e.g. "With openings / Without openings") | LOW | MkDocs Material `=== "Tab"` syntax, built-in |
| Parameter reference tables | Engineers need to know: what is the valid range, what is the default, what happens at the boundary — a table is the right form | LOW | Standard Markdown tables; requires authoring discipline |
| Keyboard shortcut for search visible in header | `Ctrl+K` or `/` displayed prominently reduces time-to-answer | LOW | MkDocs Material config: `search.suggest`, `search.highlight` |
| Search result highlighting | When users arrive at a page from search, the matched term is highlighted — confirms they landed in the right place | LOW | MkDocs Material built-in with `search.highlight` |
| "Edit this page" link to GitHub | Lowers the friction for the author (or future contributors) to fix an error found while reading | LOW | MkDocs Material `repo_url` + `edit_uri` config |
| Version badge / plugin version callout | Engineers need to know if the doc applies to their installed version | LOW | Simple Markdown badge or admonition at page top |
| Print-friendly CSS | Engineers sometimes print reference pages; MkDocs Material's print styles are good but need a check | LOW | MkDocs Material includes print styles; no extra work |
| Consistent UI terminology (matches the actual plugin labels) | When the doc says "Krytí [mm]" and the plugin says "Krytí [mm]" — no translation friction | LOW | Authoring discipline, not a site feature; critical for Czech audience |

### Anti-Features (Deliberately NOT Building)

Features that seem useful but would add maintenance overhead or scope-creep without commensurate benefit.

| Feature | Why Requested | Why Problematic | Alternative |
|---------|---------------|-----------------|-------------|
| Comment/feedback system (Disqus, giscus) | Users want to report errors or ask questions inline | Adds JS dependency, moderation overhead, and maintenance; users are a small, known audience (internal/customer) | Provide a support email or GitHub Issues link in the footer |
| Full-text video embed tutorials | Video is engaging; users ask for "show me" walkthroughs | Out of scope per PROJECT.md; video requires recording/editing tooling and goes stale fast when UI changes | Annotated screenshots + step-by-step numbered lists achieve 80% of the value |
| Multi-language (English) version | Broader audience reach | Out of scope per PROJECT.md; translating technical UI strings doubles maintenance; v1 audience is Czech-speaking only | Defer to v2+ if the plugin gets an English UI |
| User accounts / gated access | "Private" documentation for paying customers | Static site on GitHub Pages has no auth layer; adds infrastructure complexity far beyond project scope | Keep documentation public; the plugin itself is the protected asset |
| AI chatbot / LLM Q&A | "Ask the docs" trend in 2025-2026 | Requires backend, API costs, hallucination risk on technical parameters; audience is small enough that search suffices | Full-text search + good heading structure achieves the same for this audience size |
| Interactive parameter calculator | Users could input values and see computed outputs | Requires JavaScript application embedded in static site; the plugin itself serves this purpose | Link to the plugin; describe parameters in prose + tables |
| Version dropdown (multiple doc versions) | If the plugin is updated, users want docs for their version | MkDocs versioning (mike plugin) adds significant CI/CD complexity; at v1 there is one version | Use a version admonition at page top noting the applicable plugin version; add versioning later if needed |
| Dark-pattern SEO optimization | Rank higher in search engines | The site is a reference tool for existing users, not a discovery channel; over-optimizing meta tags wastes time | Use descriptive page titles; MkDocs Material's social plugin handles basic OG tags |
| Developer/API documentation | Complete picture of the codebase | Explicitly out of scope per PROJECT.md | Keep internal architecture docs in the source repo under `docs/` |

---

## Feature Dependencies

```
[Navigation structure (sidebar)]
    └──requires──> [mkdocs.yml nav config]
                       └──requires──> [Page files created]

[Full-text search]
    └──requires──> [Page files with content]
    └──enhances──> [Search highlight]
                       └──enhances──> [Search suggestions]

[Screenshots]
    └──requires──> [Running Tekla Structures + model]
    └──enhances──> [Getting Started section]
    └──enhances──> [Feature reference pages]

[Annotated screenshots]
    └──requires──> [Screenshots]
    └──requires──> [Image editing tool (external)]

[Admonitions / callouts]
    └──requires──> [Page content exists]

[Parameter reference tables]
    └──requires──> [Feature reference pages]

[FAQ / Troubleshooting]
    └──enhances──> [Feature reference pages] (cross-links)
    └──requires──> [Domain knowledge of common errors]
```

### Dependency Notes

- **Screenshots require Tekla Structures.** This is the primary external dependency. Text-only pages can be written and deployed first; screenshots are added as they become available. The site is deployable without them.
- **Search depends on content volume.** Search is zero-config but only becomes useful once meaningful pages exist. Build content first.
- **FAQ depends on feature pages.** Troubleshooting sections should cross-link to feature reference pages. Write feature pages before FAQ to know what to link.
- **Admonitions enhance but do not block.** They can be added to any page at any time without restructuring.

---

## MVP Definition

### Launch With (v1)

Minimum viable product — what users need to start using the plugin without calling the author.

- [ ] Getting Started — install, connect to Tekla, open the plugin dialog
- [ ] Feature reference for every major UI section: main parameters (bar diameters, cover, spacing, edge bars), openings, U-bars, stirrups, diagonal bars, preview panel, validation window, PDF export
- [ ] FAQ / Troubleshooting — minimum 5-10 known problems with solutions
- [ ] Screenshots at the most critical steps (plugin dialog, preview, validation) — placeholder text acceptable at launch if screenshots not yet available
- [ ] Working search
- [ ] Deployed to GitHub Pages

### Add After Validation (v1.x)

Features to add once the base wiki is live and the author has received feedback.

- [ ] Annotated screenshots with numbered callouts — after unnannotated screenshots exist
- [ ] Content tabs for variant workflows — when parameter combinations become a common source of confusion
- [ ] "Edit this page" GitHub link — low effort, add in first maintenance pass
- [ ] Version badge on each page — once a second plugin version is released

### Future Consideration (v2+)

Defer until the plugin has a wider audience or English-language UI.

- [ ] English translation — only if the plugin UI is translated to English
- [ ] Versioned docs (mike plugin) — only if the plugin has multiple maintained versions simultaneously
- [ ] Comment/feedback system — only if the audience grows beyond a known user group

---

## Feature Prioritization Matrix

| Feature | User Value | Implementation Cost | Priority |
|---------|------------|---------------------|----------|
| Full-text search | HIGH | LOW | P1 |
| Hierarchical navigation | HIGH | LOW | P1 |
| Getting Started section | HIGH | LOW | P1 |
| Feature reference pages | HIGH | LOW | P1 |
| Screenshots at key steps | HIGH | MEDIUM | P1 |
| FAQ / Troubleshooting | HIGH | MEDIUM | P1 |
| On-page TOC | MEDIUM | LOW | P1 |
| Admonitions (warnings, tips) | HIGH | LOW | P1 |
| Parameter reference tables | HIGH | LOW | P1 |
| Light/dark mode | LOW | LOW | P1 (free via MkDocs Material) |
| Annotated screenshots | HIGH | MEDIUM | P2 |
| Content tabs for variants | MEDIUM | LOW | P2 |
| "Edit this page" link | LOW | LOW | P2 |
| Version badge | MEDIUM | LOW | P2 |
| Search highlight | MEDIUM | LOW | P2 |
| Print-friendly CSS | LOW | LOW | P2 |
| Versioned docs | MEDIUM | HIGH | P3 |
| English translation | MEDIUM | HIGH | P3 |
| Comment system | LOW | HIGH | P3 |

**Priority key:**
- P1: Must have for launch
- P2: Should have, add when possible
- P3: Nice to have, future consideration

---

## Competitor Feature Analysis

Reference sites comparable to what this wiki should achieve:

| Feature | Tekla User Assistance (official) | Read the Docs style sites | Our Approach |
|---------|----------------------------------|--------------------------|--------------|
| Navigation | Tree sidebar, tabs by product | Left sidebar + on-page TOC | MkDocs Material sidebar + on-page TOC |
| Search | Enterprise-grade, faceted | Client-side full-text | MkDocs Material client-side (sufficient for this scale) |
| Screenshots | Professional, annotated | Varies | Screenshots + annotations; start un-annotated |
| Dark mode | No (as of 2025) | Varies | Yes — free via MkDocs Material |
| Version dropdown | Yes (multiple Tekla versions) | Yes (common) | v1: single version + admonition; versioning deferred |
| Localization | Multiple languages | Varies | Czech only (v1) |
| Video | Yes | Rare | No — out of scope |
| Mobile | Responsive | Responsive | Responsive (built-in) |
| Edit link | No | Common in OSS docs | Yes — low-effort, good for maintenance |

---

## Sources

- [Material for MkDocs — Reference](https://squidfunk.github.io/mkdocs-material/reference/) — comprehensive list of available components (HIGH confidence)
- [Material for MkDocs — Home](https://squidfunk.github.io/mkdocs-material/) — feature overview including search, navigation, social cards (HIGH confidence)
- [Material for MkDocs — Setting up navigation](https://squidfunk.github.io/mkdocs-material/setup/setting-up-navigation/) — navigation patterns (HIGH confidence)
- [AltexSoft — User Manuals and Other Documentation](https://www.altexsoft.com/blog/user-manuals-documentation/) — user manual structure conventions (MEDIUM confidence)
- [GitBook — Documentation structure tips](https://gitbook.com/docs/guides/docs-best-practices/documentation-structure-tips) — information architecture best practices (MEDIUM confidence)
- [TechSmith — How to Build the Best User Manual](https://www.techsmith.com/blog/user-documentation/) — screenshots and visual elements guidance (MEDIUM confidence)

---

*Feature research for: Technical documentation wiki — Wall Reinforcement Wizard user manual*
*Researched: 2026-03-25*
