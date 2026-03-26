# Phase 4: Parameter Reference and FAQ - Research

**Researched:** 2026-03-26
**Domain:** MkDocs Material content authoring — reference tables, FAQ, cross-links
**Confidence:** HIGH

---

<user_constraints>
## User Constraints (from CONTEXT.md)

### Locked Decisions

**Parameter Table Format**
- Markdown tabulky seskupené po UI sekcích — jedna tabulka per sekce
- Sloupce: Parametr | Popis | Výchozí | Rozsah/Možnosti
- Seskupení odpovídá UI struktuře pluginu (10 sekcí — viz Architecture Patterns níže)
- Version badge admonition na začátku stránky
- Názvy parametrů tučně a musí přesně odpovídat XAML labelům

**FAQ Content Sourcing**
- Kombinace zdrojů: warning admonitions z guide stránek, plugin source code, typické Tekla integrace problémy
- Minimum 10 problémů, seskupených do 3 kategorií (FAQ-02/03/04): Připojení, Generování, Validace
- Formát FAQ: Otázka jako H3 nadpis, odpověď jako prose s konkrétním řešením
- Styl: stručný, orientovaný na řešení

**Cross-Link Strategy (UX-04)**
- Guide → Reference: inline linky + sekce "Viz také" na konci každé guide stránky
  - Formát: `Podrobnosti viz [Tabulka parametrů](../reference/parametry.md#sekce-anchor)`
- Reference → Guide: každá sekce tabulky obsahuje odkaz zpět na příslušnou guide stránku
- FAQ → Guide/Reference: FAQ odpovědi odkazují na relevantní stránky
- Cross-linky musí projít `mkdocs build --strict`

**Reference Page Scope**
- reference/parametry.md je kompletní lookup tabulka VŠECH parametrů včetně Settings
- Neopakovat vysvětlení workflow — reference je pro rychlý lookup
- Zdroj dat: RebarParameters.cs (defaults), XAML soubory (názvy, rozsahy), guide stránky (descriptions)

**Writing Style (carried from Phase 3)**
- Stručný a přímý, krátké věty; česky s tučnými názvy UI prvků
- Terminologie z XAML labelů (Prostupy, Lemování, Třmínky, Prapory, Závlače)
- Version badge: `!!! info "Verze pluginu: [VERZE]"`

### Claude's Discretion
- Přesný počet FAQ položek nad minimum 10
- Přesné formulace FAQ odpovědí
- Zda přidat collapsible sections (??? note) pro méně časté FAQ
- Pořadí sekcí v reference tabulce (doporučeno: workflow order jako v guide)
- Zda přidat úvodní odstavec k reference tabulce vysvětlující strukturu

### Deferred Ideas (OUT OF SCOPE)
None — discussion stayed within phase scope
</user_constraints>

---

<phase_requirements>
## Phase Requirements

| ID | Description | Research Support |
|----|-------------|-----------------|
| REF-01 | Tabulka parametrů s názvy odpovídajícími UI pluginu | XAML labels extracted — exact names documented in Standard Stack section |
| REF-02 | Každý parametr má popis, výchozí hodnotu a platný rozsah | RebarParameters.cs defaults + XAML slider ranges fully catalogued |
| REF-03 | Parametry jsou seskupeny podle sekcí UI (stejně jako v pluginu) | 10 UI sections identified from MainWindow.xaml + SettingsWindow.xaml |
| FAQ-01 | Minimálně 10 známých problémů s řešením | 13 FAQ items identified from guide warnings + source error messages |
| FAQ-02 | FAQ obsahuje problémy s připojením k Tekle | 4 connection problems catalogued from pripojeni.md + MainWindow.xaml.cs |
| FAQ-03 | FAQ obsahuje problémy s generováním výztuže | 5 generation problems from guide warnings + source edge cases |
| FAQ-04 | FAQ obsahuje problémy s validací | 4 validation/post-generation problems documented |
| UX-04 | Stránky obsahují křížové odkazy mezi průvodcem a referencí | 11 guide pages × bidirectional link targets — all mapped |
</phase_requirements>

---

## Summary

Phase 4 is a pure content authoring phase with no infrastructure changes. The MkDocs Material site is fully operational, all guide pages exist as cross-link targets, and the stub files (`docs/reference/parametry.md`, `docs/faq.md`) already carry the correct H2 category structure required by the requirements. The work is replacing those stubs with full content.

