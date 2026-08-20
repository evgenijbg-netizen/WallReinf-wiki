# Okrajové podmínky

Expander **Okrajové podmínky** určuje nezávisle levý, pravý, horní a dolní okraj stěny. V jednom směru je vždy aktivní právě jedna volba. Změna obnoví náhled výztuže; před generováním proto výsledek zkontrolujte v [Preview panelu](preview.md).

!!! warning "Předpoklad správné orientace"
    Levá a pravá strana vycházejí ze směru stěny v modelu. Nejdříve ověřte startovní a koncový bod stěny a strany S1/S2. Jinak můžete vybraný detail použít na opačném konci stěny.

## Automaticky a detekce kontextu

Volba **Automaticky** používá okolní konstrukce pro návrh horní návaznosti. Tlačítko **Detect boundary context** znovu načte kontext hran. Automatické vytrnování se použije jen tehdy, když detekce najde vhodnou navazující horní stěnu; mezery a nevhodné části nad stěnou se do návrhu promítají jako blokovací zóny.

Manuální změna boční volby se zachovává jako ruční nastavení. Manuální přepnutí horní volby rovněž potlačí automatiku pro aktuální stěnu, s výjimkou návratu k automaticky doporučenému vytrnování.

!!! warning "K OVĚŘENÍ"
    Automatická detekce je pomůcka, nikoli náhrada kontroly konstrukčního detailu. Před generováním ověřte v náhledu skutečně rozpoznané návaznosti, zejména u složených stěn, otvorů nebo geometricky posunutých objektů.

## Boční hrany

Každá boční strana má stejnou sadu čtyř voleb.

| Volba | Účinek |
|---|---|
| **Rohové napojení** | Zkrátí přímé vodorovné pruty a protáhne krajní U-pruty do připojené stěny podle zadané tloušťky. |
| **Volná hrana** | Přidá dva svislé lemovací pruty. |
| **T-spoj** | Protáhne lemovací prvky do sousední stěny a přidá čtyři automaticky rozmístěné svislé závlače. |
| **Vodorovné H** | Nahradí zakončení na zvolené straně prodloužením vodorovných prutů; délka je přesah plus levá nebo pravá korekce. |

Pod volbami je pole tloušťky/korekce. U rohového napojení a T-spoje představuje tloušťku navazující stěny. U **Vodorovné H** je pole korekcí přesahu; aplikace nepřipustí záporný součet délky přesahu a korekce.

Při automatické detekci kolmé stěny se výsledek použije jen pro dostatečně jednoznačnou a blízkou navazující konstrukci. Kandidát mimo toleranci nebo nejednoznačný kontext nemá být nahrazen domněnkou. V takovém případě zvolte boční podmínku ručně a ověřte náhled.

!!! note "Omezení voleb"
    Volná hrana a Vodorovné H jsou odlišné režimy. Jejich závlače a zakončení se nekombinují; zvolením Vodorovné H se nepoužije režim volné hrany se závlačemi.

## Horní hrana

| Volba | Účinek |
|---|---|
| **T-spoj do desky** | Protáhne lemovací U-pruty, prapory nebo třmínky do desky o zadanou tloušťku. |
| **Vytrnování** | Zruší horní lemování a nechá svislou výztuž pokračovat do stěny o patro výše. |
| **Volná hrana** | Přidá dva vodorovné lemovací pruty. |

Pole **Tl. desky** je aktivní pro T-spoj do desky i vytrnování. T-spoj do desky a vytrnování jsou vzájemně výlučné; při obou režimech se nevytváří zakončení určené pro volný horní roh.

!!! warning "K OVĚŘENÍ"
    Zdroje potvrzují, že vytrnování pracuje s nalezenou stěnou nad aktuální stěnou a s blokovacími zónami. Správnost konkrétní délky, kotvení a návaznosti musí projektant ověřit v modelu a podle platného detailu.

## Dolní hrana

| Volba | Účinek |
|---|---|
| **Nic** | Zachová původní výstup bez dodatečné výztuže dolní hrany. |
| **Volná hrana** | Přidá dolní lemovací U-pruty uvnitř fyzického rozsahu stěny; neprorůstají pod stěnu. |
| **Vytrnování z desky** | Vytvoří dolní U-pruty prodloužené dolů o zadanou délku. Nevytváří závlače. |

Pole **Prodloužení** je dostupné jen pro vytrnování z desky. Vyžaduje nezáporné celé číslo v milimetrech; výchozí hodnota v dialogu je 200 mm.

Při vytrnování z desky mohou být dolní pruty směrovány na rozpoznaný spodní podporující prvek. Pokud nelze podporu bezpečně určit, zkontrolujte výstup v Tekla modelu před jeho použitím.

Při změně mezi **Volnou hranou** a **Vytrnováním z desky** aplikace smí nahradit pouze ověřenou, jí vlastněnou rodinu dolní výztuže. Pokud narazí na cizí, ručně změněný nebo nejednoznačně rozpoznaný prut, bezpečný postup je generování zastavit a výsledek vyřešit po kontrole modelu.

## Bezpečný pracovní postup

1. Načtěte stěnu a ověřte její orientaci, fyzický obrys a strany S1/S2; u složené nebo nepravidelné stěny použijte také [Geometrii a typy stěn](geometrie-a-typy-sten.md).
2. Pokud používáte automatiku, spusťte detekci kontextu a prohlédněte náhled. Nejednoznačný výsledek nahraďte ruční volbou, ne odhadem.
3. Pro každou boční, horní a dolní hranu vyberte jeden režim podle skutečné návaznosti konstrukce.
4. Zadejte tloušťku navazující stěny, tloušťku desky, korekci nebo prodloužení pouze pro režim, který danou hodnotu používá.
5. Zkontrolujte vrstvy, délky, blokovací zóny a varování v Preview. U otvoru, výřezu nebo šikmého obrysu ověřte, že detail patří ke správné fyzické hraně.
6. Pokud aplikace blokuje nahrazení dříve vytvořené výztuže, nepokračujte odstraněním neznámých prutů. Nejprve určete jejich původ a zkontrolujte model.
7. Po generování ověřte skutečnou výztuž ve [Validačním okně](validace.md).

## Viz také

- [Hlavní parametry](parametry.md)
- [Preview panel](preview.md)
- [Validační okno](validace.md)
- [Geometrie a typy stěn](geometrie-a-typy-sten.md)
