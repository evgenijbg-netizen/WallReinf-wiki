# Optimalizace délek výztuže

Okno **Optimalizace délek** hledá návrhy úprav délek skutečných přímých prutů načtených z Tekla modelu. Nepracuje jen s obrazem v Preview; nejprve proto výztuž vygenerujte a ověřte připojení k modelu.

## Práce s návrhy

1. Vyberte stěnu nebo načtěte požadovaný rozsah stěn a otevřete **Optimalizace** z hlavního okna.
2. Podle potřeby omezte sken filtry **Stěna**, **Průměr**, **Rodina / typ**, **Vrstva**, minimální zdrojová délka, maximální změna a směr změny.
3. Vyberte skupinu délek a potom konkrétní návrh. V části **Dopad** a v tabulce **Položky návrhu** zkontrolujte dotčené stěny, vrstvu, současnou délku, cílovou délku a změnu.
4. Teprve po kontrole použijte tlačítko pro aplikaci návrhu.
5. Přečtěte výsledky jednotlivých položek. Pokud okno vyžádá úplný nový sken, použijte **Obnovit** před další aplikací.
6. Výsledek ověřte výběrem odpovídajících prutů v Tekla modelu a následně ve [Validačním okně](validace.md).

## Vlastnictví prutů a souhlas

Tabulky rozlišují vlastnictví a stav položek. Pruty WallReinf se vyhodnocují se svým uloženým stavem; ručně změněné nebo vyřazené položky proto mohou být ve výsledku uvedeny s důvodem, proč je nelze použít.

Volba **Zahrnout cizí pruty** rozšíří rozsah jen po výslovném zaškrtnutí. Platí pouze v právě otevřeném dialogu a jen pro cizí pruty, které současně projdou aktivními filtry. Před aplikací zkontrolujte počet **Dotčené cizí objekty** i označení vlastnictví u jednotlivých položek. Zapnutím této volby dáváte souhlas se změnou výztuže, kterou WallReinf nevytvořil.

!!! warning "Nejdřív ověřte dopad"
    Cizí nebo ručně upravené pruty mohou mít vlastní návaznosti a projektový význam. Nezahrnujte je hromadně jen proto, že mají stejný průměr nebo délku jako pruty WallReinf.

## Dílčí výsledek

Výsledek aplikace se uvádí po položkách, včetně stěny, vlastnictví, počtu dotčených prutů a důvodu výsledku. Některé položky tedy mohou uspět, zatímco jiné mohou být vyřazeny nebo selhat. V takovém případě nepokračujte dalšími návrhy bez nového skenu a kontroly skutečného stavu modelu.

!!! note "K OVĚŘENÍ"
    Konkrétní kombinace rodin prutů, geometrie a ručních změn, které jsou pro optimalizaci způsobilé, ověřte na reprezentativní stěně. Nezaměňujte návrh optimalizace za automatické schválení konstrukčního detailu.

## Viz také

- [Re-edit — bezpečná opakovaná úprava](re-edit.md)
- [Preview panel](preview.md)
- [Validační okno](validace.md)