Parameter data is fully available from two authoritative sources: `RebarParameters.cs` provides defaults and C# property names, and `MainWindow.xaml` / `SettingsWindow.xaml` provide exact Czech UI labels and slider ranges. All 10 UI sections are identified. FAQ content is abundant: the 11 guide pages contain 8 `!!! warning` admonitions, the source code reveals 5 distinct error message patterns, and Tekla gRPC integration adds 4 connection failure scenarios — giving 17+ candidate FAQ items against the minimum 10.

The only content judgment calls left to the implementer are: exact FAQ phrasing, whether to use `??? note` collapsibles for rare items, and introductory paragraph text on the reference page. Cross-link anchors must use MkDocs Material anchor format (`#sekce-anchor` derived from H2/H3 headings) and must survive `mkdocs build --strict`.

**Primary recommendation:** Write `reference/parametry.md` first (defines anchors), then update guide pages with "Viz také" back-links, then write `faq.md` with its forward links — in this dependency order, all links are verifiable.

---

## Standard Stack

### Core (already installed — no new packages)

| Tool/Pattern | Version | Purpose | Why Standard |
|---|---|---|---|
| MkDocs Material | 9.7.6 (pinned) | Site framework | Already deployed; nav/admonitions/strict mode in use |
| `admonition` extension | included | `!!! warning`, `!!! tip`, `!!! info` | Established pattern in all 11 guide pages |
| `pymdownx.details` | included | `??? note` collapsibles | Available; used in parametry.md and diagonaly.md |
| Markdown tables | GFM | Parameter reference tables | Simplest format; renders well in MkDocs Material |
| `mkdocs build --strict` | CLI | Cross-link validation gate | Established quality gate from Phase 1 |

**No new packages.** This phase adds no dependencies.

---

## Architecture Patterns

### Files to Create / Replace

```
docs/
├── reference/
│   ├── index.md          # UPDATE: add proper link to parametry.md (currently stub)
│   └── parametry.md      # REPLACE stub with 10-section reference table
├── faq.md                # REPLACE stub with 13+ FAQ items in 3 categories
└── pruvodce/
    ├── pripojeni.md      # ADD "Viz také" section at end
    ├── zakladni-workflow.md  # ADD "Viz také" section at end
    ├── parametry.md      # ADD "Viz také" section at end
    ├── otvory.md         # ADD "Viz také" section at end
    ├── trminky.md        # ADD "Viz také" section at end
    ├── diagonaly.md      # ADD "Viz také" section at end
    ├── preview.md        # ADD "Viz také" section at end
    ├── validace.md       # ADD "Viz také" section at end
    ├── pdf-export.md     # ADD "Viz také" section at end
    ├── pozadavky.md      # ADD "Viz také" if relevant
    └── instalace.md      # ADD "Viz také" if relevant
```

### Pattern 1: Reference Table Section

Each of the 10 UI sections becomes one H2 heading in `reference/parametry.md`.
The anchor is derived from the heading text by MkDocs Material.

**Template:**

```markdown
## Výztuž

Podrobný popis viz [Hlavní parametry](../pruvodce/parametry.md).

| Parametr | Popis | Výchozí | Rozsah / Možnosti |
|---|---|---|---|
| **Orientace S1** | Která vrstva je vnější (nosná) | Svislá (nosná) | Svislá (nosná) / Vodorovná (nosná) |
| **Svislá výztuž S1** | Průměr svislých prutů vnější vrstvy | Ø12 | Ø8 / Ø10 / Ø12 / Ø14 / Ø16 / Ø18 / Ø20 / Ø22 / Ø25 |
...
```

**Cross-link from guide page end:**

```markdown
## Viz také

- [Tabulka parametrů — Výztuž](../reference/parametry.md#vyztu)
```

Note: MkDocs Material derives anchors by lowercasing, replacing spaces with `-`, and stripping diacritics. Czech `Výztuž` → `#vyztu` (MkDocs strips `ž`). Verify all anchors with an actual build.

### Pattern 2: FAQ Item

