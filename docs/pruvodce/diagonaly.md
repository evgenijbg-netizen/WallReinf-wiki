# Diagonální pruty

Šikmá výztuž doplňuje rohy zpracovávaných otvorů. Aktivuje ji volba šikmé výztuže v hlavním dialogu.

## Chování

Diagonály se vytvářejí pod úhlem 45° a jsou navrženy pro obě strany stěny, S1 i S2. Platí pro otvory s úplným přerušením i pro otvory, které pouze ořezávají rastr; ignorované otvory diagonály nemají.

Ne každý otvor musí mít čtyři diagonály. Roh, který leží na hraně stěny, se při generování vynechává.

Diagonály náleží k otevřením zpracovaným jako úplné přerušení i jako pouze oříznutí rastru. Pro ignorovaný otvor se nevytvářejí. Kruhový otvor nemá rohy, proto se pro něj nepoužívají diagonály určené pro rohy obdélníkového otvoru.

U více otvorů nad sebou kontrolujte, zda diagonály a lemování patří ke správnému otvoru. Návrh nesmí vyvozovat diagonálu pouze z blízkosti jiného otvoru v sousedním sloupci.

## Délka a poloha

Délka diagonálního prutu se odvozuje z kotevní délky: vypočítá se jako dvojnásobek kotevní délky a zaokrouhlí se nahoru na 50 mm. Prut se umísťuje u rohu otvoru s odsazením od otvoru.

!!! note "K OVĚŘENÍ"
    Průměr diagonály je součástí vstupních parametrů návrhu otvoru. Jeho přesné uživatelské označení v hlavním dialogu ověřte v běžící aplikaci před vytvořením návodu se snímky obrazovky.

## Kontrola před generováním

1. V [Preview panelu](preview.md) zkontrolujte rohy, které skutečně patří otvoru, a ověřte strany S1/S2.
2. U otvoru na hraně stěny počítejte s vynecháním diagonály v dotčeném rohu.
3. U kruhového nebo nepravidelného otvoru neodvozujte výsledek z pravidel pro obdélník; ověřte jej v modelu.
4. Po generování zkontrolujte skutečné pruty ve [Validačním okně](validace.md).

## Viz také

- [Otvory](otvory.md)
- [Hlavní parametry](parametry.md)
- [Preview panel](preview.md)
- [Validační okno](validace.md)
