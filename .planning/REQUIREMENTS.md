# Requirements: WallReinf Wiki

**Defined:** 2026-03-25
**Core Value:** Uživatel najde srozumitelný návod, jak plugin používat — od spuštění přes nastavení parametrů až po generování a validaci výztuže.

## v1 Requirements

### Infrastruktura

- [x] **INFRA-01**: Site je postaven na MkDocs Material 9.7.6 s pinovanými závislostmi (mkdocs==1.6.1, mkdocs-material==9.7.6) v requirements.txt
- [x] **INFRA-02**: Site je automaticky deployován na GitHub Pages přes GitHub Actions CI při push na main
- [x] **INFRA-03**: Fulltext vyhledávání funguje s českou jazykovou podporou (lang: cs)
- [x] **INFRA-04**: Site podporuje přepínání light/dark mode
- [x] **INFRA-05**: mkdocs.yml má správně nastavené site_url pro GitHub Pages
- [x] **INFRA-06**: .gitignore vylučuje site/ adresář
- [x] **INFRA-07**: GitHub Actions workflow má permissions: contents: write

### Navigace

- [x] **NAV-01**: Site má explicitní nav: konfiguraci v mkdocs.yml (ne auto-discovery)
- [x] **NAV-02**: Navigace je rozdělena na dvě sekce: Průvodce (task-based) a Reference
- [x] **NAV-03**: Sidebar navigace zobrazuje všechny sekce a podsekce
- [x] **NAV-04**: Každá stránka má on-page TOC (table of contents)
- [x] **NAV-05**: Breadcrumbs jsou viditelné na každé stránce
- [x] **NAV-06**: Soubory používají ASCII slugy (žádné české znaky v názvech souborů)

### Obsah — Začínáme

- [ ] **START-01**: Stránka popisuje požadavky (Tekla Structures verze, .NET, OS)
- [ ] **START-02**: Stránka popisuje instalaci/spuštění pluginu
- [ ] **START-03**: Stránka popisuje připojení k modelu v Tekle
- [ ] **START-04**: Stránka popisuje základní workflow (výběr stěny → nastavení → generování)

### Obsah — Průvodce funkcemi

- [ ] **GUIDE-01**: Stránka pro hlavní parametry (průměry prutů, krytí, rozteče, okrajové pruty)
- [ ] **GUIDE-02**: Stránka pro otvory (detekce, nastavení, U-pruty kolem otvorů)
- [ ] **GUIDE-03**: Stránka pro třmínky a interakce segmentů
- [ ] **GUIDE-04**: Stránka pro diagonální pruty
- [ ] **GUIDE-05**: Stránka pro preview panel (vizualizace plánované výztuže)
- [ ] **GUIDE-06**: Stránka pro validační okno
- [ ] **GUIDE-07**: Stránka pro PDF export

### Obsah — Reference

- [ ] **REF-01**: Tabulka parametrů s názvy odpovídajícími UI pluginu
- [ ] **REF-02**: Každý parametr má popis, výchozí hodnotu a platný rozsah
- [ ] **REF-03**: Parametry jsou seskupeny podle sekcí UI (stejně jako v pluginu)

### Obsah — FAQ

- [ ] **FAQ-01**: Minimálně 10 známých problémů s řešením
- [ ] **FAQ-02**: FAQ obsahuje problémy s připojením k Tekle
- [ ] **FAQ-03**: FAQ obsahuje problémy s generováním výztuže
- [ ] **FAQ-04**: FAQ obsahuje problémy s validací

### Screenshoty

- [ ] **IMG-01**: Screenshot hlavního dialogu pluginu
- [ ] **IMG-02**: Screenshot preview panelu
- [ ] **IMG-03**: Screenshot validačního okna
- [ ] **IMG-04**: Screenshoty u klíčových kroků v Průvodci
- [ ] **IMG-05**: Screenshoty mají deskriptivní názvy souborů (ne screenshot01.png)
- [ ] **IMG-06**: Screenshoty mají v popisku verzi pluginu

### Styl a UX