```markdown
### Plugin hlásí "Tekla není spuštěna"

Tekla Structures není otevřena nebo model není načten. Otevřete Tekla Structures, načtěte model a znovu spusťte plugin. Pouhé spuštění aplikace nestačí — model musí být aktivní.

Viz [Připojení k modelu](pruvodce/pripojeni.md) pro postup ověření připojení.
```

### Pattern 3: "Viz také" Section on Guide Pages

Added as the last section on each guide page. Example for `parametry.md`:

```markdown
## Viz také

- [Tabulka parametrů — Výztuž](../reference/parametry.md#vyztu)
- [Tabulka parametrů — Krytí a okraje](../reference/parametry.md#kryti-a-okraje)
- [Tabulka parametrů — Detaily](../reference/parametry.md#detaily)
- [FAQ — Generování výztuže](../faq.md#generovani-vyztuze)
```

### Anti-Patterns to Avoid

- **Anchors guessed without verification:** MkDocs Material's anchor derivation for Czech strings is not obvious. Run `mkdocs build --strict` after each file to catch broken links immediately, not at the end.
- **Duplicating guide prose in reference:** The reference table must be lookup-only (Parametr | Popis | Výchozí | Rozsah). No workflow explanation, no "how to" text.
- **FAQ as theory:** FAQ answers must state the fix in the first sentence, not explain the cause. Pattern: "Tekla není spuštěna. Otevřete model a znovu spusťte plugin."
- **Bidirectional links in wrong direction only:** Both directions (guide → reference AND reference → guide) must be implemented. Missing either direction fails UX-04.

---

## Don't Hand-Roll

| Problem | Don't Build | Use Instead | Why |
|---|---|---|---|
| Anchor verification | Manual anchor-to-heading mapping table | `mkdocs build --strict` | --strict catches broken refs automatically |
| Parameter range lookup | Reading XAML each time | This RESEARCH.md catalogue | Already extracted below |
| FAQ content inventory | Re-reading all guide pages | Warning admonitions list below | Already catalogued |

---

## Complete Parameter Catalogue

Extracted from `RebarParameters.cs` (defaults) and `MainWindow.xaml` / `SettingsWindow.xaml` (labels, ranges). This is the authoritative data for implementing REF-01, REF-02, REF-03.

### Section 1: Výztuž — Orientace S1

| Parametr | C# Property | Výchozí | Rozsah / Možnosti |
|---|---|---|---|
| **Orientace S1** | `OuterIsVertical` | Svislá (nosná) = true | Svislá (nosná) / Vodorovná (nosná) |

### Section 2: Výztuž — Svislá výztuž

| Parametr | C# Property | Výchozí | Rozsah / Možnosti |
|---|---|---|---|
| **Svislá výztuž S1** (Průměr) | `DiameterVerticalOuter` | 12 mm | Ø8 / Ø10 / Ø12 / Ø14 / Ø16 / Ø18 / Ø20 / Ø22 / Ø25 |
| **Svislá výztuž S2** (Průměr) | `DiameterVerticalInner` | 12 mm | Ø8 / Ø10 / Ø12 / Ø14 / Ø16 / Ø18 / Ø20 / Ø22 / Ø25 |
| **Rozteč** (svislá) | `SpacingVerticalOuter` / `SpacingVerticalInner` | 200 mm | 100 / 125 / 150 / 175 / 200 / 250 / 300 mm |

Note: One spacing ComboBox drives both S1 and S2 (`cmbSpacingVertical`). S2 uses same spacing as S1 unless overridden.

### Section 3: Výztuž — Vodorovná výztuž

| Parametr | C# Property | Výchozí | Rozsah / Možnosti |
|---|---|---|---|
| **Vodorovná výztuž S1** (Průměr) | `DiameterHorizontalOuter` | 10 mm | Ø8 / Ø10 / Ø12 / Ø14 / Ø16 / Ø18 / Ø20 / Ø22 / Ø25 |
| **Vodorovná výztuž S2** (Průměr) | `DiameterHorizontalInner` | 10 mm | Ø8 / Ø10 / Ø12 / Ø14 / Ø16 / Ø18 / Ø20 / Ø22 / Ø25 |
| **Rozteč** (vodorovná) | `SpacingHorizontalOuter` / `SpacingHorizontalInner` | 200 mm | 100 / 125 / 150 / 175 / 200 / 250 / 300 mm |

### Section 4: Výztuž — Lemování a Prostupy

