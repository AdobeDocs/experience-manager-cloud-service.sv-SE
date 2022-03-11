---
title: Hantera testade produktkataloger
description: Lär dig hur du hanterar upplevelser i mellanlagrade produktkataloger.
exl-id: 1db18818-b8e0-4127-8a65-dc3dea1f2927
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 1%

---

# Bygger testversioner av produktkataloger {#building-experiences}

Lär dig hur du hanterar upplevelser i mellanlagrade produktkataloger.

## Story hittills {#story-so-far}

I det föregående dokumentet om AEM- och handelsresan [Hantera sidor och mallar för produktkataloger](catalog-templates.md)lärde du dig att hantera och bygga produktkataloger baserat på mallar.

Den här artikeln bygger på dessa grunder.

## Syfte {#objective}

Det här dokumentet hjälper dig att förstå hur du hanterar produktkatalogsupplevelser baserat på mellanlagrade produktdata och AEM. Många gånger måste man förbereda parallella och kommande program (till exempel en ny klädsamling). Detta kräver åtkomst till testade produktdata (inte live än) och möjlighet att förbereda innehållet. Det nya innehållet kommer att publiceras när produkten lanseras.

    >[!OBS!]
    >
    >Den här funktionen är endast tillgänglig med Adobe Commerce eller Cloud Edition och tredjepartsanslutningar som stöder tokenbaserad autentisering. Mer information finns i [Komma igång](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content-and-commerce/storefront/getting-started.html).

Först ska vi se hur författare kan komma åt testade produktdata med CIF.

## Arbeta med mellanlagrade produktdata {#staged-product-data}

Ett sätt att få tillgång till testade produktdata är att använda produktcockpit. Öppna produktkatalogen genom att klicka på Commerce-ikonen på AEM huvudmeny. Detta ger er tillgång till liveproduktdata. Öppna filterfliken till vänster och expandera **STAGAD KATALOG**. Med hjälp av förhandsgranskningsdata kan du nu komma åt testproduktdata när som helst. Mellanlagrade data innehåller nya kategorier, produkter eller uppdaterade fält som pris.

![scen cockpit](assets/staged-cockpit.png)

Det går att förhandsgranska en butik med mellanlagrade data i vyn för tidsförvrängning. Öppna redigeraren och växla läge till timewarp. Välj ett framtida datum. Observera informationen ovanför redigeraren om att du visar sidan ett visst datum.

![timewarp för scenen](assets/staged-timewarp.png)

Nu kan du bläddra i katalogen med mellanlagrade data. Om du öppnar en mellanlagrad kategori eller produktsida visas en visuell indikator.

![stage plp](assets/staged-plp.png)

    >[!OBS!]
    >
    >Omnisearch har inget sammanhang och returnerar därför endast liveproduktkatalogdata

## AEM {#launches}

Med AEM Launches kan du skapa innehåll för mellanlagrade produktdata. Om du inte är bekant med Launches, följ dokumentationslänken under [Avsnittet Ytterligare resurser](#additional-resources). Startdatumet används sedan för att komma åt testproduktsdata.

![start av scenen](assets/staged-launch.png)

Observera att väljarna respekterar startdatumet med den mellanlagrade indikatorn till höger.

![scenväljare](assets/staged-picker.png)

## What&#39;s Next {#what-is-next}

Nu när du är klar med den här delen av resan bör du:

* förstå begreppen för mellanlagrad produktkatalog och innehåll med Launches
* kunna komma åt data i mellanlagrade produktkataloger via produktcockpit och redigerare

Du är nu redo att hantera [produktupplevelser](product-experience-management.md). AEM Innehåll och handel har dock många ytterligare alternativ. Se vilka ytterligare resurser som finns i [Avsnittet Ytterligare resurser](#additional-resources) om du vill veta mer om de funktioner du såg under den här resan.

## Ytterligare resurser {#additional-resources}

* [Product Cockpit](/help/commerce-cloud/authoring/product-cockpit.md)
* [Komma igång](/help/commerce-cloud/getting-started.md)
* [Launches](/help/sites-cloud/authoring/launches/overview.md)
