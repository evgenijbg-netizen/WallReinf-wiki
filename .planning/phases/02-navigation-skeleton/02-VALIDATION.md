---
phase: 2
slug: navigation-skeleton
status: draft
nyquist_compliant: false
wave_0_complete: false
created: 2026-03-26
---

# Phase 2 — Validation Strategy

> Per-phase validation contract for feedback sampling during execution.

---

## Test Infrastructure

| Property | Value |
|----------|-------|
| **Framework** | MkDocs built-in strict build (`mkdocs build --strict`) |
| **Config file** | `mkdocs.yml` (root) |
| **Quick run command** | `mkdocs build --strict` |
| **Full suite command** | `mkdocs build --strict` |
| **Estimated runtime** | ~5 seconds |

---

## Sampling Rate

- **After every task commit:** Run `mkdocs build --strict`
- **After every plan wave:** Run `mkdocs build --strict`
- **Before `/gsd:verify-work`:** Full suite must be green
- **Max feedback latency:** 5 seconds

---

## Per-Task Verification Map

| Task ID | Plan | Wave | Requirement | Test Type | Automated Command | File Exists | Status |
|---------|------|------|-------------|-----------|-------------------|-------------|--------|
| 02-01 | 01 | 1 | NAV-01 | smoke | `grep "nav:" mkdocs.yml` | Wave 0 | ⬜ pending |
| 02-02 | 01 | 1 | NAV-02, NAV-06 | smoke | `mkdocs build --strict` + `find docs/ -name "*.md" \| grep -P "[^\x00-\x7F]"` | Wave 0 | ⬜ pending |

*Status: ⬜ pending · ✅ green · ❌ red · ⚠️ flaky*

---

## Wave 0 Requirements

- [ ] `docs/pruvodce/index.md` — section index
- [ ] `docs/pruvodce/pozadavky.md` through `docs/pruvodce/pdf-export.md` — 11 guide stubs
- [ ] `docs/reference/index.md` — section index
- [ ] `docs/reference/parametry.md` — parameter reference stub
- [ ] `docs/faq.md` — FAQ stub
- [ ] `mkdocs.yml` nav expansion — full tree

---

## Manual-Only Verifications

| Behavior | Requirement | Why Manual | Test Instructions |
|----------|-------------|------------|-------------------|
| Sidebar shows Průvodce and Reference sections | NAV-03 | Requires visual browser check | Open site, verify sidebar has both sections with subsections |
| On-page TOC on every page | NAV-04 | Requires visual browser check | Navigate to a page with H2 headings, verify right-side TOC |
| Breadcrumbs visible | NAV-05 | Requires visual browser check | On any subpage, verify breadcrumbs above content |
| URLs contain no encoded Czech chars | NAV-06 | Requires URL inspection | Check browser URL bar on 3+ pages |

---

## Validation Sign-Off

- [ ] All tasks have `<automated>` verify or Wave 0 dependencies
- [ ] Sampling continuity: no 3 consecutive tasks without automated verify
- [ ] Wave 0 covers all MISSING references
- [ ] No watch-mode flags
- [ ] Feedback latency < 5s
- [ ] `nyquist_compliant: true` set in frontmatter

**Approval:** pending
