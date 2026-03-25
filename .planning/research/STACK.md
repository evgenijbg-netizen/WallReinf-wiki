# Stack Research

**Domain:** Static documentation wiki / user manual site
**Researched:** 2026-03-25
**Confidence:** HIGH (verified with PyPI, official Material for MkDocs docs, GitHub releases)

---

## Recommended Stack

### Core Technologies

| Technology | Version | Purpose | Why Recommended |
|------------|---------|---------|-----------------|
| MkDocs | 1.6.1 | Static site build engine | Markdown-in, HTML-out. Minimal config. Purpose-built for docs, not a general SSG repurposed for docs. |
| Material for MkDocs | 9.7.6 | Theme + feature layer | The de-facto standard for technical documentation. Provides built-in search, navigation, admonitions, tabs, image lightbox hooks, and full Czech (`cs`) UI localization out of the box. |
| Python | 3.10+ | Runtime for MkDocs | Required by mkdocs + mkdocs-material. 3.10+ recommended for CI; >=3.8 is the official minimum. |
| GitHub Actions | — | CI/CD deploy pipeline | Official recommended deploy path for GitHub Pages. `mkdocs gh-deploy --force` pushes to `gh-pages` branch automatically on every push to `main`. |

### Supporting Libraries

| Library | Version | Purpose | When to Use |
|---------|---------|---------|-------------|
| mkdocs-glightbox | 0.5.2 | Image lightbox / zoom on click | Always — the wiki is screenshot-heavy. Lets users click any image to see it full-size without leaving the page. Pure JS, zero-config. |
| pymdownx (PyMdown Extensions) | bundled with material | Admonitions, content tabs, superfences, annotations | Always — ships with mkdocs-material, no separate install. Enables `!!! note`, collapsible blocks, and nested code tabs. |

### Development Tools

| Tool | Purpose | Notes |
|------|---------|-------|
| `mkdocs serve` | Local preview with live-reload | Run locally during authoring; auto-refreshes on file save. Access at `http://127.0.0.1:8000`. |
| `pip` + `requirements.txt` | Dependency pinning | Pin exact versions in `requirements.txt` so CI reproduces local builds exactly. Use `pip freeze > requirements.txt` after local install. |
| VS Code + Markdown Preview Enhanced | Authoring experience | Optional but practical; gives side-by-side preview. MkDocs extensions (admonitions etc.) won't render in VS Code preview, but prose structure is visible. |

---

## Installation

```bash
# Core — run once to set up the project
pip install mkdocs-material==9.7.6
pip install mkdocs-glightbox==0.5.2

# Pin versions for reproducible CI builds
pip freeze > requirements.txt
```

GitHub Actions workflow (`.github/workflows/deploy.yml`):

```yaml
name: Deploy docs

on:
  push:
    branches: [main]

permissions:
  contents: write

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-python@v5
        with:
          python-version: 3.x
          cache: pip
      - run: pip install -r requirements.txt
      - run: mkdocs gh-deploy --force
```

Minimal `mkdocs.yml`:

```yaml
site_name: Wall Reinforcement Wizard — Uživatelský manuál
site_url: https://<org>.github.io/WallReinf-wiki/

theme:
  name: material
  language: cs
  features:
    - navigation.tabs
    - navigation.sections
    - navigation.top
    - search.highlight
    - content.code.copy

plugins:
  - search:
      lang: cs
  - glightbox

markdown_extensions:
  - admonition
  - pymdownx.details
  - pymdownx.superfences
  - pymdownx.tabbed:
      alternate_style: true
  - attr_list
  - md_in_html
```

---

## Alternatives Considered

| Recommended | Alternative | When to Use Alternative |
|-------------|-------------|-------------------------|
| MkDocs Material | Docusaurus (React/Node) | When you need versioned docs, or the team is JS-native and wants to embed React components. Overkill for a single-version user manual with no code samples. Requires Node.js build chain. |
| MkDocs Material | VitePress (Vue/Vite) | When you're already in the Vue ecosystem. No advantage here; adds JS toolchain without benefit. |
| MkDocs Material | Sphinx + Read the Docs theme | When the primary audience is Python developers expecting API reference docs in RST. Wrong fit for a Czech-language user manual. |
| MkDocs Material | Zensical | When Zensical reaches 1.0 and has feature parity with Material. Currently at v0.0.29 (March 2026), pre-release, actively fixing Windows bugs. **Not ready for production.** |
| GitHub Actions deploy | `mkdocs gh-deploy` from local machine | Never do this — manual deploys from dev machines break CI/CD, cause branch conflicts, and make the deploy process invisible to collaborators. |

---

## What NOT to Use

