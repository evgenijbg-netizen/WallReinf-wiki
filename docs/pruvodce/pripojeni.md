# Připojení k modelu

!!! info "Verze pluginu: [VERZE]"
    Tato stránka popisuje chování pluginu verze [VERZE].

Tato stránka popisuje, jak ověřit připojení pluginu k modelu a jak načíst stěny pro vyztužení.

## Ověření připojení

Po spuštění pluginu zkontrolujte, že je připojení k Tekla modelu funkční.

1. Klikněte na ikonu **Nastavení** v pravém horním rohu hlavního okna.
2. V dialogu **Nastavení** přejděte do sekce **Připojení**.
3. Klikněte na tlačítko **Test připojení**.
4. Status pod tlačítkem se změní na `Status: Připojeno` při úspěšném připojení.

!!! warning "Pozor"
    Pokud **Test připojení** selže, zkontrolujte, že Tekla Structures je spuštěna a model je otevřen. Plugin komunikuje s Tekla přes gRPC — připojení vyžaduje aktivní model, ne jen spuštěnou aplikaci.

![Sekce Připojení v dialogu Nastavení](../assets/screenshots/pripojeni-nastaveni.png)

*[VERZE] — Dialog Nastavení, sekce Připojení. Zachytit: tlačítko Test připojení a status text "Status: Připojeno".*

## Načtení stěn

Po ověření připojení načtěte stěny z modelu do dropdownu **Stěna**.

1. Do pole **Prefix** zadejte prefix označení stěn v modelu (např. `1W` pro stěny s prefixem `1W`).
2. Klikněte na tlačítko **Načíst**.
3. Dropdown **Stěna** se naplní nalezenými stěnami.
4. Vyberte stěnu z dropdownu — plugin ji zobrazí v preview panelu vpravo.

!!! tip "Tip"
    Prefix je volitelný. Prázdné pole načte všechny stěny v modelu. Pro velké modely doporučujeme použít prefix pro rychlejší filtrování.

### Filtr materiálu

V **Nastavení → Načítání stěn** lze nastavit **Filtr materiálu (prefix)**. Načtou se pouze prvky, jejichž materiál začíná zadaným prefixem (např. `C` pro beton). Tím se z výběru vyloučí ocelové nebo dřevěné prvky.

### Navigace mezi stěnami

Po načtení stěn můžete přecházet mezi nimi bez opakovaného výběru z dropdownu:

- **Předchozí stěna (◀)** — přechod na předchozí stěnu v seznamu
- **Další stěna (▶)** — přechod na následující stěnu v seznamu
- **Vybrat z Tekla** — načte stěnu aktuálně vybranou v Tekla Structures (výběr musí být proveden v Tekla před kliknutím)
- **Zobrazit pouze vybranou stěnu** — přepne Tekla pohled tak, aby byla viditelná pouze vybraná stěna

### Stav stěny

Každé stěně lze přiřadit stav kliknutím pravým tlačítkem na název stěny v dropdownu:

- **Hotovo** — výztuž je vygenerována a schválena
- **Ke kontrole** — výztuž čeká na kontrolu
- **Bez výztuže** — stěna nebude vyztužena

![Hlavní okno po načtení stěn](../assets/screenshots/pripojeni-nacist-steny.png)

*[VERZE] — Hlavní okno pluginu, top bar po načtení stěn. Zachytit: vyplněný Prefix, Stěna dropdown s vybranou stěnou, tlačítka navigace (◀ ▶), ikona Nastavení.*

---

Pokračujte na [Základní workflow](zakladni-workflow.md) pro kompletní postup práce se stěnou.
