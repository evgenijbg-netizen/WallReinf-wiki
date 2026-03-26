# Phase 3: User Guide Content - Context

**Gathered:** 2026-03-26
**Status:** Ready for planning

<domain>
## Phase Boundary

Write all 12 workflow-based guide pages (docs/pruvodce/) with full prose content, admonitions, version placeholders, UI-matching terminology, and screenshot placeholders. No reference content, no FAQ, no actual screenshots.

</domain>

<decisions>
## Implementation Decisions

### Writing Style
- **Stručný a přímý** — krátké věty, minimum úvodů, orientovaný na akci
- Formát: číslované kroky pro workflow, admonitions pro warningy/tipy
- Žádné "esejistické" úvody — rovnou k věci
- Cílová skupina: **zkušený uživatel Tekla Structures** — nepopisovat základy Tekly (co je model, assembly, jak vybrat prvek), jen funkce pluginu

### UI Element Formatting
- Názvy UI prvků **tučně česky**: **Generovat**, **Načíst**, **Výztuž**, **Orientace S1**
- Pro netextová tlačítka (ikony) ideálně replikovat ikonu ve wiki — kde to nejde, tučně popsat funkci: **Předchozí stěna (←)**
- Názvy sekcí UI rovněž tučně: **Krytí a okraje**, **Detaily**

### Terminology Source
- Autoritativní zdroj názvů: XAML labely pluginu (ne vlastní překlad)
- Klíčové termíny: Prostupy (ne Otvory), Lemování (U-čka), Rozteč, Třmínky, Prapory, Závlače, Šikmá výztuž v rozích
- S1 = vnější strana, S2 = vnitřní strana
- "Svislá (nosná)" / "Vodorovná (nosná)" pro orientaci

### Version Badge
- Formát: `[VERZE]` placeholder na každé stránce
- Bude doplněno konkrétní verzí pluginu později
- Implementace: admonition `!!! info "Verze pluginu: [VERZE]"` na začátku stránky

### Screenshot Placeholders
- Formát: standardní MkDocs image syntax s popisným alt textem
- Caption pod obrázkem obsahuje instrukce pro fázi 5 (co vyfotit, jaké nastavení)
- Pojmenování souborů: popis obsahu (`hlavni-dialog-vyztu.png`, `preview-panel-vrstvy.png`)
- Příklad:
  ```markdown
  ![Hlavní dialog — sekce Výztuž s nastavenými průměry](../assets/screenshots/hlavni-dialog-vyztu.png)

  *[VERZE] — Hlavní okno pluginu se sekcí Výztuž. Zachytit: průměry Ø10, rozteč 150mm, S1 i S2 viditelné.*
  ```

### Content Structure — pruvodce/parametry.md
- **Workflow-oriented** — vysvětluje JAK a KDY nastavit parametry
- Pokrývá **všechny 3 sekce UI podrobně**: Výztuž, Krytí a okraje, Detaily
- Sekce Detaily zahrnuje pokročilé funkce: T-spoj (navazující stěny), Volný konec stěny, Pokračuje výš (deska)
- Typické hodnoty a doporučení v kontextu (ne jen výčet polí)
- Žádné tabulky s default hodnotami a rozsahy — to je pro reference/parametry.md (fáze 4)

### Cross-Referencing Between Guide Pages
- Feature stránky (otvory, třmínky, diagonály) **odkazují** na pruvodce/parametry.md pro společné koncepty (S1/S2, orientace)
- Neopakovat vysvětlení konceptů na každé stránce
- Formát: `[Orientace S1](parametry.md#orientace-s1)` — interní linky v rámci průvodce

### Settings Window Coverage
- Settings okno **nemá vlastní stránku** — pokrýt kontextuálně na feature stránkách
- Prahy třmínků → stránka třmínků
- Filtry otvorů (ignorovat kapsy/výřezy) → stránka otvorů
- Segmentace rastru → stránka parametrů
- Výchozí hodnoty → stránka parametrů (zmínit že existují v Settings)
- Normy (poloha výztuže, tabulka přesahů) → stránka parametrů

### Peripheral Features
- **Poznámky ke stěně** (NoteWindow) → stručná sekce v zakladni-workflow.md
- **Heatmapa** (Ø × délka matice) → sekce v preview.md
- **Tabulka přesahů a kotevních délek** → zmínka v parametry.md u sekce Normy
- Každá dostane krátkou sekci, ne celou stránku

