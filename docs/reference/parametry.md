# Parametry

!!! info "Verze pluginu: [VERZE]"
    Tato stránka popisuje chování pluginu verze [VERZE].

Tato stránka je rychlá referenční tabulka všech parametrů pluginu Wall Reinforcement Wizard seskupených podle 10 sekcí uživatelského rozhraní. Pro podrobné vysvětlení workflow a chování parametrů viz [Průvodce parametry](../pruvodce/parametry.md).

## Výztuž

Podrobný popis viz [Hlavní parametry](../pruvodce/parametry.md).

| Parametr | Popis | Výchozí | Rozsah / Možnosti |
|---|---|---|---|
| **Orientace S1** | Která vrstva je vnější (nosná) | Svislá (nosná) | Svislá (nosná) / Vodorovná (nosná) |
| **Svislá výztuž S1** (Průměr) | Průměr svislých prutů vnější vrstvy | Ø12 | Ø8 / Ø10 / Ø12 / Ø14 / Ø16 / Ø18 / Ø20 / Ø22 / Ø25 |
| **Svislá výztuž S2** (Průměr) | Průměr svislých prutů vnitřní vrstvy | Ø12 | Ø8 / Ø10 / Ø12 / Ø14 / Ø16 / Ø18 / Ø20 / Ø22 / Ø25 |
| **Rozteč** (svislá) | Rozteč svislých prutů (platí pro S1 i S2) | 200 mm | 100 / 125 / 150 / 175 / 200 / 250 / 300 mm |
| **Vodorovná výztuž S1** (Průměr) | Průměr vodorovných prutů vnější vrstvy | Ø10 | Ø8 / Ø10 / Ø12 / Ø14 / Ø16 / Ø18 / Ø20 / Ø22 / Ø25 |
| **Vodorovná výztuž S2** (Průměr) | Průměr vodorovných prutů vnitřní vrstvy | Ø10 | Ø8 / Ø10 / Ø12 / Ø14 / Ø16 / Ø18 / Ø20 / Ø22 / Ø25 |
| **Rozteč** (vodorovná) | Rozteč vodorovných prutů | 200 mm | 100 / 125 / 150 / 175 / 200 / 250 / 300 mm |
| **Lemování (U-čka)** (aktivace) | Generování okrajových U-prutů | zaškrtnuto | ano / ne |
| **Lemování — Průměr** | Průměr okrajových U-prutů | Ø14 | Ø8 / Ø10 / Ø12 / Ø14 / Ø16 / Ø18 / Ø20 / Ø22 / Ø25 |
| **Prostupy — Průměr** | Průměr U-prutů kolem prostupů | Ø12 | Ø8 / Ø10 / Ø12 / Ø14 / Ø16 / Ø18 / Ø20 / Ø22 / Ø25 |
| **Šikmá výztuž v rozích (45°)** | Diagonální pruty v rozích prostupů | zaškrtnuto | ano / ne |
| **Třmínky nad dveřmi** | Třmínky nad dveřními otvory | zaškrtnuto | ano / ne |

## Krytí a okraje

Podrobný popis viz [Hlavní parametry](../pruvodce/parametry.md).

| Parametr | Popis | Výchozí | Rozsah / Možnosti |
|---|---|---|---|
| **Krytí** | Tloušťka krycí vrstvy betonu | 40 mm | 30 / 35 / 40 / 50 / 60 mm |
| **Ocel** | Třída oceli | B500B | informační (nelze měnit) |
| **Odsazení** | Počáteční odsazení prutu od spodního/horního okraje | 50 mm | Slider 0–200 mm, tick 10 mm |
| **Odsazení od kraje H** | Vodorovné odsazení od bočních hran stěny | 50 mm | Slider 0–300 mm, tick 10 mm |
| **Odsazení od kraje V** | Svislé odsazení od horní a dolní hrany stěny | 50 mm | Slider 0–300 mm, tick 10 mm |

## Detaily

Podrobný popis viz [Hlavní parametry](../pruvodce/parametry.md).

| Parametr | Popis | Výchozí | Rozsah / Možnosti |
|---|---|---|---|
| **Volný konec stěny** | Stěna má volný (nenavazující) konec | nezaškrtnuto | ano / ne |
| **Pokračuje výš** | Stěna pokračuje nad stropní desku | nezaškrtnuto | ano / ne |
| **Tl. desky** | Tloušťka navazující stropní desky | 200 mm | TextBox (mm); aktivní jen když Pokračuje výš zaškrtnuto |
| **Zleva** (aktivace) | Navazující stěna přichází zleva | nezaškrtnuto | ano / ne |
| **Tloušťka zleva** | Tloušťka navazující stěny zleva | 200 mm | 150 / 200 / 250 / 300 / 350 / 400 mm |
| **Zprava** (aktivace) | Navazující stěna přichází zprava | nezaškrtnuto | ano / ne |
| **Tloušťka zprava** | Tloušťka navazující stěny zprava | 200 mm | 150 / 200 / 250 / 300 / 350 / 400 mm |
| **Závlače** | Rozteč závlačových prutů (kotevní pruty) | 100 mm | Slider 40–200 mm, tick 10 mm |