| Parametr | C# Property | Výchozí | Rozsah / Možnosti |
|---|---|---|---|
| **Lemování (U-čka)** (aktivace) | (checkbox binding) | zaškrtnuto | ano / ne |
| **Lemování — Průměr** | `DiameterEdge` | 14 mm | Ø8 / Ø10 / Ø12 / Ø14 / Ø16 / Ø18 / Ø20 / Ø22 / Ø25 |
| **Prostupy — Průměr** | `DiameterOpening` | 12 mm | Ø8 / Ø10 / Ø12 / Ø14 / Ø16 / Ø18 / Ø20 / Ø22 / Ø25 |
| **Šikmá výztuž v rozích (45°)** | `DiagonalRebar` | zaškrtnuto | ano / ne |
| **Třmínky nad dveřmi** | `StirrupsAboveDoor` | zaškrtnuto | ano / ne |

### Section 5: Krytí a okraje

| Parametr | C# Property | Výchozí | Rozsah / Možnosti |
|---|---|---|---|
| **Krytí** | `Cover` | 40 mm | 30 / 35 / 40 / 50 / 60 mm |
| **Ocel** | `Grade` | B500B | informační (nelze měnit) |
| **Odsazení** | `StartOffset` | 50 mm | Slider 0–200 mm, tick 10 mm |
| **Odsazení od kraje H** | `EdgeMarginHorizontal` | 50 mm | Slider 0–300 mm, tick 10 mm |
| **Odsazení od kraje V** | `EdgeMarginVertical` | 50 mm | Slider 0–300 mm, tick 10 mm |

Source: `RebarParameters.cs` lines 43–44 confirm `EdgeMarginHorizontal = 50`, `EdgeMarginVertical = 50`; Slider `sliderStartOffset` default Value="50".

### Section 6: Detaily — Okrajové podmínky

| Parametr | C# Property | Výchozí | Rozsah / Možnosti |
|---|---|---|---|
| **Volný konec stěny** | `HasFreeEnd` | nezaškrtnuto | ano / ne |
| **Pokračuje výš** | `ContinuesUp` | nezaškrtnuto | ano / ne |
| **Tl. desky** | `SlabThickness` | 200 mm | TextBox (mm); aktivní jen když Pokračuje výš zaškrtnuto |

### Section 7: Detaily — T-spoj (navazující stěny)

| Parametr | C# Property | Výchozí | Rozsah / Možnosti |
|---|---|---|---|
| **Zleva** (aktivace) | `AdjacentWallLeft` | nezaškrtnuto | ano / ne |
| **Tloušťka zleva** | `AdjacentWallThicknessLeft` | 200 mm | 150 / 200 / 250 / 300 / 350 / 400 mm |
| **Zprava** (aktivace) | `AdjacentWallRight` | nezaškrtnuto | ano / ne |
| **Tloušťka zprava** | `AdjacentWallThicknessRight` | 200 mm | 150 / 200 / 250 / 300 / 350 / 400 mm |
| **Závlače** | `TieBarSquareSize` | 100 mm | Slider 40–200 mm, tick 10 mm |

Note: T-spoj sekce je dostupná pouze pokud je zaškrtnuto **Lemování (U-čka)** (XAML: `IsEnabled="{Binding IsChecked, ElementName=chkGenerateEdge}"`).

### Section 8: Nastavení — Výchozí hodnoty

| Parametr | C# Property | Výchozí | Rozsah / Možnosti |
|---|---|---|---|
| **Svislá S1** (výchozí průměr) | (settings field) | dle aktuálního | TextBox mm |
| **Svislá S2** (výchozí průměr) | (settings field) | dle aktuálního | TextBox mm |
| **Vodorovná S1** (výchozí průměr) | (settings field) | dle aktuálního | TextBox mm |
| **Vodorovná S2** (výchozí průměr) | (settings field) | dle aktuálního | TextBox mm |
| **Lemování** (výchozí průměr) | (settings field) | dle aktuálního | TextBox mm |
| **Prostupy** (výchozí průměr) | (settings field) | dle aktuálního | TextBox mm |
| **Svislá S1** (výchozí rozteč) | (settings field) | dle aktuálního | TextBox mm |
| **Vodorovná S1** (výchozí rozteč) | (settings field) | dle aktuálního | TextBox mm |
| **Krytí** (výchozí) | (settings field) | dle aktuálního | TextBox mm |
| **Odsazení od okraje** (výchozí) | (settings field) | dle aktuálního | Slider 0–200 mm, tick 10 mm |

