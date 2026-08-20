# Otvory

Plugin při načtení stěny pracuje s detekovanými otvory z modelu Tekla a podle jejich zpracování upravuje rastr přímé výztuže i doplňkovou výztuž u otvoru.

## Zpracování otvorů

Otvory mohou mít režim úplného přerušení, pouze oříznutí rastru nebo ignorování. Diagonální pruty se mohou vytvářet pro otvory s úplným přerušením i pro otvory, které rastr pouze ořezávají; ignorované otvory se nezpracovávají.

| Režim | Ověřené chování návrhu |
|---|---|
| **Úplné přerušení** | Přímý rastr se v oblasti otvoru přeruší; návrh může obsahovat lemování, pruty nad/pod otvorem, kotevní pruty a podle volby diagonály. |
| **Pouze oříznutí rastru** | Přímý rastr zůstává souvislý, ale návrh může přidat interakční pruty, lemování, kotevní pruty a diagonály. |
| **Ignorovat** | Otvor se do návrhu nezařadí; nevytváří se k němu ani diagonály. |

V okně **Nastavení** je doložena volba **Ignorovat všechny prostupy**. Pokud ji zapnete, plugin otvory do návrhu nezařadí.

!!! warning "K OVĚŘENÍ"
    Konkrétní rozlišení kapes, výřezů a dalších typů objektů závisí na geometrii a na běžící aplikaci. Nepovažujte je za samostatné přepínače, dokud je neověříte v aktuálním dialogu Nastavení.

## Lemování a diagonály

Průměr výztuže otvoru se nastavuje v hlavním dialogu. Lemování hran otvoru a jeho délky se řídí parametry návrhu; šikmá výztuž se zapíná samostatnou volbou. Diagonály popisuje stránka [Diagonální pruty](diagonaly.md).

U dveřního otvoru se nevytváří spodní U-prut otvoru. U běžného okenního otvoru se vytvářejí horní i dolní U-pruty. Roh otvoru, který leží na hraně stěny, nemá odpovídající diagonálu.

Více otvorů nad sebou se vyhodnocuje po sloupcích překryvu: doplňková výztuž nemá přetékat do sousedního sloupce jen proto, že je v jiné výšce další otvor. U takové geometrie vždy ověřte náhled i výsledek v modelu.

### Kruhové otvory

Rozpoznaný kruhový otvor se zpracovává odlišně od obdélníkového. Pro velký kruhový otvor může návrh vytvořit kruhové rodiny třmínků; nevytvářejí se pro něj kotevní pruty ani diagonály určené pro rohy obdélníkového otvoru.

!!! warning "K OVĚŘENÍ"
    Rozpoznání kruhového profilu i hranice, od níž se použije kruhové lemování, závisí na skutečné geometrii modelu. Před výrobním použitím ověřte výsledek na konkrétním objektu Tekla.

## Fiktivní zvětšení otvoru

V nastavení lze zadat fiktivní zvětšení otvoru ve vodorovném (H) a svislém (V) směru v rozsahu 0–200 mm. Tato hodnota rozšiřuje zónu, v níž se segmentuje přímá výztuž.

Fiktivní zvětšení nemění skutečnou geometrii otvoru. Kotevní tvary třmínků a praporů se ukotvují ke skutečným hranám otvoru, nikoli k jeho fiktivně zvětšenému obrysu.

## Otvor není fyzický výřez stěny

Koncový výřez, schod nebo lokální zúžení obrysu stěny není automaticky otvor. Takový prvek nevyvolává rodiny výztuže pro otvor ani diagonály kolem rohů otvoru. Kontrolu skutečného obrysu a jeho podporovaných tvarů popisuje [Geometrie a typy stěn](geometrie-a-typy-sten.md).

## Viz také

- [Hlavní parametry](parametry.md)
- [Třmínky](trminky.md)
- [Diagonální pruty](diagonaly.md)
- [Geometrie a typy stěn](geometrie-a-typy-sten.md)
