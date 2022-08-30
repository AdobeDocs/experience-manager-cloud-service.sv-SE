---
title: AEM versionsuppdateringar
description: 'AEM versionsuppdateringar '
feature: Deploying
exl-id: 36989913-69db-4f4d-8302-57c60f387d3d
source-git-commit: 575be022704e998e63162f19c37ece877efef627
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 2%

---


# AEM versionsuppdateringar {#aem-version-updates}

## Introduktion {#introduction}

AEM as a Cloud Service använder nu kontinuerlig integrering och kontinuerlig leverans (CI/CD) för att säkerställa att dina projekt har den senaste AEM versionen. Detta innebär att produktions- och mellanlagringsinstanser uppdateras till den senaste AEM utan avbrott i användarens service.

>[!NOTE]
>
>Om uppdateringen till produktionsmiljön misslyckas kommer Cloud Manager automatiskt att återställa testmiljön. Detta görs automatiskt för att säkerställa att både testnings- och produktionsmiljöerna har samma AEM när uppdateringen är klar.

Det finns två typer AEM versionsuppdateringar:

* **AEM underhållsuppdateringar**

   * Kan släppas dagligen.
   * Är främst avsedda för underhåll, inklusive de senaste felkorrigeringarna och säkerhetsuppdateringarna.
   * Påverkar inte särskilt mycket eftersom ändringarna tillämpas regelbundet.

* **Nya funktionsuppdateringar**

   * släpps enligt ett förutsägbart månadsschema.

AEM uppdateringar genomgår en intensiv och helt automatiserad produktvalideringsplan som omfattar flera steg, vilket säkerställer att ingen tjänst avbryts för system i produktionen. Hälsokontroller används för att övervaka programmets hälsa. Om dessa kontroller misslyckas under en AEM as a Cloud Service uppdatering fortsätter inte releasen och Adobe undersöker varför uppdateringen orsakade detta oväntade beteende.

[Produkttester och kundfunktionstester,](/help/implementing/cloud-manager/overview-test-results.md#functional-testing) som förhindrar att produktuppgraderingar och kundkodspush bryter mot produktionssystemen valideras också under en AEM versionsuppdatering.

>[!NOTE]
>
>Om anpassad kod publicerades till mellanlagring och sedan avvisades av dig, kommer nästa AEM att ta bort dessa ändringar för att återspegla Git-taggen för den senaste lyckade kundreleasen till produktionen.

## Sammansatt nodarkiv {#composite-node-store}

Uppdateringar medför i de flesta fall inga driftavbrott, inklusive för redigeringsinstansen, som är ett kluster med noder. Rullande uppdateringar är möjliga på grund av den sammansatta nodbutiksfunktionen i Oak.

Med den här funktionen kan AEM referera till flera databaser samtidigt. I en rullande driftsättning innehåller den nya gröna AEM en egen `/libs` (den tjärMK-baserade oföränderliga databasen), som skiljer sig från den äldre blå AEM-versionen, även om båda refererar till en delad DocumentMK-baserad mutable-databas som innehåller områden som `/content` , `/conf` , `/etc` och andra. Eftersom både den blå och den gröna har sina egna versioner av `/libs`kan de båda vara aktiva under den rullande uppdateringen, som båda tar på trafik tills det blå ersätts helt av det gröna.
