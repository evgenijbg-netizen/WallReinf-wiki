# Základní workflow

Tato stránka provádí procesem vyztužení jedné stěny: od výběru přes nastavení parametrů až po generování a kontrolu.

## 1. Načtěte a vyberte stěnu

Nejprve musí být aplikace připojená k otevřenému Tekla modelu. V horní liště zvolte režim **Prefix** nebo **Stěna**, zadejte hledanou hodnotu a klikněte na **Načíst**. Poté vyberte stěnu v nabídce **Stěna**.

K pohybu mezi načtenými stěnami použijte tlačítka **Předchozí stěna (◀)** a **Další stěna (▶)**. Pokud je stěna již označena přímo v Tekla Structures, můžete po načtení seznamu použít ikonu **Vybrat z Tekla**.

## 2. Nastavte parametry

Parametry jsou v levém panelu rozděleny do skupin. Ve skupině **Výztuž** nastavte parametry S1/S2, krytí, lemování a odsazení. Ve skupině **Okrajové podmínky** nastavte podmínky navazujících konstrukcí podle konkrétní stěny.

Pro podrobný popis všech voleb použijte [Hlavní parametry](parametry.md). Nastavení pro prostupy popisují [Prostupy](otvory.md), pro třmínky a prapory [Třmínky a prapory](trminky.md) a pro šikmou výztuž [Šikmá výztuž](diagonaly.md).

## 3. Zkontrolujte náhled a generujte

V pravém panelu zkontrolujte náhled plánované výztuže — zejména rozložení prutů, okrajovou výztuž a prostupy. Poté klikněte na **Generovat**.

!!! warning "Nahrazení existující výztuže"
    Generování nahrazuje existující výztuž vytvořenou aplikací WallReinf pro vybranou stěnu. Pokud aplikace nedokáže existující data bezpečně určit nebo odstranit, generaci zastaví před vložením nové výztuže.

Po vygenerování můžete v kontextové nabídce **Stěna** nastavit stav:

- **Označit jako hotovo** — pouze pro stěnu s výztuží WallReinf.
- **Označit ke kontrole** — pouze pro stěnu s výztuží WallReinf.
- **Označit bez výztuže** — pouze pro stěnu bez výztuže.

Stavové filtry v horní liště umožňují zobrazit nebo skrýt hotové stěny, stěny ke kontrole a stěny bez výztuže.

## 4. Přidejte poznámku podle potřeby

Kliknutím na ikonu **Poznámka ke stěně** otevřete dialog pro textovou poznámku. Poznámka se ukládá do vlastnosti `Comment` vybrané stěny v Tekla modelu, takže je vázaná na tento modelový prvek.

## Viz také

- [Referenční parametry hlavního okna](../reference/parametry.md#hlavni-okno)
- [Okrajové podmínky](okrajove-podminky.md)
- [Nastavení](../reference/parametry.md#nastaveni)
- [FAQ — Generování a opakovaná úprava](../faq.md#generovani-a-opakovana-uprava)
