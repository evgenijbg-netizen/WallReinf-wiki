# Hlavní parametry

!!! info "Verze pluginu: [VERZE]"
    Tato stránka popisuje chování pluginu verze [VERZE].

Tato stránka vysvětluje nastavení všech parametrů v hlavním dialogu pluginu — od průměrů prutů a roztečí přes krytí až po pokročilé detaily a kontextová nastavení v okně **Nastavení**.

## Orientace S1

Sekce **Orientace S1** je první volbou v expanderu **Výztuž**. Určuje, která strana stěny je vnější (nosná):

- **Svislá (nosná)** — svislá výztuž tvoří vnější vrstvu (S1); typické pro stěny namáhané svislým zatížením.
- **Vodorovná (nosná)** — vodorovná výztuž tvoří vnější vrstvu (S1); typické pro stěny namáhané vodorovným (větrovým) zatížením.

S1 = vnější strana stěny, S2 = vnitřní strana stěny. Toto přiřazení je pevné pro celý dialog.

!!! warning "Pozor — orientace ovlivňuje všechny parametry"
    Změna orientace S1 mění přiřazení průměrů a roztečí. Nastavte orientaci **před** zadáním průměrů a roztečí, jinak budou hodnoty přiřazeny k opačné vrstvě.

![Sekce Orientace S1 v expanderu Výztuž](../assets/screenshots/vyztu-orientace-s1.png)

*[VERZE] — Expander Výztuž, sekce Orientace S1. Zachytit: vybrané RadioButton Svislá (nosná), obě možnosti viditelné.*

## Svislá výztuž

Sekce **Svislá výztuž** obsahuje nastavení pro svislé pruty:

- **S1:** — průměr svislé výztuže na vnější straně (ComboBox). Typické hodnoty: Ø10, Ø12, Ø14.
- **S2:** — průměr svislé výztuže na vnitřní straně (ComboBox). Lze nastavit shodně se S1 nebo rozdílně.
- **Rozteč:** — rozteč svislých prutů v mm (platí pro S1 i S2 společně). Typické hodnoty: 150, 200, 250 mm.

