---
title: utrullningskonflikter
description: Lär dig hur du hanterar och löser flera sammanslagningskonflikter för Platshanteraren.
feature: Multi Site Manager
role: Administratör
translation-type: tm+mt
source-git-commit: 0f2b7176b44bb79bdcd1cecf6debf05bd652a1a1
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 1%

---


# utrullningskonflikter {#msm-rollout-conflicts}

Konflikter kan uppstå om nya sidor med samma sidnamn skapas både i den blå grenen och i en beroende Live Copy-gren. Sådana konflikter måste hanteras och lösas vid utrullning.

## Konflikthantering {#conflict-handling}

När det finns sidor som är i konflikt (i grenarna utkast och Live Copy) kan du med MSM definiera hur (eller till och med om) de ska hanteras.

För att säkerställa att utrullningen inte blockeras kan möjliga definitioner omfatta:

* Vilken sida (utkast eller Live Copy) som ska ha prioritet vid utrullning
* Vilka sidor som ska namnändras (och hur)
* Hur detta påverkar publicerat innehåll

Standardbeteendet för AEM är att publicerat innehåll inte påverkas. Om en sida som skapades manuellt i Live Copy-grenen har publicerats kommer det innehållet fortfarande att publiceras efter konflikthanteringen och utrullningen.

Förutom standardfunktionerna kan anpassade konflikthanterare läggas till för att implementera olika regler. Detta kan även möjliggöra publiceringsåtgärder som en enskild process.

### Exempelscenario {#example-scenario}

I följande avsnitt använder vi exemplet med en ny sida `b`, som skapats både i planbilden och i Live Copy-grenen (skapas manuellt), för att illustrera de olika lösningmetoderna:

* skiss: `/b`

   En överordnad sida med 1 underordnad sida, `bp-level-1`

* Live Copy: `/b`

   En sida som skapats manuellt i Live Copy-grenen med en underordnad sida, `lc-level-1`

   * Aktiverad vid publicering som `/b`, tillsammans med den underordnade sidan

#### Före utrullning {#before-rollout}

|  | Utskrift före utrullning | Live Copy Before Rolling | Publicera före utrullning |
|---|---|---|---|
| Värde | `b` | `b` | `b` |
| Kommentar | Skapat i en designgren, klar för utrullning | Manuellt skapat i Live Copy-grenen | Innehåller innehållet på sidan `b` som skapades manuellt i Live Copy-grenen |
| Värde | `/bp-level-1` | `/lc-level-1` | `/lc-level-1` |
| Kommentar |  | Manuellt skapat i Live Copy-grenen | innehåller innehållet på sidan `child-level-1` som skapades manuellt i Live Copy-grenen |

## Utrullningshanteraren och konflikthantering {#rollout-manager-and-conflict-handling}

Med utrullningshanteraren kan du aktivera eller inaktivera konflikthantering.

Detta görs med [OSGi-konfiguration](/help/implementing/deploying/configuring-osgi.md) av **Day CQ WCM Rollout Manager**. Ange värdet **Hantera konflikt med manuellt skapade sidor** ( `rolloutmgr.conflicthandling.enabled`) till true om rollout-hanteraren ska hantera konflikter från en sida som skapats i Live Copy med ett namn som finns i ritningen.

