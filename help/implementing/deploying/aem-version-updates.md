---
title: Uppdateringar av AEM
description: Lär dig hur AEM as a Cloud Service använder kontinuerlig integrering och leverans (CI/CD) för att hålla dina projekt uppdaterade med den senaste versionen.
feature: Deploying
exl-id: 36989913-69db-4f4d-8302-57c60f387d3d
source-git-commit: 7cdbda468221c42325a957131c6817c9f85a574a
workflow-type: tm+mt
source-wordcount: '801'
ht-degree: 1%

---


# Uppdateringar av AEM {#aem-version-updates}

Lär dig hur AEM as a Cloud Service använder kontinuerlig integrering och leverans (CI/CD) för att hålla dina projekt uppdaterade med den senaste versionen.

## CI/CD {#ci-cd}

AEM as a Cloud Service använder kontinuerlig integrering och kontinuerlig leverans (CI/CD) för att säkerställa att dina projekt finns i den senaste AEM versionen. Den här processen uppdaterar dina produktions-, staging- och utvecklingsinstanser utan att störa användarna.

Innan instanserna uppdateras automatiskt kommer en ny AEM att publiceras 3-5 dagar i förväg. Under den här perioden kan du välja att [aktivera manuella uppdateringar för dina utvecklingsinstanser](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment).När tiden är slut tillämpas versionsuppdateringar automatiskt i dina utvecklingsmiljöer först. Om uppdateringen lyckas fortsätter den till din scen och dina produktionsinstanser. Utvecklings- och mellanlagringsinstanserna fungerar som en automatiserad kvalitetsport, där dina anpassade tester utförs innan uppdateringen tillämpas i produktionsmiljön.

>[!NOTE]
>
> Obs! De automatiska uppdateringarna för utvecklingsmiljöer kommer att aktiveras successivt under 2023 för alla kunder. Om utvecklingsmiljöerna inte uppdateras automatiskt kan du använda manuella uppdateringar för att synkronisera dem med scen- och produktionsmiljöerna.


## Typ av uppdateringar {#update-types}

Det finns två typer AEM versionsuppdateringar:

* **AEM underhållsuppdateringar**

   * Kan släppas dagligen.
   * Är främst avsedda för underhåll, inklusive de senaste felkorrigeringarna och säkerhetsuppdateringarna.
   * Påverkar inte särskilt mycket eftersom ändringarna tillämpas regelbundet.

* **Nya funktioner**

   * släpps på en [förutsägbart månadsschema.](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)

## Uppdateringsfel {#update-failure}

AEM uppdateringar genomgår en intensiv och helt automatiserad produktvalideringsplan som omfattar flera steg, vilket säkerställer att ingen tjänst avbryts för system i produktionen. Hälsokontroller används för att övervaka programmets hälsa. Om dessa kontroller misslyckas under en AEM as a Cloud Service uppdatering fortsätter inte releasen och Adobe undersöker varför uppdateringen orsakade detta oväntade beteende.

När du distribuerar en ny version av en anpassad kod för dina miljöer, [Funktionstester för produkter och anpassade](/help/implementing/cloud-manager/overview-test-results.md#functional-testing) spela en viktig roll för att säkerställa att produktionssystemen förblir stabila och fungerar även efter det att en ändring har gjorts. De här testerna används också i uppdateringsprocessen för AEM.

Om uppdateringen till produktionsmiljön misslyckas kommer Cloud Manager automatiskt att återställa testmiljön. Detta görs automatiskt för att säkerställa att både testnings- och produktionsmiljöerna finns i samma AEM när uppdateringen är klar.
På samma sätt kommer mellanlagrings- och produktionsmiljöer inte att uppdateras om en automatisk uppdatering av en utvecklingsmiljö misslyckas.

>[!NOTE]
>
>Om anpassad kod flyttades till staging och inte till produktion, kommer nästa AEM att ta bort dessa ändringar för att återspegla Git-taggen för den senaste lyckade kundreleasen till produktion. Därför måste den anpassade koden som bara var tillgänglig för mellanlagring distribueras igen.

## Bästa praxis {#best-practices}

* **Användning av scenmiljö**
* Använd en annan miljö (inte Stage) för långa QA-/UAT-cykler.
* När sanitetstestningen är klar på scenen går du vidare till Production.

* **Produktionspipeline**
* Pausa innan du distribuerar till Produktion.
* Om du avbryter pipelinen efter en scendistribution anges att koden är&quot;en eliminering&quot; och inte en giltig kandidat för produktion, se [Konfigurera en produktionspipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md).

* **Icke-produktionsförlopp**
* Konfigurera [Icke-produktionsförlopp](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#full-stack-code).
* Snabbare leverans/frekvens vid produktionsfel.  Identifiera problem i icke-producerade rörledningar genom att aktivera produktfunktionstestning, anpassad funktionstestning och anpassad gränssnittstestning.

* **Innehållskopia**
* Använd [Innehållskopia](/help/implementing/developing/tools/content-copy.md) om du vill flytta liknande innehållsuppsättningar till en icke-produktiv miljö.

* **Automatiserad funktionstestning**
* Inkludera automatiserad testning i pipeline för att testa kritisk funktionalitet.
* [Funktionstestning av kund](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing) och [Anpassade gränssnittstestningar](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing) blockerar, om de misslyckas kommer AEM inte att lanseras.

## Regression {#regression}

Om du stöter på ett problem som rör regression, ber vi dig ta upp ett supportärende via Admin Console.  Om problemet är blockerat och påverkar produktionen bör ett P1-fel uppstå.  Ange alla detaljer som krävs för att återskapa regressionsproblemet.

## Sammansatt nodarkiv {#composite-node-store}

I de flesta fall medför uppdateringarna inga driftavbrott, inklusive för redigeringsinstansen, som är ett kluster med noder. Rullande uppdateringar är möjliga på grund av [funktionen för lagring av sammansatta noder i Oak.](https://jackrabbit.apache.org/oak/docs/nodestore/compositens.html)

Med den här funktionen kan AEM referera till flera databaser samtidigt. I en [Driftsättning av rullande materiel.](/help/implementing/deploying/overview.md#how-rolling-deployments-work) den nya AEM-versionen innehåller en egen `/libs` (den tjärMK-baserade oföränderliga databasen), som skiljer sig från den äldre AEM, även om båda refererar till en delad DocumentMK-baserad mutable-databas som innehåller områden som `/content` , `/conf` , `/etc` och andra.

Eftersom både den gamla och den nya versionen har sina egna versioner av `/libs`kan de båda vara aktiva under den rullande uppdateringen och båda kan ta trafik tills den gamla är helt ersatt med den nya.
