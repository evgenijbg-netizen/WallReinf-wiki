# Phase 3: User Guide Content - Research

**Researched:** 2026-03-26
**Domain:** Technical writing — MkDocs Material Czech-language wiki, plugin UI mapping
**Confidence:** HIGH

---

<user_constraints>
## User Constraints (from CONTEXT.md)

### Locked Decisions

**Writing Style**
- Stručný a přímý — krátké věty, minimum úvodů, orientovaný na akci
- Formát: číslované kroky pro workflow, admonitions pro warningy/tipy
- Žádné "esejistické" úvody — rovnou k věci
- Cílová skupina: zkušený uživatel Tekla Structures — nepopisovat základy Tekly (co je model, assembly, jak vybrat prvek), jen funkce pluginu

**UI Element Formatting**
- Názvy UI prvků tučně česky: **Generovat**, **Načíst**, **Výztuž**, **Orientace S1**
- Pro netextová tlačítka (ikony) ideálně replikovat ikonu ve wiki — kde to nejde, tučně popsat funkci: **Předchozí stěna (←)**
- Názvy sekcí UI rovněž tučně: **Krytí a okraje**, **Detaily**

**Terminology Source**
- Autoritativní zdroj názvů: XAML labely pluginu (ne vlastní překlad)
- Klíčové termíny: Prostupy (ne Otvory), Lemování (U-čka), Rozteč, Třmínky, Prapory, Závlače, Šikmá výztuž v rozích
- S1 = vnější strana, S2 = vnitřní strana
- "Svislá (nosná)" / "Vodorovná (nosná)" pro orientaci

**Version Badge**
- Formát: `[VERZE]` placeholder na každé stránce
- Implementace: admonition `!!! info "Verze pluginu: [VERZE]"` na začátku stránky

**Screenshot Placeholders**
- Formát: standardní MkDocs image syntax s popisným alt textem
- Caption pod obrázkem obsahuje instrukce pro fázi 5 (co vyfotit, jaké nastavení)
- Pojmenování souborů: popis obsahu (`hlavni-dialog-vyztu.png`, `preview-panel-vrstvy.png`)
- Příklad:
  ```markdown
  ![Hlavní dialog — sekce Výztuž s nastavenými průměry](../assets/screenshots/hlavni-dialog-vyztu.png)

  *[VERZE] — Hlavní okno pluginu se sekcí Výztuž. Zachytit: průměry Ø10, rozteč 150mm, S1 i S2 viditelné.*
  ```

**Content Structure — pruvodce/parametry.md**
- Workflow-oriented — vysvětluje JAK a KDY nastavit parametry
- Pokrývá všechny 3 sekce UI podrobně: Výztuž, Krytí a okraje, Detaily
- Sekce Detaily zahrnuje pokročilé funkce: T-spoj (navazující stěny), Volný konec stěny, Pokračuje výš (deska)
- Typické hodnoty a doporučení v kontextu (ne jen výčet polí)
- Žádné tabulky s default hodnotami a rozsahy — to je pro reference/parametry.md (fáze 4)

**Cross-Referencing Between Guide Pages**
- Feature stránky (otvory, třmínky, diagonály) odkazují na pruvodce/parametry.md pro společné koncepty (S1/S2, orientace)
- Neopakovat vysvětlení konceptů na každé stránce
- Formát: `[Orientace S1](parametry.md#orientace-s1)` — interní linky v rámci průvodce

**Settings Window Coverage**
- Settings okno nemá vlastní stránku — pokrýt kontextuálně na feature stránkách
- Prahy třmínků → stránka třmínků
- Filtry otvorů (ignorovat kapsy/výřezy) → stránka otvorů
- Segmentace rastru → stránka parametrů
- Výchozí hodnoty → stránka parametrů (zmínit že existují v Settings)
- Normy (poloha výztuže, tabulka přesahů) → stránka parametrů

**Peripheral Features**
- Poznámky ke stěně (NoteWindow) → stručná sekce v zakladni-workflow.md
- Heatmapa (Ø × délka matice) → sekce v preview.md
- Tabulka přesahů a kotevních délek → zmínka v parametry.md u sekce Normy
- Každá dostane krátkou sekci, ne celou stránku

### Claude's Discretion
- Přesné pořadí sekcí na každé stránce
- Počet a umístění admonitions (minimálně tam, kde hrozí chyba)
- Počet screenshot placeholderů per stránka (dle potřeby workflow)
- Přesné formulace textů v rámci dohodnutého tónu a stylu
- Zda a jak použít `pymdownx.details` (sbalitelné sekce) pro méně důležité detaily

### Deferred Ideas (OUT OF SCOPE)

None — discussion stayed within phase scope
</user_constraints>

---

<phase_requirements>
## Phase Requirements

