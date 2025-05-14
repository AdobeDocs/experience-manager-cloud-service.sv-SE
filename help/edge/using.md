---
title: Använda Edge Delivery Services med AEM
description: Läs om hur AEM as a Cloud Service kan användas med Edge Delivery Services.
feature: Edge Delivery Services
exl-id: 41999302-b4c9-4f5a-b659-6e7398a3c4f4
role: Admin, Architect, Developer
index: false
hide: true
hidefromtoc: true
source-git-commit: e57610e4c5e498ddfdbaa0ba39c9197ecfb5d177
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---


# Använda Edge Delivery Services med AEM {#using-edge}

Edge Delivery Services är fristående från innehållskällan och kan importera innehåll från olika innehållskällor. Det innebär att du kan arbeta med flera olika innehållskällor på samma webbplats med smidig och effektiv publicering oavsett vilken källa du väljer.

Med Edge Delivery Services kan man snabbt skapa utvecklingsmiljöer där man snabbt kan uppdatera och publicera material och snabbt lansera nya webbplatser. Det tar bara några sekunder att gå från redigering till att se innehållet live på internet.

![Innehållskällor för Edge Delivery](assets/content-sources.png)

Inhämtning från olika innehållskällor ger maximal flexibilitet för användaren. Adobe ger vägledning när du ska välja vilka innehållskällor som passar bäst för ditt projekt.

Det finns fall där innehållskällan är fördefinierad eller på annat sätt inte flexibel (projektet kan t.ex. inte använda Sharepoint eller Google Drive). Men i många fall är verktyget inte förberett och valet av verktyg är inte svartvitt.

Adobe vägledande princip är enkel. Börja med dokumentbaserad redigering och lägg till komplexitet vid behov. Om en verktygsändring behövs omfattar AEM Edge Delivery Services-integrering innehållsmigrering.

![Flexibilitet för innehållskälla](assets/content-source-flexiblity.png)

## Redigering {#authoring-edge}

Med Edge Delivery Services är det enkelt, snabbt och flexibelt att skapa. Du kan välja att redigera med hjälp av dokumentbaserad redigering eller WYSIWYG-redigering med den universella redigeraren.

Mer information finns i dokumentet [Skapa innehåll för Edge Delivery Services](/help/edge/wysiwyg-authoring/authoring.md).

## Publicering {#publishing-edge}

Med Edge Delivery Services är det smidigt att publicera innehåll oavsett innehållskälla.

Mer information finns i dokumentet [Publicera innehåll för Edge Delivery Services](/help/edge/wysiwyg-authoring/publishing.md).

## Utvecklar {#developing-edge}

Edge Delivery Services bygger på konceptet med block. AEM har ett omfattande bibliotek med fördefinierade block som kan byggas ut efter dina projektbehov. Kod för Edge Delivery Services-projekt hanteras i GitHub.

Mer information finns i dokumentet [Developer Getting Started Guide for WYSIWYG Authoring with Edge Delivery Services](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md).