### Section 9: Nastavení — Segmentace rastru a Dělení prutu

| Parametr | C# Property | Výchozí | Rozsah / Možnosti |
|---|---|---|---|
| **Práh pro přerušení** | (settings field) | — | TextBox m² |
| **Max délka segmentu** | (settings field) | — | TextBox mm |
| **Min vzdálenost od otvoru** | (settings field) | — | TextBox mm |
| **Maximální délka prutu** | `MaxRebarLength` | 12 000 mm | Slider 6 000–12 000 mm, tick 500 mm |

Source: `RebarParameters.cs` line 56: `MaxRebarLength = 12000.0`. SettingsWindow.xaml: `sliderMaxRebarLength Minimum="6000" Maximum="12000" TickFrequency="500"`.

### Section 10: Nastavení — Třmínky a prapory, Prostupy, Normy

| Parametr | C# Property | Výchozí | Rozsah / Možnosti |
|---|---|---|---|
| **Prah třmínku** | `StirrupThreshold` | 300 mm | Slider 0–2 500 mm, tick 50 mm |
| **Prah praporu** | `FlagThreshold` | 1 500 mm | Slider 0–2 500 mm, tick 50 mm |
| **Limit protažení noh U-ček** | `UBarLegExtensionLimit` | 700 mm | Slider 0–2 000 mm, tick 50 mm |
| **Odsazení ohybu kotevních prutů** | `LapBarBendOffset` | 80 mm | Slider 0–200 mm, tick 10 mm |
| **Fiktivní zvětšení H** | `OpeningInflationH` | 0 mm | Slider 0–200 mm, tick 10 mm |
| **Fiktivní zvětšení V** | `OpeningInflationV` | 0 mm | Slider 0–200 mm, tick 10 mm |
| **Ignorovat kapsy** | (checkbox) | nezaškrtnuto | ano / ne |
| **Ignorovat výřezy** | (checkbox) | nezaškrtnuto | ano / ne |
| **Ignorovat všechny prostupy** | (checkbox) | nezaškrtnuto | ano / ne |
| **Filtr materiálu (prefix)** | (settings field) | prázdné = bez filtru | TextBox (text prefix, např. C) |
| **Poloha výztuže** | `UseFavorablePosition` | Příznivá | Příznivá / Nepříznivá |

Sources: `RebarParameters.cs` lines 47–50: `StirrupThreshold=300`, `FlagThreshold=1500`, `UBarLegExtensionLimit=700`, `LapBarBendOffset=80`. SettingsWindow.xaml slider ranges confirmed.

---

## FAQ Content Catalogue

All 13 identified FAQ items mapped to requirements.

### Kategorie 1: Připojení k Tekla Structures (FAQ-02)

**FAQ-C01: Plugin hlásí "Tekla není spuštěna"**
- Source: `MainWindow.xaml.cs` line 1185: `MessageBox.Show("Tekla neni spustena!", ...)`
- Fix: Otevřete Tekla Structures a načtěte model. Pouhé spuštění aplikace nestačí.

**FAQ-C02: "Nelze připojit k Tekle" při testu připojení**
- Source: `MainWindow.xaml.cs` line 1224: `MessageBox.Show($"Nelze pripojit k Tekle:\n{ex.Message}", ...)`; `pripojeni.md` warning admonition
- Fix: Plugin komunikuje přes gRPC — model musí být aktivní, ne jen Tekla. Zkontrolujte, zda je model otevřen.

**FAQ-C03: Status po "Test připojení" zůstává "Neověřeno"**
- Source: SettingsWindow.xaml `txtConnectionStatus` initial text "Status: Neověřeno"; gRPC connection failure pattern
- Fix: Klikněte přímo na tlačítko Test připojení; výsledek se zobrazí pod tlačítkem.

**FAQ-C04: Dropdown Stěna je po kliknutí Načíst prázdný**
- Source: prefix filter logic; `pripojeni.md` tip admonition
- Fix: Zkontrolujte hodnotu v poli Prefix. Prázdné pole načte všechny stěny; chybný prefix nevrátí žádné výsledky. Zkontrolujte také Nastavení → Načítání stěn → Filtr materiálu.

