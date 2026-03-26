# Diagonální pruty

!!! info "Verze pluginu: [VERZE]"
    Tato stránka popisuje chování pluginu verze [VERZE].

Tato stránka popisuje generování diagonálních prutů v rozích prostupů — jejich aktivaci, umístění a účel. Diagonální pruty se generují automaticky ve všech rozích každého detekovaného prostupu, pokud je aktivován příslušný CheckBox.

## Nastavení diagonálních prutů

CheckBox **Šikmá výztuž v rozích (45°)** se nachází v sekci **Prostupy** expanderu **Výztuž** v hlavním dialogu.

Po zaškrtnutí plugin generuje diagonální pruty pod úhlem 45° ve všech rozích každého detekovaného prostupu. Tyto pruty zachycují tahová napětí, která vznikají v rozích prostupů při zatížení stěny — zejména u větších otvorů.

Základní nastavení sekce **Prostupy** (průměr U-prutů, třmínky nad dveřmi) viz [Otvory](otvory.md).
Průměry a rozteče přímé výztuže viz [Hlavní parametry](parametry.md).

## Umístění diagonál

Plugin umístí diagonální pruty takto:

- Pruty se generují ve všech 4 rozích každého detekovaného prostupu.
- Úhel diagonály je 45° vůči hranám prostupu.
- Délka prutu závisí na velikosti prostupu a hustotě rastru přímé výztuže.
- Diagonály se generují v obou vrstvách (S1 i S2).

![Prostup s diagonálními pruty v rozích](../assets/screenshots/diagonaly-rohy-prostupu.png)

*[VERZE] — Prostup ve stěně s diagonálními pruty v rozích. Zachytit: všechny 4 rohy prostupu, pruty pod úhlem 45°, viditelné v obou vrstvách výztuže.*

!!! tip "Tip — velké prostupy"
    Diagonální pruty jsou zvláště důležité u velkých prostupů (okna, dveřní otvory), kde koncentrace napětí v rozích může vést ke vzniku trhlin. Pro malé prostupy (technické kapsy) je přínos diagonál menší.

## Průměr diagonálních prutů

Diagonální pruty používají stejný průměr jako U-pruty z pole **Průměr:** v sekci **Prostupy**. Neexistuje samostatné pole pro průměr diagonál — jsou svázány s nastavením lemovací výztuže.

Pokud chcete použít jiný průměr pro diagonály a U-pruty, není to v aktuální verzi pluginu možné. Obě skupiny sdílejí hodnotu z pole **Průměr:** v sekci **Prostupy**.

??? note "Pokročilé: diagonály a Fiktivní zvětšení otvorů"
    Diagonální pruty se generují na fyzickém rozměru prostupu, stejně jako U-pruty. **Fiktivní zvětšení otvorů** (nastavení v okně **Nastavení**) ovlivňuje pouze rastr přímé výztuže a na polohu ani délku diagonálních prutů nemá vliv. Viz [Otvory](otvory.md) pro podrobnosti o fiktivním zvětšení.

Aktivaci diagonálních prutů a nastavení průměru prostupů lze také nastavit jako výchozí hodnotu v okně **Nastavení** → **Výchozí hodnoty**. Viz [Hlavní parametry](parametry.md#nastaveni-a-vychozi-hodnoty).
