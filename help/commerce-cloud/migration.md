---
title: Migrering till tillägget AEM Commerce integration framework (CIF)
description: Migrera till tillägget AEM Commerce integration framework (CIF) från en gammal version
exl-id: 0db03a05-f527-4853-b52f-f113bce929cf
feature: Commerce Integration Framework
role: Admin
index: false
source-git-commit: 173b70aa6f9ad848d0f80923407bf07540987071
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---

# Migreringsguide för Experience Manager Cloud Service {#cif-migration}

Den här guiden hjälper dig att identifiera de områden du behöver uppdatera för migrering från Experience Manager Cloud Service.

## CIF-tillägg

För Experience Manager as a Cloud Service är CIF-tillägget den enda e-handelslösningen som stöds för Adobe Commerce och e-handelslösningar från tredje part. CIF-tillägget distribueras automatiskt till kunder med Experience Manager as a Cloud Service, och ingen manuell driftsättning behövs. Se [Komma igång med AEM Commerce as a Cloud Service](getting-started.md).

Om du vill ha stöd för projekt som distribuerar CIF Adobe tillhandahåller du [AEM CIF Core Components](https://github.com/adobe/aem-core-cif-components).

CIF-tillägg är tillgängligt för AEM 6.5 och via [portalen för programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). Den är kompatibel och innehåller samma funktioner som CIF-tillägget för Experience Manager as a Cloud Service - inga justeringar krävs.

Klassisk CIF med sina beroenden är inte längre tillgänglig. Kod som är beroende av den här CIF-versionen med `com.adobe.cq.commerce.api` Java API:er måste justeras efter CIF-tillägget och dess principer.

Den tidigare tillgängliga CIF-anslutningen kan inte installeras längre. Kod som är beroende av den här kopplingen måste justeras till CIF-tillägget och dess principer.

## Projektstruktur

Lär dig [AEM projektstruktur](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) och egenskaperna för AEM as a Cloud Service. Anpassa projektinställningarna till AEM as a Cloud Service layout.
Jämfört med AEM 6.5 finns det två stora skillnader här:

* GraphQL-klientens OSGI-paket **får inte** längre ingå i AEM-projektet, det distribueras via CIF-tillägget
* OSGI-konfigurationer för GraphQL-klienten och Graphql Data Service **får inte** längre inkluderas i AEM-projektet

>[!TIP]
>
>Kolla in [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia) -projektet på GitHub. Detta projekt innehåller Maven-profiler för AEM as a Cloud Service och anläggningsdistributioner som tar hänsyn till de olika ramverksvillkoren.

## Produktkatalog

Import av produktkatalogdata stöds inte längre. Med CIF-tilläggsobjekt kan man vid behov begära produkter och kataloger via realtidsanrop till en extern handelslösning. Gå till kapitlet Integrating för att lära dig mer om att integrera en e-handelslösning.

>[!TIP]
>
>Om det inte finns några API:er i realtid bör en extern produktcache med API:er användas för integreringen. Exempel: [Magento öppen källkod](https://business.adobe.com/products/magento/open-source.html).

## Produktkatalogupplevelser med AEM rendering

Om du använder katalogutkast med Classic CIF måste du uppdatera produktkatalogarbetsflödet. CIF-tillägget återger nu produktkatalogupplevelser direkt med AEM katalogmallar. Du behöver inte längre replikera produktdata eller produktsidor.

## Data och shoppinginteraktion som inte är tillgängliga

Begäranden på klientsidan om icke-cachelagrade data och interaktioner (t.ex. tillägg i kundvagnen, sökning) ska gå direkt till slutpunkten för e-handeln (antingen e-handelslösningen eller integreringslagret) via CDN/Dispatcher. Ta bort alla samtal där AEM bara var en proxy.
