# PDF export

Exporty jsou dostupné z [Validačního okna](validace.md): **Export PDF**, **Export PNG** a **Tisk**.

## PDF

Export PDF vytváří validační report pro vybrané stěny. Při exportu se nejprve vyberou stěny a potom soubor PDF; aplikace do něj sestaví data a geometrii validačních vrstev. Nabídka exportu obsahuje také **Hromadný export**.

!!! important "PDF není snímek obrazovky"
    PDF report není prosté uložení aktuálně viditelného plátna. Neuvádějte proto, že automaticky zachová aktuální přepínače vrstev nebo průhlednost, dokud to neověříte v běžící aplikaci.

## PNG a tisk

**Export PNG** uloží obraz validačního pohledu jako obrázek. **Tisk** předá validační plátno dialogu systému Windows pro tisk.

!!! note "K OVĚŘENÍ"
    Předávají-li PNG a tisk přesně aktuální viditelnost skupin, nastavení průhlednosti a měřítko, ověřte v běžící aplikaci na reprezentativní stěně. Nezaměňujte toto chování s hromadným PDF reportem.

## Doporučený postup

1. Vygenerujte výztuž a otevřete validační okno.
2. Pomocí **Obnovit** načtěte aktuální data z Tekla modelu.
3. Zkontrolujte skupiny a zvolený režim zobrazení.
4. Pro report více stěn zvolte **Export PDF** a vyberte požadované stěny.
5. Pro rychlý obraz aktuální validace použijte PNG nebo tisk; výsledek před předáním ověřte.

## Viz také

- [Validační okno](validace.md)