### Kategorie 2: Generování výztuže (FAQ-03)

**FAQ-G01: Generovat přepíše existující výztuž**
- Source: `zakladni-workflow.md` `!!! warning "Pozor — přepis existující výztuže"`
- Fix: Před generováním zkontrolujte parametry v preview panelu. Přepis je záměrný — plugin vždy nahradí veškerou existující výztuž dané stěny.

**FAQ-G02: U-pruty kolem prostupů se negenerují**
- Source: `otvory.md` `!!! warning "Pozor — Lemování musí být aktivní"`
- Fix: Zaškrtněte volbu **Lemování (U-čka)** v expanderu **Výztuž**. Bez aktivního lemování se U-pruty kolem prostupů negenerují.

**FAQ-G03: T-spoj (závlače) je zašedlý**
- Source: `parametry.md` `!!! warning "T-spoj je dostupný pouze s Lemováním"`; XAML binding `IsEnabled="{Binding IsChecked, ElementName=chkGenerateEdge}"`
- Fix: Zaškrtněte **Lemování (U-čka)**. T-spoj vyžaduje aktivní lemování.

**FAQ-G04: Plugin generuje příliš mnoho třmínků nebo praporů**
- Source: `trminky.md` `!!! tip "příliš mnoho třmínků"`
- Fix: Upravte prahy v Nastavení → Třmínky a prapory. Snižte Prah třmínku pro kratší segmenty nebo zvyšte Prah praporu.

**FAQ-G05: Prah praporu nastavený níže než Prah třmínku — neočekávané chování**
- Source: `trminky.md` `!!! warning "Pozor — překrývající se prahy"`
- Fix: Prah praporu musí být vždy vyšší než Prah třmínku. Plugin tuto podmínku nekontroluje automaticky.

**FAQ-G06: Orientace S1 — průměry přiřazeny k opačné vrstvě**
- Source: `parametry.md` `!!! warning "Pozor — orientace ovlivňuje všechny parametry"`
- Fix: Nastavte **Orientaci S1** jako první krok před zadáním průměrů a roztečí. Změna orientace po zadání hodnot přehodí přiřazení vrstev.

**FAQ-G07: Diagonální pruty a U-pruty mají stejný průměr — nelze oddělit**
- Source: `diagonaly.md` prose section "Průměr diagonálních prutů"
- Fix: V aktuální verzi pluginu sdílejí diagonální pruty průměr s U-pruty z pole **Průměr:** v sekci **Prostupy**. Samostatné nastavení průměru diagonál není k dispozici.

### Kategorie 3: Validace (FAQ-04)

**FAQ-V01: Validační okno je prázdné**
- Source: `validace.md` `!!! note "Poznámka — Validace vs. Preview"`
- Fix: Nejprve vygenerujte výztuž přes **Generovat**. Validační okno zobrazuje skutečnou výztuž z Tekla modelu, ne plánovaný návrh. Prázdné plátno = výztuž ještě nebyla vygenerována.

**FAQ-V02: Validační okno neodpovídá aktuálnímu stavu modelu**
- Source: `validace.md` tlačítko Obnovit
- Fix: Klikněte na **Obnovit** v záhlaví validačního okna. Data se znovu načtou z Tekla modelu.

**FAQ-V03: PDF export selhal s chybou**
- Source: `MainWindow.PdfExport.cs` line 54: `MessageBox.Show($"Chyba při exportu PDF:\n{ex.Message}", ...)`; `ValidationPdfExporter.cs` `throw new InvalidOperationException("Není co exportovat.")`
- Fix: Ověřte, že jsou data ve validačním okně načtena (klikněte Obnovit). Export je možný pouze pokud validační okno obsahuje výztuž.

**FAQ-V04: Po úpravě délek v preview se pruty kříží s okraji nebo otvory**
- Source: `preview.md` `!!! warning "Pozor — Po úpravě délek vždy zkontrolujte kolize"`
- Fix: Po každé úpravě délek klikněte na **Zkontrolovat kolize** (nebo **Kolize** v inline doku). Generujte až po ověření, že kolize nejsou hlášeny.

---

## Cross-Link Map

