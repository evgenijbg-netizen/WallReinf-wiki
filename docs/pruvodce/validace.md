# Validační okno

Okno **Grafická validace výztuže** kontroluje skutečnou výztuž načtenou z Tekla modelu. Na rozdíl od [Preview panelu](preview.md) nezobrazuje pouze plán před generováním.

## Otevření a obnovení

Po vygenerování otevřete validaci z hlavního okna. Tlačítko **Obnovit** znovu načte data z Tekla modelu; použijte je po změně modelu nebo po dalším generování.

Pokud okno hlásí, že v modelu není žádná výztuž, nejprve výztuž vygenerujte a pak data obnovte.

## Režimy a navigace

Validační okno nabízí režimy **Plochy** a **Pruty**, ovládání přiblížení a indikaci, zda jsou zobrazeny přesahy mimo stěnu. V pravé části jsou **Skupiny výztuže**, které lze hromadně zobrazit nebo skrýt; průhlednost upravuje samostatný posuvník.

Legenda pracuje se skupinami **Svislá**, **Vodorovná**, **Hrany a vazby**, **Otvory** a **Třmínky placeholder**.

!!! warning "Třídy výztuže"
    Nepoužívejte pevnou tabulku Tekla Class jako univerzální legendu. Přiřazení tříd je v aplikaci konfigurovatelné; pro konkrétní projekt ověřte konfiguraci tříd v modelu.

## Co kontrolovat

- zda jsou ve zobrazených skupinách očekávané pruty;
- zda výztuž respektuje hranice stěny a otvory;
- zda se neočekávaně nezobrazují přesahy nebo prázdné oblasti;
- zda souhlasí výsledek v modelu s návrhem, který byl před generováním zkontrolován v Preview.

## Export

Z validačního okna lze spustit export PDF, PNG a tisk. Rozdíly mezi nimi popisuje [PDF export](pdf-export.md).

## Viz také

- [Preview panel](preview.md)
- [PDF export](pdf-export.md)