| ID | Description | Research Support |
|----|-------------|-----------------|
| START-01 | Stránka popisuje požadavky (Tekla Structures verze, .NET, OS) | pozadavky.md stub exists; no system requirement data in XAML — must be sourced from plugin installer/documentation |
| START-02 | Stránka popisuje instalaci/spuštění pluginu | instalace.md stub exists; flow is: copy files → launch from Tekla applications panel |
| START-03 | Stránka popisuje připojení k modelu v Tekle | pripojeni.md stub exists; SettingsWindow.xaml: **Test připojení**, **Filtr materiálu (prefix)** |
| START-04 | Stránka popisuje základní workflow (výběr stěny → nastavení → generování) | zakladni-workflow.md stub exists; maps to: Prefix → **Načíst** → **Stěna:** selector → set params → **Generovat** |
| GUIDE-01 | Stránka pro hlavní parametry (průměry prutů, krytí, rozteče, okrajové pruty) | parametry.md stub; maps to MainWindow Expanders: **Výztuž**, **Krytí a okraje**, **Detaily** |
| GUIDE-02 | Stránka pro otvory (detekce, nastavení, U-pruty kolem otvorů) | otvory.md stub; maps to MainWindow **Prostupy** sub-section + SettingsWindow **Generace otvorů**, **Prostupy**, **Fiktivní zvětšení otvorů** |
| GUIDE-03 | Stránka pro třmínky a interakce segmentů | trminky.md stub; maps to SettingsWindow **Třmínky a prapory** + MainWindow segment logic |
| GUIDE-04 | Stránka pro diagonální pruty | diagonaly.md stub; maps to MainWindow **Prostupy** → CheckBox **Šikmá výztuž v rozích (45°)** |
| GUIDE-05 | Stránka pro preview panel (vizualizace plánované výztuže) | preview.md stub; maps to RebarPreviewWindow.xaml + inline preview in MainWindow right column |
| GUIDE-06 | Stránka pro validační okno | validace.md stub; maps to RebarValidationWindow.xaml — "Grafická validace výztuže", reality mode |
| GUIDE-07 | Stránka pro PDF export | pdf-export.md stub; maps to RebarValidationWindow **Export PDF**, **Export PNG**, **Tisk** buttons |
| UX-01 | Admonitions (warning, tip, note) jsou použity u důležitých upozornění | MkDocs Material admonition extension already enabled in mkdocs.yml |
| UX-02 | Na každé stránce je badge/admonition s verzí pluginu | Locked format: `!!! info "Verze pluginu: [VERZE]"` at top of each page |
| UX-03 | Terminologie v wiki odpovídá labelům v UI pluginu | XAML files verified as authoritative source — see Canonical Terminology section below |
</phase_requirements>

---

## Summary

Phase 3 writes full prose content into 12 existing stub files in `docs/pruvodce/`. The stubs already have correct H1 headings and H2 section skeletons from Phase 2. The task is to fill each file with actionable Czech prose, admonitions, version badge, and `[SCREENSHOT]` placeholders.

All infrastructure is in place: MkDocs Material 9.7.6 with admonition, pymdownx.details, pymdownx.superfences, and other extensions already enabled. The canonical source for all UI terminology is the plugin's XAML files, which have been read and catalogued below. No library research or toolchain changes are needed — this phase is purely a content authoring task.

The primary writing challenge is maintaining workflow orientation (explain when and how, not just what) while keeping the Czech prose concise and action-focused for an audience that already knows Tekla Structures.

**Primary recommendation:** Write each page in content-fill order matching the user workflow, not the UI section order. Use the UI terminology catalogue below as the single source of truth. Never coin new Czech terms for UI elements that already have labels in the XAML.

---

## Standard Stack

### Already Enabled (mkdocs.yml verified)

| Extension | Purpose | Config Status |
|-----------|---------|---------------|
| `admonition` | `!!! warning`, `!!! tip`, `!!! note`, `!!! info` blocks | Enabled |
| `pymdownx.details` | Collapsible `??? note` blocks for secondary content | Enabled |
| `pymdownx.superfences` | Code blocks inside admonitions | Enabled |
| `pymdownx.tabbed` | Content tabs (alternate_style: true) | Enabled |
| `attr_list` | `{ .class }` attribute syntax | Enabled |
| `md_in_html` | Markdown inside HTML blocks | Enabled |
| `glightbox` plugin | Lightbox for images | Enabled |
| `search` (lang: cs) | Czech fulltext search | Enabled |

No new packages required for this phase.

### Admonition Types Available

```markdown
!!! info "Verze pluginu: [VERZE]"
    Tato stránka popisuje chování pluginu verze [VERZE].

!!! warning "Pozor"
    Text varování.

!!! tip "Tip"
    Text tipu.

!!! note "Poznámka"
    Text poznámky.

??? note "Rozbalit pro podrobnosti"
    Sbalitelná sekce (pymdownx.details).
```

---

## Canonical Terminology (from XAML — HIGH confidence)

These are the exact Czech labels as they appear in the plugin UI. Use these verbatim; do not translate or paraphrase.

### MainWindow.xaml — Top Bar

