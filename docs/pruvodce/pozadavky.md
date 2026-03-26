# Požadavky

!!! info "Verze pluginu: [VERZE]"
    Tato stránka popisuje chování pluginu verze [VERZE].

Tato stránka uvádí, co musí být nainstalováno a spuštěno před použitím pluginu Wall Reinforcement Wizard.

## Tekla Structures

Plugin je rozšíření (WPF aplikace) pro Tekla Structures. Před spuštěním pluginu musí být Tekla Structures spuštěna s otevřeným modelem.

- Minimální verze: **Tekla Structures 2025** (plugin využívá Tekla Open API 2025)
- Plugin komunikuje s Tekla přes gRPC — model musí být aktivní a přístupný

!!! warning "Pozor"
    Plugin nelze spustit bez otevřeného modelu v Tekla Structures. Pokud model není otevřen, připojení selže.

![Verze Tekla Structures](../assets/screenshots/pozadavky-tekla-verze.png)

*[VERZE] — Informace o verzích. Zachytit: About dialog Tekla Structures s verzí (Help → About Tekla Structures).*

## Operační systém

- **Windows 10** nebo novější (64-bit)
- 64-bit OS je vyžadováno — Tekla Structures i plugin jsou 64-bitové aplikace

## .NET Framework

Plugin vyžaduje **.NET Framework 4.8**.

.NET Framework 4.8 je součástí Windows 10 (aktualizace od roku 2019) a Windows 11. Na starších sestavách Windows 10 může být nutná ruční instalace.

!!! warning "Pozor"
    Plugin vyžaduje přesně .NET Framework 4.8. Starší verze způsobí chybu při spuštění. Verze lze ověřit v Ovládacích panelech → Programy → Zapnout nebo vypnout funkce systému Windows.
