# Otvory

!!! info "Verze pluginu: [VERZE]"
    Tato stránka popisuje chování pluginu verze [VERZE].

Tato stránka vysvětluje, jak plugin detekuje prostupy ve stěně, jak generuje lemovací U-pruty kolem prostupů a jaká nastavení z okna **Nastavení** ovlivňují tento proces.

## Detekce otvorů

Plugin detekuje prostupy automaticky z geometrie modelu Tekla Structures. Rozlišuje tyto typy:

- **Dveřní a okenní otvory** — plné průchody zdí (prostupující otvory)
- **Kapsy** (neprostupující otvory) — prohlubně v povrchu stěny, které neprocházejí celou tloušťkou
- **Výřezy** (Beam/slab cutouty) — geometrické řezy stěny způsobené napojenými průvlaky nebo deskami

Detekce probíhá při kliknutí na **Načíst** — plugin prohledá geometrii vybrané stěny a sestaví seznam prostupů. Výsledek detekce lze zkontrolovat v okně **Nastavení** → **Prostupy** → tlačítko **Debug detekce**.

## Prostupy — nastavení v hlavním dialogu

Sekce **Prostupy** se nachází v expanderu **Výztuž** (označena barevným ohraničením).

- **Průměr:** — průměr U-prutů generovaných kolem prostupů (ComboBox). Dostupné hodnoty: Ø8 až Ø25. Výchozí hodnota: Ø12.

Zakladní nastavení průměrů a roztečí přímé výztuže viz [Hlavní parametry](parametry.md).

Sekce **Prostupy** dále obsahuje:

- **Šikmá výztuž v rozích (45°)** — CheckBox pro generování diagonálních prutů v rozích prostupů. Viz [Diagonální pruty](diagonaly.md).
- **Třmínky nad dveřmi** — CheckBox pro generování třmínků nad dveřními otvory. Viz [Třmínky](trminky.md).

## Lemovací výztuž kolem prostupů

Lemovací U-pruty kolem prostupů se generují, pokud je zaškrtnuta volba **Lemování (U-čka)** v expanderu **Výztuž**.

!!! warning "Pozor — Lemování musí být aktivní"
    Bez zaškrtnutého **Lemování (U-čka)** se U-pruty kolem prostupů negenerují, i když jsou prostupy v modelu detekovány. Aktivaci **Lemování (U-čka)** viz [Hlavní parametry](parametry.md#lemovani-u-cka).

Plugin generuje U-pruty podél všech hran každého detekovaného prostupu:

- U-prut objímá hranu prostupu a jeho nožky se protáhnou do rastru přímé výztuže.
- Průměr U-prutů je nastaven v poli **Průměr:** v sekci **Prostupy**.
- Délka nožek U-prutů je omezena nastavením **Limit protažení noh U-ček** (viz níže).

![Stěna s prostupem a lemovacími U-pruty](../assets/screenshots/otvory-lemovaci-u-pruty.png)

*[VERZE] — Stěna s prostupem. Zachytit: U-pruty kolem všech čtyř hran prostupu, nožky zasahující do rastru přímé výztuže na obou stranách.*

## Nastavení v okně Nastavení

Otevřete okno **Nastavení** tlačítkem v horní liště hlavního dialogu.

### Filtry prostupů

Sekce **Prostupy** v okně **Nastavení** obsahuje filtry, které určují, které typy prostupů plugin zpracovává:

- **Ignorovat kapsy (neprostupující otvory)** — plugin přeskočí kapsy a nebude kolem nich generovat U-pruty.
- **Ignorovat výřezy (Beam/slab cutouty)** — plugin přeskočí výřezy způsobené napojením průvlaků nebo desek.
- **Ignorovat všechny prostupy** — plugin přeskočí všechny prostupy; lemovací výztuž kolem prostupů se negeneruje úplně.

!!! warning "Pozor — Ignorovat kapsy"
    Zaškrtněte **Ignorovat kapsy (neprostupující otvory)** pouze tehdy, když model obsahuje technické kapsy, které nemají přerušovat rastr výztuže (např. kapsy pro instalační krabice bez statické funkce). Běžné otvory (okna, dveře) by nikdy neměly být ignorovány.

### Generace otvorů

Sekce **Generace otvorů** obsahuje dvě nastavení ovlivňující tvar a umístění U-prutů:

- **Limit protažení noh U-ček** (Slider, 0–2 000 mm) — maximální délka nožek U-prutů přesahujících za hranu prostupu do rastru přímé výztuže. Nižší hodnota = kratší nožky; vyšší hodnota = delší přesah do rastru.
- **Odsazení ohybu kotevních prutů** (Slider, 0–200 mm) — vzdálenost, o kterou se ohyb kotevního prutu odsazuje od hrany prostupu.

### Fiktivní zvětšení otvorů

Sekce **Fiktivní zvětšení otvorů** umožňuje fiktivně zvětšit prostupy pro výpočet rastru přímé výztuže:

- **H** (Slider, 0–200 mm) — fiktivní zvětšení prostupu v horizontálním směru (na každou stranu).
- **V** (Slider, 0–200 mm) — fiktivní zvětšení prostupu ve vertikálním směru (na každou stranu).

??? note "Pokročilé: Fiktivní zvětšení otvorů"
    Fiktivní zvětšení ovlivňuje pouze rastr přímé výztuže (kde se pruty přerušují kolem prostupu). Lemovací U-pruty se generují vždy na skutečném rozměru prostupu z modelu — fiktivní zvětšení je neovlivní. Použijte tuto funkci, pokud potřebujete větší přerušovací zónu přímé výztuže kolem prostupu než je jeho fyzická velikost.

![Okno Nastavení — sekce Prostupy a Generace otvorů](../assets/screenshots/settings-prostupy.png)

*[VERZE] — Okno Nastavení, sekce Prostupy a Generace otvorů. Zachytit: všechny tři filtry viditelné, Limit protažení noh U-ček nastaven na 150 mm, Odsazení ohybu kotevních prutů na 50 mm.*