| UI Element | XAML Label | Bold Wiki Format |
|-----------|-----------|-----------------|
| Prefix input | `Prefix:` | **Prefix** |
| Load walls button | `Načíst` | **Načíst** |
| Show-only toggle | ToolTip: "Zobrazit pouze vybranou stěnu" | **Zobrazit pouze vybranou stěnu** |
| Wall selector | `Stěna:` | **Stěna** |
| Previous wall | `◀` (icon button) | **Předchozí stěna (◀)** |
| Next wall | `▶` (icon button) | **Další stěna (▶)** |
| Select from Tekla | ToolTip: "Vybrat stenu z aktualniho oznaceni v Tekla" | **Vybrat z Tekla** |
| Fit work area | ToolTip: "Oříznout pohled na tloušťku stěny" | **Oříznout pohled (S1/S2)** |
| Status: done | Context menu: "Označit jako hotovo" | **Hotovo** |
| Status: review | Context menu: "Označit ke kontrole" | **Ke kontrole** |
| Status: no rebar | Context menu: "Označit bez výztuže" | **Bez výztuže** |
| Settings | ToolTip: "Nastavení" | **Nastavení** |

### MainWindow.xaml — Expander 1: Výztuž

| UI Element | XAML Label | Notes |
|-----------|-----------|-------|
| Expander header | `Výztuž` | Section **Výztuž** |
| Orientation sub-header | `Orientace S1` | **Orientace S1** |
| Outer vertical | `Svislá (nosná)` | RadioButton |
| Outer horizontal | `Vodorovná (nosná)` | RadioButton |
| Vertical rebar section | `Svislá výztuž` | sub-section label |
| Horizontal rebar section | `Vodorovná výztuž` | sub-section label |
| S1 label | `S1:` | outer face |
| S2 label | `S2:` | inner face |
| Spacing label | `Rozteč:` | both directions |
| Edge rebar | `Lemování (U-čka)` | CheckBox — section **Lemování** |
| Diameter label | `Průměr:` | inside Lemování |
| Edge spacing note | `Rozteč: dle přímé výztuže` | informational |
| Openings section | `Prostupy` | section header |
| Opening diameter | `Průměr:` | inside Prostupy |
| Diagonal rebar | `Šikmá výztuž v rozích (45°)` | CheckBox |
| Stirrups above door | `Třmínky nad dveřmi` | CheckBox |
| Unify all | `Sjednotit vše` | ToolTip: "Sjednotit průměry S2 podle S1" |
| Note button | ToolTip: `Poznámka ke stěně` | icon button |

### MainWindow.xaml — Expander 2: Krytí a okraje

| UI Element | XAML Label | Notes |
|-----------|-----------|-------|
| Expander header | `Krytí a okraje` | Section **Krytí a okraje** |
| Cover | `Krytí:` | ComboBox, values 30/35/40/50/60 mm |
| Steel grade | `Ocel:` shown as `B500B` | informational |
| Offset | `Odsazení:` | ToolTip: "Počáteční odsazení prutu od spodního/horního okraje" |
| Edge offsets section | `Odsazení od kraje` | sub-section |
| Horizontal offset | `H:` | ToolTip: "Vodorovný směr" |
| Vertical offset | `V:` | ToolTip: "Svislý směr" |

### MainWindow.xaml — Expander 3: Detaily

| UI Element | XAML Label | Notes |
|-----------|-----------|-------|
| Expander header | `Detaily` | Section **Detaily** |
| Boundary conditions | `Okrajové podmínky` | sub-section |
| Free end | `Volný konec stěny` | CheckBox |
| Continues up | `Pokračuje výš` | CheckBox |
| Slab thickness | `Tl. desky:` | TextBox, mm |
| T-joint | `T-spoj (navazující stěny)` | sub-section; only active when **Lemování** enabled |
| Adjacent left | `Zleva` | CheckBox |
| Adjacent right | `Zprava` | CheckBox |
| Adjacent thickness | `tl:` | ComboBox, 150–400 mm |
| Tie bars | `Závlače:` | Slider, 40–200 mm |

### MainWindow.xaml — Right Column (inline preview dock)

| UI Element | XAML Label | Notes |
|-----------|-----------|-------|
| Length adjustments header | `Úpravy délek:` | adjustment control strip |
| Shorten -50 | `-50` (button) | ToolTip: "Zkrátit o 50 mm" |
| Shorten -10 | `-10` (button) | ToolTip: "Zkrátit o 10 mm" |
| Lengthen +10 | `+10` (button) | ToolTip: "Prodloužit o 10 mm" |
| Lengthen +50 | `+50` (button) | ToolTip: "Prodloužit o 50 mm" |
| Collision check | `Kolize` (button) | ToolTip: "Zkontrolovat kolize" |
| Normalize | `Sjednotit` (button) | ToolTip: "Sjednotit delky vybranych rad" |
| Heatmap | `Heatmapa` | label in dock |
| Layers | `Vrstvy` | label in dock |
| Show all layers | `Zobrazit vše` (button) | toggle button |

