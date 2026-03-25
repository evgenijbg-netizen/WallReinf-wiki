# Architecture Research

**Domain:** Static documentation wiki — MkDocs Material, GitHub Pages
**Researched:** 2026-03-25
**Confidence:** HIGH (official MkDocs Material docs + verified patterns)

## Standard Architecture

### System Overview

```
┌─────────────────────────────────────────────────────────────────────┐
│                        AUTHORING LAYER                              │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐              │
│  │  Markdown    │  │  mkdocs.yml  │  │  Assets      │              │
│  │  docs/*.md   │  │  (config)    │  │  screenshots │              │
│  └──────┬───────┘  └──────┬───────┘  └──────┬───────┘              │
│         └─────────────────┴──────────────────┘                      │
│                            │                                         │
├────────────────────────────▼────────────────────────────────────────┤
│                        BUILD LAYER                                  │
│  ┌──────────────────────────────────────────────────────────────┐   │
│  │              MkDocs Material (Python, local or CI)           │   │
│  │  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌────────────┐   │   │
│  │  │  Theme   │  │  Search  │  │  Nav     │  │  Plugins   │   │   │
│  │  │  engine  │  │  index   │  │  builder │  │  (built-in)│   │   │
│  │  └──────────┘  └──────────┘  └──────────┘  └────────────┘   │   │
│  └──────────────────────────────────────────────────────────────┘   │
│                            │                                         │
│                      site/ (output)                                  │
│                  static HTML + CSS + JS                              │
├────────────────────────────▼────────────────────────────────────────┤
│                        DELIVERY LAYER                               │
│  ┌──────────────────────────────────────────────────────────────┐   │
│  │  GitHub Actions CI  →  gh-pages branch  →  GitHub Pages CDN  │   │
│  └──────────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────────┘
```

### Component Responsibilities

| Component | Responsibility | Communicates With |
|-----------|----------------|-------------------|
| `mkdocs.yml` | Master config: site name, URL, nav tree, theme settings, plugins | MkDocs build engine reads this first |
| `docs/` | All source content: Markdown pages, images, extra CSS/JS | Build engine reads every file here |
| `docs/index.md` | Homepage / landing page of the site | Rendered as site root `index.html` |
| `docs/assets/` | Screenshots, images, diagrams referenced from Markdown | Copied verbatim to `site/assets/` |
| `docs/stylesheets/` | Optional custom CSS overrides | Appended after Material theme CSS |
| `overrides/` | Jinja2 template partials to customise theme HTML | Build engine merges with Material templates |
| `.github/workflows/ci.yml` | GitHub Actions: triggers build + deploy on push to main | Runs `mkdocs gh-deploy --force` |
| `gh-pages` branch | Auto-generated static site output; GitHub Pages serves from here | Populated entirely by CI, never edited manually |
| GitHub Pages CDN | Public hosting at `<user>.github.io/<repo>` | Serves files from `gh-pages` branch |

---

## Recommended Project Structure

```
WallReinf-wiki/
├─ mkdocs.yml                     # Master configuration
├─ requirements.txt               # pip deps (mkdocs-material + plugins)
├─ .github/
│  └─ workflows/
│     └─ ci.yml                   # Build + deploy on push to main
├─ docs/
│  ├─ index.md                    # Homepage / landing page (required)
│  ├─ uvod.md                     # Co je Wall Reinforcement Wizard (overview)
│  ├─ instalace.md                # Instalace a spuštění pluginu
│  ├─ pruvodce/                   # Průvodce použitím (user guide section)
│  │  ├─ index.md                 # Section intro
│  │  ├─ prvni-spusteni.md        # První spuštění, připojení k Tekle
│  │  ├─ parametry-steny.md       # Nastavení parametrů stěny
│  │  ├─ hlavni-vyztu.md          # Hlavní výztuž (průměry, krytí, rozteče)
│  │  ├─ otvory.md                # Konfigurace otvorů
│  │  ├─ u-pruty.md               # U-pruty a okrajové prvky
│  │  ├─ trminky.md               # Třmínky a diagonály
│  │  ├─ preview.md               # Preview panel
│  │  ├─ validace.md              # Validační okno
│  │  └─ pdf-export.md            # PDF export
│  ├─ reference/                  # Referenční popis (all parameters)
│  │  ├─ index.md                 # Section intro
│  │  └─ parametry.md             # Kompletní seznam parametrů a jejich hodnot
│  ├─ faq.md                      # FAQ / Troubleshooting
│  └─ assets/                     # Images and screenshots
│     ├─ screenshots/             # UI screenshots (supplied later)
│     └─ diagrams/                # Workflow diagrams if needed
└─ overrides/                     # (optional) theme HTML overrides
   └─ partials/
      └─ ...
```

