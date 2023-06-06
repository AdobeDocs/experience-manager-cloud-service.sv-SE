---
title: AEM versionsuppdateringar
description: Lär dig hur AEM as a Cloud Service använder kontinuerlig integrering och leverans (CI/CD) för att hålla projekten uppdaterade med den senaste versionen.
feature: Deploying
exl-id: 36989913-69db-4f4d-8302-57c60f387d3d
source-git-commit: dd1560aa4d260320f565ad993a8b3650c3ee5288
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 1%

---


# AEM versionsuppdateringar {#aem-version-updates}

Lär dig hur AEM as a Cloud Service använder kontinuerlig integrering och leverans (CI/CD) för att hålla projekten uppdaterade med den senaste versionen.

## CI/CD {#ci-cd}

AEM as a Cloud Service använder kontinuerlig integrering och kontinuerlig leverans (CI/CD) för att säkerställa att dina projekt finns i den senaste AEM versionen. Detta innebär att produktions- och mellanlagringsinstanserna uppdateras till den senaste AEM utan avbrott i användarens service.

Versionsuppdateringar tillämpas automatiskt endast på produktions- och mellanlagringsinstanser. [AEM uppdateringar måste tillämpas manuellt på alla andra instanser.](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment)

## Typ av uppdateringar {#update-types}

Det finns två typer AEM versionsuppdateringar:

* **AEM underhållsuppdateringar**

   * Kan släppas dagligen.
   * Är främst avsedda för underhåll, inklusive de senaste felkorrigeringarna och säkerhetsuppdateringarna.
   * Påverkar inte särskilt mycket eftersom ändringarna tillämpas regelbundet.

* **Nya funktionsuppdateringar**

   * släpps på en [förutsägbart månadsschema.](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)

## Uppdateringsfel {#update-failure}

AEM uppdateringar genomgår en intensiv och helt automatiserad produktvalideringsplan som omfattar flera steg, vilket säkerställer att ingen tjänst avbryts för system i produktionen. Hälsokontroller används för att övervaka programmets hälsa. Om dessa kontroller misslyckas under en AEM as a Cloud Service uppdatering fortsätter inte releasen och Adobe undersöker varför uppdateringen orsakade detta oväntade beteende.

[Produkttester och kundfunktionstester,](/help/implementing/cloud-manager/overview-test-results.md#functional-testing) som förhindrar att produktuppgraderingar och kundkodspush bryter mot produktionssystemen valideras också under en AEM versionsuppdatering.

Om uppdateringen till produktionsmiljön misslyckas kommer Cloud Manager automatiskt att återställa testmiljön. Detta görs automatiskt för att säkerställa att både testnings- och produktionsmiljöerna har samma AEM när uppdateringen är klar.

>[!NOTE]
>
>Om anpassad kod flyttades till staging och inte till produktion, kommer nästa AEM att ta bort dessa ändringar för att återspegla Git-taggen för den senaste lyckade kundreleasen till produktion. Därför måste den anpassade koden som bara var tillgänglig för mellanlagring distribueras igen.

## Sammansatt nodarkiv {#composite-node-store}

I de flesta fall medför uppdateringarna inga driftavbrott, inklusive för redigeringsinstansen, som är ett kluster med noder. Rullande uppdateringar är möjliga på grund av [funktionen för lagring av sammansatta noder i Oak.](https://jackrabbit.apache.org/oak/docs/nodestore/compositens.html)

Med den här funktionen kan AEM referera till flera databaser samtidigt. I en [Driftsättning av rullande materiel.](/help/implementing/deploying/overview.md#how-rolling-deployments-work) den nya AEM-versionen innehåller en egen `/libs` (den tjärMK-baserade oföränderliga databasen), som skiljer sig från den äldre AEM, även om båda refererar till en delad DocumentMK-baserad mutable-databas som innehåller områden som `/content` , `/conf` , `/etc` och andra.

Eftersom både den gamla och den nya versionen har sina egna versioner av `/libs`kan de båda vara aktiva under den rullande uppdateringen och båda kan ta trafik tills den gamla är helt ersatt med den nya.
