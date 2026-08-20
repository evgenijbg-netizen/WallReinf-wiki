# Otvory

Plugin při načtení stěny pracuje s detekovanými otvory z modelu Tekla a podle jejich zpracování upravuje rastr přímé výztuže i doplňkovou výztuž u otvoru.

## Zpracování otvorů

Otvory mohou mít režim úplného přerušení, pouze oříznutí rastru nebo ignorování. Diagonální pruty se mohou vytvářet pro otvory s úplným přerušením i pro otvory, které rastr pouze ořezávají; ignorované otvory se nezpracovávají.

V okně **Nastavení** je doložena volba **Ignorovat všechny prostupy**. Pokud ji zapnete, plugin otvory do návrhu nezařadí.

!!! warning "K OVĚŘENÍ"
    Konkrétní rozlišení kapes, výřezů a dalších typů objektů závisí na geometrii a na běžící aplikaci. Nepovažujte je za samostatné přepínače, dokud je neověříte v aktuálním dialogu Nastavení.

## Lemování a diagonály

Průměr výztuže otvoru se nastavuje v hlavním dialogu. Lemování hran otvoru a jeho délky se řídí parametry návrhu; šikmá výztuž se zapíná samostatnou volbou. Diagonály popisuje stránka [Diagonální pruty](diagonaly.md).

## Fiktivní zvětšení otvoru

V nastavení lze zadat fiktivní zvětšení otvoru ve vodorovném (H) a svislém (V) směru v rozsahu 0–200 mm. Tato hodnota rozšiřuje zónu, v níž se segmentuje přímá výztuž.

Fiktivní zvětšení nemění skutečnou geometrii otvoru. Kotevní tvary třmínků a praporů se ukotvují ke skutečným hranám otvoru, nikoli k jeho fiktivně zvětšenému obrysu.

## Viz také

- [Hlavní parametry](parametry.md)
- [Třmínky](trminky.md)
- [Diagonální pruty](diagonaly.md)