Tlačítko **Sjednotit vše** (tooltip: „Sjednotit průměry S2 podle S1") přepíše průměry S2 v obou směrech (svislém i vodorovném) hodnotami ze S1.

## Vodorovná výztuž

Sekce **Vodorovná výztuž** má stejnou strukturu jako **Svislá výztuž**:

- **S1:** — průměr vodorovné výztuže na vnější straně.
- **S2:** — průměr vodorovné výztuže na vnitřní straně.
- **Rozteč:** — rozteč vodorovných prutů v mm.

Vodorovná výztuž má obvykle menší průměr než svislá. Standardní kombinace: svislá Ø12, vodorovná Ø10, rozteče 200 mm.

![Expander Výztuž — svislá a vodorovná výztuž](../assets/screenshots/vyztu-svisle-vodorovna.png)

*[VERZE] — Expander Výztuž s nastavenými průměry. Zachytit: Svislá výztuž S1 Ø12, S2 Ø12, rozteč 200 mm; Vodorovná výztuž S1 Ø10, S2 Ø10, rozteč 200 mm.*

## Lemování (U-čka)

CheckBox **Lemování (U-čka)** aktivuje generování okrajových U-prutů po obvodu stěny a kolem prostupů.

Po zaškrtnutí se zpřístupní:

- **Průměr:** — průměr U-prutů (ComboBox). Volte průměr roven nebo větší než průměr přímé výztuže.
- **Rozteč: dle přímé výztuže** — informační popis; rozteč U-prutů odpovídá rozteči přímé výztuže (nelze samostatně nastavit).

!!! note "Poznámka — Lemování a T-spoj"
    Aktivace **Lemování (U-čka)** je předpokladem pro sekci **T-spoj (navazující stěny)** v expanderu **Detaily**. Bez zaškrtnutého lemování jsou ovládací prvky T-spoje zašedlé.

Lemovací výztuž kolem prostupů viz [Prostupy](otvory.md).

## Krytí a okraje

Expander **Krytí a okraje** obsahuje nastavení tloušťky krycí vrstvy a odsazení prutů od okrajů stěny.

### Krytí

- **Krytí:** — tloušťka betonového krytí v mm (ComboBox). Dostupné hodnoty: 30, 35, 40, 50, 60 mm. Zvolte hodnotu dle platné normy a expozice prostředí.
- **Ocel:** — zobrazena třída oceli `B500B` (informační; nelze měnit v dialogu).
- **Odsazení:** — počáteční odsazení prvního prutu od spodního a horního okraje stěny v mm. Tooltip: „Počáteční odsazení prutu od spodního/horního okraje".

### Odsazení od kraje

Sekce **Odsazení od kraje** nastavuje vzdálenost krajních prutů od bočních hran stěny:

- **H:** — odsazení v vodorovném směru (od levé a pravé hrany stěny) v mm. Tooltip: „Vodorovný směr".
- **V:** — odsazení ve svislém směru (od spodní a horní hrany stěny) v mm. Tooltip: „Svislý směr".

![Expander Krytí a okraje](../assets/screenshots/kryti-a-okraje.png)

*[VERZE] — Expander Krytí a okraje. Zachytit: Krytí 30 mm vybrané, Ocel B500B, Odsazení 25 mm, Odsazení od kraje H 25 mm, V 25 mm.*

## Detaily

Expander **Detaily** pokrývá dvě sekce: **Okrajové podmínky** a **T-spoj (navazující stěny)**.

### Okrajové podmínky

Sekce **Okrajové podmínky** definuje chování výztuže na krajích stěny:

- **Volný konec stěny** — zaškrtněte, pokud hrana stěny není navázána na jinou stěnu nebo pilíř (volný konec bez navazující konstrukce). Plugin upraví délky krajních prutů a okrajové lemování.
- **Pokračuje výš** — zaškrtněte, pokud stěna v horní části přechází do stropní desky. Po zaškrtnutí se aktivuje pole:
    - **Tl. desky:** — tloušťka stropní desky v mm. Plugin tuto hodnotu použije pro výpočet délky přesahů výztuže do desky.

### T-spoj (navazující stěny)

Sekce **T-spoj (navazující stěny)** umožňuje generovat závlačové pruty v místě napojení navazujících stěn.

!!! warning "T-spoj je dostupný pouze s Lemováním"
    Sekce **T-spoj (navazující stěny)** je aktivní pouze pokud je zaškrtnuta volba **Lemování (U-čka)**. Bez lemování jsou ovládací prvky T-spoje zašedlé a závlače se negenerují.

Nastavení T-spoje:

- **Zleva** — zaškrtněte, pokud navazující stěna přichází zleva (při pohledu na S1).
- **Zprava** — zaškrtněte, pokud navazující stěna přichází zprava.
- **tl:** — tloušťka navazující stěny v mm (ComboBox, rozsah 150–400 mm). Ovlivňuje délku závlaček.
- **Závlače:** — rozteč závlačových prutů v mm (Slider, rozsah 40–200 mm). Závlače se generují rovnoměrně podél celé výšky stěny.

![Expander Detaily s aktivním T-spojem](../assets/screenshots/detaily-t-spoj.png)

*[VERZE] — Expander Detaily, sekce T-spoj aktivní (Lemování zaškrtnuto). Zachytit: Volný konec stěny nezaškrtnut, Pokračuje výš zaškrtnuto s Tl. desky 200 mm, Zleva a Zprava zaškrtnuto, tl. 200 mm, Závlače slider na 150 mm.*

## Nastavení a výchozí hodnoty

Výchozí hodnoty průměrů a roztečí pro nové stěny se nastavují v okně **Nastavení** → **Výchozí hodnoty**.

!!! tip "Tip — Výchozí hodnoty v Nastavení"
    Opakovaně používané hodnoty průměrů a roztečí lze nastavit jako výchozí v okně **Nastavení** → **Výchozí hodnoty**. Plugin je předvyplní při každém přepnutí na novou stěnu — nemusíte zadávat stejné hodnoty znovu a znovu.

Sekce **Výchozí hodnoty** obsahuje:

- 6-polní mřížku průměrů (Svislá S1, Svislá S2, Vodorovná S1, Vodorovná S2, Lemování, Prostupy)
- 6-polní mřížku roztečí (Svislá, Vodorovná, a doplňkové hodnoty)
- **Krytí** — výchozí hodnota krytí
- **Odsazení od okraje** — výchozí odsazení

### Segmentace rastru

V okně **Nastavení** → **Segmentace rastru** lze nastavit chování přerušení přímé výztuže kolem prostupů:

- **Práh pro přerušení** (m²) — minimální plocha prostupu, od které plugin přeruší prut (menší prostupy prut přeruší méně agresivně).
- **Max délka segmentu** (mm) — maximální délka jednoho segmentu přímého prutu.
- **Min vzdálenost od otvoru** (mm) — minimální vzdálenost konce prutu od hrany prostupu.

### Dělení prutu

V okně **Nastavení** → **Dělení prutu** nastavte **Maximální délka prutu** (Slider, 6 000–12 000 mm). Pruty delší než tato hodnota budou automaticky děleny se přesahem.

### Normy

V okně **Nastavení** → **Normy** jsou dostupné:

- **Poloha výztuže** — ComboBox s hodnotami **Nepříznivá** / **Příznivá** — určuje součinitel polohy výztuže při výpočtu kotevních délek dle normy.
- **Tabulka přesahů a kotevních délek** — tlačítko pro otevření tabulky minimálních přesahů a kotevních délek dle průměru prutu.

??? note "Pokročilé: Tabulka přesahů a kotevních délek"
    V okně **Nastavení** → **Normy** → **Tabulka přesahů a kotevních délek** lze zobrazit a upravit tabulku minimálních přesahů a kotevních délek dle průměru prutu. Tyto hodnoty ovlivňují délky přesahů generovaných prutů a tím množství spotřebovaného materiálu. Výchozí hodnoty odpovídají ČSN EN 1992.

![Okno Nastavení — sekce Výchozí hodnoty](../assets/screenshots/settings-vychozi-hodnoty.png)

*[VERZE] — Okno Nastavení, sekce Výchozí hodnoty. Zachytit: 6-polní mřížka průměrů a roztečí s typickými hodnotami, Krytí 30 mm, Odsazení od okraje 25 mm.*

## Viz také

- [Tabulka parametrů — Výztuž](../reference/parametry.md#vyztuz)
- [Tabulka parametrů — Krytí a okraje](../reference/parametry.md#kryti-a-okraje)
- [Tabulka parametrů — Detaily](../reference/parametry.md#detaily)
- [Tabulka parametrů — Nastavení — Výchozí hodnoty](../reference/parametry.md#nastaveni-vychozi-hodnoty)
- [Tabulka parametrů — Nastavení — Segmentace rastru a Dělení prutu](../reference/parametry.md#nastaveni-segmentace-rastru-a-deleni-prutu)
- [Tabulka parametrů — Nastavení — Třmínky a prapory](../reference/parametry.md#nastaveni-trminky-a-prapory)
- [FAQ — Generování výztuže](../faq.md#generovani-vyztuze)
