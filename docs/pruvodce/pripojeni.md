# Připojení k modelu

Tato stránka popisuje ověření připojení k Tekla modelu a načtení stěn pro vyztužení.

## Ověření připojení

1. V horní liště hlavního okna klikněte na ikonu **Nastavení**.
2. V dialogu **Nastavení** otevřete skupinu **Připojení**.
3. Klikněte na **Test připojení**.
4. Při úspěchu se pod tlačítkem zobrazí stav připojení.

Pokud test selže, ověřte, že Tekla Structures běží a že je otevřený model. Aplikace pro práci s modelem vyžaduje aktivní připojení k Tekla modelu.

## Načtení stěn

V levé části horní lišty zvolte režim načtení:

- **Prefix** — načte skupinu stěn se zadaným prefixem, například `1W`.
- **Stěna** — načte jednu stěnu podle jejího úplného identifikátoru, například `1W12`.

Poté zadejte hodnotu do vstupního pole a klikněte na **Načíst**. Nalezené stěny se zobrazí v nabídce **Stěna**; výběrem stěny se připraví její parametry a náhled.

!!! note "K OVĚŘENÍ"
    Chování prázdné hodnoty v režimu **Prefix** není v uživatelském rozhraní výslovně popsáno. Pro předvídatelný výsledek vždy zadejte prefix nebo úplný identifikátor.

### Cast unit a složená stěna

Je-li stěna tvořena více díly jednoho cast unitu, aplikace může sestavit společnou logickou stěnu. V dialogu načítání lze pro tento případ zvolit díl cast unitu, který bude použit jako základ výběru. Po změně výběru obnovte načtení a zkontrolujte obrys v náhledu.

!!! warning "Nevybírejte jen podle názvu"
    Složené díly mohou mít schod, výřez nebo jinou výšku. Před generováním ověřte fyzický obrys, polohu otvorů a orientaci S1/S2. Pokud aplikace hlásí neslučitelné díly, mezeru nebo nepodporovaný obrys, generování zastavte.

Podrobnosti ke složeným, polygonálním, šikmým a vertikálním stěnám uvádí [Geometrie a typy stěn](geometrie-a-typy-sten.md).

### Filtr materiálu

V **Nastavení → Načítání stěn** lze vyplnit **Filtr materiálu (prefix)**. Načtou se jen prvky, jejichž materiál tímto prefixem začíná; například `C` pro beton. Prázdná hodnota filtr nepoužije.

### Navigace a zobrazení

- **Předchozí stěna (◀)** a **Další stěna (▶)** mění vybranou stěnu v načteném seznamu.
- **Vybrat z Tekla** vybere z načteného seznamu stěnu, která je právě označena v Tekla Structures. Nejdříve je nutné načíst seznam stěn.
- Ikona oka přepíná zobrazení pouze vybrané stěny v Tekla pohledu.

### Stav stěny

Kontextová nabídka výběru **Stěna** umožňuje označit stěnu jako **Hotovo**, **Ke kontrole** nebo **Bez výztuže**. Aplikace nedovolí označit stěnu s výztuží jako „Bez výztuže“ ani označit stěnu bez výztuže jako „Ke kontrole“.

---

Pokračujte na [Základní workflow](zakladni-workflow.md) pro kompletní postup práce se stěnou.

## Viz také

- [Požadavky](pozadavky.md)
- [Instalace a spuštění](instalace.md)
- [Geometrie a typy stěn](geometrie-a-typy-sten.md)
