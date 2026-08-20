# Audit dokumentace

Úplný audit wiki proběhl 20. srpna 2026 ve dvou průchodech nad aktuálním pracovním stromem programu Wall Reinforcement Wizard. Druhý průchod historicky porovnal zdrojový snapshot z 24. března 2026 (`25a8bc17`) s aktuálním stavem (`e0d5c637`) a ověřil nové uživatelské funkce také podle milníků a testů. Zdroj pravdy tvořil aktuální kód (včetně lokálních, dosud necommitnutých změn); chování vyžadující spuštěnou Teklu je ve wiki označené **K OVĚŘENÍ**.

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
| Licence a aktivace | Nová stránka | Aktivace při spuštění, běžné chyby a bezpečný postup podpory. |
| První spuštění a nápověda | Nová stránka | Onboarding galerie při prvním spuštění a opětovné otevření nápovědy. |
| Připojení k modelu | Upraveno | Režimy Prefix/Stěna, aktivní Tekla model a načtení výběru. |
| Geometrie a typy stěn | Nová stránka | Cast unit/dílec, složené, polygonální, šikmé a vertikální stěny. |
| Základní workflow | Přepsáno | Aktuální skupiny UI, bezpečný re-edit, pravidla stavů a modelové poznámky. |
| Re-edit | Nová stránka | Uložené nastavení, podmínky bezpečné opakované úpravy a blokace. |
| Převzetí zkopírované výztuže | Nová stránka | Souhlas, kontrola kategorií, výsledek převzetí a následná validace. |
| Optimalizace délek | Nová stránka | Filtry, návrhy, souhlas s cizí výztuží, částečné výsledky a opětovná kontrola. |
| Hlavní parametry | Přepsáno | Krytí S1/S2, orientace a odkaz na přepracované okrajové podmínky. |
| Okrajové podmínky | Nová stránka | Boční, horní a dolní režimy, automatická detekce a bezpečný postup. |
| Otvory | Upraveno | Aktuální zacházení s prostupy, fyzickými výřezy, inflací a diagonály. |
| Třmínky | Upraveno | Vzájemně hlídané prahy a reálné chování praporů. |
| Diagonální pruty | Upraveno | Skutečné podmínky generování, rohy a délka. |
| Preview panel | Přepsáno | Výběr řad, úpravy délek, filtry a blocker zones. |
| Validační okno | Přepsáno | Režimy Plochy/Pruty, skupiny, zoom a přesahy. |
| PDF export | Přepsáno | Hromadný export vybraných stěn, PNG a tisk. |
| Reference | Přepsáno | Bez zastaralých počtů sekcí; doplněné aktuální nastavení a okrajové podmínky. |
| FAQ | Přepsáno | Aktuální připojení, re-edit, licence, převzetí a optimalizace. |

## Otevřené položky

| Oblast | Co ověřit ve spuštěné aplikaci |
| --- | --- |
| Okrajové podmínky | Automatická detekce u složených/geometricky posunutých stěn a skutečné výsledky detailů v Tekla modelu. |
| Složitá geometrie | Složené, polygonální, šikmé a vertikální stěny zkontrolujte vždy v náhledu a validačním okně; zdroj definuje i diagnostické/odmítací stavy závislé na modelu. |
| Re-edit a převzetí | Před zápisem ověřte stavové zprávy a po akci proveďte validaci; konkrétní výsledek závisí na existující výztuži v modelu. |
| Distribuce | Kanonický instalační balíček pro dané vydání a minimální podporovaná verze Windows. |
| Screenshoty | Pořídit nové snímky aktuálního UI před jejich vrácením do návodů. |
