---
title: Migrering till AEM Commerce integration framework (CIF)
description: Så här migrerar du till AEM Commerce integration framework (CIF)-tillägget från en gammal version
exl-id: 0db03a05-f527-4853-b52f-f113bce929cf
feature: Commerce Integration Framework
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---

# Migreringsguide för Experience Manager Cloud Servicen {#cif-migration}

Den här guiden hjälper dig att identifiera de områden du behöver uppdatera för migrering av Experience Manager Cloud Service.

## CIF

För Experience Manager as a Cloud Service är CIF-tillägget den enda e-handelslösningen som stöds för Adobe Commerce och e-handelslösningar från tredje part. Tillägget CIF driftsätts automatiskt för kunder i Experience Manager as a Cloud Service, och ingen manuell driftsättning behövs. Se [Komma igång med AEM Commerce as a Cloud Service](getting-started.md).

Om du vill ha stöd för projekt som distribueras CIF Adobe tillhandahåller du [AEM CIF kärnkomponenter](https://github.com/adobe/aem-core-cif-components).

CIF är tillgängligt för AEM 6.5 och via [Programdistributionsportalen](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). Den är kompatibel och innehåller samma funktioner som CIF för Experience Manager as a Cloud Service - inga justeringar krävs.

Klassisk CIF med sina beroenden är inte längre tillgänglig. Kod som är beroende av den här CIF versionen med `com.adobe.cq.commerce.api` Java API:er måste justeras till CIF och dess principer.

Den tidigare tillgängliga CIF-kopplingen kan inte installeras längre. Kod som är beroende av den här kopplingen måste justeras till CIF och dess principer.

## Projektstruktur

Lär dig [AEM projektstruktur](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) och egenskaperna för AEM as a Cloud Service. Anpassa projektinställningarna till AEM as a Cloud Service layout.
Jämfört med AEM 6.5-distributioner finns det två huvudsakliga skillnader här:

* GraphQL-klientens OSGI-paket **får inte** längre inkluderas i AEM, det distribueras via CIF.
* OSGI-konfigurationer för GraphQL-klienten och Graphql-datatjänsten **får inte** längre inkluderas i AEM

>[!TIP]
>
>Kolla in projektet [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia) på GitHub. Detta projekt innehåller Maven-profiler för AEM as a Cloud Service och anläggningsdistributioner som tar hänsyn till de olika ramverksvillkoren.

## Produktkatalog

Import av produktkatalogdata stöds inte längre. Med hjälp av CIF tilläggsobjekt kan produkt- och katalogförfrågningar on demand skickas via realtidsanrop till en extern e-handelslösning. Gå till kapitlet Integrating för att lära dig mer om att integrera en e-handelslösning.

>[!TIP]
>
>Om det inte finns några API:er i realtid bör en extern produktcache med API:er användas för integreringen. Exempel: [Magento öppen källkod](https://business.adobe.com/products/magento/open-source.html).

## Produktkatalogupplevelser med AEM rendering

Om du använder katalogutkast med klassiska CIF måste du uppdatera produktkatalogarbetsflödet. Tillägget CIF renderar nu produktkataloger direkt med hjälp AEM katalogmallar. Du behöver inte längre replikera produktdata eller produktsidor.

## Data och shoppinginteraktion som inte är tillgängliga

Begäranden på klientsidan om icke-cachelagrade data och interaktioner (t.ex. tillägg i kundvagnen, sökning) ska gå direkt till slutpunkten för e-handeln (antingen e-handelslösningen eller integreringslagret) via CDN/Dispatcher. Ta bort alla samtal där AEM bara var en proxy.
