---
title: Migrering till tillägget AEM Commerce Integration Framework (CIF)
description: Så här migrerar du till CIF-tillägget (AEM Commerce Integration Framework) från en gammal version
exl-id: 0db03a05-f527-4853-b52f-f113bce929cf
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 0%

---

# Migreringsguide för Experience Manager Cloud Servicen {#cif-migration}

Den här guiden hjälper dig att identifiera de områden du behöver uppdatera för migrering av Experience Manager Cloud Service.

## CIF-tillägg

För Experience Manager som Cloud Service är CIF-tillägget den enda handelslösningen som stöds för Adobe Commerce och e-handelslösningar från tredje part. CIF-tillägget distribueras automatiskt till kunder på Experience Manager som Cloud Service, och ingen manuell driftsättning behövs. Se [Komma igång med AEM Commerce som en Cloud Service](getting-started.md).

För att stödja projekt som distribuerar CIF Adobe ska du tillhandahålla [AEM CIF Core Components](https://github.com/adobe/aem-core-cif-components).

CIF-tillägg är tillgängligt för AEM 6.5 och via [portalen för programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). Den är kompatibel och har samma funktioner som CIF-tillägget för Experience Manager som en Cloud Service - inga justeringar krävs.

Klassisk CIF med sina beroenden är inte längre tillgänglig. Kod som använder denna CIF-version med `com.adobe.cq.commerce.api` Java API:er måste justeras till CIF-tillägget och dess principer.

Den tidigare tillgängliga CIF-kopplingen kan inte installeras längre. Kod som är beroende av den här kopplingen måste justeras till CIF-tillägget och dess principer.

## Projektstruktur

Lär dig [AEM projektstruktur](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) och AEM egenskaper som en Cloud Service. Anpassa projektinställningarna till AEM som en Cloud Service layout.
Jämfört med AEM 6.5-distributioner finns det två huvudsakliga skillnader här:

* OSGI-paketet **för GraphQL-klienten får inte** längre inkluderas i AEM, det distribueras via CIF-tillägget
* OSGI-konfigurationer för GraphQL-klienten och Graphql Data Service **får inte** längre inkluderas i AEM

>[!TIP]
>
>Kolla in projektet [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia) på GitHub. Detta projekt innehåller Maven-profiler för AEM som Cloud Service och lokal driftsättning som tar hänsyn till de olika ramverksvillkoren.

## Produktkatalog

Import av produktkatalogdata stöds inte längre. Med CIF-tilläggsobjekt används produkt- och katalogbegäranden på begäran via realtidsanrop till en extern handelslösning. Gå till kapitlet Integrating för att lära dig mer om att integrera en e-handelslösning.

>[!TIP]
>
>Om det inte finns några API:er i realtid bör en extern produktcache med API:er användas för integreringen. Exempel [Magento öppen källkod](https://magento.com/products/magento-open-source).

## Produktkatalogupplevelser med AEM rendering

Om du använder katalogutkast med klassisk CIF måste du uppdatera arbetsflödet för produktkatalogen. Tillägget CIF återger nu produktkatalogupplevelser direkt med hjälp AEM katalogmallar. Du behöver inte längre replikera produktdata eller produktsidor.

## Data och shoppinginteraktion som inte är tillgängliga

Klientförfrågningar om icke-cachelagrade data och interaktioner (t.ex. tillägg i kundvagnen, sökning) ska gå direkt till slutpunkten för e-handeln (antingen e-handelslösningen eller integreringslagret) via CDN/Dispatcher. Ta bort alla samtal där AEM bara var en proxy.