- [ ] **UX-01**: Admonitions (warning, tip, note) jsou použity u důležitých upozornění
- [ ] **UX-02**: Na každé stránce je badge/admonition s verzí pluginu
- [ ] **UX-03**: Terminologie v wiki odpovídá labelům v UI pluginu
- [ ] **UX-04**: Stránky obsahují křížové odkazy mezi průvodcem a referencí

## v2 Requirements

### Vylepšení

- **V2-01**: Anotované screenshoty s číslovanými callouts
- **V2-02**: Content tabs pro variantní workflow (s otvory / bez otvorů)
- **V2-03**: "Edit this page" odkaz na GitHub
- **V2-04**: Zvýraznění výsledků vyhledávání (search.highlight)
- **V2-05**: Lightbox pro zvětšení screenshotů (mkdocs-glightbox)

### Budoucnost

- **V2-06**: Anglická verze (pouze pokud plugin dostane anglické UI)
- **V2-07**: Verzované docs přes mike plugin (pouze pokud existuje více verzí pluginu současně)

## Out of Scope

| Feature | Reason |
|---------|--------|
| Komentáře/feedback systém | Malá známá skupina uživatelů — stačí email/GitHub Issues |
| Video tutoriály | Vysoké náklady na tvorbu a údržbu; screenshoty + text stačí |
| AI chatbot / LLM Q&A | Fulltext search stačí pro tuto velikost audience |
| Interaktivní kalkulátor parametrů | Plugin sám slouží tomuto účelu |
| Vývojářská dokumentace | Wiki je čistě uživatelská; dev docs zůstávají v source repo |
| OAuth / uživatelské účty | Statický site bez backendu; dokumentace je veřejná |

## Traceability

| Requirement | Phase | Status |
|-------------|-------|--------|
| INFRA-01 | Phase 1 | Complete |
| INFRA-02 | Phase 1 | Complete |
| INFRA-03 | Phase 1 | Complete |
| INFRA-04 | Phase 1 | Complete |
| INFRA-05 | Phase 1 | Complete |
| INFRA-06 | Phase 1 | Complete |
| INFRA-07 | Phase 1 | Complete |
| NAV-01 | Phase 2 | Complete |
| NAV-02 | Phase 2 | Complete |
| NAV-03 | Phase 2 | Complete |
| NAV-04 | Phase 2 | Complete |
| NAV-05 | Phase 2 | Complete |
| NAV-06 | Phase 2 | Complete |
| START-01 | Phase 3 | Pending |
| START-02 | Phase 3 | Pending |
| START-03 | Phase 3 | Pending |
| START-04 | Phase 3 | Pending |
| GUIDE-01 | Phase 3 | Pending |
| GUIDE-02 | Phase 3 | Pending |
| GUIDE-03 | Phase 3 | Pending |
| GUIDE-04 | Phase 3 | Pending |
| GUIDE-05 | Phase 3 | Pending |
| GUIDE-06 | Phase 3 | Pending |
| GUIDE-07 | Phase 3 | Pending |
| REF-01 | Phase 4 | Pending |
| REF-02 | Phase 4 | Pending |
| REF-03 | Phase 4 | Pending |
| FAQ-01 | Phase 4 | Pending |
| FAQ-02 | Phase 4 | Pending |
| FAQ-03 | Phase 4 | Pending |
| FAQ-04 | Phase 4 | Pending |
| IMG-01 | Phase 5 | Pending |
| IMG-02 | Phase 5 | Pending |
| IMG-03 | Phase 5 | Pending |
| IMG-04 | Phase 5 | Pending |
| IMG-05 | Phase 5 | Pending |
| IMG-06 | Phase 5 | Pending |
| UX-01 | Phase 3 | Pending |
| UX-02 | Phase 3 | Pending |
| UX-03 | Phase 3 | Pending |
| UX-04 | Phase 4 | Pending |

**Coverage:**
- v1 requirements: 41 total
- Mapped to phases: 41
- Unmapped: 0 ✓

---
*Requirements defined: 2026-03-25*
*Last updated: 2026-03-25 after initial definition*
