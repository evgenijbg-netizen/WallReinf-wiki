# Validační okno

!!! info "Verze pluginu: [VERZE]"
    Tato stránka popisuje chování pluginu verze [VERZE].

Validační okno zobrazuje skutečnou výztuž načtenou z Tekla modelu pro vizuální kontrolu po generování.

## Spuštění validace

Okno **Grafická validace výztuže** otevřete z hlavního okna pluginu po vygenerování výztuže.

!!! note "Poznámka — Validace vs. Preview"
    Validační okno zobrazuje **skutečnou výztuž z Tekla modelu** (již vygenerovanou), nikoliv plánovaný návrh jako preview panel. Nejprve je nutné výztuž vygenerovat přes **Generovat**.

    Preview plánované výztuže viz [Preview panel](preview.md).

## Skutečná výztuž z Tekla modelu

Záhlaví okna nese popis **Skutečná výztuž z Tekla modelu** — indikátor, že zobrazená výztuž odpovídá aktuálnímu stavu Tekla modelu, nikoli pouze plánovanému navrhu.

- **Obnovit** — znovu načte data z Tekla modelu. Použijte po každé manuální úpravě výztuže přímo v Tekle nebo po opakovaném generování.

![Validační okno se zobrazenou výztuží z Tekla modelu](../assets/screenshots/validace-okno.png)

*[VERZE] — Okno Grafická validace výztuže. Zachytit: plátno s vygenerovanou výztuží, záhlaví Skutečná výztuž z Tekla modelu, tlačítko Obnovit.*

## Vrstvy a legenda

**Vrstvy výztuže** — panel vpravo s přepínači viditelnosti; zobrazuje stejné vrstvy jako preview, ale pro skutečnou výztuž v modelu.

### Legenda barev

Expander **Legenda barev** zobrazuje barevné kódování jednotlivých typů výztuže podle třídy Tekla:

| Vrstva | Tekla třída |
|--------|-------------|
| Svislá | Class 3 |
| Vodorovná | Class 6 |
| Lemování hrany | Class 7, 8 |
| Lemování otvoru | Class 9 |
| Prapory | Class 9 — Flag |
| Třmínky | Class 11 |

Barvy odpovídají barevnému kódování v Tekla modelu — validační pohled a model jsou konzistentní.

### Průhlednost

Slider **Průhlednost:** upravuje průhlednost vrstev v plátně. Snížení průhlednosti usnadňuje rozlišení překrývajících se vrstev výztuže.

![Validační okno s rozbalenou legendou a více vrstvami](../assets/screenshots/validace-vrstvy-legenda.png)

*[VERZE] — Validační okno s rozbaleným expanderem Legenda barev. Zachytit: barevně odlišené vrstvy v plátně, legenda s třídami Tekla, slider Průhlednost.*

## Interpretace výsledků

Při vizuální kontrole výztuže zaměřte pozornost na:

- **Chybějící výztuž** — oblasti plátna bez prutů v místech, kde by výztuž být měla.
- **Mezery a přesahy** — nepravidelné délky prutů nebo neočekávané přesahy v řadách.
- **Kolize** — pruty zasahující do okrajů, otvorů nebo navazujících konstrukcí.
- **Třídy výztuže** — ověřte pomocí legendy, zda jsou všechny typy výztuže (svislá, vodorovná, lemování, třmínky) přítomny ve správných polohách.

Zapínáním a vypínáním vrstev v panelu **Vrstvy výztuže** lze izolovat a zkontrolovat každý typ výztuže samostatně.

Pro export validačního pohledu do PDF nebo PNG viz [PDF export](pdf-export.md).

## Viz také

- [FAQ — Validace](../faq.md#validace)
