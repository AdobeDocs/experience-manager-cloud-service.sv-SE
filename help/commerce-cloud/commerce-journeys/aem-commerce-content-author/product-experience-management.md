---
title: Bygga produktupplevelser
description: Lär dig hur du skapar produktinnehåll som sedan kan användas i olika kanaler för att skapa en engagerande shoppingupplevelse.
exl-id: 4ae70e40-fdf1-4a37-b4dd-0c4882d77908
feature: Commerce Integration Framework
role: Admin
index: false
source-git-commit: 173b70aa6f9ad848d0f80923407bf07540987071
workflow-type: tm+mt
source-wordcount: '1157'
ht-degree: 0%

---

# Bygga produktupplevelser {#building-experiences}

Lär dig hantera produktupplevelser.

## Story hittills {#story-so-far}

I det föregående dokumentet om Adobe Experience Manager (AEM) Content and Commerce, [Hantera upplevelser i mellanlagrade produktkataloger](staged-catalog.md), lärde du dig att hantera upplevelser i mellanlagrade produktkataloger.

## Syfte {#objective}

Det här dokumentet hjälper er att förstå hur ni bygger produktinnehåll och upplevelser.

## Product Experience Management {#management}

Product Experience Management är ett område där man kan dekorera produktdata (som ägs av en PIM- eller e-handelslösning) med marknadsföringsmaterial i AEM. Dessa berikade produktdata med innehåll kan sedan användas i olika kanaler för att skapa en engagerande shoppingupplevelse.

I AEM kan du skapa olika typer av innehåll och länka dem till produktkatalogen. Associerat innehåll kan enkelt hittas och användas, vilket leder till hög produktivitet.

### Assets {#assets}

På en hög nivå finns det två typer av mediefiler relaterade till produkter: produkt och marknadsföring. Produktresurserna hanteras av handlarna och fokuserar på att visa produkten (främst framför en neutral bakgrund). Resurserna hanteras antingen i e-handelslösningen eller i AEM Assets (med en Assets-integrering till e-handelslösningen/pim-lösningen).

Marknadsföringsresurser handlar om att marknadsföra och använda produkten som ägs av marknadsföringen. Det kan till exempel vara olika produkter (&quot;gå till väga som det ser ut&quot;), i en viss kontext (&quot;utomhusfall&quot;) eller hur man gör-gör-PDF-filer. CIF är ett enkelt sätt att länka alla AEM-resurser till ett produktkatalogobjekt.

Öppna resursegenskaperna och växla till fliken **Commerce**. På den här fliken kan du hantera associationen med produkter. Tabellen nedanför väljaren innehåller ytterligare information för de länkade objekten (endast synlig med en markering). Klicka på detaljikonen så får du en fullständig vy i produktcockpit. Om du vill associera ett nytt objekt klickar du på produktväljarikonen (mappikonen), markerar ett objekt och stänger väljaren.

![pem assets](assets/pem-assets.png)

### Upplevelsefragment {#experience-fragments}

Upplevelsefragment är ett bra sätt att skapa återanvändbart eller individuellt produktinnehåll i stor skala. Associationen fungerar på liknande sätt som en tillgång. Öppna egenskaper och växla till fliken **Commerce**. På den här fliken kan du hantera associationen med produkter och kategorier. Tabellerna under väljarna innehåller ytterligare information om de länkade objekten (visas bara med en markering). Klicka på detaljikonen så får du en fullständig vy i produktcockpit. Om du vill associera ett nytt objekt klickar du på produktväljarikonen (mappikonen), markerar ett objekt och stänger väljaren.

![pem xf](assets/pem-xf.png)

### Innehållsfragment {#content-fragments}

Innehållsfragment är den bästa innehållstypen för alla typer av strukturerat innehåll. Detta kan användas för att utöka externa produktdata med ytterligare marknadsföringsdata eller för att skapa innehåll utan rubrik. Kopplingen mellan ett innehållsfragment och ett produktkatalogobjekt sker via referenstyperna för produkt eller kategori i modellredigeraren för innehållsfragment. Dra och släpp rätt referenstyp på modellen och konfigurera fältet. De här typerna har stöd för en eller flera markeringar.

![pem cf-modell](assets/pem-cf-model.png)

Om du skapar ett innehållsfragment baserat på den här modellen ger de här referenstyperna dig ett enkelt sätt att markera rätt objekt med respektive väljare.

![pem cf](assets/pem-cf.png)

### Product Cockpit {#product-cockpit}

