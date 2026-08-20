# Re-edit — bezpečná opakovaná úprava

**Re-edit** upravuje výztuž, kterou WallReinf již dříve vytvořil pro vybranou stěnu. Není to obecný nástroj pro úpravu libovolné výztuže v modelu: pracuje se stavem uloženým společně s dřívější generací.

## Kdy je dostupný

Po načtení a výběru stěny aplikace načte její uložený snapshot nastavení. Tlačítko **Re-edit** se zpřístupní jen tehdy, když je tento stav pro vybranou stěnu bezpečně k dispozici.

Při výběru stěny se uložené hodnoty běžně obnoví do ovládacích prvků. Pokud chcete hodnoty zatím neobnovovat, použijte volbu **Ignorovat uložená nastavení**. Tím ale nevzniká nový bezpečný stav pro Re-edit; před samotnou úpravou si vždy ověřte, že pracujete se správnou stěnou a jejími parametry.

## Doporučený postup

1. Načtěte seznam stěn, vyberte požadovanou stěnu a zkontrolujte její orientaci, okrajové podmínky a náhled.
2. Ověřte, že je aktivní tlačítko **Re-edit**.
3. Upravte požadované parametry a znovu zkontrolujte Preview.
4. Spusťte **Re-edit**. Aplikace porovná dříve evidované pruty s novým návrhem a podle výsledku může existující pruty upravit, odstranit již nepotřebné pruty nebo vložit chybějící pruty.
5. Po dokončení otevřete [Validační okno](validace.md) a zkontrolujte skutečnou výztuž v Tekla modelu.

## Kdy Re-edit nepokračuje

Aplikace úpravu zablokuje, pokud nedokáže bezpečně určit uložený stav nebo identitu sledovaných prutů. Typickými důvody jsou změna topologie, nejednoznačná identita prutů nebo ruční úprava sledovaných objektů. Neobcházejte takové hlášení novou generací bez kontroly, protože generování může existující výztuž WallReinf nahradit.

!!! warning "Částečně provedená úprava"
    Pokud se po změně Tekla objektů zobrazí hlášení o částečném selhání, model mohl zůstat částečně změněný a původní snapshot už nemusí odpovídat výsledku. Použijte ihned **Undo** v Tekla Structures, nebo stěnu znovu vygenerujte před dalším pokusem o Re-edit.

## Vztah k převzaté výztuži

Po [převzetí zkopírované výztuže](prevzeti-zkopirovane-vyztuze.md) se převzaté skupiny stanou součástí stavu stěny. Pozdější Re-edit je proto může změnit nebo odstranit. Převzetí používejte jen pro kopii, jejíž výztuž má WallReinf dále spravovat.

!!! note "K OVĚŘENÍ"
    Přesný rozsah ručních zásahů, které vedou k blokaci, závisí na identitě a geometrii objektů v konkrétním Tekla modelu. Před rozsáhlou změnou si postup vyzkoušejte na kopii stěny.

## Viz také

- [Základní workflow](zakladni-workflow.md)
- [Preview panel](preview.md)
- [Validační okno](validace.md)
