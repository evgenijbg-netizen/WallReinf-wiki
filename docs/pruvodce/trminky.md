# Třmínky a prapory

Plugin klasifikuje krátké segmenty výztuže jako třmínky nebo prapory podle jejich délky a nastavených prahů.

## Prahy

V okně **Nastavení** jsou dva slidery v rozsahu 0–2 500 mm:

- **Třmínek:** segment dlouhý nejvýše nastavený práh dostane třmínek.
- **Prapor:** delší segment až do tohoto prahu dostane prapor.

Výchozí práh třmínku je 300 mm a výchozí práh praporu 1 500 mm. Aplikace synchronizuje hodnoty tak, aby práh třmínku nemohl být vyšší než práh praporu.

Pokud prapor nelze vytvořit s potřebným přesahem, může plugin použít třmínek jako náhradní řešení. Po generování proto zkontrolujte hlášení a náhled.

## Třmínky nad dveřmi

Při sestavení parametrů návrhu je generování třmínků nad dveřmi zapnuté.

!!! warning "K OVĚŘENÍ"
    V aktuálním zdroji není pro tuto volbu doložen samostatný ovládací prvek hlavního dialogu. Dokumentace proto neuvádí postup, jak ji uživatelsky vypnout; ověřte jej v běžící aplikaci.

## Vztah k otvorům

Segmenty vznikají zejména u otvorů a hran stěny. Fiktivní zvětšení otvoru ovlivní segmentaci přímé výztuže, ale kotevní tvar třmínku nebo praporu se vztahuje ke skutečným hranám otvoru.

## Viz také

- [Otvory](otvory.md)
- [Hlavní parametry](parametry.md)
- [Preview panel](preview.md)
