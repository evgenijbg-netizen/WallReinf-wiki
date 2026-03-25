# Pitfalls Research

**Domain:** Static documentation wiki for a desktop application plugin (MkDocs Material + GitHub Pages)
**Researched:** 2026-03-25
**Confidence:** HIGH

---

## Critical Pitfalls

### Pitfall 1: Feature-Based Structure Instead of Task-Based Structure

**What goes wrong:**
The wiki mirrors the UI structure — one page per dialog, one section per parameter group — rather than organizing around what users are trying to accomplish. Users arrive with questions like "how do I add openings to a wall?" not "what is the Openings dialog?". Feature-based docs force them to hunt across multiple pages to complete a single task.

**Why it happens:**
It is natural to document what you built. When you know the software deeply, the UI structure feels logical. The temptation is to walk through every tab and field in order.

**How to avoid:**
Start content planning from user goals, not from the UI tree. Main sections should be workflows ("Nastavení projektu", "Generování výztuže", "Export do PDF"), not UI panels. Keep reference content (field-by-field descriptions) as a secondary section. Use the Diátaxis framework as a mental model: tutorials and how-to guides first, reference second.

**Warning signs:**
- Section titles that match dialog or tab names exactly
- Pages that describe every field on a screen without explaining when or why to change them
- No "getting started" flow — docs open directly into parameter descriptions

**Phase to address:**
Information architecture phase (before any content is written). Define the navigation structure and page outline before drafting a single page.

---

### Pitfall 2: Missing `site_url` Causes Broken Navigation and Search on GitHub Pages

**What goes wrong:**
When `site_url` is not set (or set incorrectly) in `mkdocs.yml`, deployed assets use relative paths that break when a user lands on a 404 page, a deep-linked URL, or the root of a GitHub Pages project site (e.g., `https://user.github.io/WallReinf-wiki/`). Navigation links, CSS, and the search index all stop working from the 404 page.

**Why it happens:**
`site_url` is optional during local development (`mkdocs serve`) where everything works from localhost. The problem only surfaces after deploy to GitHub Pages with a subpath URL.

**How to avoid:**
Set `site_url` in `mkdocs.yml` from day one with the full GitHub Pages URL including trailing slash:
```yaml
site_url: https://<username>.github.io/WallReinf-wiki/
```
Also configure `use_directory_urls: true` (the default) and verify it before the first deploy. Create a custom `docs/404.md` page using absolute links only.

**Warning signs:**
- Navigating to a non-existent page results in a completely broken layout (no CSS, no nav)
- Search bar does not function after a hard refresh on a deep page
- Assets 404 when URL contains a subpath

**Phase to address:**
Infrastructure setup phase. Fix `mkdocs.yml` configuration before deploying anything, even a skeleton site.

---

### Pitfall 3: Screenshots Become Stale and Erode Trust

**What goes wrong:**
Screenshots show UI elements, dialogs, or parameter names that no longer match the current version of the plugin. Engineers following the docs get confused when the screenshot does not match what they see. In niche professional software (Tekla plugin), users have high domain expertise and notice discrepancies immediately — outdated screenshots destroy credibility faster than missing content.

**Why it happens:**
Screenshots are expensive to produce (require running Tekla Structures with a real model), so they are taken once and never updated. Plugin UI evolves. The disconnect grows silently.

**How to avoid:**
- Use screenshots strategically: only for high-value steps where visual confirmation genuinely helps (first launch, main dialog overview, validation result). Do not screenshot every field.
- Caption every screenshot with the plugin version it was taken from (e.g., "Screenshot: WRW v1.0").
- Keep screenshots in a dedicated folder (`docs/assets/screenshots/`) with descriptive filenames that include the dialog name, making replacements easy to track.
- Treat "update screenshots" as a required step in any release checklist for the plugin.

**Warning signs:**
- Screenshots are numbered sequentially (screenshot01.png) rather than named by subject — indicates no update strategy was planned
- No version annotation on screenshots
- Screenshot count exceeds 20 for a v1 manual — likely over-screenshotted

**Phase to address:**
Content creation phase. Establish the screenshot strategy (what to capture, naming conventions, version tagging) before taking any screenshots. The constraint that screenshots require a running Tekla instance means this must be planned, not improvised.

---

### Pitfall 4: MkDocs 1.x / Material Ecosystem Instability (MkDocs 2.0 Incompatibility)

**What goes wrong:**
MkDocs 2.0 (released 2026) is fundamentally incompatible with Material for MkDocs. MkDocs 2.0 removes the plugin system, switches from YAML to TOML configuration, and changes how theming works. Material for MkDocs has entered maintenance mode — no new features, only critical bug fixes for ~12 months. Upgrading MkDocs to 2.x will silently or loudly break the entire site.

**Why it happens:**
Running `pip install --upgrade mkdocs` or unpinned dependencies in `requirements.txt` will install MkDocs 2.x.

