# Instalace a spuštění

!!! info "Verze pluginu: [VERZE]"
    Tato stránka popisuje chování pluginu verze [VERZE].

Tato stránka popisuje, jak nainstalovat plugin Wall Reinforcement Wizard do Tekla Structures a jak ho poprvé spustit.

## Instalace pluginu

Plugin se instaluje zkopírováním souborů do složky aplikací Tekla Structures.

1. Stáhněte archiv s pluginem (složka `WallReinforcementWizard`).
2. Zkopírujte celou složku do adresáře aplikací Tekla Structures:
   `C:\ProgramData\Trimble\Tekla Structures\[TEKLA_VERSION]\applications\`
3. Výsledná cesta ke spustitelnému souboru:
   `...\applications\WallReinforcementWizard\WallReinf.exe`

!!! note "Poznámka"
    Složka `applications` je sdílená pro všechny projekty v dané verzi Tekla. Plugin bude dostupný ve všech modelech.

![Složka aplikací Tekla](../assets/screenshots/instalace-slozka.png)

*[VERZE] — Souborová struktura složky applications. Zachytit: složka WallReinforcementWizard viditelná v průzkumníku, obsah složky s WallReinf.exe.*

## Spuštění pluginu

Plugin se spouští přímo z Tekla Structures přes panel Applications & Components.

1. Otevřete Tekla Structures a načtěte model.
2. Otevřete panel **Applications & Components** (klávesa `F5` nebo menu **Applications → Applications & Components**).
3. Do vyhledávacího pole zadejte `Wall Reinforcement`.
4. Dvakrát klikněte na **Wall Reinforcement Wizard** v seznamu výsledků.
5. Plugin se otevře jako samostatné okno.

!!! note "Poznámka"
    Tekla Structures musí být spuštěna s otevřeným modelem před spuštěním pluginu. Pokud model není načten, plugin se otevře, ale připojení k modelu bude nedostupné.

![Applications & Components panel s pluginem](../assets/screenshots/instalace-spusteni.png)

*[VERZE] — Tekla Structures Applications & Components panel. Zachytit: vyhledávací pole s textem "Wall Reinforcement", plugin viditelný v seznamu výsledků.*