### Structure Rationale

- **`docs/index.md`:** MkDocs requires this as the root page. Keep it short — a paragraph about the plugin and links to Getting Started and the User Guide.
- **`docs/pruvodce/`:** User guide organised as a linear workflow. Follows the natural order a user performs steps in Tekla. Each page covers one screen / one concern.
- **`docs/reference/`:** Parameter reference is intentionally separate from the guide. Users return here frequently to look up a single value without re-reading the guide.
- **`docs/faq.md`:** Flat — not a folder. FAQ/Troubleshooting for this project's scope fits in a single page.
- **`docs/assets/screenshots/`:** Screenshots are stored inside `docs/` so MkDocs copies them to the built site. Grouped in a subfolder to avoid cluttering the page source files.
- **`requirements.txt`:** Pin exact versions of `mkdocs-material` and any plugins. Guarantees reproducible CI builds.
- **`.github/workflows/ci.yml`:** Single workflow file. Triggers on `push` to `main`. Runs `mkdocs gh-deploy --force`. No manual deployment steps needed.

---

## Architectural Patterns

### Pattern 1: Content-as-Config Navigation

**What:** The `nav:` key in `mkdocs.yml` defines the complete site navigation tree explicitly rather than relying on auto-discovery. Each entry maps a display label to a Markdown file path.

**When to use:** Always, when the page order matters (linear user guide). Auto-discovery sorts alphabetically, which rarely matches intended reading order.

**Trade-offs:** Navigation must be updated in `mkdocs.yml` when pages are added or renamed. This is a minor maintenance cost with a significant UX gain.

**Example:**
```yaml
nav:
  - Domů: index.md
  - Úvod: uvod.md
  - Instalace: instalace.md
  - Průvodce:
    - pruvodce/index.md
    - První spuštění: pruvodce/prvni-spusteni.md
    - Hlavní výztuž: pruvodce/hlavni-vyztu.md
    - Otvory: pruvodce/otvory.md
    - U-pruty: pruvodce/u-pruty.md
    - Třmínky: pruvodce/trminky.md
    - Preview: pruvodce/preview.md
    - Validace: pruvodce/validace.md
    - PDF export: pruvodce/pdf-export.md
  - Reference: reference/parametry.md
  - FAQ: faq.md
```

### Pattern 2: Admonitions for Contextual Callouts

**What:** MkDocs Material's built-in admonition syntax (`!!! note`, `!!! warning`, `!!! tip`) renders styled callout blocks without custom HTML.

**When to use:** Throughout the user guide — tip blocks for UI hints, warning blocks for destructive actions (e.g., overwriting existing rebars), note blocks for version-specific behaviour.

**Trade-offs:** Zero extra setup. Pure Markdown. The only cost is learning the syntax — which is trivial.

**Example:**
```markdown
!!! warning "Přepis existující výztuže"
    Plugin přepíše existující výztužné pruty v modelu Tekla.
    Ujistěte se, že máte zálohu modelu před generováním.

!!! tip
    Parametry lze uložit jako šablonu pro opakované použití.
```

### Pattern 3: Separate Guide vs. Reference Sections

**What:** User guide (how to do tasks) lives in `docs/pruvodce/`, parameter reference (what each setting means) lives in `docs/reference/`. These are distinct content types per the Diátaxis framework: "how-to" vs. "reference."

**When to use:** Any documentation that has both procedural steps and a large parameter set. The plugin has many parameters (diameters, cover, spacing, edge bars, openings, stirrups, diagonals) — burying them in the guide makes both worse.