**How to avoid:**
Pin all dependencies explicitly in `requirements.txt`:
```
mkdocs==1.6.x
mkdocs-material==9.x.x
```
Use a `requirements.txt` committed to the repository. In the GitHub Actions workflow, install from the pinned file (`pip install -r requirements.txt`), never from unpinned `pip install mkdocs-material`.

The Material for MkDocs team is developing Zensical as a forward-compatible alternative — monitor this, but do not block on it for v1.

**Warning signs:**
- `requirements.txt` absent or contains `mkdocs-material` without a pinned version
- GitHub Actions workflow installs `mkdocs-material` without specifying version
- Build fails after a routine `pip upgrade`

**Phase to address:**
Infrastructure setup phase. Pin dependencies in the very first commit.

---

### Pitfall 5: GitHub Actions Deploy Fails Silently Due to Missing Write Permissions

**What goes wrong:**
The GitHub Actions workflow runs without error but the `gh-pages` branch is never updated, or the first deploy silently fails because the `GITHUB_TOKEN` does not have write access to the repository contents. The GitHub Pages URL either 404s or shows stale content.

**Why it happens:**
GitHub repository defaults changed — workflow permissions default to read-only in newer repositories. The deploy step requires `contents: write` permission explicitly.

**How to avoid:**
In `mkdocs.yml` CI workflow, add explicit permissions:
```yaml
permissions:
  contents: write
```
After the first successful deploy, manually verify GitHub Pages is configured to serve from the `gh-pages` branch in repository Settings > Pages. The URL will not appear in Settings until the first deploy completes successfully.

**Warning signs:**
- Workflow completes with green checkmark but GitHub Pages URL returns 404
- No `gh-pages` branch exists in the repository after a deploy run
- Settings > Pages shows no URL

**Phase to address:**
Infrastructure setup phase. Test the full deploy pipeline with a minimal one-page skeleton before writing any real content.

---

## Technical Debt Patterns

| Shortcut | Immediate Benefit | Long-term Cost | When Acceptable |
|----------|-------------------|----------------|-----------------|
| Undeclared nav in `mkdocs.yml` (auto-discovery) | No nav to maintain | File renames silently reorder or break navigation; no control over page order | Never — define nav explicitly from the start |
| No `requirements.txt`, install latest | Simpler setup | MkDocs 2.x upgrade breaks the entire build | Never |
| Screenshot every dialog and field | Feels complete | High update burden when UI changes; content feels like a UI walkthrough rather than a guide | Never for v1 — screenshot sparingly |
| Mixing Czech and English in filenames/slugs | Familiar naming | URLs contain special characters or transliterations that break bookmarks and links | Never — use ASCII slugs, Czech content |
| Writing all content in one long page | Fast initial draft | Hard to navigate, no anchor links, impossible to search effectively | Never — use a proper page-per-topic structure |

---

## Integration Gotchas

| Integration | Common Mistake | Correct Approach |
|-------------|----------------|------------------|
| GitHub Pages | Configuring Pages to serve from `main` branch `/docs` folder instead of `gh-pages` branch | Set Pages source to `gh-pages` branch root; let the CI workflow manage it |
| GitHub Actions | Using deprecated `actions/checkout@v2` or `actions/setup-python@v2` | Use `@v4` versions — older versions have known issues with newer GitHub runners |
| MkDocs search | Forgetting to set `lang: cs` in search plugin config | Czech text without the Czech stemmer produces poor search results — set `plugins.search.lang: cs` |
| MkDocs language | Setting `theme.language: cs` but forgetting search lang | These are separate settings; both must be set for full Czech support |

---

## Performance Traps

Static sites for documentation at this scale (< 50 pages, single language) have no meaningful performance concerns. The only trap relevant here:

| Trap | Symptoms | Prevention | When It Breaks |
|------|----------|------------|----------------|
| Unoptimized screenshots (full-resolution PNGs from Tekla) | Slow page load, large repository size | Compress screenshots before committing (target < 200 KB per image); use PNG for UI screenshots, not JPEG | At > 10 uncompressed screenshots, repository size and page load become noticeable |

---

## UX Pitfalls

| Pitfall | User Impact | Better Approach |
|---------|-------------|-----------------|
| No getting-started path — docs open directly into parameter reference | New users are overwhelmed; experienced users cannot find workflow guidance | Add a prominent "Začínáme" (Getting Started) section as the first nav item, covering installation and first use |
| All pages at the same nav level (flat structure) | Users cannot gauge complexity or find related content | Use a two-level nav: top-level sections (Úvod, Návod k použití, Reference, FAQ), sub-pages within each |
| FAQ buried deep in nav | Users with problems cannot find troubleshooting content | FAQ / Troubleshooting should be a top-level nav item, not nested inside a section |
| No cross-links between pages | Users read one page and do not know where to go next | Every procedure page should link to "related" reference content; the reference should link back to the how-to that uses it |
| Czech content with English UI element names (from plugin) | Inconsistent reading experience; engineers may not recognize dialog names | Decide a consistent convention: either translate UI element names or quote them in their original English form in italics |

