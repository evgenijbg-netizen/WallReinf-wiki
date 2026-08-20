# Licence a aktivace

WallReinf při spuštění ověřuje platnost licence, ještě než otevře hlavní pracovní okno. Pokud není možné použít dříve uložené ověření, zobrazí se okno **Aktivace licence**.

## První aktivace

1. Připojte počítač k internetu.
2. Do pole **E-mail** zadejte e-mailovou adresu, pro kterou byla licence poskytnuta.
3. Klikněte na **Aktivovat** a vyčkejte na potvrzení.
4. Po úspěšné aktivaci pokračuje spuštění aplikace do hlavního okna.

E-mail musí odpovídat licenci založené pro zákazníka. Dojde-li k odmítnutí aktivace, zkontrolujte adresu a obraťte se na správce licence nebo podporu; aplikace sama licenci nevytváří ani nemění.

## Běžný provoz a práce offline

Po úspěšném ověření aplikace ukládá lokální licenční token. Platný token umožňuje krátkodobou práci bez připojení k internetu; pro tento mechanismus je implementovaný časový limit 24 hodin. Při dostupném připojení aplikace token průběžně obnovuje.

!!! warning "Před prací mimo síť"
    Spusťte WallReinf alespoň jednou online a ověřte, že licence byla přijata. Po vypršení uloženého tokenu je k dalšímu spuštění nutné opětovné online ověření.

Počet zařízení, délka komerční licence a postup při výměně počítače závisí na konkrétní licenci. Tyto podmínky jsou **K OVĚŘENÍ** u poskytovatele licence.

## Když aktivace nebo spuštění selže

- Ověřte připojení k internetu a správný systémový čas.
- Zadejte znovu stejný e-mail, pro který byla licence vydána.
- Pokud se hlášení týká zařízení nebo vypršení licence, nepokoušejte se problém řešit ručním mazáním aplikačních dat; kontaktujte podporu s textem hlášení.
- Pokud licenční okno hlásí nedostupnou službu, zkuste spuštění později. Máte-li dosud platný lokální token, může krátkodobě fungovat spuštění bez sítě.

## Viz také

- [Instalace](instalace.md)
- [Požadavky](pozadavky.md)
