# FAQ

!!! info "Verze pluginu: 2.5.0"
    Odpovědi vycházejí ze zdrojového stavu WallReinf 2.5.0. Výsledek vždy ověřte v konkrétním Tekla modelu.

## Připojení k Tekla Structures

### Plugin hlásí, že není k dispozici připojení k modelu

Otevřete Tekla Structures s aktivním modelem a v dialogu **Nastavení** spusťte **Test připojení**. Aplikace ověřuje připojení k Tekla modelu; vlastní transportní mechanismus není pro uživatelský postup podstatný.

Viz [Připojení k modelu](pruvodce/pripojeni.md).

### Status po „Test připojení“ zůstává „Neověřeno“

Klikněte přímo na tlačítko **Test připojení** v dialogu **Nastavení**. Pokud se stav nezmění nebo test selže, ověřte, že je otevřen aktivní Tekla model, a případně Tekla Structures restartujte.

Viz [Připojení k modelu](pruvodce/pripojeni.md#overeni-pripojeni).

### Načtení stěn nevrací očekávané položky

Zkontrolujte filtr materiálu (prefix) v **Nastavení**. Chování prázdného filtru a kombinace s konkrétním typem objektu je **K OVĚŘENÍ** pro váš model.

Viz [Připojení k modelu](pruvodce/pripojeni.md#nacteni-sten) a [Parametry](reference/parametry.md).

## Generování a opakovaná úprava

### Co se stane s dříve vytvořenou výztuží WallReinf?

Při generování může aplikace nahradit dříve vytvořenou výztuž WallReinf příslušné stěny. Aplikace používá uložený stav a identitu vytvořených objektů; přesný dopad na ručně vytvořené nebo cizí pruty je **K OVĚŘENÍ** před nasazením do produkčního modelu.

Viz [Základní workflow](pruvodce/zakladni-workflow.md).

### Kdy použít Re-edit?

Tlačítko **Re-edit** je určeno pro bezpečnou opakovanou úpravu stěny s uloženým stavem WallReinf. Může být zablokováno například po změně topologie, při nejednoznačné identitě prutů nebo po ruční úpravě sledovaných objektů.

### Co znamená převzetí zkopírované výztuže?

Při práci s kopií stěny může aplikace nabídnout kontrolované převzetí zkopírované výztuže. Dialog rozlišuje objekty k převzetí, ponechání, odstranění identických kopií a konflikty. Výsledek vždy zkontrolujte ve vybraném Tekla modelu.

### Optimalizace délek nenachází žádné pruty

Optimalizace pracuje se skutečnými přímými pruty WallReinf v modelu; samotný náhled není vstupem pro optimalizační změnu. Nejprve proto výztuž vygenerujte a ověřte, že je model připojen.

## Otvory, lemování a diagonály

### U-pruty kolem prostupů se negenerují

Zkontrolujte parametry lemování a prostupů a následně výsledek v preview i Tekla modelu. Přesná závislost všech detailů na geometrii otvoru je **K OVĚŘENÍ**.

Viz [Otvory a prostupy](pruvodce/otvory.md) a [Parametry](reference/parametry.md).

### Diagonální pruty a pruty kolem prostupů

V hlavním okně je k dispozici volba **Šikmá výztuž v rozích (45°)**. Vztah mezi jejím průměrem a průměrem prutů kolem prostupů je pro tuto verzi **K OVĚŘENÍ**.

Viz [Diagonální pruty](pruvodce/diagonaly.md).

### Dolní vytrnování vytvořilo závlače

Nemělo by k tomu dojít: pro dolní volbu **Vytrnování z desky** aplikace nevytváří závlače. Pokud výsledek v modelu neodpovídá, nepokračujte v generování bez kontroly a zaznamenejte geometrii stěny a zvolené okrajové podmínky.

## Validace a PDF

### Validační okno je prázdné

Nejprve vygenerujte výztuž a potom otevřete validaci. Validační okno pracuje se skutečnou výztuží načtenou z Tekla modelu, ne pouze s plánovaným návrhem.

Viz [Validační okno](pruvodce/validace.md).

### Po úpravě délek v preview se pruty kříží s okraji nebo otvory

Před generováním spusťte kontrolu kolizí v preview. U složitější geometrie nebo po ručních úpravách je výsledek kontroly **K OVĚŘENÍ** také ve vlastním modelu.

Viz [Preview panel](pruvodce/preview.md#upravy-vybranych-rad).

### PDF export selhal

Ověřte, že jsou data ve validačním okně načtena. Pokud validační okno neobsahuje výztuž, není co exportovat.

Viz [PDF export](pruvodce/pdf-export.md) a [Validační okno](pruvodce/validace.md).

## Licence

### Aplikace při startu požaduje aktivaci licence

Postupujte podle aktivačního dialogu. Aplikace používá uložený licenční token a při potřebě jeho obnovení může komunikovat s licenční službou. Dostupnost síťové služby a podmínky konkrétní licence jsou **K OVĚŘENÍ**.
