---
title: Migrering till tillägget AEM Commerce Integration Framework (CIF)
description: Så här migrerar du till CIF-tillägget (AEM Commerce Integration Framework) från en gammal version
exl-id: 0db03a05-f527-4853-b52f-f113bce929cf
source-git-commit: 47910a27118a11a8add6cbcba6a614c6314ffe2a
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 0%

---

# Migreringsguide för Experience Manager Cloud Servicen {#cif-migration}

Den här guiden hjälper dig att identifiera de områden du behöver uppdatera för migrering av Experience Manager Cloud Service.

## CIF-tillägg

För Experience Manager as a Cloud Service är CIF-tillägget den enda handelslösningen som stöds för Adobe Commerce och tredjepartslösningar för e-handel. CIF-tillägget distribueras automatiskt till kunder på Experience Manager as a Cloud Service, och ingen manuell driftsättning behövs. Se [Komma igång med AEM Commerce as a Cloud Service](getting-started.md).

Att stödja projekt som distribuerar CIF Adobe tillhandahåller [AEM CIF-kärnkomponenter](https://github.com/adobe/aem-core-cif-components).

CIF-tillägg finns för AEM 6.5 och via [Programdistributionsportal](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). Den är kompatibel och har samma funktioner som CIF-tillägget för Experience Manager as a Cloud Service - inga justeringar krävs.

Klassisk CIF med sina beroenden är inte längre tillgänglig. Kod som förlitar sig på den här CIF-versionen med `com.adobe.cq.commerce.api` Java-API:er måste justeras till CIF-tillägget och dess principer.

Den tidigare tillgängliga CIF-kopplingen kan inte installeras längre. Kod som är beroende av den här kopplingen måste justeras till CIF-tillägget och dess principer.

## Projektstruktur

Lär dig [AEM projektstruktur](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) och egenskaperna hos AEM as a Cloud Service. Anpassa projektinställningarna till den AEM as a Cloud Service layouten.
Jämfört med AEM 6.5-distributioner finns det två huvudsakliga skillnader här:

* GraphQL-klientens OSGI-paket **får inte** längre inkluderas i AEM, distribueras det via CIF-tillägget
* OSGI-konfigurationer för GraphQL-klient och Graphql Data Service **får inte** längre ingå i AEM

>[!TIP]
>
>Kolla in [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia) på GitHub. Detta projekt innehåller Maven-profiler för AEM as a Cloud Service och lokala driftsättningar som tar hänsyn till de olika ramverksvillkoren.

## Produktkatalog

Import av produktkatalogdata stöds inte längre. Med CIF-tilläggsobjekt används produkt- och katalogbegäranden på begäran via realtidsanrop till en extern handelslösning. Gå till kapitlet Integrating för att lära dig mer om att integrera en e-handelslösning.

>[!TIP]
>
>Om det inte finns några API:er i realtid bör en extern produktcache med API:er användas för integreringen. Exempel [Magento öppen källkod](https://business.adobe.com/products/magento/open-source.html).

## Produktkatalogupplevelser med AEM rendering

Om du använder katalogutkast med klassisk CIF måste du uppdatera arbetsflödet för produktkatalogen. Tillägget CIF återger nu produktkatalogupplevelser direkt med hjälp AEM katalogmallar. Du behöver inte längre replikera produktdata eller produktsidor.

## Data och shoppinginteraktion som inte är tillgängliga

Begäranden på klientsidan om icke-cachelagrade data och interaktioner (t.ex. tillägg i kundvagnen, sökning) ska gå direkt till slutpunkten för e-handeln (antingen e-handelslösningen eller integreringslagret) via CDN/Dispatcher. Ta bort alla samtal där AEM bara var en proxy.
