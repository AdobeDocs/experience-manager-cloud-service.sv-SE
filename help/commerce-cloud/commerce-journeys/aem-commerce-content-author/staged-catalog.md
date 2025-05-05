---
title: Hantera testade produktkataloger
description: Lär dig hur du hanterar upplevelser i mellanlagrade produktkataloger.
exl-id: 1db18818-b8e0-4127-8a65-dc3dea1f2927
feature: Commerce Integration Framework
role: Admin
source-git-commit: f172f514eaa8f1337359f00fad964f5781fba769
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 0%

---

# Bygger testversioner av produktkataloger {#building-experiences}

Lär dig hur du hanterar upplevelser i mellanlagrade produktkataloger.

## Story hittills {#story-so-far}

I det föregående dokumentet om AEM och Commerce-resan, [Hantera produktkatalogsidor och mallar](catalog-templates.md), lärde du dig att hantera och skapa produktkatalogsupplevelser baserat på mallar.

Den här artikeln bygger på dessa grunder.

## Syfte {#objective}

Det här dokumentet hjälper dig att förstå hur du hanterar produktkatalogsupplevelser baserat på mellanlagrade produktdata och AEM. Många gånger måste man förbereda parallella och kommande program (till exempel en ny klädsamling). Detta kräver åtkomst till testade produktdata (inte live än) och möjlighet att förbereda innehållet. Det nya innehållet kommer att publiceras när produkten lanseras.

>[!NOTE]
>
>Den här funktionen är endast tillgänglig med Adobe Commerce eller Cloud Edition och tredjepartsanslutningar som stöder tokenbaserad autentisering. Mer information finns i [Komma igång](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content-and-commerce/storefront/getting-started.html?lang=sv-SE).

Först ska vi se hur författare kan få åtkomst till testade produktdata med CIF.

## Arbeta med mellanlagrade produktdata {#staged-product-data}

Ett sätt att få tillgång till testade produktdata är att använda produktcockpiten. Öppna produktkatalogen genom att klicka på ikonen Commerce i AEM. Detta ger er tillgång till liveproduktdata. Öppna filterfliken till vänster och expandera **STAGED CATALOG**. Med hjälp av förhandsgranskningsdata kan du nu komma åt testproduktdata när som helst. Mellanlagrade data innehåller nya kategorier, produkter eller uppdaterade fält som pris.

![stage cockpit](assets/staged-cockpit.png)

Det går att förhandsgranska en butik med mellanlagrade data i vyn för tidsförvrängning. Öppna redigeraren och växla läge till timewarp. Välj ett framtida datum. Observera informationen ovanför redigeraren om att du visar sidan ett visst datum.

![tidsförvrängning för scenen](assets/staged-timewarp.png)

Nu kan du bläddra i katalogen med mellanlagrade data. Om du öppnar en mellanlagrad kategori eller produktsida visas en visuell indikator.

![stage plp](assets/staged-plp.png)

>[!NOTE]
>
>Omnisearch har inget sammanhang och returnerar därför bara liveproduktkatalogdata

## AEM {#launches}

Med AEM Launches kan du skapa innehåll för mellanlagrade produktdata. Om du inte är bekant med Launches, följ dokumentationslänken under avsnittet [Ytterligare resurser](#additional-resources). Startdatumet används sedan för att komma åt testproduktsdata.

![scenstart](assets/staged-launch.png)

Observera att väljarna respekterar startdatumet med den mellanlagrade indikatorn till höger.

![scenväljare](assets/staged-picker.png)

## What&#39;s Next {#what-is-next}

Nu när du är klar med den här delen av resan bör du:

* förstå begreppen för mellanlagrad produktkatalog och innehåll med Launches
* kunna komma åt data i mellanlagrade produktkataloger via produktcockpit och redigerare

Du kan nu hantera [produktupplevelser](product-experience-management.md). AEM och Commerce har dock många ytterligare alternativ. Ta en titt på några av de ytterligare resurser som är tillgängliga i avsnittet [Ytterligare resurser](#additional-resources) om du vill veta mer om de funktioner du såg under den här resan.

## Ytterligare resurser {#additional-resources}

* [Product Cockpit](/help/commerce-cloud/authoring/product-cockpit.md)
* [Komma igång](/help/commerce-cloud/getting-started.md)
* [Launches](/help/sites-cloud/authoring/launches/overview.md)
