# FAQ

!!! info "Verze pluginu: [VERZE]"
    Tato stránka popisuje chování pluginu verze [VERZE].

Tato stránka shromažďuje časté problémy a jejich řešení. Každá položka uvádí konkrétní opravu a odkaz na příslušnou stránku průvodce nebo referenční tabulky.

## Připojení k Tekla Structures

### Plugin hlásí „Tekla není spuštěna"

Tekla Structures není otevřena nebo model není načten. Otevřete Tekla Structures, načtěte model a znovu spusťte plugin. Pouhé spuštění aplikace nestačí — model musí být aktivní.

Viz [Připojení k modelu](pruvodce/pripojeni.md) pro postup ověření připojení.

### „Nelze připojit k Tekle" při testu připojení

Plugin komunikuje přes gRPC — model musí být aktivní, ne jen Tekla. Zkontrolujte, zda je model otevřen. Pokud problém přetrvá, restartujte Tekla Structures.

Viz [Připojení k modelu](pruvodce/pripojeni.md).

### Status po „Test připojení" zůstává „Neověřeno"

Klikněte přímo na tlačítko **Test připojení**; výsledek se zobrazí pod tlačítkem. Pokud status zůstává Neověřeno, model není aktivní.

Viz [Připojení k modelu](pruvodce/pripojeni.md#overeni-pripojeni).

### Dropdown Stěna je po kliknutí Načíst prázdný

Zkontrolujte hodnotu v poli **Prefix**. Prázdné pole načte všechny stěny; chybný prefix nevrátí žádné výsledky. Zkontrolujte také Nastavení → Načítání stěn → Filtr materiálu.

Viz [Připojení k modelu](pruvodce/pripojeni.md) a [Parametry — Nastavení — Prostupy](reference/parametry.md#nastaveni-prostupy).

## Generování výztuže

### Generovat přepíše existující výztuž

Před generováním zkontrolujte parametry v preview panelu. Přepis je záměrný — plugin vždy nahradí veškerou existující výztuž dané stěny.

Viz [Základní workflow](pruvodce/zakladni-workflow.md).

### U-pruty kolem prostupů se negenerují

Zaškrtněte volbu **Lemování (U-čka)** v expanderu **Výztuž**. Bez aktivního lemování se U-pruty kolem prostupů negenerují.

Viz [Otvory a prostupy](pruvodce/otvory.md) a [Parametry — Výztuž](reference/parametry.md#vyztuz).

### T-spoj (závlače) je zašedlý

Zaškrtněte **Lemování (U-čka)**. T-spoj vyžaduje aktivní lemování.

Viz [Hlavní parametry — Detaily](pruvodce/parametry.md#t-spoj-navazujici-steny) a [Parametry — Detaily](reference/parametry.md#detaily).

### Plugin generuje příliš mnoho třmínků nebo praporů

Upravte prahy v Nastavení → Třmínky a prapory. Snižte **Prah třmínku** pro kratší segmenty nebo zvyšte **Prah praporu**.

Viz [Třmínky a prapory](pruvodce/trminky.md) a [Parametry — Nastavení — Třmínky a prapory](reference/parametry.md#nastaveni-trminky-a-prapory).

### Prah praporu nastavený níže než Prah třmínku — neočekávané chování

**Prah praporu** musí být vždy vyšší než **Prah třmínku**. Plugin tuto podmínku nekontroluje automaticky.

Viz [Třmínky a prapory](pruvodce/trminky.md#prahy-v-nastaveni).

### Orientace S1 — průměry přiřazeny k opačné vrstvě

Nastavte **Orientaci S1** jako první krok před zadáním průměrů a roztečí. Změna orientace po zadání hodnot přehodí přiřazení vrstev.

Viz [Hlavní parametry](pruvodce/parametry.md#orientace-s1) a [Parametry — Výztuž](reference/parametry.md#vyztuz).

### Diagonální pruty a U-pruty mají stejný průměr — nelze oddělit

V aktuální verzi pluginu sdílejí diagonální pruty průměr s U-pruty z pole **Průměr:** v sekci **Prostupy**. Samostatné nastavení průměru diagonál není k dispozici.

Viz [Diagonální pruty](pruvodce/diagonaly.md) a [Parametry — Výztuž](reference/parametry.md#vyztuz).

## Validace

### Validační okno je prázdné

Nejprve vygenerujte výztuž přes **Generovat**. Validační okno zobrazuje skutečnou výztuž z Tekla modelu, ne plánovaný návrh. Prázdné plátno = výztuž ještě nebyla vygenerována.

Viz [Validační okno](pruvodce/validace.md).

### Validační okno neodpovídá aktuálnímu stavu modelu

Klikněte na **Obnovit** v záhlaví validačního okna. Data se znovu načtou z Tekla modelu.

Viz [Validační okno](pruvodce/validace.md#skutecna-vyztuz-z-tekla-modelu).

### PDF export selhal s chybou

Ověřte, že jsou data ve validačním okně načtena (klikněte Obnovit). Export je možný pouze pokud validační okno obsahuje výztuž. Chyba „Není co exportovat" znamená prázdné validační okno.

Viz [PDF export](pruvodce/pdf-export.md) a [Validační okno](pruvodce/validace.md).

### Po úpravě délek v preview se pruty kříží s okraji nebo otvory

Po každé úpravě délek klikněte na **Zkontrolovat kolize** (nebo **Kolize** v inline doku). Generujte až po ověření, že kolize nejsou hlášeny.

Viz [Preview panel](pruvodce/preview.md#upravy-delek).
