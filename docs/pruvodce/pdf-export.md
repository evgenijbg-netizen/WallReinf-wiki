# PDF export

!!! info "Verze pluginu: [VERZE]"
    Tato stránka popisuje chování pluginu verze [VERZE].

Export grafického pohledu na výztuž jako PDF, PNG nebo tisk — vše přímo z validačního okna.

## Vytvoření exportu

Export probíhá z okna **Grafická validace výztuže**. Postup:

1. Otevřete [Validační okno](validace.md) po vygenerování výztuže.
2. Nastavte viditelnost vrstev — exportuje se přesně to, co je zobrazeno v plátně.
3. Zvolte typ exportu:
   - **Export PDF** — uloží pohled do PDF souboru.
   - **Export PNG** — uloží pohled jako PNG obrázek.
   - **Tisk** — odešle pohled na tiskárnu.

!!! tip "Tip — Před exportem upravte vrstvy"
    Vypněte vrstvy, které v exportu nepotřebujete. Export zachytí přesně to, co vidíte ve validačním okně — včetně zapnutých/vypnutých vrstev a nastavené průhlednosti.

![Validační okno s tlačítky Export PDF, Export PNG a Tisk](../assets/screenshots/validace-export-tlacitka.png)

*[VERZE] — Validační okno s viditelným exportním panelem. Zachytit: tlačítka Export PDF, Export PNG a Tisk, plátno s výztuží, nastavené vrstvy.*

## Obsah exportu

Export obsahuje grafický pohled na stěnu s viditelnou výztuží tak, jak ji zobrazuje validační okno:

- Barevné kódování odpovídá legendě vrstev (Svislá Class 3, Vodorovná Class 6, atd.).
- Viditelnost vrstev odpovídá stavu v okně v okamžiku exportu.
- Průhlednost vrstev se v exportu zachová.
- Měřítko a rozměry závisí na velikosti stěny v modelu.

![Příklad exportovaného PDF s výztuží stěny](../assets/screenshots/pdf-export-vystup.png)

*[VERZE] — Příklad výstupu exportu. Zachytit: exportovaný pohled s výztuží, viditelné barevné odlišení vrstev, popisky rozměrů stěny.*

## Formáty exportu — kdy použít

| Formát | Použití |
|--------|---------|
| **Export PDF** | Dokumentace, předání projektantovi, archivace |
| **Export PNG** | Vložení do zpráv, prezentací, e-mailů |
| **Tisk** | Rychlé vytisknutí pro kontrolu na staveništi |

Podrobnosti o vrstvách a legendě viz [Validační okno](validace.md#vrstvy-a-legenda).
