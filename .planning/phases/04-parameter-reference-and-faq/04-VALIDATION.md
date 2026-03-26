---
phase: 04
slug: parameter-reference-and-faq
status: draft
nyquist_compliant: true
wave_0_complete: true
created: 2026-03-26
---

# Phase 04 — Validation Strategy

> Per-phase validation contract for feedback sampling during execution.

---

## Test Infrastructure

| Property | Value |
|----------|-------|
| **Framework** | mkdocs build --strict |
| **Config file** | `mkdocs.yml` |
| **Quick run command** | `mkdocs build --strict 2>&1 \| grep -E "WARNING\|ERROR\|CRITICAL"` |
| **Full suite command** | `python -m mkdocs build --strict` |
| **Estimated runtime** | ~3 seconds |

---

## Sampling Rate

- **After every task commit:** Run `mkdocs build --strict 2>&1 | grep -E "WARNING|ERROR"` — verify no new broken links
- **After every plan wave:** Run `python -m mkdocs build --strict` — full clean build
- **Before `/gsd:verify-work`:** Full suite must be green
- **Max feedback latency:** 3 seconds

---

## Per-Task Verification Map

| Task ID | Plan | Wave | Requirement | Test Type | Automated Command | File Exists | Status |
|---------|------|------|-------------|-----------|-------------------|-------------|--------|
| 04-01-01 | 01 | 1 | REF-01, REF-02, REF-03 | build + manual | `python -m mkdocs build --strict` | ✅ | ⬜ pending |
| 04-02-01 | 02 | 1 | FAQ-01, FAQ-02, FAQ-03, FAQ-04 | build + grep | `grep "^###" docs/faq.md \| wc -l` | ✅ | ⬜ pending |
| 04-03-01 | 03 | 2 | UX-04 | build strict | `python -m mkdocs build --strict` | ✅ | ⬜ pending |

*Status: ⬜ pending · ✅ green · ❌ red · ⚠️ flaky*

---

## Wave 0 Requirements

Existing infrastructure covers all phase requirements. `mkdocs build --strict` is the primary validation gate and is already configured.

---

## Manual-Only Verifications

| Behavior | Requirement | Why Manual | Test Instructions |
|----------|-------------|------------|-------------------|
| Parameter names match UI labels | REF-01 | Requires visual comparison with plugin XAML | Compare 5 parameter names in reference/parametry.md against MainWindow.xaml labels |
| Every parameter has default + range | REF-02 | Requires domain knowledge to verify values | Spot-check 5 parameters have non-empty Default and Range columns |
| Parameters grouped by UI sections | REF-03 | Requires understanding of UI structure | Verify H2/H3 sections in reference/parametry.md match plugin dialog sections |
| FAQ covers connection issues | FAQ-02 | Requires reading FAQ content | Verify at least 2 FAQ items under Připojení section |
| FAQ covers generation issues | FAQ-03 | Requires reading FAQ content | Verify at least 3 FAQ items under Generování section |
| FAQ covers validation issues | FAQ-04 | Requires reading FAQ content | Verify at least 2 FAQ items under Validace section |

---

## Validation Sign-Off

- [x] All tasks have automated verify or Wave 0 dependencies
- [x] Sampling continuity: no 3 consecutive tasks without automated verify
- [x] Wave 0 covers all MISSING references
- [x] No watch-mode flags
- [x] Feedback latency < 3s
- [x] `nyquist_compliant: true` set in frontmatter

**Approval:** pending