!!! warning "Závislost T-spoje na Lemování"
    Sekce T-spoj (Zleva, Zprava, Tloušťka, Závlače) je dostupná pouze pokud je zaškrtnuto **Lemování (U-čka)**. Bez aktivního lemování jsou ovládací prvky T-spoje zašedlé.

## Nastavení — Výchozí hodnoty

Podrobný popis viz [Hlavní parametry](../pruvodce/parametry.md).

| Parametr | Popis | Výchozí | Rozsah / Možnosti |
|---|---|---|---|
| **Svislá S1** (výchozí průměr) | Výchozí průměr svislé výztuže vnější vrstvy | dle aktuálního nastavení | TextBox mm |
| **Svislá S2** (výchozí průměr) | Výchozí průměr svislé výztuže vnitřní vrstvy | dle aktuálního nastavení | TextBox mm |
| **Vodorovná S1** (výchozí průměr) | Výchozí průměr vodorovné výztuže vnější vrstvy | dle aktuálního nastavení | TextBox mm |
| **Vodorovná S2** (výchozí průměr) | Výchozí průměr vodorovné výztuže vnitřní vrstvy | dle aktuálního nastavení | TextBox mm |
| **Lemování** (výchozí průměr) | Výchozí průměr lemovacích U-prutů | dle aktuálního nastavení | TextBox mm |
| **Prostupy** (výchozí průměr) | Výchozí průměr U-prutů kolem prostupů | dle aktuálního nastavení | TextBox mm |
| **Svislá S1** (výchozí rozteč) | Výchozí rozteč svislých prutů | dle aktuálního nastavení | TextBox mm |
| **Vodorovná S1** (výchozí rozteč) | Výchozí rozteč vodorovných prutů | dle aktuálního nastavení | TextBox mm |
| **Krytí** (výchozí) | Výchozí tloušťka krycí vrstvy | dle aktuálního nastavení | TextBox mm |
| **Odsazení od okraje** (výchozí) | Výchozí odsazení prutu od okraje | dle aktuálního nastavení | Slider 0–200 mm, tick 10 mm |

## Nastavení — Segmentace rastru a Dělení prutu

Podrobný popis viz [Hlavní parametry](../pruvodce/parametry.md).

| Parametr | Popis | Výchozí | Rozsah / Možnosti |
|---|---|---|---|
| **Práh pro přerušení** | Minimální plocha prostupu pro přerušení prutu | — | TextBox m² |
| **Max délka segmentu** | Maximální délka jednoho segmentu přímého prutu | — | TextBox mm |
| **Min vzdálenost od otvoru** | Minimální vzdálenost konce prutu od hrany prostupu | — | TextBox mm |
| **Maximální délka prutu** | Pruty delší než tato hodnota jsou automaticky děleny | 12 000 mm | Slider 6 000–12 000 mm, tick 500 mm |

## Nastavení — Třmínky a prapory

Podrobný popis viz [Třmínky a prapory](../pruvodce/trminky.md).

| Parametr | Popis | Výchozí | Rozsah / Možnosti |
|---|---|---|---|
| **Prah třmínku** | Maximální délka otvoru, pro který plugin generuje třmínek (kratší = třmínek, delší = prapor) | 300 mm | Slider 0–2 500 mm, tick 50 mm |
| **Prah praporu** | Maximální délka otvoru, pro který plugin generuje prapor | 1 500 mm | Slider 0–2 500 mm, tick 50 mm |
| **Limit protažení noh U-ček** | Maximální délka noh U-prutů před přechodem na jiný typ | 700 mm | Slider 0–2 000 mm, tick 50 mm |
| **Odsazení ohybu kotevních prutů** | Vzdálenost ohybu kotevního prutu od hrany otvoru | 80 mm | Slider 0–200 mm, tick 10 mm |

## Nastavení — Prostupy

Podrobný popis viz [Otvory a prostupy](../pruvodce/otvory.md).

| Parametr | Popis | Výchozí | Rozsah / Možnosti |
|---|---|---|---|
| **Fiktivní zvětšení H** | Rozšíření detekované oblasti prostupu ve vodorovném směru | 0 mm | Slider 0–200 mm, tick 10 mm |
| **Fiktivní zvětšení V** | Rozšíření detekované oblasti prostupu ve svislém směru | 0 mm | Slider 0–200 mm, tick 10 mm |
| **Ignorovat kapsy** | Prostupy typu kapsa jsou ignorovány | nezaškrtnuto | ano / ne |
| **Ignorovat výřezy** | Prostupy typu výřez jsou ignorovány | nezaškrtnuto | ano / ne |
| **Ignorovat všechny prostupy** | Všechny prostupy jsou ignorovány | nezaškrtnuto | ano / ne |
| **Filtr materiálu (prefix)** | Pouze prostupy s materiálem začínajícím tímto prefixem | prázdné = bez filtru | TextBox (text prefix, např. C) |

## Nastavení — Normy

Podrobný popis viz [Hlavní parametry](../pruvodce/parametry.md).

| Parametr | Popis | Výchozí | Rozsah / Možnosti |
|---|---|---|---|
| **Poloha výztuže** | Součinitel polohy výztuže pro výpočet kotevních délek dle normy | Příznivá | Příznivá / Nepříznivá |
