# Požadavky

Tato stránka uvádí podmínky pro spuštění Wall Reinforcement Wizard a práci s Tekla modelem.

## Tekla Structures

Wall Reinforcement Wizard je 64bitová WPF aplikace pro Tekla Structures. Pro načítání stěn, generování výztuže a práci s modelem musí být Tekla Structures spuštěná s otevřeným modelem.

Použijte instalační balíček určený pro svou verzi Tekla Structures. Aktuální zdrojový projekt má výchozí cílení na Tekla Structures 2025.0 a podporuje sestavení balíčku také pro Tekla Structures 2026.0.

!!! warning "Pozor"
    Aplikace se bez aktivního Tekla modelu může otevřít, ale operace nad modelem nebudou dostupné.

## Operační systém

- 64bitový Windows
- 64bitová instalace Tekla Structures odpovídající instalačnímu balíčku

!!! note "K OVĚŘENÍ"
    Zdrojový projekt potvrzuje 64bitový cíl aplikace, ale neurčuje minimální podporovanou verzi Windows. Konkrétní minimální verzi proto zde neuvádíme.

## .NET Framework

Aplikace cílí na **.NET Framework 4.8**. Pokud se aplikace nespustí, ověřte instalaci .NET Frameworku ve Windows nebo se obraťte na správce IT.

## Viz také

- [Instalace a spuštění](instalace.md)
- [Připojení k modelu](pripojeni.md)
