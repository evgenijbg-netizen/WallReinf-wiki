# Instalace a spuštění

Tato stránka popisuje instalaci distribuovaného balíčku Wall Reinforcement Wizard a jeho spuštění pro práci s Tekla modelem.

## Instalace aplikace

1. Zvolte instalační balíček určený pro svou verzi Tekla Structures.
2. Spusťte instalační soubor a dokončete průvodce instalací.
3. Instalátor uloží aplikaci do složky:
   `%ProgramData%\Trimble\Tekla Structures\[TEKLA_VERSION].0\Environments\common\extensions\WallReinf`

V této složce jsou aplikace `WallReinf.exe` a její potřebné soubory. Instalátor může vytvořit také zástupce v nabídce Start a volitelně na ploše.

!!! warning "Pozor"
    Nepoužívejte postup ručního kopírování do složky `applications` ani spuštění přes panel **Applications & Components**. Aktuální distribuovaný instalátor používá složku Tekla extensions a vytváří samostatně spouštěnou aplikaci.

## Spuštění

1. Otevřete Tekla Structures a načtěte model, se kterým budete pracovat.
2. Spusťte **Wall Reinforcement Wizard** z nabídky Start, zástupce na ploše nebo souborem `WallReinf.exe` v instalační složce.
3. V aplikaci ověřte připojení a načtěte stěny podle postupu [Připojení k modelu](pripojeni.md).

!!! note "K OVĚŘENÍ"
    Dostupnost zástupce na ploše závisí na volbě provedené v instalačním průvodci.

## Viz také

- [Požadavky](pozadavky.md)
- [Připojení k modelu](pripojeni.md)
