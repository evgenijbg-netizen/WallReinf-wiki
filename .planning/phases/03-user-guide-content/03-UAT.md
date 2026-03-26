---
status: complete
phase: 03-user-guide-content
source: 03-01-SUMMARY.md, 03-02-SUMMARY.md, 03-03-SUMMARY.md, 03-04-SUMMARY.md
started: 2026-03-26T14:00:00Z
updated: 2026-03-26T14:10:00Z
---

## Current Test

[testing complete]

## Tests

### 1. MkDocs build --strict
expected: Spuštění `python -m mkdocs build --strict` proběhne bez chyb a bez varování. Exit code 0.
result: pass

### 2. Stránka pozadavky.md
expected: Stránka docs/pruvodce/pozadavky.md obsahuje systémové požadavky: Tekla Structures 2025, Windows 10 64-bit, .NET Framework 4.8. Na začátku stránky je version badge admonition. Text je v češtině s tučnými názvy UI prvků.
result: pass

### 3. Stránka instalace.md
expected: Stránka docs/pruvodce/instalace.md obsahuje krok-za-krokem postup instalace (kopírování do složky applications) a první spuštění přes Applications & Components panel. Má screenshot placeholdery a admonitions.
result: pass

### 4. Stránka pripojeni.md
expected: Stránka docs/pruvodce/pripojeni.md pokrývá ověření připojení (Settings dialog), načtení stěn (Prefix pole), navigaci mezi stěnami (předchozí/další/výběr z Tekly) a stavy stěn (Hotovo/Ke kontrole/Bez výztuže). Cross-link na zakladni-workflow.md.
result: pass

### 5. Stránka zakladni-workflow.md
expected: Stránka docs/pruvodce/zakladni-workflow.md obsahuje end-to-end walkthrough od výběru stěny přes nastavení parametrů po generování výztuže. Cross-linky na pripojeni.md, parametry.md a feature stránky. 4 screenshot placeholdery.
result: pass

### 6. Stránka parametry.md
expected: Stránka docs/pruvodce/parametry.md je hub pro všechny 3 MainWindow expandery (Výztuž, Krytí a okraje, Detaily) + Settings (Výchozí hodnoty, Segmentace rastru, Dělení prutu, Normy). Obsahuje T-spoj dependency warning admonition. ~151 řádků.
result: pass

### 7. Stránka otvory.md
expected: Stránka docs/pruvodce/otvory.md pokrývá typy otvorů (dveřní/okenní, kapsy, výřezy), Prostupy sekci v hlavním dialogu, lemovací U-pruty s dependency warning, Settings Prostupy (Ignorovat kapsy/výřezy/všechny), Generace otvorů a Fiktivní zvětšení. ~82 řádků.
result: pass

### 8. Stránka trminky.md
expected: Stránka docs/pruvodce/trminky.md vysvětluje třmínky (closed loops) vs. prapory (L-shaped, Class 9), prahové hodnoty (300mm/1500mm z RebarParameters.cs), Třmínky nad dveřmi CheckBox, warning o invertovaných prazích. Cross-link na parametry.md#segmentace-rastru.
result: pass

### 9. Stránka diagonaly.md
expected: Stránka docs/pruvodce/diagonaly.md popisuje Šikmá výztuž v rozích CheckBox, umístění ve všech 4 rozích (S1 i S2), průměr sdílený s U-pruty. Collapsible note o Fiktivním zvětšení. ~42 řádků.
result: pass

### 10. Stránka preview.md
expected: Stránka docs/pruvodce/preview.md pokrývá inline dock (Vrstvy, Heatmapa, Úpravy délek, Kolize, Sjednotit) i standalone Preview výztuže okno. Heatmapa sekce (Ø × délka matice). Cross-link na parametry.md. ~98 řádků.
result: pass

### 11. Stránka validace.md
expected: Stránka docs/pruvodce/validace.md popisuje Grafická validace výztuže okno, Skutečná výztuž z Tekla modelu režim, legendu vrstev se všemi 6 Tekla class čísly (3/6/7/8/9/11), Průhlednost slider. !!! note admonition rozlišující validaci od preview. ~65 řádků.
result: pass

### 12. Stránka pdf-export.md
expected: Stránka docs/pruvodce/pdf-export.md pokrývá Export PDF / Export PNG / Tisk workflow z validačního okna. Tip o viditelnosti vrstev před exportem. Srovnávací tabulka formátů (PDF/PNG/Tisk). Cross-linky na validace.md. ~47 řádků.
result: pass

### 13. Cross-linky mezi stránkami
expected: Všechny cross-linky mezi stránkami (např. pripojeni→zakladni-workflow, parametry→otvory/trminky/diagonaly, pdf-export→validace) jsou funkční — cílové soubory existují a anchory odpovídají skutečným nadpisům.
result: pass

### 14. Screenshot placeholdery
expected: Všechny screenshot soubory referencované v markdown stránkách existují jako placeholder PNG soubory v docs/assets/screenshots/. Žádný chybějící obrázek.
result: pass

## Summary

total: 14
passed: 14
issues: 0
pending: 0
skipped: 0

## Gaps

[none yet]