### SettingsWindow.xaml — All Sections

| Section | XAML Header | Key Controls |
|---------|------------|--------------|
| Connection | `Připojení` | **Test připojení** button, status text |
| Wall loading | `Načítání stěn` | **Filtr materiálu (prefix):** TextBox |
| Grid segmentation | `Segmentace rastru` | **Práh pro přerušení** (m2), **Max délka segmentu** (mm), **Min vzdálenost od otvoru** (mm) |
| Stirrups and flags | `Třmínky a prapory` | Two sliders: stirrup threshold, flag threshold |
| Opening generation | `Generace otvorů` | **Limit protažení noh U-ček** slider, **Odsazení ohybu kotevních prutů** slider |
| Opening inflation | `Fiktivní zvětšení otvorů` | H and V sliders |
| Openings filter | `Prostupy` | **Ignorovat kapsy**, **Ignorovat výřezy**, **Ignorovat všechny prostupy** checkboxes |
| Default values | `Výchozí hodnoty` | Průměry 6-field grid, Rozteče 6-field grid, **Krytí**, **Odsazení od okraje** |
| Bar splitting | `Dělení prutu` | **Maximální délka prutu** slider (6000–12000 mm) |
| Standards | `Normy` | **Poloha výztuže** ComboBox (Nepříznivá/Příznivá), **Tabulka přesahů a kotevních délek** button |

### RebarPreviewWindow.xaml — Standalone Preview

| UI Element | XAML Label | Notes |
|-----------|-----------|-------|
| Window title | `Preview výztuže` | separate window |
| Layers panel | `Vrstvy výztuže` | right panel header |
| Show all | `Vše` (button) | ToolTip: "Zobrazit všechny vrstvy" |
| Hide all | `Nic` (button) | ToolTip: "Skrýt všechny vrstvy" |
| Length edit label | `Úprava délky (vybrané řady):` | |
| Statistics | `Celkem: 0 prutů, 0 délek, 0 varování` | status bar text pattern |
| Check collisions | `Zkontrolovat kolize` | ToolTip: "Zkontrolovat kolize s okraji a otvory" |
| Normalize selected | `Sjednotit vybrané` | ToolTip: "Sjednotit délky vybraných řad" |
| Generate button | `Generovat` | primary action in preview |
| Cancel button | `Zrušit` | |
| Heatmap | `Heatmapa (Ø × délka)` | Expander header |

### RebarValidationWindow.xaml — Validation

| UI Element | XAML Label | Notes |
|-----------|-----------|-------|
| Window title | `Grafická validace výztuže` | |
| Mode indicator | `Skutečná výztuž z Tekla modelu` | "reality mode" label |
| Refresh | `Obnovit` | ToolTip: "Znovu načíst data z Tekla modelu" |
| Export PDF | `Export PDF` | primary action button |
| Export PNG | `Export PNG` | |
| Print | `Tisk` | |
| Layers panel | `Vrstvy výztuže` | right panel |
| Layer legend entries | Svislá (Class 3), Vodorovná (Class 6), Lemování hrany (Class 7,8), Lemování otvoru (Class 9), Prapory (Class 9 - Flag), Třmínky (Class 11) | exact legend text |
| Transparency | `Průhlednost:` | slider |
| Legend section | `Legenda barev` | collapsible expander |

---

## Architecture Patterns

### Page File Map

All 12 stub files already exist in `docs/pruvodce/`. Content goes into these exact files:

```
docs/pruvodce/
├── index.md              # Průvodce index — short intro only, no new content needed
├── pozadavky.md          # START-01 — requirements page
├── instalace.md          # START-02 — installation page
├── pripojeni.md          # START-03 — connection page
├── zakladni-workflow.md  # START-04 — basic workflow (end-to-end demo)
├── parametry.md          # GUIDE-01 — longest page, all 3 expanders + Settings refs
├── otvory.md             # GUIDE-02 — openings (Prostupy section + Settings)
├── trminky.md            # GUIDE-03 — stirrups + segments + Settings thresholds
├── diagonaly.md          # GUIDE-04 — diagonal rebar
├── preview.md            # GUIDE-05 — preview panel (both inline dock and standalone window)
├── validace.md           # GUIDE-06 — validation window
└── pdf-export.md         # GUIDE-07 — PDF export from validation window
```

### Standard Page Template

Every page MUST begin with the version badge admonition, then proceed directly to content:

```markdown
# [H1 Title matching nav label]

!!! info "Verze pluginu: [VERZE]"
    Tato stránka popisuje chování pluginu verze [VERZE].

[One-sentence orientation — what this page covers, max 1 sentence]

## [Section heading]

[Numbered steps or prose]
```

### Workflow Step Pattern

For any sequence of user actions, use numbered lists:

```markdown
1. Zadejte prefix stěn do pole **Prefix** (například `1W`).
2. Klikněte na **Načíst** — plugin načte všechny stěny z modelu odpovídající prefixu.
3. Vyberte stěnu z rozbalovací nabídky **Stěna**.
```