Complete mapping of guide pages to reference section anchors. Implementer uses this to add "Viz také" sections.

| Guide stránka | Reference sekce (anchor) | FAQ kategorie |
|---|---|---|
| `pruvodce/parametry.md` | `#vyztu`, `#kryti-a-okraje`, `#detaily`, `#nastaveni-vychozi-hodnoty`, `#nastaveni-segmentace-rastru-a-deleni-prutu`, `#nastaveni-trminky-a-prapory-prostupy-normy` | `faq.md#generovani-vyztuze` |
| `pruvodce/otvory.md` | `#vyztu` (Prostupy řádky), `#nastaveni-trminky-a-prapory-prostupy-normy` | `faq.md#generovani-vyztuze` |
| `pruvodce/trminky.md` | `#nastaveni-trminky-a-prapory-prostupy-normy` | `faq.md#generovani-vyztuze` |
| `pruvodce/diagonaly.md` | `#vyztu` (Šikmá výztuž řádek) | `faq.md#generovani-vyztuze` |
| `pruvodce/pripojeni.md` | (no direct parameter link) | `faq.md#pripojeni-k-tekla-structures` |
| `pruvodce/zakladni-workflow.md` | `#vyztu`, `#kryti-a-okraje`, `#detaily` | `faq.md#generovani-vyztuze` |
| `pruvodce/preview.md` | (no direct parameter link) | `faq.md#validace` |
| `pruvodce/validace.md` | (no direct parameter link) | `faq.md#validace` |
| `pruvodce/pdf-export.md` | (no direct parameter link) | `faq.md#validace` |

---

## Common Pitfalls

### Pitfall 1: MkDocs Czech Anchor Generation

**What goes wrong:** Czech heading `## Krytí a okraje` does not produce anchor `#krytí-a-okraje`. MkDocs Material strips diacritics differently than expected — `ý` may or may not be stripped depending on the Python Markdown version.

**Why it happens:** MkDocs anchor generation lowercases and replaces spaces but may keep or strip non-ASCII characters depending on config.

**How to avoid:** Run `mkdocs build --strict` immediately after writing `reference/parametry.md` and before adding cross-links to guide pages. Check the generated HTML anchor IDs directly. Use the verified anchors in all cross-links.

**Warning signs:** Any `WARNING  -  Doc file ... contains a link '...' that is not found in the documentation files` in build output.

### Pitfall 2: Stub H2 Structure Conflicts with New Content

**What goes wrong:** `docs/reference/parametry.md` currently has three H2 headings (`## Obecné parametry`, `## Parametry výztuže`, `## Parametry otvorů`) that do not match the 10 required UI sections. Simply appending new content would create duplicate or conflicting sections.

**Why it happens:** The stub was a placeholder — its headings were not designed to match the final structure.

**How to avoid:** The entire stub file must be replaced, not appended to. Same for `docs/faq.md` stub — replace the file completely while preserving the three H2 categories.

### Pitfall 3: T-spoj IsEnabled Binding Not Documented in Reference

**What goes wrong:** Reference table for T-spoj parameters does not mention the Lemování dependency, leaving users confused when the section is greyed out.

**Why it happens:** Reference tables tempt implementers to list only parameter names and values, omitting conditional availability.

**How to avoid:** Add a note row or inline note in the T-spoj section of reference/parametry.md: "Sekce dostupná pouze pokud je zaškrtnuto **Lemování (U-čka)**."

### Pitfall 4: FAQ Answers Too Long

**What goes wrong:** FAQ answers become mini-guides, repeating content already in guide pages.

**Why it happens:** Temptation to explain causes, not just fixes.

**How to avoid:** Every FAQ answer must state the fix in sentence 1. Max 3-4 sentences per answer. Link to guide page for details — do not embed the guide in the FAQ.

---

## Validation Architecture

### Test Framework

| Property | Value |
|---|---|
| Framework | mkdocs build --strict |
| Config file | `mkdocs.yml` (root of repo) |
| Quick run command | `mkdocs build --strict 2>&1 | grep -E "WARNING|ERROR|CRITICAL"` |
| Full suite command | `mkdocs build --strict` |

### Phase Requirements → Test Map

