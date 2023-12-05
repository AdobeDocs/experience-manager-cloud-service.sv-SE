---
title: Hantera produktkatalogsidor och mallar
description: Lär dig hur du hanterar produktkatalogsidor och mallar
exl-id: 0d795d85-c865-40d5-941e-e02ee96fdd11
source-git-commit: abe5f8a4b19473c3dddfb79674fb5f5ab7e52fbf
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 0%

---

# Hantera produktkatalogsidor och mallar {#product-catalog}

Lär dig hur du hanterar produktkatalogsidor och mallar.

## Story hittills {#story-so-far}

I det föregående dokumentet om redigeringsresan AEM innehåll och handel [Komma igång med AEM CIF grunderna](getting-started.md)har du lärt dig grunderna i CIF.

Den här artikeln bygger på dessa grunder.

## Syfte {#objective}

Det här dokumentet hjälper dig att förstå hur du hanterar produktkatalogsidor och mallar. När du har läst bör du:

* förstå begreppen för katalogmallar
* hur generiska mallar fungerar
* har skapat en enskild mall

## Det grundläggande konceptet {#basic-concept}

Venia storefront har en typisk produktkatalogsupplevelse med navigering, landning, kategori (PLP) och produktinformationssidor (PDP).

Katalogsidor skapas dynamiskt med en AEM CIF katalogmall och produktdata i realtid som hämtas från e-handelsslutpunkten vid behov. Varje katalog har en allmän mall för produkt- och kategorisidor.
![katalogstruktur](assets/catalog-structure.png)

Navigeringskomponenten visar innehåll och katalogsidor. Det går att visa antingen kataloglandningssidan eller kategorierna på första nivån i navigeringen. Om du placerar pekaren över en kategori visas kategorier på andra nivån som en andra rad.
![katalognavigering](assets/catalog-navigation.png)

När du klickar på en kategori öppnas kategorisidan (eller produktlistsidan).

![PLP](assets/catalog-plp.png)

När du klickar på en produkt öppnas informationssidan.

![PLP](assets/catalog-pdp.png)

## Mallarna {#templates}

### Allmänna mallar {#generic}

Den generiska mallen för Venedig-katalog använder kärnkomponenten för produktlistan. Den här komponenten visar kategoribilden om den är tillgänglig och produkter från kategorin.
![kategorimall](assets/category-template.png)

Den generiska Venias produktmall använder kärnkomponenten för produktinformation. Den här komponenten visar produktinformation för olika produkttyper och åtgärd för att lägga till i kundvagnen.
![produktmall](assets/product-template.png)

### Redigera mallar {#edit-templates}

Du kan redigera mallar antingen genom att öppna mallsidan direkt eller genom att växla till redigeringsläge när du bläddrar på en produktkatalogsida. Tänk på att om du ändrar sidan ändras mallen och inte bara den specifika sidan i produkten/kategorin.

### Kategori- eller produktspecifika mallar {#specific}

CIF stöder flera mallar med bara några klick. Om du vill skapa en annan mall väljer du den generiska mallen från respektive kategori och skapar en sida med **Skapa** åtgärd.

![skapa mallsida](assets/create-template-page.png)

Välj respektive produkt- eller kategorimall.

![skapa mallval](assets/create-template-select.png)

Ange rubriken och skapa sidan.

![skapa mallinmatning](assets/create-template-enter.png)

Observera att du nu har en specifik mall under den generiska.

![skapa mallhierarki](assets/create-template-hierachry.png)

Öppna mallen. Den ser ut precis som den allmänna kategorimallen.

![skapa mall ny](assets/create-template-new.png)

Lägg till en bild ovanpå sidan.

![skapa malluppdatering](assets/create-template-update.png)

Mallen kan förhandsgranskas med alla kategorier och produkter. Öppna **Sidinformation** och sedan **Visa med kategori/produkt**. Välj produkt/kategori i väljaren för att få en förhandsvisning av den här produkten/kategorin. Välj **Köp looken** för att få en förhandsgranskning av den uppdaterade mallen.

![skapa mall ](assets/create-template-picker.png)

Nu måste du tilldela mallen till den specifika kategorin. Öppna egenskaper i **Sidinformation** och växla till fliken E-handel. Klicka på mappikonen och välj **Köp looken** -kategorin i kategoriväljaren. Du kan tilldela flera kategorier till en mall och även inkludera underkategorier genom att markera kryssrutan.

![skapa mallkoppling](assets/create-template-associate.png)

Gå tillbaka till startsidan och klicka på **Köp looken** för att se den specifika mallen. Alla andra kategorier använder fortfarande den allmänna mallen.

![skapa mallresultat](assets/create-template-result.png)

Samma arbetsflöde kan användas för att skapa enskilda produktmallar.

## What&#39;s Next {#what-is-next}

Nu när du är klar med den här delen av resan bör du:

* förstå begreppen för katalogmallar
* hur generiska mallar fungerar
* har skapat en enskild mall

Bygg vidare på denna kunskap och fortsätt din resa genom att nästa gång du granskar dokumentet [Hantera testade produktkataloger](staged-catalog.md), där du får lära dig hur du arbetar med mellanlagrade produktdata och AEM.

## Ytterligare resurser {#additional-resources}

Vi rekommenderar att du går vidare till nästa del av resan genom att granska dokumentet [Hantera testade produktkataloger](staged-catalog.md), är följande ytterligare, valfria resurser som gör en djupdykning i vissa koncept som nämns i det här dokumentet, men som inte behöver fortsätta på den lösa resan:

* [Skapa flera kategori- och produktsidor](/help/commerce-cloud/authoring/multi-template-usage.md)
* [Migreringsguide för Experience Manager Cloud Servicen](/help/commerce-cloud/migration.md) - Så här migrerar du till AEM Commerce integration framework (CIF)-tillägget från en gammal version