### Claude's Discretion
- Přesné pořadí sekcí na každé stránce
- Počet a umístění admonitions (minimálně tam, kde hrozí chyba)
- Počet screenshot placeholderů per stránka (dle potřeby workflow)
- Přesné formulace textů v rámci dohodnutého tónu a stylu
- Zda a jak použít `pymdownx.details` (sbalitelné sekce) pro méně důležité detaily

</decisions>

<canonical_refs>
## Canonical References

**Downstream agents MUST read these before planning or implementing.**

### Plugin Source (Terminology & UI Structure)
- `../WallReinf/WallReinf/MainWindow.xaml` — Hlavní dialog: české labely, sekce, parametry
- `../WallReinf/WallReinf/SettingsWindow.xaml` — Settings dialog: globální konfigurace
- `../WallReinf/WallReinf/Preview/RebarPreviewWindow.xaml` — Preview panel: vrstvy, heatmapa, úpravy délek
- `../WallReinf/WallReinf/Validation/RebarValidationWindow.xaml` — Validační okno: reality mode, export
- `../WallReinf/WallReinf.Core/RebarParameters.cs` — Všechny parametry: názvy, typy, defaults

### Existing Stub Files
- `docs/pruvodce/*.md` — 12 stub souborů s nadpisy a sekcemi (fáze 2 output)

### MkDocs Configuration
- `mkdocs.yml` — Nav config, enabled extensions, theme features

### Requirements
- `.planning/REQUIREMENTS.md` — START-01..04, GUIDE-01..07, UX-01..03

### Prior Phases
- `.planning/phases/01-infrastructure-and-deploy-pipeline/01-CONTEXT.md` — Site identity, logo
- `.planning/phases/02-navigation-skeleton/02-CONTEXT.md` — Page structure, file naming, stub pattern

</canonical_refs>

<code_context>
## Existing Code Insights

### Reusable Assets
- 12 stub files in `docs/pruvodce/` — each has H1, description, and H2 section headings already defined
- `mkdocs.yml` — Extensions ready: admonition, pymdownx.details, pymdownx.superfences, pymdownx.tabbed, attr_list, md_in_html
- Plugin source code in `../WallReinf/` — authoritative source for terminology and parameter names

### Established Patterns
- Czech prose in Markdown files, ASCII filenames (fáze 2)
- `mkdocs build --strict` as quality gate (zero warnings)
- Bold text for internal cross-references where targets exist within pruvodce/ section
- MkDocs Material admonitions: `!!! warning`, `!!! tip`, `!!! note`, `!!! info`

### Key Plugin UI Structure (for content mapping)
- **MainWindow** — 3 expandable sections: Výztuž, Krytí a okraje, Detaily
- **Top bar** — Wall selector, prefix filter, status filters (Hotovo/Ke kontrole/Bez výztuže)
- **Right column** — Live preview canvas, heatmap, layer groups
- **Settings** — Connection, Wall Loading, Segmentation, Stirrups/Flags, Openings, Defaults, Standards
- **Preview window** — Layer visibility, series adjustment (+/- délka), collision check, normalize
- **Validation window** — Reality mode from Tekla model, layer legend, Export PDF/PNG/Print

### Integration Points
- Cross-links within pruvodce/ section (parametry.md as hub for shared concepts)
- No cross-links to reference/ yet (that's Phase 4, UX-04)
- Screenshot paths will use `../assets/screenshots/` relative from pruvodce/

</code_context>

<specifics>
## Specific Ideas

- Ikony tlačítek by ideálně měly být replikovány ve wiki pro netextová tlačítka — pokud plugin používá ikonová tlačítka (šipky, zoom, oko), zvážit inline SVG nebo emoji alternativu
- Stránka zakladni-workflow.md by měla být "end-to-end demo" — provede uživatele celým procesem jedné stěny od výběru po generování, s cross-linky na detail na feature stránkách
- Stránka parametry.md bude nejdelší — pokrývá 3 UI sekce podrobně včetně pokročilých funkcí (T-spoj, volný konec)

</specifics>

<deferred>
## Deferred Ideas

None — discussion stayed within phase scope

</deferred>

---

*Phase: 03-user-guide-content*
*Context gathered: 2026-03-26*