| Req ID | Behavior | Test Type | Automated Command | Infrastructure Exists? |
|---|---|---|---|---|
| REF-01 | Parameter names match UI labels | manual review | `mkdocs build --strict` (build passes) | Yes |
| REF-02 | Every parameter has default + range | manual review | `mkdocs build --strict` (build passes) | Yes |
| REF-03 | Parameters grouped by UI sections | manual review | `mkdocs build --strict` (build passes) | Yes |
| FAQ-01 | 10+ problems listed | manual count | `grep "^###" docs/faq.md | wc -l` | Yes |
| FAQ-02 | Connection problems in FAQ | manual review | `grep -i "připojení\|Tekla" docs/faq.md` | Yes |
| FAQ-03 | Generation problems in FAQ | manual review | `grep -i "generov" docs/faq.md` | Yes |
| FAQ-04 | Validation problems in FAQ | manual review | `grep -i "validac\|export" docs/faq.md` | Yes |
| UX-04 | Bidirectional cross-links exist | build gate | `mkdocs build --strict` (no broken refs) | Yes |

### Sampling Rate

- **Per task commit:** `mkdocs build --strict 2>&1 | grep -E "WARNING|ERROR"` — verify no new broken links
- **Per wave merge:** `mkdocs build --strict` — full clean build
- **Phase gate:** Full suite green before `/gsd:verify-work`

### Wave 0 Gaps

None — existing test infrastructure (mkdocs.yml, GitHub Actions workflow) covers all phase requirements. No new test files needed.

---

## State of the Art

| Old Approach | Current Approach | Impact |
|---|---|---|
| Parameter info scattered across guide pages | Single lookup table at `reference/parametry.md` | Users can find default/range without reading full guide |
| No cross-links between guide and reference | Bidirectional "Viz také" + inline links | UX-04 satisfied; reduces navigation friction |
| FAQ stub with empty categories | 13+ FAQ items in 3 categories | FAQ-01 through FAQ-04 satisfied |

---

## Open Questions

1. **Exact anchor names for Czech headings**
   - What we know: MkDocs Material generates anchors from headings; Czech diacritics handling is version-dependent
   - What's unclear: Whether `## Výztuž` → `#vyztu` or `#výztuž` in MkDocs 1.6.1
   - Recommendation: Write parametry.md first, run `mkdocs build --strict`, inspect generated HTML, then add cross-links using verified anchors

2. **Settings "Výchozí hodnoty" defaults for diameter/spacing fields**
   - What we know: The SettingsWindow.xaml shows TextBox fields (`txtDefaultDiameterVerticalOuter` etc.) with no `Text=` default — they are populated from saved settings
   - What's unclear: What initial values are shown to a first-time user with no saved settings
   - Recommendation: Document as "dle aktuálního nastavení v hlavním dialogu" (matches how the guide describes it)

---

## Sources

### Primary (HIGH confidence)

- `../WallReinf/WallReinf.Core/RebarParameters.cs` — all C# property defaults verified by reading source
- `../WallReinf/WallReinf/MainWindow.xaml` — all Czech UI labels, ComboBox items, Slider ranges from XAML
- `../WallReinf/WallReinf/SettingsWindow.xaml` — Settings dialog labels, GroupBox headers, Slider ranges
- `docs/pruvodce/*.md` (11 files) — warning/tip admonitions catalogued as FAQ sources
- `mkdocs.yml` — nav structure, extensions, site config confirmed

### Secondary (MEDIUM confidence)

- `../WallReinf/WallReinf/MainWindow.xaml.cs` (error messages via grep) — FAQ-C01/C02 error strings from exception handlers
- `../WallReinf/WallReinf/Validation/ValidationPdfExporter.cs` — FAQ-V03 "Není co exportovat" exception

### Tertiary (LOW confidence)

- None — all findings verified against source files or XAML

---

## Metadata

**Confidence breakdown:**
- Standard stack: HIGH — no new packages; existing stack confirmed from project files
- Parameter catalogue: HIGH — extracted directly from XAML and RebarParameters.cs source
- FAQ content: HIGH — sourced from existing guide warning admonitions and source exception messages
- Architecture patterns: HIGH — follows established Phase 3 patterns, verified against existing pages
- Cross-link anchors: MEDIUM — anchor generation behavior for Czech strings needs runtime verification (see Open Questions #1)

**Research date:** 2026-03-26
**Valid until:** 2026-06-26 (stable stack; content is static)
