# Phase 4: Parameter Reference and FAQ - Context

**Gathered:** 2026-03-26
**Status:** Ready for planning

<domain>
## Phase Boundary

Create a complete parameter reference table (docs/reference/parametry.md) grouped by UI section with defaults and ranges, a FAQ page (docs/faq.md) with at least 10 known problems covering connection/generation/validation, and bidirectional cross-links between guide and reference pages. No new guide content, no screenshots, no infrastructure changes.

</domain>

<decisions>
## Implementation Decisions

### Parameter Table Format
- **Markdown tabulky seskupené po UI sekcích** — jedna tabulka per sekce
- Sloupce: Parametr | Popis | Výchozí | Rozsah/Možnosti
- Seskupení odpovídá UI struktuře pluginu:
  1. **Výztuž** — Orientace S1, Svislá výztuž, Vodorovná výztuž, Lemování
  2. **Krytí a okraje** — Krytí, Odsazení
  3. **Detaily** — Okrajové podmínky, T-spoj
  4. **Prostupy** — Průměr, Šikmá výztuž, Třmínky nad dveřmi
  5. **Nastavení — Výchozí hodnoty** — mřížka průměrů a roztečí
  6. **Nastavení — Segmentace rastru** — prahy přerušení
  7. **Nastavení — Dělení prutu** — max délka
  8. **Nastavení — Třmínky a prapory** — prahy třmínku/praporu
  9. **Nastavení — Prostupy** — filtry, generace otvorů, fiktivní zvětšení
  10. **Nastavení — Normy** — poloha výztuže, tabulka přesahů
- Version badge admonition na začátku stránky (konzistence s guide stránkami)
- Názvy parametrů **tučně** a musí přesně odpovídat XAML labelům

### FAQ Content Sourcing
- Kombinace zdrojů:
  1. **Warning admonitions z guide stránek** — každý !!! warning v pruvodce/ identifikuje potenciální problém uživatele
  2. **Plugin source code** — error handling, exception messages, edge cases z RebarParameters.cs a dalších
  3. **Typické Tekla integrace problémy** — gRPC connection, model access, API verze
- Minimum 10 problémů, seskupených do 3 kategorií per FAQ-02/03/04:
  1. Připojení k Tekla Structures (FAQ-02)
  2. Generování výztuže (FAQ-03)
  3. Validace (FAQ-04)
- Formát FAQ: **Otázka jako H3 nadpis**, odpověď jako prose s konkrétním řešením
- Styl: stručný, orientovaný na řešení — ne esej o příčinách

### Cross-Link Strategy (UX-04)
- **Guide → Reference**: Inline linky v textu guide stránek kde je parametr zmíněn
  - Formát: `Podrobnosti viz [Tabulka parametrů](../reference/parametry.md#sekce-anchor)`
  - Přidat na konec každé guide stránky sekci "Viz také" s odkazem na reference
- **Reference → Guide**: Každá sekce reference tabulky obsahuje odkaz zpět na příslušnou guide stránku
  - Formát: `Podrobný popis viz [Hlavní parametry](../pruvodce/parametry.md)`
- **FAQ → Guide/Reference**: FAQ odpovědi odkazují na relevantní guide i reference stránky
- Cross-linky musí projít `mkdocs build --strict`

### Reference Page Scope
- **reference/parametry.md je kompletní lookup tabulka VŠECH parametrů** včetně Settings
- Neopakovat vysvětlení workflow — reference je pro rychlý lookup, ne pro učení
- Každý parametr z hlavního dialogu I z okna Nastavení musí být v tabulce
- Zdroj dat: RebarParameters.cs (defaults), XAML soubory (názvy, rozsahy), guide stránky (descriptions)

### Writing Style (carried from Phase 3)
- Stručný a přímý, krátké věty
- Česky s tučnými názvy UI prvků
- Terminologie z XAML labelů (Prostupy, Lemování, Třmínky, Prapory, Závlače)
- Version badge: `!!! info "Verze pluginu: [VERZE]"`