### Screenshot Placeholder Pattern (locked in CONTEXT.md)

```markdown
![Alt text popisující obsah screenshotu](../assets/screenshots/popisny-nazev.png)

*[VERZE] — Popis okna/sekce. Zachytit: konkrétní nastavení, stav UI který je třeba ukázat.*
```

File naming convention: all lowercase, hyphens, ASCII only, descriptive of content. Examples:
- `hlavni-dialog-vyztu.png`
- `settings-segmentace-rastru.png`
- `preview-panel-heatmapa.png`
- `validace-vrstvy-legenda.png`

### Cross-Reference Pattern

Internal links within pruvodce/ section use relative paths:

```markdown
[Orientace S1](parametry.md#orientace-s1)
[sekci Prostupy](otvory.md#prostupy)
```

No links to `reference/` in this phase (UX-04 is Phase 4).

### Admonition Placement Rules

Place admonitions at the point in the workflow where the risk or tip occurs, not at the top of the page (except the version badge):

```markdown
!!! warning "Pozor — T-spoj vyžaduje aktivní Lemování"
    Sekce **T-spoj** je dostupná pouze pokud je zaškrtnuto **Lemování (U-čka)**.
    Bez lemování se závlače negenerují.

!!! tip "Tip — Výchozí hodnoty v Nastavení"
    Opakovaně používané hodnoty průměrů a roztečí lze nastavit jako výchozí
    v okně **Nastavení** → **Výchozí hodnoty**. Plugin je předvyplní při každém
    přepnutí na novou stěnu.
```

---

## Don't Hand-Roll

| Problem | Don't Build | Use Instead | Why |
|---------|-------------|-------------|-----|
| Collapsible "advanced" sections | Custom HTML/JS toggle | `??? note` (pymdownx.details) | Already enabled, MkDocs-native |
| Tabbed variant workflows | Manual headers + conditional prose | `=== "Tab name"` (pymdownx.tabbed) | Already enabled, clean rendering |
| Code/terminal blocks inside admonitions | Nested HTML | pymdownx.superfences | Already enabled |
| Image zoom | Link-wrapped images | glightbox plugin | Already enabled in mkdocs.yml |
| Custom warning icons | Unicode or SVG inline | MkDocs Material admonition icons | Built into theme |

**Key insight:** The full MkDocs Material feature set is already configured. No new extensions or plugins are needed. Don't create HTML workarounds for things that already work with standard Markdown.

---

## Common Pitfalls

### Pitfall 1: Inventing Terminology
**What goes wrong:** Writer uses "otvory" where the plugin says "Prostupy", or "U-pruty" where the plugin says "U-čka" (in Lemování context) vs. "noh U-ček" (in Settings context).
**Why it happens:** Casual Czech usage differs from the XAML labels.
**How to avoid:** Before writing any UI label, check the Canonical Terminology table above. The XAML is the authority.
**Warning signs:** Any term not present in the Canonical Terminology section should be treated as suspect.

### Pitfall 2: mkdocs build --strict Failures from Cross-Links
**What goes wrong:** A page links to `reference/parametry.md#some-anchor` but that anchor doesn't exist yet (Phase 4).
**Why it happens:** Natural urge to link forward.
**How to avoid:** Only link within `pruvodce/` in this phase. No links to `reference/`, `faq.md`, or any anchor that doesn't exist in a Phase 2 stub.
**Warning signs:** `mkdocs build --strict` reports warnings about broken anchors.

### Pitfall 3: Broken Image References
**What goes wrong:** Screenshot placeholder uses a path that doesn't resolve, causing --strict failure.
**Why it happens:** The `assets/screenshots/` directory may not exist yet.
**How to avoid:** Create `docs/assets/screenshots/.gitkeep` (empty placeholder) before writing image references, OR use a comment format that MkDocs won't parse. The recommended approach: create the directory and use standard image syntax — MkDocs will warn but won't break if the file is missing under --strict only for broken links, not missing images.
**Warning signs:** Check whether `docs/assets/screenshots/` exists before writing any `![...]` syntax.

### Pitfall 4: Indentation Errors in Admonitions
**What goes wrong:** Content inside `!!! warning` is not indented 4 spaces, causing the admonition to render as plain text.
**Why it happens:** Markdown indentation sensitivity.
**How to avoid:** Always indent admonition body content exactly 4 spaces.

```markdown
!!! warning "Správně"
    Tento text je správně odsazený o 4 mezery.

!!! warning "Špatně"
Tento text NENÍ odsazený — nezobrazí se jako admonition.
```

### Pitfall 5: Sections That Are UI Descriptions Instead of Workflows
**What goes wrong:** Page describes "this button does X" rather than "to achieve Y, do X".
**Why it happens:** It is easier to describe UI elements than to explain when to use them.
**How to avoid:** For each section, ask "what is the user trying to accomplish here?" before writing. Start with the user goal, then describe the steps.