**Trade-offs:** User must navigate between two sections when learning. Mitigated by cross-links: the guide page for each feature links to the relevant reference entry.

---

## Data Flow

### Content Build Flow

```
Author writes/edits .md file in docs/
          │
          ▼
git commit + push to main branch
          │
          ▼
GitHub Actions ci.yml triggers
          │
          ▼
pip install mkdocs-material (or cached)
          │
          ▼
mkdocs gh-deploy --force
    │
    ├── reads mkdocs.yml (nav, theme, plugins)
    ├── reads all docs/*.md (Markdown → HTML)
    ├── builds search index (lunr.js)
    ├── copies assets/ verbatim
    └── writes site/ output
          │
          ▼
ghp-import commits site/ to gh-pages branch
          │
          ▼
GitHub Pages CDN serves updated site
(usually live within 1-2 minutes)
```

### Reader Navigation Flow

```
User opens browser → GitHub Pages URL
          │
          ▼
Landing page (index.md) with overview + links
          │
    ┌─────┴──────────────────────┐
    │                            │
    ▼                            ▼
Navigation sidebar          Search bar
(linear guide flow)         (jump directly to topic)
    │                            │
    ▼                            ▼
Individual guide page        Search results → target page
    │
    ▼
Cross-links to Reference section (for parameter details)
    │
    ▼
FAQ / Troubleshooting (linked from error-prone guide steps)
```

### Key Data Flows

1. **Screenshot workflow:** Screenshots are created externally (user runs Tekla + plugin) and placed in `docs/assets/screenshots/`. The Markdown pages reference them with relative paths. The build pipeline copies them to `site/` unchanged. No transformation.

2. **Search index build:** MkDocs Material's built-in search plugin generates a client-side search index (JSON) at build time from all Markdown content. No server needed — search works entirely in the browser via JavaScript.

3. **Navigation state:** Navigation is stateless — all state lives in the URL. Each page is a standalone HTML file. The sidebar highlights the current page via URL matching in the Material theme JavaScript.

---

## Suggested Build Order

Dependencies between components determine what must exist before the next phase:

```
Phase 1: Foundation (no dependencies)
  mkdocs.yml skeleton
  docs/index.md
  requirements.txt
  .github/workflows/ci.yml
  GitHub Pages configured on gh-pages branch
  → Confirms: deploy pipeline works end-to-end

Phase 2: Content skeleton (depends on Phase 1)
  All page files created (empty or stub content)
  nav: tree completed in mkdocs.yml
  → Confirms: navigation structure is correct before writing content

Phase 3: User guide content (depends on Phase 2)
  docs/pruvodce/*.md written
  Admonitions, tips, warnings added
  Screenshot placeholders marked with [SCREENSHOT: dialog X]
  → First meaningful version of the wiki

Phase 4: Reference + FAQ (depends on Phase 3)
  docs/reference/parametry.md compiled
  docs/faq.md written
  Cross-links from guide to reference added

Phase 5: Screenshots (depends on Phase 3-4 knowing what to capture)
  Screenshots captured with running Tekla + plugin
  Placed in docs/assets/screenshots/
  Markdown image references substituted for placeholders

Phase 6: Polish (depends on Phase 5)
  Theme customisation (colours, logo) if desired
  SEO: site_description, social cards
  Final navigation review
```

Build order rationale:
- Phase 1 must come first: broken CI discovered early costs nothing; discovered at the end costs rework.
- Content skeleton before content: ensures nav structure is agreed before writing begins. Renaming pages after content is written breaks internal links.
- Screenshots last: they depend on a stable Tekla installation and a built model — an external dependency outside the wiki author's control. Text content must not wait on screenshots.

---

## Anti-Patterns

### Anti-Pattern 1: Screenshots inline with parameter descriptions

**What people do:** Mix procedural guide steps with exhaustive parameter lists on the same page.

**Why it's wrong:** Guide pages become huge and hard to scan. Users doing a task have to scroll past reference material; users looking up a parameter wade through narrative prose. Both audiences are poorly served.

**Do this instead:** Keep guide pages task-focused. Link to `reference/parametry.md` for the full parameter table.

