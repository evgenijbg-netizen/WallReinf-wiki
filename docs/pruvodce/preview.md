# Preview panel

Preview je pracovní plocha pro kontrolu návrhu výztuže před zápisem do modelu Tekla. Nejde jen o obrázek: umožňuje kontrolovat vrstvy, upravovat vybrané řady a pracovat s blokovacími zónami.

## Vrstvy a zobrazení

Samostatné okno **Preview výztuže** obsahuje panel vrstev výztuže a přepínače **Vše** a **Nic**. Zobrazuje také měřítko, ovládání přiblížení a stavový řádek s počtem prutů, délek a varování.

## Úpravy vybraných řad

Vybrané řady lze zkracovat nebo prodlužovat tlačítky **-50**, **-10**, **+10** a **+50** mm. K dispozici je i cílová délka a funkce **Sjednotit vybrané**.

Po úpravě délky použijte **Zkontrolovat kolize**. Před generováním ověřte varování v náhledu a zkontrolujte, že upravené pruty odpovídají požadovanému detailu.

## Heatmapa a filtr

Expander **Heatmapa (Ø × délka)** pomáhá najít skupiny prutů podle průměru a délky. Po použití filtru je k dispozici tlačítko **Zrušit filtr**.

!!! note "K OVĚŘENÍ"
    Přesný způsob výběru buněk heatmapy a rozsah skrytí ostatních prvků ověřte v běžící aplikaci. Popis proto neslibuje konkrétní chování kliknutí nad rámec použití filtru.

## Další interakce

V náhledu lze přes kontextovou nabídku pracovat s viditelností, pozicemi dělení a blokovacími zónami. Tyto úpravy patří do kontroly návrhu před tlačítkem **Generovat**.

!!! warning "K OVĚŘENÍ"
    Rozmístění ovládání v inline náhledu hlavního okna se může lišit od samostatného okna Preview. Před vytvořením konkrétního postupu nebo snímku obrazovky jej ověřte v aktuální aplikaci.

## Dokončení

- **Generovat** zapíše zkontrolovaný návrh do Tekla modelu.
- **Zrušit** zavře okno bez generování.

Po generování použijte [Validační okno](validace.md), které čte skutečnou výztuž z modelu.

## Viz také

- [Validační okno](validace.md)
- [Třmínky](trminky.md)
