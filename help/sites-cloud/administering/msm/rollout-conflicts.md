---
title: utrullningskonflikter
description: Lär dig hur du hanterar och löser flera sammanslagningskonflikter för Platshanteraren.
feature: Multi Site Manager
role: Admin
exl-id: 733e9411-50a7-42a5-a5a8-4629f6153f10
solution: Experience Manager Sites
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '919'
ht-degree: 0%

---

# utrullningskonflikter {#msm-rollout-conflicts}

Konflikter kan uppstå om nya sidor med samma sidnamn skapas både i den blå grenen och i en beroende Live Copy-gren. Sådana konflikter måste hanteras och lösas vid utrullning.

## Konflikthantering {#conflict-handling}

När det finns sidor som är i konflikt (i grenarna utkast och Live Copy) kan du ange hur (eller till och med om) de ska hanteras i MSM.

För att säkerställa att utrullningen inte blockeras kan möjliga definitioner omfatta:

* Vilken sida (utkast eller Live Copy) som har prioritet vid utrullning
* Vilka sidor som får nya namn och hur
* Hur detta påverkar publicerat innehåll

Standardbeteendet för Adobe Experience Manager (AEM) är att publicerat innehåll inte påverkas. Om en sida som skapades manuellt i Live Copy-grenen har publicerats, kommer det innehållet fortfarande att publiceras efter konflikthanteringen och utrullningen.

Förutom standardfunktionerna kan anpassade konflikthanterare läggas till för att implementera olika regler. Detta kan även möjliggöra publiceringsåtgärder som en enskild process.

### Exempelscenario {#example-scenario}

I följande avsnitt används ett exempel på den nya sidan `b`, som har skapats både i ritningen och i grenen Live Copy (som har skapats manuellt), för att illustrera olika metoder för konfliktlösning:

* utkast: `/b`

  En mallsida med en underordnad sida, `bp-level-1`

* Live-kopia: `/b`

  En sida som har skapats manuellt i Live Copy-grenen med en underordnad sida, `lc-level-1`

   * Aktiverad vid publicering som `/b`, tillsammans med den underordnade sidan

#### Före utrullning {#before-rollout}

|  | Utskrift före utrullning | Live Copy Before Rolling | Publish före utrullning |
|---|---|---|---|
| Värde | `b` | `b` | `b` |
| Kommentar | Skapat i en designgren, klar för utrullning | Manuellt skapat i Live Copy-grenen | Innehåller innehållet på sidan `b` som skapades manuellt i Live Copy-grenen |
| Värde | `/bp-level-1` | `/lc-level-1` | `/lc-level-1` |
| Kommentar |  | Manuellt skapat i Live Copy-grenen | innehåller innehållet på sidan `child-level-1` som skapades manuellt i grenen Live Copy |

## Utrullningshanteraren och konflikthantering {#rollout-manager-and-conflict-handling}

Med utrullningshanteraren kan du aktivera eller inaktivera konflikthantering.

Detta görs med [OSGi-konfiguration](/help/implementing/deploying/configuring-osgi.md) av **Day CQ WCM Rollout Manager**. Ange värdet **Hantera konflikt med manuellt skapade sidor** ( `rolloutmgr.conflicthandling.enabled`) till true om rollout-hanteraren ska hantera konflikter från en sida som skapats i Live Copy med ett namn som finns i planen.