### Pitfall 6: T-spoj Dependency Not Documented
**What goes wrong:** User cannot find T-spoj controls because they are grayed out — the page doesn't explain why.
**Why it happens:** The XAML binding shows `IsEnabled="{Binding IsChecked, ElementName=chkGenerateEdge}"` — T-spoj is only active when **Lemování (U-čka)** is checked.
**How to avoid:** The parametry.md T-spoj section MUST include an admonition explaining this dependency.

### Pitfall 7: Default Values Not Mentioned
**What goes wrong:** User doesn't know default values come from Settings, not hardcoded.
**Why it happens:** The relationship between MainWindow defaults and SettingsWindow **Výchozí hodnoty** is not obvious.
**How to avoid:** parametry.md MUST mention that all diameter and spacing defaults can be changed in **Nastavení** → **Výchozí hodnoty**. A `!!! tip` is appropriate here.

---

## Code Examples

### Version Badge (every page)

```markdown
!!! info "Verze pluginu: [VERZE]"
    Tato stránka popisuje chování pluginu verze [VERZE].
```

### Numbered Workflow Steps

```markdown
1. Otevřete plugin v Tekla Structures.
2. Do pole **Prefix** zadejte prefix označení stěn (např. `1W`).
3. Klikněte na **Načíst** — rozbalovací nabídka **Stěna** se naplní nalezenými stěnami.
4. Vyberte stěnu. Plugin zobrazí live preview výztuže v pravém panelu.
```

### Screenshot Placeholder with Instruction Caption

```markdown
![Hlavní dialog — sekce Výztuž, průměry a rozteče nastaveny](../assets/screenshots/hlavni-dialog-vyztu.png)

*[VERZE] — Hlavní okno pluginu, expander **Výztuž** rozbalen. Zachytit: Svislá výztuž Ø12 S1 i S2, rozteč 200 mm; Vodorovná výztuž Ø10 S1 i S2, rozteč 200 mm; **Lemování (U-čka)** zaškrtnuto, Ø14.*
```

### Collapsible Advanced Section (pymdownx.details)

```markdown
??? note "Pokročilé: Fiktivní zvětšení otvorů"
    V okně **Nastavení** → **Fiktivní zvětšení otvorů** lze otvory pro účely
    výpočtu rastru přímé výztuže fiktivně zvětšit. Lemovací výztuž se vždy
    generuje na fyzickém (nezvetšeném) otvoru.
```

### Internal Cross-Link

```markdown
Koncepty S1 a S2 jsou vysvětleny v části [Orientace S1](parametry.md#orientace-s1).
```

### Admonition with Dependency Warning

```markdown
!!! warning "T-spoj je dostupný pouze s Lemováním"
    Sekce **T-spoj (navazující stěny)** je aktivní pouze pokud je zaškrtnuta
    volba **Lemování (U-čka)**. Bez lemování jsou ovládací prvky T-spoje
    zašedlé a závlače se negenerují.
```

---

## Content Guide per Page

### pozadavky.md (START-01)

**Sections to fill:** Tekla Structures, Operační systém, .NET Framework
**Key content:** Minimum Tekla version, .NET version, OS. These are not in the XAML — they must come from the plugin project file or installer. **Open question: exact version requirements.**
**Admonitions:** `!!! warning` if minimum versions have known compatibility issues.

### instalace.md (START-02)

**Sections to fill:** Instalace pluginu, Spuštění pluginu
**Key content:** Where to copy plugin DLL/files → Tekla applications panel → first launch → connection to model.
**Admonitions:** `!!! note` about Tekla needing to be open with a model before launching plugin.

### pripojeni.md (START-03)

**Sections to fill:** Otevření modelu, Výběr stěny
**Key content:** Open **Nastavení** → **Připojení** → **Test připojení**; **Filtr materiálu (prefix)** in Settings; prefix field in main window; wall selection; status filters (Hotovo / Ke kontrole / Bez výztuže).
**Admonitions:** `!!! warning` if Tekla model must be open before plugin connect.

### zakladni-workflow.md (START-04)

**Sections to fill:** Výběr stěny, Nastavení parametrů, Generování výztuže
**Additional sections to add (per CONTEXT.md):** Poznámky ke stěně (brief)
**Key content:** End-to-end walkthrough of one wall. Cross-link to parametry.md, otvory.md, preview.md for details. Note button (icon button) → NoteWindow for per-wall notes.
**Admonitions:** `!!! tip` about status workflow (Ke kontrole → Hotovo), `!!! note` about preview being shown before final generation.

### parametry.md (GUIDE-01) — longest page

**Sections to cover:**
- Expander **Výztuž** in full: Orientace S1, Svislá výztuž, Vodorovná výztuž, Lemování (U-čka), Prostupy
- Expander **Krytí a okraje**: Krytí, Odsazení, Odsazení od kraje
- Expander **Detaily**: Okrajové podmínky (Volný konec stěny, Pokračuje výš + Tl. desky), T-spoj (Zleva/Zprava, tl., Závlače)
- Settings context: Výchozí hodnoty, Segmentace rastru, Normy (Poloha výztuže, Tabulka přesahů)
**Admonitions:** T-spoj dependency warning, tip about defaults in Settings, note about Normy affecting material quantities.

