# Preview panel

!!! info "Verze pluginu: [VERZE]"
    Tato stránka popisuje chování pluginu verze [VERZE].

Preview panel zobrazuje plánovanou výztuž před generováním — dostupný jako inline dok v hlavním okně i jako samostatné okno **Preview výztuže**.

## Inline preview (hlavní okno)

Pravý sloupec hlavního okna pluginu zobrazuje živý náhled plánované výztuže. Náhled se automaticky aktualizuje při každé změně parametrů — není třeba nic potvrzovat.

Ovládací prvky v inline doku:

- **Vrstvy** — přepínání viditelnosti vrstev; tlačítko **Zobrazit vše** zapne všechny vrstvy najednou.
- **Heatmapa** — rozbalí matici průměrů a délek (viz sekci [Heatmapa](#heatmapa) níže).
- **Úpravy délek:** — lišta tlačítek **-50**, **-10**, **+10**, **+50** pro úpravu délek vybraných řad prutů.
- **Kolize** — zkontroluje kolize prutů s okraji a otvory stěny.
- **Sjednotit** — sjednotí délky vybraných řad na stejnou hodnotu.

![Inline preview v pravém sloupci hlavního okna](../assets/screenshots/preview-inline-dok.png)

*[VERZE] — Hlavní okno pluginu s inline preview v pravém sloupci. Zachytit: viditelné vrstvy výztuže v plátně, lišta Úpravy délek pod plátnem, tlačítka Kolize a Sjednotit.*

## Samostatné okno preview

Okno **Preview výztuže** otevřete z hlavního okna pluginu. Zobrazuje stejný náhled jako inline dok, ale v plné velikosti — vhodné pro detailní kontrolu před generováním.

Rozvržení samostatného okna:

- **Vrstvy výztuže** — panel na pravé straně s přepínači viditelnosti jednotlivých vrstev.
  - **Vše** — zobrazí všechny vrstvy.
  - **Nic** — skryje všechny vrstvy.
- **Úprava délky (vybrané řady):** — stejná lišta tlačítek jako v inline doku (**-50**, **-10**, **+10**, **+50**).
- **Zkontrolovat kolize** — spustí kontrolu kolizí prutů s okraji a otvory.
- **Sjednotit vybrané** — sjednotí délky vybraných řad.
- Stavový řádek: **Celkem: X prutů, Y délek, Z varování** — přehled počtu prutů a varování.
- **Generovat** — vygeneruje výztuž do Tekla modelu a zavře preview.
- **Zrušit** — zavře preview bez generování.

!!! tip "Tip — Úpravy v preview se zachovají"
    Všechny změny délek a jiné úpravy provedené v preview se zachovají po kliknutí na **Generovat**. Není třeba je zadávat znovu.

![Samostatné okno Preview výztuže s viditelným panelem vrstev](../assets/screenshots/preview-samostatne-okno.png)

*[VERZE] — Okno Preview výztuže. Zachytit: plátno s výztuží, panel Vrstvy výztuže vpravo s přepínači, stavový řádek s počty, tlačítka Generovat a Zrušit.*

## Vrstvy výztuže

Každý typ výztuže tvoří samostatnou vrstvu. Vrstvy lze zapínat a vypínat nezávisle — výhodné při kontrole jednoho typu výztuže najednou.

Dostupné vrstvy v preview:

| Vrstva | Popis |
|--------|-------|
| Svislá S1 | Svislé pruty na vnější straně |
| Svislá S2 | Svislé pruty na vnitřní straně |
| Vodorovná S1 | Vodorovné pruty na vnější straně |
| Vodorovná S2 | Vodorovné pruty na vnitřní straně |
| Lemování hrany | U-pruty po obvodu stěny |
| Lemování otvoru | U-pruty kolem prostupů |
| Prapory | Praporcové pruty |
| Třmínky | Třmínkové pruty |

## Heatmapa

**Heatmapa (Ø × délka)** je rozbalovací matice zobrazující počet prutů pro každou kombinaci průměru a délky.

Jak pracovat s heatmapou:

1. Klikněte na **Heatmapa** v inline doku nebo rozbalte expander **Heatmapa (Ø × délka)** v samostatném okně.
2. Matice zobrazuje sloupce pro průměry prutů (Ø8, Ø10, Ø12, ...) a řádky pro délky.
3. Číslo v každé buňce udává počet prutů dané kombinace průměru a délky.
4. Kliknutím na buňku filtrujete zobrazené vrstvy na pruty té kombinace — ostatní vrstvy se dočasně skryjí.

Heatmapa je užitečná pro:
- identifikaci dominantních průměrů a délek
- odhalení neobvyklých délek (výrazně odlišné od ostatních)
- kontrolu celkového počtu prutů před generováním

![Heatmapa s maticí průměrů a délek](../assets/screenshots/preview-panel-heatmapa.png)

*[VERZE] — Expander Heatmapa (Ø × délka) rozbalený v preview. Zachytit: matice s vyplněnými buňkami, různé průměry ve sloupcích, délky v řádcích, zvýrazněná vybraná buňka.*

## Úpravy délek

Délky prutů lze upravit přímo v preview bez nutnosti vracet se do nastavení parametrů.

Postup úpravy délek:

1. Vyberte řady prutů v plátně preview (kliknutím nebo označením více řad).
2. Použijte tlačítka **-50**, **-10**, **+10**, **+50** pro zkrácení nebo prodloužení o daný počet mm.
3. Po úpravách klikněte na **Zkontrolovat kolize** (**Kolize** v inline doku) pro ověření, že pruty nekolidují s okraji nebo otvory.
4. Volitelně použijte **Sjednotit vybrané** pro srovnání délek označených řad na stejnou hodnotu.

!!! warning "Pozor — Po úpravě délek vždy zkontrolujte kolize"
    Zkrácené nebo prodloužené pruty mohou kolidovat s okraji stěny nebo otvory. Vždy spusťte **Zkontrolovat kolize** po každé úpravě délek, než přistoupíte ke generování.

Nastavení průměrů a roztečí viz [Hlavní parametry](parametry.md).