### Anti-Pattern 2: Manual deployment from local machine

**What people do:** Run `mkdocs gh-deploy` locally instead of from CI.

**Why it's wrong:** Deployment becomes person-dependent. Local environment differences can produce different output. No audit trail of what was deployed and when.

**Do this instead:** Set up GitHub Actions CI in Phase 1 and never deploy manually after that.

### Anti-Pattern 3: Committing the `site/` build output to main branch

**What people do:** Add `site/` to git on the main branch alongside source files.

**Why it's wrong:** `site/` is regenerated on every build. Committing it pollutes history, creates merge conflicts, and doubles repo size. `gh-deploy` manages the `gh-pages` branch separately — this is its entire purpose.

**Do this instead:** Add `site/` to `.gitignore`. Let `gh-deploy` manage `gh-pages` branch exclusively.

### Anti-Pattern 4: All documentation in a single flat directory

**What people do:** Put every page directly in `docs/` with no subfolders.

**Why it's wrong:** Works at 5-8 pages; becomes unnavigable at 15+. File names like `otvory.md` and `otvory-parametry.md` at the same level create confusion.

**Do this instead:** Group by section (`docs/pruvodce/`, `docs/reference/`) from the start. Reorganising later breaks all existing internal links.

---

## Integration Points

### External Services

| Service | Integration Pattern | Notes |
|---------|---------------------|-------|
| GitHub Pages | `gh-pages` branch auto-served by GitHub | Free for public repos; configure in repo Settings → Pages |
| GitHub Actions | CI reads `requirements.txt`, builds, deploys | Needs `contents: write` permission in workflow |
| Tekla Structures (screenshot source) | None — screenshots delivered as static files | External dependency; no API or live integration |

### Internal Boundaries

| Boundary | Communication | Notes |
|----------|---------------|-------|
| `mkdocs.yml` ↔ `docs/` | MkDocs engine joins nav config with file system | File paths in `nav:` must match actual `.md` file paths exactly |
| `docs/*.md` ↔ `docs/assets/` | Relative Markdown image paths | Use `../assets/screenshots/dialog.png` from subfolders or `assets/screenshots/dialog.png` from root |
| GitHub Actions ↔ `gh-pages` branch | `ghp-import` force-pushes built output | `gh-pages` is fully managed by CI — never manually edit it |
| Reader browser ↔ Search index | Client-side JS (lunr) reads JSON index | No server required; works offline after first load |

---

## Scaling Considerations

This is a single-product user documentation wiki. Scaling in terms of traffic is handled entirely by GitHub Pages CDN — no action required. Scaling in terms of content volume is the relevant concern.

| Scale | Architecture Adjustments |
|-------|--------------------------|
| Up to ~20 pages (expected) | Current structure is sufficient. No changes needed. |
| 20-50 pages | Add section index pages (`docs/pruvodce/index.md`, `docs/reference/index.md`) as overviews. Enable `navigation.tabs` in Material for top-level section tabs. |
| 50+ pages | Enable `navigation.sections` + `navigation.expand` in Material. Consider splitting guide into "Základy" and "Pokročilé" sub-sections. |

---

## Sources

- [Creating your site — Material for MkDocs](https://squidfunk.github.io/mkdocs-material/creating-your-site/)
- [Publishing your site — Material for MkDocs](https://squidfunk.github.io/mkdocs-material/publishing-your-site/)
- [Setting up navigation — Material for MkDocs](https://squidfunk.github.io/mkdocs-material/setup/setting-up-navigation/)
- [Customization — Material for MkDocs](https://squidfunk.github.io/mkdocs-material/customization/)
- [Writing Your Docs — MkDocs](https://www.mkdocs.org/user-guide/writing-your-docs/)
- [Information architecture best practices — GitBook](https://gitbook.com/docs/guides/docs-best-practices/documentation-structure-tips)
- [Admonitions — Material for MkDocs](https://squidfunk.github.io/mkdocs-material/reference/admonitions/)

---
*Architecture research for: MkDocs Material static wiki, GitHub Pages deployment*
*Researched: 2026-03-25*
