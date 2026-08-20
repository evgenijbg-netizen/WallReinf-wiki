# Audit dokumentace

Úplný audit wiki proběhl 20. srpna 2026 nad aktuálním pracovním stromem programu Wall Reinforcement Wizard. Zdroj pravdy tvořil aktuální kód (včetně lokálních, dosud necommitnutých změn); chování vyžadující spuštěnou Teklu je ve wiki označené **K OVĚŘENÍ**.

## Pravidla ověřování

- Každé uživatelské tvrzení musí být doložené kódem nebo ověřené ve spuštěné aplikaci.
- Neověřený obsah se neprezentuje jako fakt: nese značku **K OVĚŘENÍ** nebo se z návodu odstraní.
- Staré screenshoty se nepoužívají jako potvrzení současného UI. Nejsou smazané, ale žádná aktualizovaná stránka na ně neodkazuje.

## Přehled stránek

| Stránka | Stav | Důkaz / poznámka |
| --- | --- | --- |
| Domů | Upraveno | Aktuální rozsah produktu: licence, re-edit, převzetí zkopírované výztuže a optimalizace délek. |
| Průvodce | Upraveno | Současný tok načtení, generace, validace a vestavěné nápovědy. |
| Požadavky | Přepsáno | .NET Framework 4.8, x64 a samostatné balíčky Tekla 2025.0/2026.0. |
| Instalace | Přepsáno | Inno Setup do Tekla extensions, nikoli Applications & Components. |
| Připojení k modelu | Upraveno | Režimy Prefix/Stěna, aktivní Tekla model a načtení výběru. |
| Základní workflow | Přepsáno | Aktuální skupiny UI, bezpečný re-edit, pravidla stavů a modelové poznámky. |
| Hlavní parametry | Přepsáno | Krytí S1/S2, orientace a odkaz na přepracované okrajové podmínky. |
| Okrajové podmínky | Nová stránka | Boční, horní a dolní režimy, automatická detekce a bezpečný postup. |
| Otvory | Upraveno | Aktuální zacházení s prostupy, inflace a diagonály. |
| Třmínky | Upraveno | Vzájemně hlídané prahy a reálné chování praporů. |
| Diagonální pruty | Upraveno | Skutečné podmínky generování, rohy a délka. |
| Preview panel | Přepsáno | Výběr řad, úpravy délek, filtry a blocker zones. |
| Validační okno | Přepsáno | Režimy Plochy/Pruty, skupiny, zoom a přesahy. |
| PDF export | Přepsáno | Hromadný export vybraných stěn, PNG a tisk. |
| Reference | Přepsáno | Bez zastaralých počtů sekcí a starých bloků parametrů. |
| FAQ | Přepsáno | Aktuální připojení, re-edit, licence, převzetí a optimalizace. |

## Otevřené položky

| Oblast | Co ověřit ve spuštěné aplikaci |
| --- | --- |
| Okrajové podmínky | Automatická detekce u složených/geometricky posunutých stěn a skutečné výsledky detailů v Tekla modelu. |
| Distribuce | Kanonický instalační balíček pro dané vydání a minimální podporovaná verze Windows. |
| Screenshoty | Pořídit nové snímky aktuálního UI před jejich vrácením do návodů. |
