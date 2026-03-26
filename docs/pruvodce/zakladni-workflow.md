# Základní workflow

!!! info "Verze pluginu: [VERZE]"
    Tato stránka popisuje chování pluginu verze [VERZE].

Tato stránka provádí kompletním procesem vyztužení jedné stěny — od výběru přes nastavení parametrů až po generování a kontrolu.

## Výběr stěny

Před výběrem stěny musí být plugin připojen k otevřenému modelu v Tekla Structures. Podrobnosti viz [Připojení k modelu](pripojeni.md).

1. Do pole **Prefix** zadejte prefix označení stěn (např. `1W`).
2. Klikněte na **Načíst** — plugin načte všechny stěny z modelu odpovídající prefixu a naplní rozbalovací nabídku **Stěna**.
3. Vyberte stěnu z rozbalovací nabídky **Stěna**. Plugin okamžitě zobrazí live preview plánované výztuže v pravém panelu.

Mezi stěnami se pohybujte tlačítky **Předchozí stěna (◀)** a **Další stěna (▶)**. Pokud chcete přejít na stěnu vybranou přímo v modelu, použijte ikonu **Vybrat z Tekla**.

![Horní lišta pluginu — pole Prefix, tlačítko Načíst a výběr stěny](../assets/screenshots/top-bar-nacist-stena.png)

*[VERZE] — Horní lišta pluginu. Zachytit: pole Prefix s hodnotou `1W`, tlačítko Načíst, rozbalovací nabídka Stěna s vybranou stěnou, počítadlo stěn (např. 3 / 12).*

## Nastavení parametrů

Hlavní dialog pluginu obsahuje tři sekce (expandery). Pro typické vyztužení stěny postupujte takto:

1. Otevřete sekci **Výztuž** — nastavte průměry a rozteče svislé a vodorovné výztuže pro S1 (vnější stranu) a S2 (vnitřní stranu). Pokud jsou potřeba okrajové U-pruty, zaškrtněte **Lemování (U-čka)** a zvolte průměr.
2. Otevřete sekci **Krytí a okraje** — zvolte hodnotu krytí z nabídky **Krytí** (30–60 mm) a dle potřeby upravte odsazení od okraje.
3. Otevřete sekci **Detaily** — nastavte okrajové podmínky (**Volný konec stěny**, **Pokračuje výš**) a případně T-spoje s navazujícími stěnami.

Podrobný popis všech parametrů viz [Hlavní parametry](parametry.md).

Pro nastavení výztuže kolem prostupů viz [Prostupy](otvory.md). Pro třmínky a prapory viz [Třmínky a prapory](trminky.md). Pro šikmou výztuž v rozích viz [Šikmá výztuž](diagonaly.md).

![Hlavní dialog pluginu se všemi třemi expandery](../assets/screenshots/hlavni-dialog-expandery.png)

*[VERZE] — Hlavní okno pluginu se třemi expandery (Výztuž, Krytí a okraje, Detaily) rozbalenými. Zachytit: typické hodnoty průměrů a roztečí, zaškrtnuté Lemování (U-čka).*

## Generování výztuže

1. Zkontrolujte výztuž v preview panelu vpravo — ověřte rozložení prutů, okrajovou výztuž a prostupy.
2. Klikněte na **Generovat** — plugin vytvoří výztuž ve Tekla modelu.

!!! warning "Pozor — přepis existující výztuže"
    **Generovat** přepíše veškerou existující výztuž dané stěny. Před generováním zkontrolujte parametry v preview panelu.

Po vygenerování klikněte pravým tlačítkem na nabídku **Stěna** a označte stěnu přes kontextové menu:

- **Označit jako hotovo** — stěna je vyztužena a zkontrolována.
- **Označit ke kontrole** — stěna čeká na přezkoumání.
- **Označit bez výztuže** — stěna nebude vyztužena (např. atika, parapet).

!!! tip "Tip — sledování postupu"
    Průběh projektu sledujte pomocí filtrů stavu v horní liště. Přepínejte zobrazení stěn dle stavu: hotovo, ke kontrole, bez výztuže.

![Tlačítko Generovat a výsledný stav stěny](../assets/screenshots/generovat-stav-steny.png)

*[VERZE] — Tlačítko Generovat v hlavním dialogu. Zachytit: stav před generováním (preview viditelný) a kontextové menu se stavovými volbami.*

## Poznámky ke stěně

Plugin umožňuje přidat k libovolné stěně textové poznámky. Klikněte na ikonu **Poznámka ke stěně** (ikona poznámky v horní liště). Otevře se okno pro zadání textu.

- Poznámky jsou uloženy per stěna a přetrvávají mezi relacemi.
- Slouží k označení stěn vyžadujících zvláštní pozornost — například nestandardní detail, čekání na podklady nebo připomínka pro kolegu.

![Okno Poznámka ke stěně](../assets/screenshots/poznamka-ke-stene.png)

*[VERZE] — Okno Poznámka ke stěně s textovým polem. Zachytit: prázdné nebo vzorově vyplněné pole poznámky.*

## Viz také

- [Tabulka parametrů — Výztuž](../reference/parametry.md#vyztuz)
- [Tabulka parametrů — Krytí a okraje](../reference/parametry.md#kryti-a-okraje)
- [Tabulka parametrů — Detaily](../reference/parametry.md#detaily)
- [FAQ — Generování výztuže](../faq.md#generovani-vyztuze)