### otvory.md (GUIDE-02)

**Sections to fill:** Detekce otvorů, Nastavení otvorů, U-pruty kolem otvorů
**Key content:** How plugin detects openings; **Prostupy** section in **Výztuž** expander (diameter, **Šikmá výztuž v rozích (45°)**, **Třmínky nad dveřmi**); Settings: **Prostupy** filter checkboxes (Ignorovat kapsy / Ignorovat výřezy / Ignorovat všechny prostupy), **Generace otvorů** (Limit protažení noh U-ček, Odsazení ohybu kotevních prutů), **Fiktivní zvětšení otvorů**.
**Admonitions:** `!!! warning` about "Ignorovat kapsy" — use only if niches should not interrupt rebar grid.

### trminky.md (GUIDE-03)

**Sections to fill:** Nastavení třmínků, Interakce segmentů
**Key content:** Settings **Třmínky a prapory** — two threshold sliders (stirrup threshold, flag threshold); what happens at segment boundaries; short vs. long segment behavior. Prapory as alternative to stirrups for short segments.
**Admonitions:** `!!! note` explaining threshold logic (segment < stirrup threshold → stirrups; segment < flag threshold → flags/prapory; segment > flag threshold → normal rebar).

### diagonaly.md (GUIDE-04)

**Sections to fill:** Nastavení diagonálních prutů, Umístění diagonál
**Key content:** CheckBox **Šikmá výztuž v rozích (45°)** in **Prostupy** section; when diagonal rebar is generated (corners of openings); 45° angle; interaction with opening size.
**Note:** This is a compact feature page — cross-reference to parametry.md for the Prostupy section context.

### preview.md (GUIDE-05)

**Sections to fill:** Zobrazení preview, Interpretace vizualizace
**Additional sections (per CONTEXT.md):** Heatmapa sekce
**Key content:** Two preview modes: (1) inline dock in MainWindow right column — live preview with **Vrstvy**, **Heatmapa**, **Úpravy délek**, **Kolize**, **Sjednotit**; (2) standalone **RebarPreviewWindow** — same features but full screen with **Generovat** button.
**Heatmapa:** Matrix of Ø × délka showing how many bars of each combination exist. Click cell to filter visible layers.
**Admonitions:** `!!! tip` — adjustments made in preview are preserved when you click **Generovat**.

### validace.md (GUIDE-06)

**Sections to fill:** Spuštění validace, Interpretace výsledků
**Key content:** "Grafická validace výztuže" window; "Skutečná výztuž z Tekla modelu" mode (reality mode — shows actual generated rebar from Tekla model, not planned); **Obnovit** button; layer legend (Svislá/Vodorovná/Lemování hrany/Lemování otvoru/Prapory/Třmínky with class numbers); **Průhlednost** slider; **Legenda barev** expander.
**Admonitions:** `!!! note` that validation window shows *already generated* rebar from Tekla model, not the planned preview — user must generate first.

### pdf-export.md (GUIDE-07)

**Sections to fill:** Vytvoření exportu, Obsah PDF dokumentu
**Key content:** Three export actions in RebarValidationWindow: **Export PDF**, **Export PNG**, **Tisk**; what the export contains (graphical wall view with visible layers); use of layer visibility to control what is exported.
**Admonitions:** `!!! tip` — turn off layers you don't want before exporting to get cleaner output.

---

## State of the Art

| Old Approach | Current Approach | Notes |
|--------------|-----------------|-------|
| MkDocs auto-discovery nav | Explicit `nav:` in mkdocs.yml | Already in place from Phase 2 |
| Plain Markdown warnings in prose | `!!! warning` admonitions | Extension enabled, use it |
| Inline HTML for collapsibles | `??? note` (pymdownx.details) | Extension enabled |

**No deprecated approaches need replacing in this phase.**

---

## Open Questions

1. **pozadavky.md — Exact version requirements not in XAML**
   - What we know: Plugin runs on Tekla Structures and requires .NET (WPF application)
   - What's unclear: Minimum Tekla version, .NET version (4.8? 6.0?), OS (Windows 10+ only?)
   - Recommendation: Check `WallReinf.csproj` or installer readme; if unavailable, use placeholder `[TEKLA_VERSION]` similar to `[VERZE]` pattern

2. **instalace.md — Installation method not documented**
   - What we know: Plugin is a WPF .NET application loaded by Tekla
   - What's unclear: How it is distributed (xcopy, installer, Tekla extensions marketplace?), exact folder path
   - Recommendation: Check project output path or deployment notes; if unavailable, use `[INSTALACNI_CESTA]` placeholder

3. **assets/screenshots/ directory existence**
   - What we know: CONTEXT.md specifies `../assets/screenshots/` path
   - What's unclear: Whether `docs/assets/screenshots/` directory exists
   - Recommendation: Implementer must create `docs/assets/screenshots/.gitkeep` before writing any image references, to prevent --strict issues

