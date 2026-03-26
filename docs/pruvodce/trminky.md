# Třmínky

!!! info "Verze pluginu: [VERZE]"
    Tato stránka popisuje chování pluginu verze [VERZE].

Tato stránka vysvětluje, jak plugin generuje třmínky a prapory, jakou logiku používá při rozhodování mezi nimi a kde nastavit příslušné prahy v okně **Nastavení**. Rozhodnutí vychází z délky každého segmentu výztuže a ze dvou nastavitelných prahových hodnot.

## Co jsou třmínky a prapory

Plugin používá dva typy příčné výztuže spojující vrstvy S1 a S2:

- **Třmínky** — uzavřené smyčky (ocelové svorky) probíhající kolem prutů obou vrstev. Generují se v krátkých segmentech stěny, kde uzavřený tvar poskytuje potřebné sevření výztuže.
- **Prapory** — L-tvarované pruty jako alternativa třmínků pro segmenty střední délky. Mají otevřený tvar — jeden hák — místo uzavřené smyčky.

Plugin automaticky rozhoduje, zda pro daný segment použije třmínky, prapory nebo standardní přímou výztuž — na základě délky segmentu a nastavených prahů.

## Prahy v Nastavení

Sekce **Třmínky a prapory** v okně **Nastavení** obsahuje dva slidery:

- **Prah třmínku** (Slider, 0–2 500 mm, výchozí hodnota: 300 mm) — segmenty kratší než tato hodnota dostanou třmínky.
- **Prah praporu** (Slider, 0–2 500 mm, výchozí hodnota: 1 500 mm) — segmenty kratší než tato hodnota, ale delší než prah třmínku, dostanou prapory.

!!! note "Poznámka — logika prahů"
    Segment kratší než **Prah třmínku** → generují se třmínky.
    Segment delší než **Prah třmínku**, ale kratší než **Prah praporu** → generují se prapory.
    Segment delší než **Prah praporu** → standardní přímá výztuž bez třmínků nebo praporů.

Prahové hodnoty se nastavují v okně **Nastavení** → **Třmínky a prapory**.

![Okno Nastavení — sekce Třmínky a prapory](../assets/screenshots/settings-trminky-prapory.png)

*[VERZE] — Okno Nastavení, sekce Třmínky a prapory. Zachytit: oba slidery viditelné, Prah třmínku 300 mm, Prah praporu 1 500 mm.*

## Třmínky nad dveřmi

CheckBox **Třmínky nad dveřmi** v sekci **Prostupy** expanderu **Výztuž** zajišťuje generování třmínků v oblasti nad dveřními otvory.

Po zaškrtnutí plugin přidá třmínky do pásu výztuže nad každým detekovaným dveřním otvorem, a to bez ohledu na délku segmentu a nastavené prahy. Tento pás třmínků přispívá k zachycení diagonálního napětí, které vzniká v oblasti nadpraží.

Nastavení dalších parametrů prostupů viz [Otvory](otvory.md).

## Interakce segmentů

Délka segmentů přímé výztuže závisí na nastavení segmentace rastru. Segmenty vznikají přerušením přímých prutů kolem prostupů a na krajích stěny.

Kratší segmenty (vzniklé přerušením kolem prostupů) mohou splňovat podmínky pro třmínky nebo prapory i v případě, kdy přímá výztuž daleko od prostupu je bez příčné výztuže. To je záměrné — krátké segmenty v blízkosti prostupů vyžadují příčné sevření.

Nastavení segmentace (prahy přerušení, max délka segmentu, min vzdálenost od otvoru) viz [Hlavní parametry](parametry.md#segmentace-rastru).

!!! tip "Tip — příliš mnoho třmínků"
    Pokud plugin generuje třmínky tam, kde byste očekávali přímou výztuž, zkontrolujte hodnotu **Prah praporu** v okně **Nastavení** → **Třmínky a prapory**. Snižte prahové hodnoty, aby kratší segmenty dostaly třmínky a delší segmenty zůstaly s přímou výztuží.

!!! warning "Pozor — překrývající se prahy"
    Hodnota **Prah praporu** musí být vždy větší než hodnota **Prah třmínku**. Pokud jsou prahy nastaveny obráceně nebo stejně, plugin se zachová neočekávaně. Plugin tuto podmínku nekontroluje automaticky.

![Stěna se segmenty zobrazujícími třmínky a prapory](../assets/screenshots/trminky-prapory-segmenty.png)

*[VERZE] — Stěna s viditelnou segmentací. Zachytit: krátký segment s třmínky, středně dlouhý segment s prapory, dlouhý segment s přímou výztuží bez příčné výztuže.*

Třída prvků třmínků a praporů v exportním výstupu: třmínky jsou označeny Class 8, prapory Class 9 (Flag) — toto označení je viditelné v legendě validačního okna. Viz [Validace výztuže](../pruvodce/validace.md).
