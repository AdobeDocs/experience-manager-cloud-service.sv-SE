---
title: Introduktion till sandlådeprogram
description: Lär dig vilka sandlådeprogram som skiljer sig från produktionsprogram.
exl-id: 4606590c-6826-4794-9d2e-5548a00aa2fa
source-git-commit: ca849bd76e5ac40bc76cf497619a82b238d898fa
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---


# Introduktion till sandlådeprogram {#sandbox-programs}

Lär dig vilka sandlådeprogram som skiljer sig från produktionsprogram.

## Introduktion {#introduction}

Ett sandlådeprogram skapas vanligtvis för att användas för utbildning, löpande demonstrationer, aktivering eller konceptbevis (POC) och är därför inte avsett för livstrafik.

Ett sandlådeprogram är ett av de två tillgängliga programmen i AEM Cloud Service, och det andra är ett [produktionsprogram.](introduction-production-programs.md) Se dokumentet [Program och programtyper](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) om du vill veta mer om programtyper.

## Automatiskt skapande {#auto-creation}

I sandlådeprogram skapas automatiskt. När du skapar ett nytt sandlådeprogram Cloud Manager automatiskt:

* Lägger till AEM Sites och AEM Assets som lösningar i programmet.
* Ställer in en projekt-Git-databas med ett exempelprojekt baserat på [AEM Project Archetype.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)
* Skapar en utvecklingsmiljö.
* Skapar en icke-produktionspipeline som distribueras till utvecklingsmiljön.

Ett sandlådeprogram har bara en utvecklingsmiljö.

## Begränsningar och villkor {#limitations}

Eftersom de inte är avsedda för direkttrafik har sandlådeprogram vissa begränsningar och villkor för användningen, vilket skiljer dem från produktionsprogrammen.

### Ingen Live-trafik {#live-traffic}

Sandlådeprogram är inte avsedda att bära trafik i realtid och omfattas därför inte av [AEM as a Cloud Service åtaganden.](https://www.adobe.com/legal/service-commitments.html)

### Ingen autoskalning {#auto-scaling}

Miljöer som skapas i ett sandlådeprogram är inte konfigurerade för automatisk skalning. Därför är dessa miljöer inte lämpliga för prestanda- eller belastningstestning.

### Inga anpassade domäner eller IP-Tillåtelselista {#ip-allow}

Anpassade domäner och IP-tillåtelselista är inte tillgängliga i sandlådeprogram.

### Inget avancerat nätverk {#advanced-networking}

[Avancerade nätverksfunktioner](/help/security/configuring-advanced-networking.md) (till exempel självbetjäning för VPN, portar som inte är standard, dedikerade IP-adresser för utgångar osv.) är inte tillgängliga i sandlådeprogram.

### Manuella AEM {#updates}

AEM uppdateras inte automatiskt i sandlådeprogram, men kan tillämpas manuellt i miljöer i ditt sandlådeprogram.

* En manuell uppdatering kan bara köras när målmiljön har en korrekt konfigurerad pipeline.
* En manuell uppdatering av antingen en produktions- eller staging-miljö uppdaterar automatiskt den andra. Miljöuppsättningen Production+Stage måste finnas i samma AEM.

Se dokumentet [AEM versionsuppdateringar](/help/implementing/deploying/aem-version-updates.md) för mer information.

Se dokumentet [Uppdaterar miljö](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment) för att lära dig hur man uppdaterar en miljö.

### Viloläge och borttagning {#hibernation}

Miljöer i ett sandlådeprogram försätts automatiskt i viloläge efter 8 timmars inaktivitet. När de har tagits i viloläge kan de tas bort manuellt.

Sandlådeprogram tas bort efter sex månader eftersom de är i viloläge, och därefter kan de återskapas.

Se [Viloläge och avvänjningsmiljöer för sandlådor](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/hibernating-environments.md) för mer information.
