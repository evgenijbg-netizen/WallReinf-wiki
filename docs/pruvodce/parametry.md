# Hlavní parametry

Tato stránka popisuje parametry, které ovlivňují návrh výztuže stěny. Před generováním vždy zkontrolujte orientaci stěny, strany S1/S2 a okrajové podmínky v náhledu.

## S1 a S2

S1 a S2 jsou dva povrchy stěny. Jejich význam se řídí orientací stěny v modelu Tekla; pro kontrolu směru slouží startovní a koncový bod stěny. Volba vnější výztuže určuje, zda je vnější vrstva orientována svisle nebo vodorovně.

Průměry a rozteče svislé i vodorovné výztuže se nastavují pro obě strany samostatně. Krytí se také zadává samostatně pro S1 a S2 — nejde o jedinou společnou hodnotu krytí.

!!! tip "Doporučený postup"
    Nejprve ověřte S1/S2 a směr stěny, potom nastavte krytí, průměry, rozteče a odsazení rastru. Teprve následně kontrolujte náhled.

## Lemování a prostupy

Lemování určuje průměry výztuže hran stěny a otvorů. Jeho rozteč vychází ze základního rastru. Volba šikmé výztuže řídí generování diagonálních prutů u rohů otvorů; podrobnosti jsou v části [Diagonální pruty](diagonaly.md).

Parametry pro prostupy, včetně fiktivního zvětšení a zpracování otvorů, popisuje stránka [Otvory](otvory.md).

## Odsazení a okrajové podmínky

Odsazení určuje vzdálenost základního rastru od hran stěny. Okrajové podmínky určují, jak se výztuž na hraně ukončí nebo naváže:

- na každé boční hraně lze nezávisle vybrat rohové napojení, volnou hranu, T-spoj nebo prodloužení vodorovné výztuže;
- nahoře lze zvolit návaznost do desky, vytrnování do stěny nad ní nebo volnou hranu;
- dole lze ponechat původní výstup bez dolního lemování, zvolit volnou hranu nebo vytrnování z desky.

Podrobný význam voleb, parametry tloušťky a bezpečný postup popisují [Okrajové podmínky](okrajove-podminky.md).

## Výchozí hodnoty a nastavení

Okno **Nastavení** uchovává výchozí hodnoty používané při práci s novou stěnou. Patří sem mimo jiné prahy třmínků a praporů, fiktivní zvětšení otvorů a parametry závlačí.

### Rastry, navazující stěny a šikmé hrany

V **Nastavení** jsou také volby pro segmentaci rastru a dělení prutů. Volba **Generovat bez překryvu** ovlivňuje rozdělení rastru; její vhodnost proto ověřte na Preview a před zápisem v Tekla modelu.

Pro automatické rozpoznání boční návaznosti se ukládá tolerance navazující kolmé stěny. Změna tolerance může změnit, které okolní prvky aplikace vyhodnotí jako návaznost; není to náhrada ruční kontroly okrajových podmínek.

Pro podporovaný případ šikmé horní hrany určuje nastavení počet přímých prutů v jedné délkové skupině. Pruty v takové skupině se řídí nejdelší teoretickou délkou skupiny, aby bylo možné jejich případné zkrácení na stavbě. Rozsah podporovaných tvarů a vhodnou hodnotu pro konkrétní projekt ověřte v Preview a v Tekla modelu — jsou **K OVĚŘENÍ**.

### Třídy a číslování výztuže

Nastavení obsahuje vzor pro prefix číslování generované výztuže. Používá se při zápisu nových prutů do Tekla; konkrétní výsledné označení ověřte podle konvence projektu.

Přiřazení Tekla **Class** lze upravit souborem `rebar-classes.txt` v uživatelské složce WallReinf (`%AppData%/WallReinf`). Soubor se založí s šablonou při prvním použití. Úprava mění pouze třídy generované výztuže, nikoli její geometrii nebo názvy skupin.

!!! warning "Změny tříd"
    Neplatná nebo nedostupná konfigurace nesmí zastavit generování; aplikace použije výchozí přiřazení. Po úpravě souboru vždy vygenerujte a ověřte reprezentativní stěnu v Tekla modelu.

### Fiktivní zvětšení otvorů

Vodorovné a svislé zvětšení otvoru mají rozsah 0–200 mm. Používají se při segmentaci přímé výztuže; kotevní tvary třmínků a praporů se nadále vážou na skutečnou hranu otvoru.

### Třmínky a prapory

Prahy pro třmínky a prapory mají rozsah 0–2 500 mm. Výchozí hodnoty jsou 300 mm pro třmínek a 1 500 mm pro prapor. Aplikace udržuje práh třmínku nejvýše na úrovni prahu praporu.

Podrobnosti viz [Třmínky](trminky.md).

## Viz také

- [Otvory](otvory.md)
- [Třmínky](trminky.md)
- [Diagonální pruty](diagonaly.md)
- [Preview panel](preview.md)
- [Okrajové podmínky](okrajove-podminky.md)
