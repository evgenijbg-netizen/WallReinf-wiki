# Převzetí zkopírované výztuže

Při práci s kopií stěny může WallReinf nabídnout dialog **Převzetí zkopírované výztuže**. Převzetí zapisuje zkopírované skupiny do stavu aktuální stěny, aby je WallReinf mohl později spravovat pomocí [Re-editu](re-edit.md).

## Nejdřív proveďte kontrolu v Tekla modelu

Dialog rozděluje nalezené skupiny do čtyř kategorií:

| Kategorie | Význam |
|---|---|
| **Skupiny k převzetí** | Skupiny navržené k převzetí aktuální stěnou. |
| **Ponechané skupiny** | Skupiny, které se při převzetí nemají změnit. |
| **Identické kopie ke konsolidaci** | Identické skupiny určené k odstranění při konsolidaci. |
| **Konfliktní skupiny** | Skupiny s konfliktem nebo neúplnou identitou. |

Kliknutím na počet u libovolné kategorie označíte přesné odpovídající objekty v Tekla modelu; dialog zůstane otevřený. Než budete pokračovat, projděte takto označené objekty a ověřte, že patří vybrané stěně.

## Převzetí

1. Zkontrolujte všechny čtyři kategorie přímo v Tekla modelu.
2. Pokud jsou přítomné konfliktní skupiny nebo neúplná identita, převzetí je zablokované. Neřešte to potvrzením naslepo; nejdříve upravte nebo vyjasněte problematické objekty v modelu.
3. Je-li tlačítko aktivní, zvolte **Převzít a označit jako hotové**.
4. V potvrzovacím dialogu zkontrolujte počet identických kopií, které budou při konsolidaci odstraněny, a teprve potom potvrďte pokračování.
5. Po úspěchu otevřete [Validační okno](validace.md) a ověřte výsledek i stav stěny.

## Důležitý důsledek

Převzetí se provádí pro všechny adoptovatelné skupiny aktuální stěny najednou. Po převzetí může pozdější Re-edit převzaté pruty změnit nebo odstranit. Pokud mají některé zkopírované pruty zůstat nezávisle ručně spravované, neprovádějte převzetí, dokud jejich vztah k aktuální stěně neověříte.

Pokud aplikace převzetí nedokončí, zobrazí důvod. Stav stěny potom před dalším pokusem ověřte v Tekla modelu a ve validaci.

!!! note "K OVĚŘENÍ"
    Rozpoznání kopií závisí na dostupné identitě objektů a na tom, jak byla stěna v modelu zkopírována. U složitých nebo ručně upravovaných kopií postup nejdříve ověřte na kopii modelu.

## Viz také

- [Re-edit — bezpečná opakovaná úprava](re-edit.md)
- [Základní workflow](zakladni-workflow.md)
- [Validační okno](validace.md)