AEM har [fördefinierat beteende när konflikthantering har inaktiverats.](#behavior-when-conflict-handling-deactivated)

## Konflikthanterare {#conflict-handlers}

AEM använder konflikthanterare för att lösa eventuella sidkonflikter som uppstår när innehåll distribueras från en plan till en Live-kopia. Att byta namn på sidor är den vanliga (inte bara) metoden att lösa sådana konflikter. Mer än en konflikthanterare kan vara användbar för att tillåta ett urval av olika beteenden.

AEM tillhandahåller:

* [standardkonflikthanteraren](#default-conflict-handler):
   * `ResourceNameRolloutConflictHandler`
* Möjligheten att implementera en [anpassad hanterare](#customized-handlers)
* Den rangordningsmekanism som gör att du kan ange prioriteten för varje enskild hanterare
   * Tjänsten med högst rankning används.

### Standardhanterare för konflikt {#default-conflict-handler}

Standardkonflikthanteraren är `ResourceNameRolloutConflictHandler`

* Med den här hanteraren får plantryckssidan företräde.
* Tjänstrankningen för den här hanteraren är låg, dvs. under standardvärdet för egenskapen `service.ranking`, eftersom antagandet är att anpassade hanterare behöver en högre rankning. Rankningen är dock inte den absolut minsta nivån för att garantera flexibilitet vid behov.

Den här konflikthanteraren ger prioritet åt ritningen. Exempelvis flyttas Live Copy-sidan `/b` inom Live Copy-grenen till `/b_msm_moved`.

* Live Copy: `/b`

   Flyttas inom Live Copy till `/b_msm_moved`. Detta fungerar som en säkerhetskopia och säkerställer att inget innehåll går förlorat.

   * `lc-level-1` flyttas inte.

* Blå: `/b`

   Går ut på sidan Live Copy `/b`.

   * `bp-level-1` i till Live Copy.

#### Efter utrullning {#after-rollout}

|  | Utskrift efter utrullning | Live Copy After Rollout | Live Copy After Rollout | Publicera efter utrullning |
|---|---|---|---|---|
| Värde | `b` | `b` | `b_msm_moved` | `b` |
| Kommentar |  | Innehåller innehållet på ritningssidan `b` som introducerades | Har innehållet på sidan `b` som skapades manuellt i Live Copy-grenen | Ingen ändring, innehåller innehållet på originalsidan `b` som skapades manuellt i Live Copy-grenen och nu kallas `b_msm_moved` |
| Värde | `/bp-level-1` | `/bp-level-1` | `/lc-level-1` | `/lc-level-1` |
| Kommentar |  |  | Ingen ändring | Ingen ändring |

### Anpassade hanterare {#customized-handlers}

Med anpassade konflikthanterare kan du implementera egna regler. Med servicerangordningsmekanismen kan du även definiera hur de interagerar med andra hanterare.

Anpassade konflikthanterare kan:

* Namnge efter behov.
* Utvecklas/konfigureras enligt dina krav.
   * Du kan t.ex. utveckla en hanterare så att sidan Live-kopia har prioritet.
* Kan konfigureras med [OSGi-konfigurationen](/help/implementing/deploying/configuring-osgi.md). Särskilt gäller följande:
   * **Service** Rankingdefinierar den ordning som hör till andra konflikthanterare (  `service.ranking`).
      * Standardvärdet är `0`.

### Beteende när Konflikthantering är inaktiverat {#behavior-when-conflict-handling-deactivated}

Om du manuellt [avaktiverar konflikthantering utför](#rollout-manager-and-conflict-handling) AEM ingen åtgärd på sidor som är i konflikt. Sidor som inte är i konflikt rullas ut som förväntat.

>[!CAUTION]
>
>När konflikthantering är inaktiverat ger AEM inga indikationer på att konflikter ignoreras. Eftersom detta beteende i sådana fall måste konfigureras explicit antas det vara det önskade beteendet.

I det här fallet har Live Copy företräde. Den blå sidan `/b` kopieras inte och Live Copy-sidan `/b` lämnas orörd.

* Blå: `/b`

   Kopieras inte alls, men ignoreras.

* Live Copy: `/b`

   Står detsamma.

#### Efter utrullning {#after-rollout-no-conflict}

|  | Utskrift efter utrullning | Live Copy After Rollout | Publicera efter utrullning |
|---|---|---|---|
| Värde | `b` | `b` | `b` |
| Kommentar |  | Har innehållet på sidan `b` som skapades manuellt i Live Copy-grenen | Ingen ändring, innehåller innehållet på sidan `b` som skapades manuellt i Live Copy-grenen |
| Värde | `/bp-level-1` | `/lc-level-1` | `/lc-level-1` |
| Kommentar |  | Ingen ändring | Ingen ändring |

### Tjänstrankningar {#service-rankings}

Tjänstrankningen [OSGi](https://www.osgi.org/) kan användas för att definiera prioriteten för enskilda konflikthanterare.