---

## "Looks Done But Isn't" Checklist

- [ ] **Navigation:** Defined explicitly in `mkdocs.yml` `nav:` key — verify no pages are missing from nav (orphan pages exist but are unreachable)
- [ ] **Search:** `lang: cs` set in search plugin config — verify by searching for a Czech-specific word with diacritics (e.g., "výztuž")
- [ ] **Deploy:** GitHub Pages URL returns 200, not 404 — verify by visiting the URL in a private browser window (no cache)
- [ ] **Internal links:** All `[text](../page.md)` links resolve — run `mkdocs build --strict` which treats broken links as errors
- [ ] **Screenshots:** Every screenshot has an alt text — required for accessibility, fails silently otherwise
- [ ] **site_url:** Set to the actual GitHub Pages URL — verify by checking that the canonical link in page source points to the correct domain
- [ ] **404 page:** Custom `404.md` exists and renders correctly with working navigation links

---

## Recovery Strategies

| Pitfall | Recovery Cost | Recovery Steps |
|---------|---------------|----------------|
| Wrong navigation structure discovered after content is written | MEDIUM | Restructure `nav:` in `mkdocs.yml`; rename/move files; update all internal cross-links; rebuild and redeploy |
| Screenshots all outdated after a plugin UI update | HIGH | Identify which dialogs changed; retake only those screenshots; re-export from Tekla; update page content to match |
| MkDocs accidentally upgraded to 2.x | LOW (if dependencies were pinned) / HIGH (if not) | Pin `mkdocs<2.0` in `requirements.txt`; if build is broken, roll back to last working commit and pin immediately |
| `site_url` misconfigured, deployed to production | LOW | Correct `site_url` in `mkdocs.yml`; push; CI redeploys automatically within minutes |
| GitHub Pages serving wrong branch | LOW | Change source branch in Settings > Pages to `gh-pages`; no content changes needed |

---

## Pitfall-to-Phase Mapping

| Pitfall | Prevention Phase | Verification |
|---------|------------------|--------------|
| Feature-based instead of task-based structure | Information architecture phase (Phase 1) | Review nav outline against user task list before writing any content |
| Missing `site_url` breaks GitHub Pages | Infrastructure setup phase (Phase 1) | Deploy a one-page skeleton and confirm the URL loads with CSS intact |
| Screenshots become stale | Content creation phase (Phase 2) | Screenshot naming conventions and version tagging established before first screenshot is taken |
| MkDocs 2.x incompatibility | Infrastructure setup phase (Phase 1) | `requirements.txt` with pinned versions committed; CI installs from it |
| GitHub Actions deploy fails silently | Infrastructure setup phase (Phase 1) | Verify `gh-pages` branch exists and Pages URL is live after first CI run |
| Search does not work for Czech diacritics | Infrastructure setup phase (Phase 1) | Search for "výztuž" on the live site and confirm results appear |
| Orphan pages unreachable from nav | Content creation phase (Phase 2) | Run `mkdocs build --strict` as part of CI to catch orphaned pages |

---

## Sources

- [Material for MkDocs — What MkDocs 2.0 means for your documentation projects](https://squidfunk.github.io/mkdocs-material/blog/2026/02/18/mkdocs-2.0/) — HIGH confidence (official blog)
- [Material for MkDocs — Publishing your site](https://squidfunk.github.io/mkdocs-material/publishing-your-site/) — HIGH confidence (official docs)
- [Material for MkDocs — Setting up site search](https://squidfunk.github.io/mkdocs-material/setup/setting-up-site-search/) — HIGH confidence (official docs)
- [Material for MkDocs — Changing the language](https://squidfunk.github.io/mkdocs-material/setup/changing-the-language/) — HIGH confidence (official docs)
- [MkDocs issue #2520 — site_url configuration and 404 support](https://github.com/squidfunk/mkdocs-material/issues/2520) — HIGH confidence (official issue tracker)
- [Should you add screenshots to documentation? — This Is Important](https://thisisimportant.net/posts/screenshots-in-documentation/) — MEDIUM confidence
- [Why Documentation Gets Outdated — Glitter AI](https://www.glitter.io/blog/process-documentation/why-documentation-gets-outdated) — MEDIUM confidence
- [How to structure technical documentation — GitBook](https://gitbook.com/docs/guides/docs-best-practices/documentation-structure-tips) — MEDIUM confidence
- [User Documentation best practices — Archbee](https://www.archbee.com/blog/user-documentation-best-practices) — MEDIUM confidence
- [Deploying MkDocs to GitHub Pages with GitHub Actions — Thomas Thornton](https://thomasthornton.cloud/2024/05/01/deploying-mkdocs-to-github-pages-with-github-actions/) — MEDIUM confidence

---

*Pitfalls research for: Static documentation wiki (MkDocs Material + GitHub Pages) for a desktop application plugin*
*Researched: 2026-03-25*