AEM har [fördefinierat beteende när konflikthantering har inaktiverats](#behavior-when-conflict-handling-deactivated).

## Konflikthanterare {#conflict-handlers}

AEM använder konflikthanterare för att lösa eventuella sidkonflikter som uppstår när innehåll distribueras från en plan till en Live-kopia. Att byta namn på sidor är den vanliga (inte bara) metoden att lösa sådana konflikter. Mer än en konflikthanterare kan vara användbar för att tillåta ett urval av olika beteenden.

AEM tillhandahåller:

* [standardkonflikthanteraren](#default-conflict-handler):
   * `ResourceNameRolloutConflictHandler`
* Möjligheten att implementera en [anpassad hanterare](#customized-handlers)
* Tjänstens rangordningsmekanism som gör att du kan ange prioriteten för varje enskild hanterare
   * Tjänsten med högst rankning används.

### Standardhanterare för konflikter {#default-conflict-handler}

Standardkonflikthanteraren är `ResourceNameRolloutConflictHandler`

* Med den här hanteraren får plantryckssidan företräde.
* Tjänstrankningen för hanteraren är låg. Detta är under standardvärdet för egenskapen `service.ranking` eftersom antagandet är att anpassade hanterare behöver en högre rankning. Rankningen är dock inte den absolut minsta nivån för att garantera flexibilitet vid behov.

Den här konflikthanteraren ger prioritet åt ritningen. Till exempel flyttas Live Copy-sidan `/b` inom Live Copy-grenen till `/b_msm_moved`.

* Live-kopia: `/b`

  Har flyttats i Live-kopian till `/b_msm_moved`. Detta fungerar som en säkerhetskopia och säkerställer att inget innehåll går förlorat.

   * `lc-level-1` flyttas inte.

* Utskrift: `/b`

  Har introducerats på Live Copy-sidan `/b`.

   * `bp-level-1` introduceras i Live Copy.

#### Efter utrullning {#after-rollout}

|  | Utskrift efter utrullning | Live Copy After Rollout | Live Copy After Rollout | Publish efter utrullning |
|---|---|---|---|---|
| Värde | `b` | `b` | `b_msm_moved` | `b` |
| Kommentar |  | Har innehållet på den planerade sidan `b` som har rullats ut | Har innehållet på sidan `b` som skapades manuellt i Live Copy-grenen | Ingen ändring; innehåller innehållet på originalsidan `b` som skapades manuellt i Live Copy-grenen och nu kallas `b_msm_moved` |
| Värde | `/bp-level-1` | `/bp-level-1` | `/lc-level-1` | `/lc-level-1` |
| Kommentar |  |  | Ingen ändring | Ingen ändring |

### Anpassade hanterare {#customized-handlers}

Med anpassade konflikthanterare kan du implementera egna regler. Med servicerangordningsmekanismen kan du även definiera hur de interagerar med andra hanterare.

Anpassade konflikthanterare kan:

* Namnge efter behov.
* Utvecklas/konfigureras enligt dina krav.
   * Du kan t.ex. utveckla en hanterare så att sidan Live-kopia har prioritet.
* Den kan konfigureras med [OSGi-konfigurationen](/help/implementing/deploying/configuring-osgi.md). Särskilt gäller följande:
   * **Tjänstrankning** definierar den ordning som är relaterad till andra konflikthanterare ( `service.ranking`).
      * Standardvärdet är `0`.

### Beteende när Konflikthantering är inaktiverat {#behavior-when-conflict-handling-deactivated}

Om du [inaktiverar konflikthantering](#rollout-manager-and-conflict-handling) manuellt utför AEM ingen åtgärd på sidor som är i konflikt. Sidor som inte är i konflikt rullas ut som förväntat.

>[!CAUTION]
>
>När konflikthantering är inaktiverat ger AEM inga indikationer på att konflikter ignoreras. Eftersom detta beteende i sådana fall måste konfigureras explicit antas det vara det önskade beteendet.

I det här fallet har Live Copy företräde. Den blå sidan `/b` kopieras inte och Live Copy-sidan `/b` lämnas orörd.

* Utskrift: `/b`

  Den kopieras inte alls, men ignoreras.

* Live-kopia: `/b`

  Det förblir likadant.

#### Efter utrullning {#after-rollout-no-conflict}

|  | Utskrift efter utrullning | Live Copy After Rollout | Publish efter utrullning |
|---|---|---|---|
| Värde | `b` | `b` | `b` |
| Kommentar |  | Ingen ändring; har innehållet på sidan `b` som skapades manuellt i Live Copy-grenen | Ingen ändring; innehåller innehållet på sidan `b` som skapades manuellt i Live Copy-grenen |
| Värde | `/bp-level-1,` | `/lc-level-1` | `/lc-level-1` |
| Kommentar |  | Ingen ändring | Ingen ändring |

### Servicerangordning {#service-rankings}

Tjänstrankningen [OSGi](https://www.osgi.org/) kan användas för att definiera prioriteten för enskilda konflikthanterare.
