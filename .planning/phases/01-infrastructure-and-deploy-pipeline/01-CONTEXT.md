# Phase 1: Infrastructure and Deploy Pipeline - Context

**Gathered:** 2026-03-26
**Status:** Ready for planning

<domain>
## Phase Boundary

Set up a working MkDocs Material site with CI/CD deploy to GitHub Pages. Deliver a live skeleton site with one index page, working Czech search, light/dark mode toggle, and pinned dependencies. No content beyond the index page stub.

</domain>

<decisions>
## Implementation Decisions

### GitHub Configuration
- GitHub username: `evgenijbg-netizen`
- Repository name: `WallReinf-wiki`
- site_url: `https://evgenijbg-netizen.github.io/WallReinf-wiki/`
- Deploy target: GitHub Pages via `gh-pages` branch
- CI trigger: push to `main`

### Index Page Content
- Stručný přehled: co je Wall Reinforcement Wizard, pro koho je, jak začít
- Odkazy na hlavní sekce (Začínáme, Průvodce funkcemi, Reference, FAQ)
- Obsah v češtině

### Site Identity
- Site name: "Wall Reinforcement Wizard"
- Theme language: `cs` (čeština)
- Theme color scheme: výchozí Material (modrá #2094f3)
- Logo: `WallReinforcementWizard_logo.png` — zkopírovat do `docs/assets/logo.png`
- Logo je tmavě modrý betonový blok s výztuží a textem "RW"

### Visual Style
- Výchozí MkDocs Material téma bez úprav barev
- Light/dark mode toggle zapnutý
- Logo v headeru místo textového názvu

### Claude's Discretion
- Přesné nastavení `mkdocs.yml` features (navigation, toc, search options)
- GitHub Actions workflow detaily (Python verze, caching)
- Přesný text na index stránce (v rámci dohodnuté struktury)
- .gitignore obsah nad rámec `site/`

</decisions>

<canonical_refs>
## Canonical References

**Downstream agents MUST read these before planning or implementing.**

### MkDocs Material Setup
- `.planning/research/STACK.md` — Pinned versions: mkdocs==1.6.1, mkdocs-material==9.7.6; installation commands
- `.planning/research/PITFALLS.md` — Critical pitfalls: site_url, MkDocs 2.x pin, GitHub Actions permissions
- `.planning/research/ARCHITECTURE.md` — Project structure, CI/CD pattern, file organization

### Requirements
- `.planning/REQUIREMENTS.md` — INFRA-01 through INFRA-07 define acceptance criteria

</canonical_refs>

<code_context>
## Existing Code Insights

### Reusable Assets
- `WallReinforcementWizard_logo.png` — Logo file in repo root, needs to be moved to `docs/assets/logo.png`

### Established Patterns
- No existing code — greenfield project

### Integration Points
- GitHub remote needs to be set up: `evgenijbg-netizen/WallReinf-wiki`

</code_context>

<specifics>
## Specific Ideas

- Logo je tmavě modré na tmavém pozadí — v dark mode by mělo být viditelné bez problémů, v light mode potřeba ověřit kontrast
- Název "Wall Reinforcement Wizard" v titulku (ne zkratka WRW)

</specifics>

<deferred>
## Deferred Ideas

None — discussion stayed within phase scope

</deferred>

---

*Phase: 01-infrastructure-and-deploy-pipeline*
*Context gathered: 2026-03-26*
