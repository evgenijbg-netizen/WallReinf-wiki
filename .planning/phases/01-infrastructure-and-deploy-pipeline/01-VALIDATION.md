---
phase: 1
slug: infrastructure-and-deploy-pipeline
status: draft
nyquist_compliant: false
wave_0_complete: false
created: 2026-03-26
---

# Phase 1 — Validation Strategy

> Per-phase validation contract for feedback sampling during execution.

---

## Test Infrastructure

| Property | Value |
|----------|-------|
| **Framework** | MkDocs built-in strict build (`mkdocs build --strict`) |
| **Config file** | `mkdocs.yml` (root) |
| **Quick run command** | `mkdocs build --strict` |
| **Full suite command** | `mkdocs build --strict` + live site smoke checks |
| **Estimated runtime** | ~5 seconds |

---

## Sampling Rate

- **After every task commit:** Run `mkdocs build --strict`
- **After every plan wave:** Run `mkdocs build --strict` + grep checks for all INFRA requirements
- **Before `/gsd:verify-work`:** Full suite must be green + live site accessible
- **Max feedback latency:** 5 seconds

---

## Per-Task Verification Map

| Task ID | Plan | Wave | Requirement | Test Type | Automated Command | File Exists | Status |
|---------|------|------|-------------|-----------|-------------------|-------------|--------|
| 01-01 | 01 | 1 | INFRA-01 | smoke | `grep "mkdocs==1.6.1" requirements.txt && grep "mkdocs-material==9.7.6" requirements.txt` | Wave 0 | ⬜ pending |
| 01-02 | 01 | 1 | INFRA-05 | smoke | `grep "evgenijbg-netizen.github.io/WallReinf-wiki" mkdocs.yml` | Wave 0 | ⬜ pending |
| 01-03 | 01 | 1 | INFRA-03 | smoke | `grep "lang: cs" mkdocs.yml` (must appear twice — theme + search) | Wave 0 | ⬜ pending |
| 01-04 | 01 | 1 | INFRA-04 | smoke | `grep "toggle" mkdocs.yml` | Wave 0 | ⬜ pending |
| 01-05 | 01 | 1 | INFRA-06 | smoke | `grep "^site/" .gitignore` | Wave 0 | ⬜ pending |
| 01-06 | 01 | 1 | INFRA-02, INFRA-07 | smoke | `grep "contents: write" .github/workflows/ci.yml && grep "branches: \[main\]" .github/workflows/ci.yml` | Wave 0 | ⬜ pending |
| 01-07 | 01 | 1 | ALL | integration | `mkdocs build --strict` | Wave 0 | ⬜ pending |

*Status: ⬜ pending · ✅ green · ❌ red · ⚠️ flaky*

---

## Wave 0 Requirements

- [ ] `mkdocs.yml` — master config covering INFRA-01 through INFRA-05
- [ ] `requirements.txt` — pinned dependencies (INFRA-01)
- [ ] `.github/workflows/ci.yml` — CI/CD pipeline (INFRA-02, INFRA-07)
- [ ] `.gitignore` — excludes site/ (INFRA-06)
- [ ] `docs/index.md` — required by MkDocs
- [ ] `docs/assets/logo.png` — copied from repo root

---

## Manual-Only Verifications

| Behavior | Requirement | Why Manual | Test Instructions |
|----------|-------------|------------|-------------------|
| Live site accessible at GitHub Pages URL | INFRA-02, INFRA-05 | Requires deployed site on GitHub Pages | Visit `https://evgenijbg-netizen.github.io/WallReinf-wiki/` — page loads with Material styling |
| Czech search returns results | INFRA-03 | Requires live search index | Type "výztuž" in search bar — result appears |
| Light/dark mode toggle works | INFRA-04 | Requires visual verification | Click toggle icon in header — theme switches |
| gh-pages branch exists | INFRA-02 | Requires GitHub API or UI check | Check GitHub repo branches — `gh-pages` present |

---

## Validation Sign-Off

- [ ] All tasks have `<automated>` verify or Wave 0 dependencies
- [ ] Sampling continuity: no 3 consecutive tasks without automated verify
- [ ] Wave 0 covers all MISSING references
- [ ] No watch-mode flags
- [ ] Feedback latency < 5s
- [ ] `nyquist_compliant: true` set in frontmatter

**Approval:** pending