Du introducerades i produktcockpit (eller konsolen) i en av de tidigare modulerna. cockpiten är ett enkelt sätt att inte bara bläddra i produktkatalogen utan också att se allt tillhörande AEM-innehåll på ett och samma ställe. Gå till produktkonsolen och öppna egenskaperna för en produkt som har associerat innehåll. Växla till respektive flik för att se det associerade innehållet.

![pem cockpit](assets/pem-cockpit.png)

När du klickar på åtgärdsikonen öppnas det innehållet på en ny webbläsarflik.

## Förbättrar enskilda produkt- och kategorisidor {#enrich}

I de tidigare modulerna har du lärt dig hur du arbetar med flera produktkatalogmallar. Flera mallar är ett bra sätt att skapa olika mallar, men behövs ofta inte. Ofta kan samma mall användas med platshållare för enstaka innehåll. CIF stöder platshållare för innehållsfragment och Experience Fragments.

Låt oss börja med Experience Fragment-platshållaren. Öppna en produktmall i AEM Editor. Dra och släpp **Commerce Experience Fragment**-komponenten på mallen och öppna sedan konfigurationsdialogrutan.

![pem-platshållare](assets/pem-placeholder.png)

Öppna komponentens dialogruta och ange ett namn för platshållaren. Du måste ange ett platshållarnamn och du kan lägga till så många platshållare som du behöver.

![Pem XF-dialogruta](assets/pem-dialog-xf.png)

Öppna den Experience Fragment som du har kopplat till en produkt i föregående steg. Öppna egenskaper och växla till fliken E-handel. Ange samma platshållarnamn under **Katalogplatshållarplatsen**.

![pem xf](assets/pem-xf.png)

Dra och släpp komponenten **Commerce Content Fragment** i mallen och öppna konfigurationsdialogrutan.

![Pem CF-dialogruta](assets/pem-dialog-cf.png)

I den här dialogrutan återanvänds dialogrutan för kärnkomponentens innehållsfragment. Mer information finns under ytterligare resurser. Den enda skillnaden är egenskapen **Link Element** som konfigurerar identifierarfältet (product SKU eller category UID) i Content Fragment-modellen.

Förhandsgranska nu en produktsida som antingen har ett associerat innehållsfragment och/eller Experience Fragment. När AEM återger en sida görs en sökning efter varje platshållare baserat på typ (Innehåll eller Experience Fragment), identifierare och platshållarnamn för Experience Fragments. AEM använder en URL-matchare för att hämta identifieraren (SKU för produkter, UID för kategorier). Om en upplevelse eller ett innehållsfragment returneras återges det på platshållarplatsen, i annat fall ignoreras platshållaren.

![pem-resultat](assets/pem-result.png)

## Gör innehåll köpbart {#making-shoppable}

Man kan också göra en vanlig AEM-sida mer tillgänglig genom att lägga in handelskomponenter. Skapa en innehållssida i AEM och öppna den tomma sidan i redigeraren.

![pem empty page](assets/pem-page-empty.png)

Först drar och släpper du en produktdetaljkomponent på sidan. Gå sedan till Assets sidopanel, byt till produkter och välj en produkt. Dra och släpp produkten på produktkomponenten. Då visas en vanlig produktkomponent på en innehållssida.

![Pem - produktsida](assets/pem-page-product.png)

Om du har skapat associerat innehåll för den produkten växlar du till **Associerat Commerce-innehåll** i sidofältet i Assets. På den här fliken visas allt AEM-innehåll som är kopplat till produkten. På så sätt kan du nu snabbt försköna sidorna med allt tillhörande innehåll.

![Pem-anrikad sida](assets/pem-page-enriched.png)

## Slut på resan? {#end-of-journey}

Grattis! Du har slutfört AEM Content and Commerce Developer travel! Nu bör du:

* förstå hur du kan koppla AEM-innehåll till produktkatalogobjekt
* använda platshållare för att berika produkt- och kategorisidor individuellt
* kunna göra innehåll till ett köpbart och använda fliken för tillhörande innehåll

Nu kan ni hantera produktupplevelser med AEM Content och Commerce. AEM Content och Commerce har dock många andra alternativ. Ta en titt på några av de ytterligare resurser som är tillgängliga i avsnittet [Ytterligare resurser](#additional-resources) där du kan läsa mer om de funktioner du såg under den här resan.

## Ytterligare resurser {#additional-resources}

* [Skapa Commerce Experience](/help/commerce-cloud/authoring/authoring-commerce-experiences.md)
* [Product Cockpit](/help/commerce-cloud/authoring/product-cockpit.md)
* [Innehållsfragmentkomponent](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=sv-SE)
