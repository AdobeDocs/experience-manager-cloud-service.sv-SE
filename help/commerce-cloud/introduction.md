---
title: Introduktion och översikt
description: Förstå de olika alternativen för butiker
thumbnail: introducing-aem-commerce.jpg
exl-id: 29410f76-a63f-4b0a-b817-2ed724ad1a3c
feature: Commerce Integration Framework
role: Admin
source-git-commit: 145cd4961bd9c0c7bb7e39a1d6dae67f240ecb4d
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 0%

---


# Innehåll och Commerce {#content-commerce}

I takt med att kundernas förväntningar på intent-baserade och högpresterande handelsupplevelser ökar, pressas varumärkena att leverera mer innehåll snabbare utan att ge avkall på kvaliteten. Med Adobe Experience Manager kan varumärken skala och förnya sig snabbare för att skapa engagerande e-handelsupplevelser och få mer trafik och ökade webbutgifter.

Adobe Experience Manager har kraftfulla verktyg för att skapa och hantera innehållsrika, personaliserade kundupplevelser. Genom att integrera AEM med en e-handelslösning - som Adobe Commerce, Salesforce Commerce, SAP Commerce Cloud eller någon annan lösning - kan varumärken sammanföra innehåll och handel för att leverera sömlösa kundresor över olika kanaler.

## Översikt över butiksstrategier {#overview}

AEM kan ge support baserat på din situation och dina önskemål. Använd följande vägledning för att välja rätt metod för dig:

* [Använd Edge Delivery Services (rekommenderas)](#edge)
* [Använd din egen butik (headless AEM integration)](#own-storefront)
* [Använd AEM CIF store](#cif)

### Använd Edge Delivery Services (rekommenderas) {#edge}

Om ditt företag vill ha den snabbaste och mest AI-vänliga butiken på webben och dina utvecklare vill ha en toppmodern utvecklarupplevelse använder du [Edge Delivery Services.](../edge/overview.md) Edge Delivery Services uppfyller alla dagens och morgondagens krav. Beroende på vår serverdel och lösning har du olika alternativ:

#### &#x200B;1. Integrering med Adobe Commerce as a Cloud Service {#acaacs}

Det här är den perfekta lösningen om du använder Edge Delivery och [Adobe Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/) som utgångspunkt. I butiken finns en standardmall som är förintegrerad med Adobe Commerce-tjänster, API:er och en mängd olika Commerce-komponenter för att snabbt skapa en butiksskylt.

Bra passform: En typisk butiksupplevelse med Adobe Commerce as a Cloud Service

#### &#x200B;2. Integrering med Adobe Commerce Optimizer (för alla tredjepartslösningar) {#aco}

Om du vill integrera din befintliga e-handelslösning och öka katalogens prestanda rekommenderar Adobe att du använder [Adobe Commerce Optimizer](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-commerce-optimizer/overview) som det moderna integreringslagret. Commerce Optimizer förbättrar er e-handelslösning med högpresterande SaaS-tjänster för katalog och marknadsföring. Precis som med Adobe Commerce as a Cloud Service fungerar [Adobe Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/) direkt med programmet.

Det finns integreringar med lösningar för kommersiell handel som Salesforce Commerce. Tala med din Adobe-representant.

Bra passform: En typisk butiksupplevelse med en befintlig e-handelslösning

#### &#x200B;3. Anpassad integrering {#custom}

Adobe rekommenderar också att du använder Edge Delivery Services om du vill skapa en anpassad integrering. Du kan antingen börja från början eller återanvända befintliga e-handelskomponenter i JS-ramverket (t.ex. för transaktionsdelen) i din Edge Delivery-butik. På så sätt får era kunder en blixtsnabb shoppingupplevelse som är autentisk, samtidigt som ni kan återanvända era befintliga investeringar för att öka TV:n. Startpunkten är [Edge Delivery-standardmallen](https://www.aem.live/developer/tutorial).

Bra passform: Lågt värde från Edge Deliery Store

### Använd din egen butik (integrering med Headless AEM) {#own-storefront}

Du har en befintlig butik (t.ex. byggd med React JS) och vill använda Adobe Experience Manager för innehållshantering och leverans (Content Fragments), resurser och sammanhangsbaserad redigering (Universal Editor). Startpunkten för en integrering är [Introduktion till Adobe Experience Manager som Headless CMS](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/headless/introduction) och [CIF-tillägget](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/content-and-commerce/storefront/authoring/enrich-product-associated-content). CIF-tillägget möjliggör en smidig integrering av dina produktdata i AEM (sök, bläddra och hitta produkter i AEM användargränssnitt) som du kan använda för att skapa e-handelsspecifika upplevelser.

### AEM CIF store {#cif}

Adobe rekommendationer och referensarkitektur är att använda Edge Delivery Services. CIF storefront med sina AEM CIF Core Components är nu i underhållsläge och bör inte användas i nya projekt. Mer information finns i [CIF-dokumentationen.](/help/commerce-cloud/cif-introduction.md)

>[!NOTE]
>
>Befintliga kunder som vill utnyttja nya funktioner i AEM/Commerce bör flytta sin webbplats till Edge Delivery. Ett vanligt mönster är att börja med att bara flytta en delmängd av sidor till Edge Delivery och köra Edge Deliery- och CIF-sidor sida vid sida. Det går också att ersätta AEM CIF-komponenter med de nya [Commerce-komponenterna](https://experienceleague.adobe.com/developer/commerce/storefront/dropins/all/introduction/) för att utnyttja de nya funktionerna i Commerce.
