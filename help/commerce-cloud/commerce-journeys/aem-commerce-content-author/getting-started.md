---
title: Komma igång med CIF-redigering
description: Komma igång med CIF.
exl-id: 0bef4d8c-0ad3-4ec8-ab08-8c83203b3b68
source-git-commit: 78ead5f15c2613d9c3bed3025b43423a66805c59
workflow-type: tm+mt
source-wordcount: '777'
ht-degree: 0%

---

# Komma igång med AEM CIF {#getting-started}

Lär dig mer om Adobe Experience Manager (AEM) CIF Authoring.

## Story hittills {#story-so-far}

I det föregående dokumentet om denna AEM- och handelsresa [Läs om AEM innehåll och handel](/help/commerce-cloud/introduction.md)har du lärt dig grunderna i och begreppen headless CMS och AEM Content and Commerce.

Den här artikeln bygger på dessa grunder.

## Syfte {#objective}

Det här dokumentet hjälper dig att förstå hur du använder CIF för innehåll- och handelsspecifik redigering. När du har läst bör du:

* Förstå begreppen för CIF med Universal Editor
* Få åtkomst till produktkatalogdata i AEM med produkt- och kategoriväljare
* Åtkomst till innehåll och e-handelsdata via produktcockpit och AEM Omnisearch

## CIF i den universella redigeraren {#cif-authoring}

CIF ger den universella redigeraren möjlighet att komma åt realtidsdata utan att lämna sammanhanget:

Öppna sidopanelen och välj Produkter i listrutan.
![Välj produkttyp](assets/asset-finder-overview.png)

Du kan bläddra i produktkatalogen eller använda textsökningsfältet för att hitta produkter.
![produkttyp](assets/asset-finder-search.png)

Produkter kan släppas på komponenter som stöder produktdroppar (t.ex. produktteaser, produktkarusell) direkt på sidan, vilket automatiskt skapar en produktteaserkomponent.

## Produkt- och kategoriväljare {#pickers}

Om produkt- och kategoridata krävs i e-handelskomponenter eller AEM dialogrutor kan AEM använda väljare som är gränssnittselement för att söka och välja produktkatalogdata på ett enkelt sätt.

### Produktväljare

När du klickar på mappikonen öppnas det modala användargränssnittet för väljaren (till exempel produktväljaren)
![produktväljare](assets/product-picker-open.png)

Du hittar produkterna antingen genom att bläddra i katalogstrukturen till vänster eller genom att söka. Fulltextsökning respekterar den valda kategorin och begränsar sökresultaten till den här kategorin.
![produktväljarmapp](assets/product-picker-folders.png)

Produkter med variationer markeras med en mappikon som du kan klicka på för att visa alla variationer.
![produktväljarvarianter](assets/product-picker-variants.png)
![produktväljarvarianter öppna](assets/product-picker-variants-open.png)

### Kategoriväljaren

Fungerar som en produktväljare. När du klickar på mappikonen öppnas det modala användargränssnittet för väljaren (t.ex. karusellkategori)
![kategoriväljare](assets/category-picker-open.png)

Bläddra i katalogstrukturen till vänster och markera kategorin.
![kategoriväljare](assets/category-picker-folders.png)

## Product Cockpit {#cockpit}

Produkcockpiten är en central plats där man snabbt kommer åt produktkatalogen med allt berikat innehåll. I en av de kommande modulerna lär du dig att berika produktdata med innehåll. För närvarande fokuserar vi på att få tillgång till produktdata.

På huvudmenyn klickar du på E-handel för att visa en lista över alla bifogade produktkataloger.
![e-postmenyalternativ](assets/commerce-menu-item.png)

Här visas en lista med alla anslutna produktkataloger.
![integrerade kataloger](assets/cockpit-Integrated-catalogs.png)

Produktkatalogen visar som standard alla förstanivåkategorier med alla produkter. Om du klickar på en kategori öppnas den kategorin med alla relaterade produkter och underkategorier, inklusive deras produkter.
![produktkatalog för cockpit](assets/cockpit-product-catalog.png)

Du kan öppna produktegenskaperna genom att klicka på egenskapsikonen. Ikonen visas genom att du håller pekaren över en produktruta.
![egenskaper för cockpit-produkter](assets/cockpit-properties.png)

Alla produktegenskaper är skrivskyddade eftersom data läses in i realtid från den anslutna serverdelen. Du måste ändra produktegenskaper i det serverdelssystem som är arkivsystemet. Fliken **Varianter** visas endast om produkten har variationer. Om du klickar på fliken visas alla variationer med dess attribut.
![cockpitproduktvarianter](assets/cockpit-properties-variants.png)

De återstående flikarna visar allt AEM som är kopplat till produkten. Dessa flikar beskrivs i en av de kommande modulerna.

## AEM Omnisearch {#omnisearch}

Att använda Omnissearch är ett enkelt sätt att hitta AEM med hjälp av fulltextsökning. CIF utökar Omnissearch med fulltextsökning av produktkataloger med tillhörande AEM.
![e-postmenyalternativ](assets/omnisearch.png)

Omnisearch kör en fulltextsökning i e-handelsservern för att hitta alla relaterade produkter. Resultatet visas under **Visa alla produkter**. Omnissearch söker även AEM efter innehåll som är kopplat till den sökda produkten. Resultaten anges i respektive AEM. I det här exemplet är ett innehållsfragment relaterat till produkten.

## What&#39;s Next {#what-is-next}

Nu när du är klar med den här delen av resan bör du:

* Förstå begreppen för CIF med Universal Editor
* Så här kommer du åt produktkatalogen i AEM med produkt- och kategoriväljare
* Åtkomst till innehåll och e-handelsdata via produktcockpit och AEM Omnisearch

Bygg vidare på denna kunskap och fortsätt din resa genom att nästa gång du granskar dokumentet [Hantera sidor och mallar för produktkataloger](catalog-templates.md), där du får lära dig hur du bygger och anpassar din första produktkatalogupplevelse.

## Ytterligare resurser {#additional-resources}

Vi rekommenderar att du går vidare till nästa del av resan[Hantera sidor och mallar för produktkataloger](catalog-templates.md)-Nedan följer några valfria resurser som gör en djupdykning i några koncept som nämns här. Dessa valfria resurser krävs dock inte för att fortsätta resan.

* [Konfigurera butiker och kataloger](/help/commerce-cloud/getting-started.md#catalog)
