# WallReinf Wiki

## What This Is

Online wiki sloužící jako uživatelský manuál pro program Wall Reinforcement Wizard — C#/WPF plugin pro Tekla Structures, který automatizuje generování výztuže betonových stěn. Wiki je určená pro stavební inženýry a detailéry pracující v Tekle a bude hostovaná na GitHub Pages.

## Core Value

Uživatel najde srozumitelný návod, jak plugin používat — od spuštění přes nastavení parametrů až po generování a validaci výztuže.

## Requirements

### Validated

(None yet — ship to validate)

### Active

- [ ] Statická wiki postavená na MkDocs Material (nebo obdobném generátoru)
- [ ] Obsah v češtině
- [ ] Návod k použití — jak plugin spustit, připojit k Tekle, nastavit parametry, generovat výztuž
- [ ] Popis jednotlivých funkcí — otvory, U-pruty, třmínky, preview, validace, PDF export
- [ ] FAQ / Troubleshooting sekce — časté problémy a jejich řešení
- [ ] Klíčové screenshoty u důležitých kroků a dialogů
- [ ] Deploy na GitHub Pages

### Out of Scope

- Vývojářská/technická dokumentace — wiki je čistě uživatelská
- Tutoriály krok-za-krokem pro specifické scénáře — v1 pokrývá referenční popis a základní návod
- Vícejazyčná verze (angličtina) — pouze čeština
- Video návody — pouze text a screenshoty

## Context

- Zdrojový kód programu je v `../WallReinf/` (C#, .NET 4.8, WPF, Tekla Structures API 2025)
- Program má bohaté UI s množstvím parametrů (průměry prutů, krytí, rozteče, okrajové pruty, otvory, třmínky, diagonály...)
- UI používá Material Design In XAML Themes
- Program má preview panel pro vizualizaci plánované výztuže a validační okno
- Existující docs/ ve zdrojovém repozitáři obsahují architekturu a flow diagramy (interní, ne uživatelské)
- Primární uživatelé jsou česky mluvící stavební inženýři/detailéři

## Constraints

- **Tech stack**: Statický generátor (MkDocs Material) + GitHub Pages hosting
- **Jazyk**: Čeština
- **Závislost**: Screenshoty vyžadují běžící Tekla Structures s modelem — budou dodány uživatelem dodatečně
- **Repozitář**: Tento repozitář (WallReinf-wiki) je oddělený od zdrojového kódu programu

## Key Decisions

| Decision | Rationale | Outcome |
|----------|-----------|---------|
| MkDocs Material jako generátor | Nejrozšířenější pro technickou dokumentaci, nativní podpora Material designu, snadný deploy na GH Pages | — Pending |
| Oddělený repozitář pro wiki | Wiki je nezávislá na zdrojovém kódu, jednodušší deploy | — Pending |
| Čistě uživatelská dokumentace | Cílová skupina jsou koncoví uživatelé, ne vývojáři | — Pending |

---
*Last updated: 2026-03-25 after initialization*
