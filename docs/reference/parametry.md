# Parametry

!!! info "Verze pluginu: 2.5.0"
    Tato stránka vychází ze zdrojového stavu WallReinf 2.5.0. Výchozí cíl sestavení je Tekla Structures 2025.0; projekt obsahuje také cestu pro sestavení s Tekla 2026.0. Provozní kompatibilita s konkrétní instalací Tekla 2026 je **K OVĚŘENÍ**.

Toto je stručná referenční tabulka aktuálně doložených ovládacích prvků. Pro praktický postup viz [Průvodce parametry](../pruvodce/parametry.md).

## Hlavní okno

| Parametr | Popis | Výchozí | Rozsah / možnosti |
|---|---|---:|---|
| **Krytí S1** | Krytí výztuže na straně S1. | 40 mm | 20 až 70 mm po 5 mm |
| **Krytí S2** | Krytí výztuže na straně S2. | 40 mm | 20 až 70 mm po 5 mm |
| **Svislá výztuž S1 / S2 — průměr** | Průměr svislých prutů pro obě strany. | Ø12 | Ø8, Ø10, Ø12, Ø14, Ø16, Ø18, Ø20, Ø22, Ø25 |
| **Svislá výztuž — rozteč** | Rozteč svislých prutů. | 200 mm | 100, 125, 150, 175, 200, 250, 300 mm |
| **Vodorovná výztuž S1 / S2 — průměr** | Průměr vodorovných prutů pro obě strany. | Ø10 | Ø8, Ø10, Ø12, Ø14, Ø16, Ø18, Ø20, Ø22, Ø25 |
| **Vodorovná výztuž — rozteč** | Rozteč vodorovných prutů. | 200 mm | 100, 125, 150, 175, 200, 250, 300 mm |
| **Lemování — průměr** | Průměr lemovacích prutů na vnějších hranách. | Ø14 | Ø8, Ø10, Ø12, Ø14, Ø16, Ø18, Ø20, Ø22, Ø25 |
| **Prostupy — průměr** | Průměr prutů pro detaily kolem prostupů. | **K OVĚŘENÍ** | Hodnoty je nutné potvrdit v běžící aplikaci. |
| **Šikmá výztuž v rozích (45°)** | Volba pro diagonální výztuž v rozích otvorů. | **K OVĚŘENÍ** | Dostupnost a výchozí stav ověřte pro konkrétní stěnu. |
| **Generovat bez překryvu** | Volba ovlivňující generování rastru. | **K OVĚŘENÍ** | Přesný dopad vyžaduje ověření v Tekla modelu. |

## Okrajové podmínky

Okrajové podmínky jsou nově sjednocené do jednoho schématu stěny. Jejich volby se ukládají pro horní, levou, pravou a dolní hranu. Podrobný význam a postup volby viz [Okrajové podmínky](../pruvodce/okrajove-podminky.md).

| Hrana / ovládací prvek | Dostupné volby | Výchozí |
|---|---|---:|
| **Automaticky** | Automatická detekce okolních konstrukcí a přizpůsobení okrajových podmínek. | **K OVĚŘENÍ** |
| **Horní hrana** | Napojení do desky, vytrnování do stěny o patro výš, volná hrana. | Volná hrana |
| **Tloušťka desky** | Hodnota pro horní napojení do desky. | 200 mm |
| **Levá hrana** | Rohové napojení, volná hrana, T-spoj, vodorovné prodloužení. | Rohové napojení |
| **Pravá hrana** | Rohové napojení, volná hrana, T-spoj, vodorovné prodloužení. | Rohové napojení |
| **Tloušťka navazující stěny vlevo / vpravo** | Hodnota zobrazená u levé a pravé hrany schématu. | 200 mm |
| **Dolní hrana** | Nic, volná hrana, vytrnování z desky. | Nic |

!!! warning "Automatické nastavení"
    Výsledek automatické detekce závisí na geometrii a okolních objektech konkrétního Tekla modelu. Výsledek před generováním vždy zkontrolujte; přesná pravidla priorit a řešení nejednoznačných případů jsou **K OVĚŘENÍ**.

## Nastavení

Následující skupiny jsou dostupné v dialogu **Nastavení**:

- načítání stěn a filtr materiálu (prefix),
- výchozí hodnoty výztuže a krytí,
- segmentace rastru a dělení prutů,
- třmínky a prapory,
- zpracování prostupů,
- normové nastavení polohy výztuže,
- prefix číslování generované výztuže,
- tolerance rozpoznání navazující kolmé stěny,
- počet prutů ve skupině délek pro podporovanou šikmou horní hranu,
- konfigurace Tekla **Class** pro generovanou výztuž v souboru `rebar-classes.txt`,
- stav licence.

Konkrétní rozsahy, výchozí hodnoty a vzájemné závislosti těchto voleb je potřeba pro tuto verzi zkontrolovat v běžící aplikaci; proto jsou **K OVĚŘENÍ**. Neuvádějte je do projektu jako návrhové pravidlo bez kontroly výsledku.

Viz také [Třmínky](../pruvodce/trminky.md), [Otvory a prostupy](../pruvodce/otvory.md) a [Hlavní parametry](../pruvodce/parametry.md).