4. **Inline preview vs. standalone RebarPreviewWindow — flow relationship**
   - What we know: Both exist; MainWindow has inline dock; RebarPreviewWindow is a separate window
   - What's unclear: How the standalone preview window is launched (button? menu?)
   - Recommendation: Check MainWindow for a "Preview" launch button — likely `btnExportPdf` area or a separate preview button not visible in the XAML excerpt read

---

## Validation Architecture

### Test Framework

| Property | Value |
|----------|-------|
| Framework | `mkdocs build --strict` (static site build validation) |
| Config file | `mkdocs.yml` (project root) |
| Quick run command | `mkdocs build --strict 2>&1 \| tail -5` |
| Full suite command | `mkdocs build --strict` |

### Phase Requirements → Test Map

| Req ID | Behavior | Test Type | Automated Command | File Exists? |
|--------|----------|-----------|-------------------|-------------|
| START-01 | pozadavky.md has substantive prose | smoke | `mkdocs build --strict` | ✅ (stub) |
| START-02 | instalace.md has substantive prose | smoke | `mkdocs build --strict` | ✅ (stub) |
| START-03 | pripojeni.md has substantive prose | smoke | `mkdocs build --strict` | ✅ (stub) |
| START-04 | zakladni-workflow.md end-to-end demo | smoke | `mkdocs build --strict` | ✅ (stub) |
| GUIDE-01 | parametry.md covers all 3 expanders | smoke | `mkdocs build --strict` | ✅ (stub) |
| GUIDE-02 | otvory.md covers detection + settings | smoke | `mkdocs build --strict` | ✅ (stub) |
| GUIDE-03 | trminky.md covers thresholds | smoke | `mkdocs build --strict` | ✅ (stub) |
| GUIDE-04 | diagonaly.md covers 45° corners | smoke | `mkdocs build --strict` | ✅ (stub) |
| GUIDE-05 | preview.md covers inline + standalone + heatmap | smoke | `mkdocs build --strict` | ✅ (stub) |
| GUIDE-06 | validace.md covers reality mode | smoke | `mkdocs build --strict` | ✅ (stub) |
| GUIDE-07 | pdf-export.md covers Export PDF/PNG/Tisk | smoke | `mkdocs build --strict` | ✅ (stub) |
| UX-01 | Admonitions present on pages with warnings | manual-only | Read each page | N/A |
| UX-02 | Version badge on every page | manual-only | `grep -l "Verze pluginu" docs/pruvodce/*.md` | N/A |
| UX-03 | Terminology matches XAML labels | manual-only | Spot-check 5 terms against XAML | N/A |

### Sampling Rate

- **Per task commit:** `mkdocs build --strict` — zero warnings required
- **Per wave merge:** `mkdocs build --strict` — zero warnings required
- **Phase gate:** Full suite green before `/gsd:verify-work`

### Wave 0 Gaps

- [ ] `docs/assets/screenshots/.gitkeep` — directory must exist before any image references are written

*(All stub .md files already exist from Phase 2. No test framework installation needed — mkdocs is already installed.)*

---

## Sources

### Primary (HIGH confidence)
- `../WallReinf/WallReinf/MainWindow.xaml` — All Czech UI labels: Výztuž expander, Krytí a okraje expander, Detaily expander, top bar, inline preview dock
- `../WallReinf/WallReinf/SettingsWindow.xaml` — All Settings sections and labels
- `../WallReinf/WallReinf/Preview/RebarPreviewWindow.xaml` — Standalone preview window labels
- `../WallReinf/WallReinf/Validation/RebarValidationWindow.xaml` — Validation window labels including legend
- `../WallReinf/WallReinf.Core/RebarParameters.cs` — Parameter names, defaults (StirrupThreshold=300, FlagThreshold=1500, MaxRebarLength=12000, etc.)
- `mkdocs.yml` — Confirmed extensions: admonition, pymdownx.details, pymdownx.superfences, pymdownx.tabbed, attr_list, md_in_html, glightbox
- `.planning/phases/03-user-guide-content/03-CONTEXT.md` — All locked decisions

### Secondary (MEDIUM confidence)
- `.planning/REQUIREMENTS.md` — Phase 3 requirements mapping
- `.planning/STATE.md` — Project decisions history (Phase 2 established ASCII filenames, no cross-links in stubs, --strict as quality gate)

---

## Metadata

**Confidence breakdown:**
- Canonical terminology: HIGH — verified directly from XAML source files
- MkDocs extensions available: HIGH — verified from mkdocs.yml
- Page content scope: HIGH — derived from CONTEXT.md locked decisions + XAML UI structure
- System requirements (pozadavky.md): LOW — not in XAML, requires separate investigation

**Research date:** 2026-03-26
**Valid until:** 2026-04-26 (stable domain — MkDocs Material and XAML labels unlikely to change)