| Avoid | Why | Use Instead |
|-------|-----|-------------|
| Zensical (now) | Pre-release (v0.0.29 as of 2026-03-24). Missing features, active Windows bug fixes, no stable API. The team is the same as Material for MkDocs so migration later will be straightforward when it matures. | MkDocs Material 9.7.6 |
| MkDocs Insider features (Sponsor tier) | As of November 2025, Insiders features were made free for everyone. The Insiders repo will be deleted May 1, 2026. All previously-gated features are now in the public release. Do not pay for or reference the old Insiders tier. | Public mkdocs-material 9.7.6 |
| mkdocs-static-i18n plugin | Only needed for multi-language sites serving the same content in multiple languages. This wiki is Czech-only. Adds unnecessary complexity. | Built-in `language: cs` in mkdocs.yml |
| Manual image resizing/optimization scripts | Material's built-in `optimize` plugin handles PNG compression via pngquant automatically. Don't add a separate image pipeline. | Built-in optimize plugin (already in mkdocs-material) |
| Wiki features of GitHub (GitHub Wiki) | No custom theme, no search across pages, no navigation tree, no admonitions, not deployable as a standalone site. | MkDocs Material on GitHub Pages |

---

## Stack Patterns by Variant

**This project — Czech-only, single-version, screenshot-heavy user manual:**
- Use `language: cs` in theme config — Material ships with a full Czech translation of all UI strings
- Use `glightbox` plugin — mandatory for a screenshot-heavy manual so users can zoom images
- Use `navigation.tabs` — organizes top-level sections (Getting Started, Features, Troubleshooting) without sidebar clutter
- No versioning plugin needed (single version of the plugin documented at a time)

**If the project later needs multiple language versions:**
- Add Docusaurus or use the `mkdocs-static-i18n` plugin
- Restructure content into `docs/cs/` and `docs/en/` subtrees
- This is out of scope for v1

**If MkDocs Material reaches end-of-life before Zensical is stable (risk: mid-2027+):**
- Zensical reads `mkdocs.yml` natively — migration is a drop-in for most projects
- Monitor Zensical for 1.0 release; migration effort should be low given same team authored both tools

---

## Version Compatibility

| Package | Compatible With | Notes |
|---------|-----------------|-------|
| mkdocs-material 9.7.6 | mkdocs 1.6.1 | Verified — PyPI dependency resolution; Material specifies `mkdocs>=1.6` |
| mkdocs-material 9.7.6 | Python >=3.8 | 3.10+ recommended in CI for broader stdlib support |
| mkdocs-glightbox 0.5.2 | mkdocs-material 9.x | Verified compatible; no known issues with 9.7.x |
| mkdocs 1.6.1 | MkDocs 2.0 (upcoming) | **Incompatible** — Material 9.x will NOT work with MkDocs 2.0 when it releases. Material 9.7.2 release notes explicitly warn about this. Zensical is the forward-compatible path. |

---

## Maintenance Mode Notice

Material for MkDocs entered maintenance mode on November 11, 2025. The team announced:

- **No new features** will be added to Material for MkDocs
- **Critical bug fixes and security patches** will be provided for at least 12 months (through ~November 2026)
- **Zensical** is the successor being built by the same team

**Impact on this project:** Zero for a documentation wiki with a focused, stable feature set. The features needed (search, navigation, admonitions, Czech UI, image lightbox, GitHub Pages deploy) are all fully present in 9.7.6 and will not be removed. Plan a migration assessment to Zensical in late 2026 / early 2027 when it approaches 1.0.

---

## Sources

- [mkdocs-material on PyPI](https://pypi.org/project/mkdocs-material/) — version 9.7.6 confirmed (March 19, 2026) — HIGH confidence
- [mkdocs on PyPI](https://pypi.org/project/mkdocs/) — version 1.6.1 confirmed (August 30, 2024) — HIGH confidence
- [mkdocs-glightbox on PyPI](https://pypi.org/project/mkdocs-glightbox/) — version 0.5.2 confirmed (October 23, 2025) — HIGH confidence
- [Material for MkDocs: Publishing your site](https://squidfunk.github.io/mkdocs-material/publishing-your-site/) — GitHub Actions workflow pattern — HIGH confidence
- [Material for MkDocs: Changing the language](https://squidfunk.github.io/mkdocs-material/setup/changing-the-language/) — Czech `cs` language support confirmed — HIGH confidence
- [Zensical GitHub releases](https://github.com/zensical/zensical/releases) — v0.0.29 pre-release status confirmed (March 24, 2026) — HIGH confidence
- [Zensical announcement](https://squidfunk.github.io/mkdocs-material/blog/2025/11/05/zensical/) — maintenance mode rationale and migration path — HIGH confidence
- [Material for MkDocs maintenance mode announcement](https://squidfunk.github.io/mkdocs-material/blog/2025/11/11/insiders-now-free-for-everyone/) — Insiders now free, MkDocs 2.0 incompatibility warning — HIGH confidence
- [Documentation Generator Comparison 2025](https://okidoki.dev/documentation-generator-comparison) — Docusaurus/VitePress/MkDocs comparison — MEDIUM confidence (third-party)

---

*Stack research for: WallReinf Wiki — static documentation site for a C#/WPF Tekla Structures plugin*
*Researched: 2026-03-25*
