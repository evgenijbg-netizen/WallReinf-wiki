# Geometrie a typy stěn

WallReinf nevychází pouze z obdélníkového rozměru vybraného dílu. Při načtení může sestavit logickou stěnu z více dílů, pracovat s jejím skutečným obrysem a podle něj oříznout návrh i náhled. Proto vždy nejdříve ověřte, co aplikace do jedné stěny zahrnula.

## Složené stěny a výběr dílů

Jestliže je stěna tvořena více částmi stejného cast unitu, aplikace může použít jejich společnou geometrii jako jednu logickou stěnu. To je důležité například u stěn se schodem, lokálním výřezem nebo rozdílnou výškou jednotlivých částí.

V dialogu načítání je pro takový případ k dispozici výběr dílu cast unitu. Zvolte díl, který má být základem načtené stěny, a před generováním ověřte obrys v Preview a ve validačním okně.

!!! warning "K OVĚŘENÍ"
    Přesné názvy voleb a pravidla, podle nichž se v aktuální verzi nabídne výběr dílu, ověřte v běžící aplikaci. Nevybírejte člen cast unitu pouze podle názvu: rozhodující je zobrazený obrys a poloha otvorů.

Složená geometrie se nepoužije bez omezení. Neodpovídající materiál, tloušťka nebo mezera mezi díly mohou znamenat, že stěnu nelze bezpečně sestavit jako jednu logickou geometrii. V takovém případě výsledek neupravujte odhadem — načtěte vhodný díl samostatně nebo upravte model a znovu jej načtěte.

## Fyzický obrys a výřezy

Skutečný obrys rozlišuje zejména koncové výřezy, schody a lokální zúžení. Přímé pruty se ořezávají na fyzický rozsah stěny; doplňková výztuž u takového výřezu se řídí jeho geometrickou klasifikací, nikoli automaticky pravidly pro otvor.

To znamená, že fyzický výřez není totéž co otvor:

- výřez nevytváří rodiny výztuže určené pro otvor (například diagonály kolem otvoru);
- u úzkého zubu nebo krčku může návrh vytvořit lokální interakční výztuž podle nastavených prahů;
- překrývající se běžné krajní pruty se v takové zóně potlačí;
- nepodporovaný nebo nejednoznačný obrys musí zůstat diagnostikou, nikoli podkladem pro generování.

!!! warning "Kontrola je nutná"
    Zejména u nepravidelných contour plates zkontrolujte fyzický obrys v Preview, potom skutečnou výztuž po generování ve [Validačním okně](validace.md). Projektant musí posoudit, zda automaticky navržený detail odpovídá konstrukčnímu návrhu.

## Schod a šikmá horní hrana

Stěna se schodovou horní nebo dolní hranou může být načtena se skutečným stupňovitým obrysem. Rastr se pak neřídí jen největším obdélníkem stěny.

U podporované šikmé horní hrany se přímé pruty generují z pracovního polygonu a ořezávají se podle sklonu. Kvůli seskupení délek mohou některé pruty ovlivněné sklonem mít společnou teoretickou délku; ostatní pruty se nemají prodlužovat jen kvůli tomuto seskupení.

!!! note "K OVĚŘENÍ"
    Sklon, krytí a konkrétní seskupení délek ověřte na reprezentativní stěně. Pokud aplikace ohlásí nepodporovaný šikmý obrys nebo neplatné odsazení krytí, negenerujte výztuž, dokud geometrii neopravíte nebo nezvolíte podporovaný postup.

## Vertikální prvky

Pro prvek orientovaný ve svislé ose aplikace používá virtuální pracovní rámec. Díky němu se délka, náhled, validace a zápis výztuže odvozují z rozměrů skutečného průřezu namísto běžného vodorovného půdorysného rozměru.

U čtvercového profilu není orientace samotnou geometrií jednoznačně daná. Ověřte proto v náhledu strany S1/S2 a směr prutů před zápisem do modelu.

## Bezpečný postup

1. Načtěte stěnu podle [Připojení k modelu](pripojeni.md) a zkontrolujte, že je vybrán správný díl nebo cast unit.
2. Porovnejte v Preview fyzický obrys, výřezy, otvory a orientaci S1/S2 s modelem Tekla.
3. U složené, šikmé nebo vertikální stěny zkontrolujte první návrh ještě před generováním; neberte obdélníkový náhled jako náhradu skutečného obrysu.
4. Pokud se objeví diagnostika nepodporovaného obrysu, mezery nebo neslučitelných dílů, generování zastavte a opravte vstupní geometrii.
5. Po generování ověřte oříznutí a lokální detaily ve [Validačním okně](validace.md).

## Viz také

- [Připojení k modelu](pripojeni.md)
- [Otvory](otvory.md)
- [Preview panel](preview.md)
- [Validační okno](validace.md)
