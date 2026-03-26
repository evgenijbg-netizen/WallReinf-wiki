---
phase: 3
slug: user-guide-content
status: draft
nyquist_compliant: false
wave_0_complete: false
created: 2026-03-26
---

# Phase 3 — Validation Strategy

> Per-phase validation contract for feedback sampling during execution.

---

## Test Infrastructure

| Property | Value |
|----------|-------|
| **Framework** | `mkdocs build --strict` (static site build validation) |
| **Config file** | `mkdocs.yml` (project root) |
| **Quick run command** | `mkdocs build --strict 2>&1 \| tail -5` |
| **Full suite command** | `mkdocs build --strict` |
| **Estimated runtime** | ~5 seconds |

---

## Sampling Rate

- **After every task commit:** Run `mkdocs build --strict 2>&1 | tail -5`
- **After every plan wave:** Run `mkdocs build --strict`
- **Before `/gsd:verify-work`:** Full suite must be green
- **Max feedback latency:** 5 seconds

---

## Per-Task Verification Map

| Task ID | Plan | Wave | Requirement | Test Type | Automated Command | File Exists | Status |
|---------|------|------|-------------|-----------|-------------------|-------------|--------|
| 03-01-01 | 01 | 1 | START-01 | smoke | `mkdocs build --strict` | ✅ (stub) | ⬜ pending |
| 03-01-02 | 01 | 1 | START-02 | smoke | `mkdocs build --strict` | ✅ (stub) | ⬜ pending |
| 03-01-03 | 01 | 1 | START-03 | smoke | `mkdocs build --strict` | ✅ (stub) | ⬜ pending |
| 03-01-04 | 01 | 1 | START-04 | smoke | `mkdocs build --strict` | ✅ (stub) | ⬜ pending |
| 03-02-01 | 02 | 1 | GUIDE-01 | smoke | `mkdocs build --strict` | ✅ (stub) | ⬜ pending |
| 03-02-02 | 02 | 1 | GUIDE-02 | smoke | `mkdocs build --strict` | ✅ (stub) | ⬜ pending |
| 03-02-03 | 02 | 1 | GUIDE-03 | smoke | `mkdocs build --strict` | ✅ (stub) | ⬜ pending |
| 03-02-04 | 02 | 1 | GUIDE-04 | smoke | `mkdocs build --strict` | ✅ (stub) | ⬜ pending |
| 03-02-05 | 02 | 1 | GUIDE-05 | smoke | `mkdocs build --strict` | ✅ (stub) | ⬜ pending |
| 03-02-06 | 02 | 1 | GUIDE-06 | smoke | `mkdocs build --strict` | ✅ (stub) | ⬜ pending |
| 03-02-07 | 02 | 1 | GUIDE-07 | smoke | `mkdocs build --strict` | ✅ (stub) | ⬜ pending |
| 03-XX-XX | all | all | UX-01 | manual | Read each page for admonitions | N/A | ⬜ pending |
| 03-XX-XX | all | all | UX-02 | grep | `grep -cl "Verze pluginu" docs/pruvodce/*.md` | N/A | ⬜ pending |
| 03-XX-XX | all | all | UX-03 | manual | Spot-check 5 terms against XAML | N/A | ⬜ pending |

*Status: ⬜ pending · ✅ green · ❌ red · ⚠️ flaky*

---

## Wave 0 Requirements

- [ ] `docs/assets/screenshots/.gitkeep` — directory must exist before any image references are written

*All stub .md files already exist from Phase 2. No framework installation needed — mkdocs is already installed.*

---

## Manual-Only Verifications

| Behavior | Requirement | Why Manual | Test Instructions |
|----------|-------------|------------|-------------------|
| Admonitions are genuine (not filler) | UX-01 | Content quality judgement | Read 3 admonitions, verify they contain real warnings/tips |
| Terminology matches plugin UI | UX-03 | Requires comparing against running plugin | Spot-check 5 parameter names against XAML labels |
| Content is substantive prose | All START/GUIDE | Content depth judgement | Read each page, verify workflow explanations not just bullet lists |

---

## Validation Sign-Off

- [ ] All tasks have `<automated>` verify or Wave 0 dependencies
- [ ] Sampling continuity: no 3 consecutive tasks without automated verify
- [ ] Wave 0 covers all MISSING references
- [ ] No watch-mode flags
- [ ] Feedback latency < 5s
- [ ] `nyquist_compliant: true` set in frontmatter

**Approval:** pending
