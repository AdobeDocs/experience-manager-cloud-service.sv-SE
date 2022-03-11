---
title: AEM versionsuppdateringar
description: 'AEM versionsuppdateringar '
feature: Deploying
exl-id: 36989913-69db-4f4d-8302-57c60f387d3d
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 5%

---

# AEM versionsuppdateringar {#aem-version-updates}

## Introduktion {#introduction}

AEM as a Cloud Service använder nu Continuous Integration och Continuous Delivery (CI/CD) för att säkerställa att dina projekt har den senaste AEM versionen. Det innebär att instanser av Production och Stage uppdateras till den senaste AEM utan att tjänsten avbryts för användarna.

>[!NOTE]
>Om uppdateringen till produktionsmiljön misslyckas kommer Cloud Manager automatiskt att återställa scenmiljön. Detta görs automatiskt för att säkerställa att både fas- och produktionsmiljöer har samma AEM när uppdateringen är klar.

AEM versionsuppdateringar är av två typer:

* **AEM Push-uppdateringar**

   * Kan släppas dagligen.

   * Mest underhållet, inklusive de senaste felkorrigeringarna och säkerhetsuppdateringarna.

      Eftersom ändringarna utförs regelbundet blir effekten inkrementell vilket minskar påverkan på tjänsten.

* **Nya funktionsuppdateringar**

   * Frisläppt via ett förutsägbart månadsschema.

AEM uppdateringar genomgår en intensiv och helt automatiserad produktvalideringsplan som omfattar flera steg, vilket säkerställer att ingen tjänst avbryts för system i produktionen. Hälsokontroller används för att övervaka programmets hälsa. Om dessa kontroller misslyckas under en AEM as a Cloud Service uppdatering fortsätter inte releasen och Adobe undersöker varför uppdateringen orsakade detta oväntade beteende.

[Produkttester och kundfunktionstester](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/understand-test-results.html#functional-testing) som förhindrar att produktuppgraderingar och kundkodspush bryter produktionen valideras också under en AEM versionsuppdatering.

>[!NOTE]
>
>Om anpassad kod publicerades till mellanlagring och sedan avvisades av dig, kommer nästa AEM att ta bort dessa ändringar för att återspegla Git-taggen för den senaste lyckade kundreleasen till produktionen.

## Sammansatt nodarkiv {#composite-node-store}

Som vi nämnt ovan kommer uppdateringarna i de flesta fall att innebära noll driftavbrott, även för författaren, som är ett kluster med noder. Rullande uppdateringar är möjliga på grund av *sammansatt nodarkiv* i Oak.

Med den här funktionen kan AEM referera till flera databaser samtidigt. I en rullande driftsättning innehåller den nya versionen av Green AEM en egen `/libs` (den tjärMK-baserade oföränderliga databasen), som skiljer sig från den äldre blå AEM-versionen, även om båda refererar till en delad DocumentMK-baserad mutable-databas som innehåller områden som `/content` , `/conf` , `/etc` och andra. Eftersom både den blå och den gröna har sina egna versioner av `/libs`kan de båda vara aktiva under den rullande uppdateringen, som båda tar på trafik tills det blå ersätts helt av det gröna.