### Claude's Discretion
- Přesný počet FAQ položek nad minimum 10
- Přesné formulace FAQ odpovědí
- Zda přidat collapsible sections (??? note) pro méně časté FAQ
- Pořadí sekcí v reference tabulce (doporučeno: workflow order jako v guide)
- Zda přidat úvodní odstavec k reference tabulce vysvětlující strukturu

</decisions>

<canonical_refs>
## Canonical References

**Downstream agents MUST read these before planning or implementing.**

### Plugin Source (Parameter Names, Defaults, Ranges)
- `../WallReinf/WallReinf/MainWindow.xaml` — Hlavní dialog: české labely, sekce, parametry
- `../WallReinf/WallReinf/SettingsWindow.xaml` — Settings dialog: konfigurace, prahy, filtry
- `../WallReinf/WallReinf.Core/RebarParameters.cs` — Všechny parametry: názvy, typy, defaults, ranges

### Existing Guide Pages (for cross-linking and FAQ sourcing)
- `docs/pruvodce/parametry.md` — Hlavní parametry hub (152 řádků)
- `docs/pruvodce/otvory.md` — Otvory guide (83 řádků)
- `docs/pruvodce/trminky.md` — Třmínky guide (62 řádků)
- `docs/pruvodce/diagonaly.md` — Diagonální pruty guide (43 řádků)
- `docs/pruvodce/preview.md` — Preview panel guide (99 řádků)
- `docs/pruvodce/validace.md` — Validační okno guide (66 řádků)
- `docs/pruvodce/pdf-export.md` — PDF export guide (48 řádků)
- `docs/pruvodce/pozadavky.md` — Požadavky (35 řádků)
- `docs/pruvodce/instalace.md` — Instalace (41 řádků)
- `docs/pruvodce/pripojeni.md` — Připojení (64 řádků)
- `docs/pruvodce/zakladni-workflow.md` — Základní workflow (69 řádků)

### Existing Stub Files (to be replaced)
- `docs/reference/parametry.md` — Stub s H2: Obecné parametry, Parametry výztuže, Parametry otvorů
- `docs/reference/index.md` — Stub overview
- `docs/faq.md` — Stub s H2: Připojení, Generování, Validace

### Requirements
- `.planning/REQUIREMENTS.md` — REF-01..03, FAQ-01..04, UX-04

### Prior Phase Context
- `.planning/phases/03-user-guide-content/03-CONTEXT.md` — Writing style, terminology, Settings coverage decisions

</canonical_refs>

<code_context>
## Existing Code Insights

### Reusable Assets
- 12 complete guide pages in `docs/pruvodce/` — source for cross-link targets and FAQ content
- `docs/reference/parametry.md` stub — H2 structure to be replaced with comprehensive tables
- `docs/faq.md` stub — H2 categories already match FAQ-02/03/04 requirements
- Plugin source in `../WallReinf/` — authoritative for parameter names, defaults, ranges

### Established Patterns
- Version badge admonition at top of every page
- Bold Czech UI element names from XAML labels
- `mkdocs build --strict` as quality gate
- Cross-links within pruvodce/ use relative paths: `[text](filename.md#anchor)`
- Cross-links between sections: `[text](../reference/parametry.md)` or `[text](../pruvodce/parametry.md)`
- Admonitions: `!!! warning`, `!!! tip`, `!!! note`, `!!! info`

### Integration Points
- `mkdocs.yml` nav already has Reference section and FAQ entry — no nav changes needed
- Guide pages need "Viz také" sections added with reference cross-links
- reference/index.md needs update to link to parametry.md properly

</code_context>

<specifics>
## Specific Ideas

- Reference tabulka by měla být "quick lookup" — uživatel hledá konkrétní parametr, chce vidět default a rozsah, ne číst vysvětlení
- FAQ by měl pokrývat problémy, které se uživatel dozví až při práci s pluginem (ne opakovat guide obsah)
- Cross-linky by měly být obousměrné — z guide do reference a zpět

</specifics>

<deferred>
## Deferred Ideas

None — discussion stayed within phase scope

</deferred>

---

*Phase: 04-parameter-reference-and-faq*
*Context gathered: 2026-03-26 via auto mode*
