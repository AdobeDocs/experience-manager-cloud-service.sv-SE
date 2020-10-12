---
title: Karusellbanner
description: Lär dig hur du arbetar med karusellbanners i Dynamic Media
translation-type: tm+mt
source-git-commit: 5da0d4cc8c6d8781dd7cce8bbbde207568a6d10b
workflow-type: tm+mt
source-wordcount: '4522'
ht-degree: 4%

---


# Karusellbanner{#carousel-banners}

Carousel-banners gör det möjligt för marknadsförare att öka konverteringsgraden genom att enkelt skapa interaktivt roterande marknadsföringsmaterial och leverera det till alla skärmar.

Det kan vara tidskrävande att skapa och ändra innehåll i reklambanners, vilket begränsar möjligheten att snabbt publicera nytt innehåll eller göra det mer riktat. Med Carousel Banners kan du snabbt skapa eller ändra roterande banners, lägga till interaktivitet, till exempel hotspot-områden som länkar till produktdetaljer eller relaterade resurser, och leverera dem till alla skärmar, så att du kan få ut nytt marknadsföringsmaterial snabbare.

Carousel Banners are designated by a banner with the word **[!UICONTROL CAROUSELSET]**:

![chlimage_1-438](assets/chlimage_1-438.png)

På din webbplats kan en karusellbanderoll se ut så här:

![chlimage_1-439](assets/chlimage_1-439.png)

Här kan du navigera bland bilderna (genom att klicka på siffrorna). Dessutom roteras bildrutorna automatiskt baserat på ett tidsintervall som du kan anpassa. Bilder som du lägger till i karusellbanderollen har stöd för både hotspot-områden och bildscheman, där användarna kan trycka eller gå till en hyperlänk eller komma åt ett snabbfönster.

I det här exemplet har användaren tryckt på eller klickat på ett bildschema och öppnat snabbvyfönstret för handskar:

![chlimage_1-440](assets/chlimage_1-440.png)

## Se hur karusellbanners skapas {#watch-how-carousel-banners-are-created}

Titta på en genomgång på 10 minuter och 33 sekunder om [hur karusellbanners skapas](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveCarouselBanner). Du får också lära dig att förhandsgranska, redigera och leverera karusellbanderoller.

>[!NOTE]
>
>Icke-administrativa användare måste läggas till i **[!UICONTROL dam-users]** gruppen för att kunna skapa eller redigera karusellbanderoller. Om du har problem med att skapa eller redigera kontaktar du systemadministratören som kan lägga till dig i **D[!UICONTROL am-users]** -gruppen.

## Snabbstart: Carousel Banners {#quick-start-carousel-banners}

Så här kommer du igång snabbt:

1. [Identifiera hotspot- och bildschemavariabler](#identifying-hotspot-and-image-map-variables) (endast för kunder som använder AEM Assets + Dynamic Media)

   Börja med att identifiera dynamiska variabler som används i den befintliga snabbvyimplementeringen, så att du kan ange klickbara områden och data från bildscheman korrekt när du skapar en karusellbanderoll i AEM Assets.

<!-- LEAVE; COMMERCE BEING ADDED AGAIN IN THE FUTURE

   >[!NOTE]
   >
   >If you are an AEM Sites or Ecommerce customer, you can use the built-in feature to navigate to product pages and lookup the existing skus in the product catalog. You do not need to manually enter hotspot or image map variables.
   >
   >
   >If you are an AEM Assets and Dynamic Media customer, you will manually enter data for hotspots and image maps, and then integrate the published URL or Embed code with your third-party content management system.

-->

1. Valfritt: [Skapa en visningsförinställning för en karuselluppsättning](/help/assets/dynamic-media/managing-viewer-presets.md) om det behövs.

   Om du är administratör kan du anpassa karusellens beteende och utseende genom att skapa en egen förinställning för Carousel-visningsprogrammet. Den största fördelen är att du kan återanvända den här anpassade visningsförinställningen för flera bildspel. Man kan också anpassa karusellens beteende och utseende direkt när man skapar karusellen. Detta är det bästa sättet när du vill ha en mycket specifik design för en viss karusell.

1. [Överför en bildbanderoll](#uploading-image-banners).

   Överför bildbanderoller som du vill göra interaktiva.

1. [Skapa en Carousel-uppsättning](#creating-carousel-sets).

   I Carousels Sets navigerar användarna genom banderollbilder och trycker på hotspot-områden eller bildscheman för att få tillgång till relevant innehåll.

   Om du vill skapa en karuselluppsättning i Assets trycker du på **[!UICONTROL Create]** och väljer sedan **[!UICONTROL Carousel Sets]**. Lägg till resurser i bilderna och tryck på **[!UICONTROL Save]**. Du kan också redigera karusellens utseende och beteende direkt i redigeraren.

1. [Lägg till aktiveringspunkter eller bildscheman i en bildbanderoll.](#adding-hotspots-or-image-maps-to-an-image-banner)

   Lägg till en eller flera hotspot-områden eller bildscheman i en bildbanderoll och koppla dem till en åtgärd som en länk, en snabbvy eller ett Experience Fragment. När du har lagt till aktiveringspunkter eller bildscheman avslutar du den här uppgiften genom att publicera karuselluppsättningen. Med Publicering skapas den inbäddningskod som du kan använda för att kopiera och tillämpa på webbplatsens landningssida.

   Se [(valfritt) Förhandsgranska Carousel Banners.](#optional-previewing-carousel-banners) - Valfritt. Om du vill kan du visa en representation av karuselluppsättningen och testa dess interaktivitet.

1. [Publicera Carousel Banners](#publishing-carousel-banners).

   Du publicerar en Carousel-uppsättning på samma sätt som andra resurser. Navigera till Carousel Set i Assets, markera den och tryck **[!UICONTROL Publish]**. När du publicerar en Carousel Set aktiveras URL:en och strängen Embed.

1. Gör något av följande:

   * [Lägg till en karusellbanderoll på webbplatsens](#adding-a-carousel-banner-to-your-website-page)sidaDu kan lägga till karusellbanderollens URL eller inbäddningskod som du har kopierat till webbplatsens sida.

      * [Integrera karusellbanderollen med en befintlig QuickView](#integrating-the-carousel-banner-with-an-existing-quickview). Om du använder ett webbinnehållshanteringssystem från tredje part måste du integrera den nya Carousel-banderollen med den befintliga Quickview-implementeringen på din webbplats.
   * [Lägg till en karusellbanderoll på din webbplats i](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)AEMIom du är AEM Sites-kund kan du lägga till karuselluppsättningen direkt på sidan i AEM med hjälp av komponenten Interactive Media.


Om du behöver redigera Carousel-uppsättningar läser du [redigera Carousel-uppsättningar.](#editing-carousel-sets) Dessutom kan du visa och redigera [Carousel Set-egenskaper](/help/assets/manage-digital-assets.md#editing-properties).

## Identifiera variabler för aktiveringspunkt och bildschema {#identifying-hotspot-and-image-map-variables}

Börja med att identifiera dynamiska variabler som används i den befintliga snabbvyimplementeringen så att du kan ange aktiveringspunkter eller data för bildscheman korrekt när du skapar karuselluppsättningar i AEM Assets.

När du lägger till aktiveringspunkter eller bildscheman i en banderollbild i AEM Assets måste du tilldela varje hotspot eller bildschema en SKU och valfria ytterligare variabler. Sådana variabler används senare för att matcha aktiveringspunkter eller bildscheman med snabbvyinnehåll.

<!-- LEAVE; COMMERCE BEING ADDED LATER

>[!NOTE]
>
>If you are an AEM Sites and/or AEM Ecommerce customer, skip this step. You do not need to manually identify hotspot or image map variables; you can use the integration with Ecommerce for product integration. See information on [setting up eCommerce](/help/sites-cloud/administering/generic.md). In addition, you can use the Interactive component and add it to your web page.
>
>If you are an AEM Assets or Media customer, you publish the URL or Embed code and then integrate with your third-party content management system and identify hotspots and image maps manually.

-->

Det är viktigt att kunna identifiera antalet och typen av variabler som ska kopplas till hotspot- eller bildschemadata. Varje hotspot eller bildschema som läggs till i en banderollbild måste innehålla tillräckligt med information för att entydigt identifiera produkten i det befintliga backend-systemet. Samtidigt bör varje hotspot eller bildschema inte innehålla mer data än vad som är nödvändigt. Orsaken är att det skulle göra inmatningsprocessen alltför komplex och pågående hotspot- eller bildschemahantering mer felbenägen.

Det finns olika sätt att identifiera en uppsättning variabler som ska användas för hotspot- eller bildschemaddata.

Ibland kan det räcka att rådfråga IT-specialister som är ansvariga för den befintliga snabbvyimplementeringen, eftersom de troligen vet vilken minimiuppsättning data som behövs för att identifiera snabbvyn i systemet. I de flesta fall går det dock även att bara analysera den befintliga beteendet för koden.

De flesta implementeringar av snabbvyn använder följande paradigm:

* Användaren aktiverar ett element i användargränssnittet på webbplatsen. Till exempel trycker de på en **[!UICONTROL Quick View]**-knapp.
* Webbplatsen skickar en Ajax-begäran till backend-servern för att läsa in snabbvydata eller -innehåll vid behov.
* Snabbvydata översätts till innehållet som förberedelse för återgivning på webbsidan.
* Slutligen återges sådant innehåll på skärmen visuellt i koden.

Då besöker man olika delar av den befintliga webbplatsen där snabbvyfunktionen är implementerad, aktiverar snabbvyn och hämtar den Ajax-URL som webbsidan skickar för att läsa in snabbvydata eller -innehåll.

Normalt behöver du inte använda några specialverktyg för felsökning. Moderna webbläsare har webbinspektörer som klarar ett bra jobb. Nedan följer några exempel på webbläsare som innehåller webbinspektörer:

* Om du vill visa alla utgående HTTP-begäranden i Google Chrome trycker du på F12 (Windows) eller Command-Option-I (Mac) för att öppna panelen Utvecklarverktyg och sedan på fliken Nätverk.
* I Firefox kan du antingen aktivera plugin-programmet för Firebug genom att trycka på F12 (Windows) eller Command-Option-I (Mac) och använda fliken Net. Du kan också använda det inbyggda inspektörsverktyget och nätverksfliken.

När nätverksövervakning är aktiverat i webbläsaren utlöser du snabbvyn på sidan.

Nu hittar du snabbvyns Ajax-URL i nätverksloggen och kopierar den inspelade URL:en för framtida analys. I de flesta fall när du utlöser snabbvyn skickas flera begäranden till servern. Vanligtvis är snabbvyns Ajax-URL en en av de första i listan. Den har antingen en komplex frågesträngsdel eller -sökväg och dess MIME-svarstyp är antingen `text/html`, `text/xml`eller `text/javascript`.

Under den här processen är det viktigt att du besöker olika delar av webbplatsen, med olika produktkategorier och typer. Anledningen är att URL:er för snabbvyn kan ha delar som är gemensamma för en viss webbplatskategori, men bara ändras om du besöker ett annat område på webbplatsen.

I det enklaste fallet är den enda variabeldelen i snabbvyns URL produktens SKU. I det här fallet är SKU-värdet den enda datadel som du behöver för att lägga till aktiveringspunkter eller bildscheman i banderollbilden.

I komplexa fall har dock snabbvyns URL-adress olika element utöver SKU:n, till exempel kategori-ID, färgkod, storlekskod osv. I sådana fall är varje element en separat variabel i hotspot- eller bildschemats datadefinition i karusellbanderollfunktionen.

Titta på följande exempel på URL:er för snabbvyn och deras resulterande hotspot- eller bildschemavariabler:

<table>
 <tbody>
  <tr>
   <td>En SKU, hittades i frågesträngen.</td>
   <td><p>De inspelade URL:erna för snabbvyn innehåller följande:</p>
    <ul>
     <li><p><code>https://server/json?productId=866558&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1196184&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1081492&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1898294&amp;source=100</code></p> </li>
    </ul> <p>Den enda variabeldelen i URL:en är värdet på <code>productId=</code> frågesträngsparametern, och det är helt klart ett SKU-värde. Därför behöver våra aktiveringspunkter eller bildscheman bara SKU-fält med värden som <code>866558,</code> <code>1196184,</code> <code>1081492,</code> <code>1898294.</code></p> </td>
  </tr>
  <tr>
   <td>En SKU, finns i URL-sökvägen.</td>
   <td><p>De inspelade URL:erna för snabbvyn innehåller följande:</p>
    <ul>
     <li><p><code>https://server/product/6422350843</code></p> </li>
     <li><p><code>https://server/product/1607745002</code></p> </li>
     <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>Variabeldelen finns i den sista delen av banan och blir SKU-värdet för hotspot-områden/bildscheman:<strong><code>6422350843</code>, <code>1607745002,</code> </strong><code>0086724882.</code></p> </td>
  </tr>
  <tr>
   <td>SKU och kategori-ID i frågesträngen.</td>
   <td><p>De inspelade URL:erna för snabbvyn innehåller följande:</p>
    <ul>
     <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
     <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
     <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>I det här fallet finns det två olika delar i URL:en. SKU:n lagras i <code>prodId</code> parametern och kategori-ID:t lagras i <code>category=</code>parametern.</p> <p>Definitionerna av hotspot/bildschema är par. Det vill säga ett SKU-värde och ytterligare en variabel som kallas <code>categoryId</code>. De resulterande paren är följande:</p>
    <ul>
     <li><p>SKU är <strong><code>305466</code></strong> och <code>categoryId</code> är <code>1100004</code>.</p> </li>
     <li><p>SKU är <strong><code>310181</code></strong> och <code>categoryId</code> är <strong><code>1100004</code></strong>.</p> </li>
     <li><p>SKU är <strong><code>308706</code></strong> och <code>categoryId</code> är <strong><code>1740148</code></strong>.</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Överför bildbanderoller {#uploading-image-banners}

Om du redan har laddat upp de bilder du vill använda går du vidare till nästa steg, [Skapa Carousel-uppsättningar](#creating-carousel-sets). Observera att bilderna som används i karusellen måste överföras när Dynamic Media har aktiverats.

Mer information om hur du överför bildbanderoller finns i [Överföra resurser](/help/assets/manage-digital-assets.md).

## Skapa Carousel-uppsättningar {#creating-carousel-sets}

>[!NOTE]
>
>Icke-administrativa användare måste läggas till i **[!UICONTROL dam-users]** gruppen för att kunna skapa eller redigera karusellbanderoller. Om du har problem med att skapa eller redigera kontaktar du systemadministratören som kan lägga till dig i **[!UICONTROL dam-users]** gruppen.

**Skapa en Carousel-uppsättning**

1. I Resurser navigerar du till den mapp där du vill skapa Carousel-uppsättningen och trycker på **[!UICONTROL Create > Carousel Set]**.
1. På Carousel Banner Editor-sidan trycker du **[!UICONTROL Tap to open Asset Selector]** för att välja bilden för din första bild.

   Gör något av följande på Carousel Banner Editor-sidan:

   * Near the upper-left corner of the page, tap **[!UICONTROL Add Slide]** icon.

   * Tryck mitt på sidan **[!UICONTROL Tap to open Asset Selector]**.
   Tryck här för att välja resurser som du vill inkludera i karuselluppsättningen. De markerade resurserna visas med en bock. When you are finished, near the upper-right corner of the page, tap **[!UICONTROL Select]**.

   Med resursväljaren kan du söka efter resurser genom att skriva ett nyckelord och trycka eller klicka på **[!UICONTROL Return]**. Du kan också använda filter för att förfina sökresultatet. Du kan filtrera efter sökväg, samling, filtyp och tagg. Markera filtret och tryck sedan på ikonen **[!UICONTROL Filter]** i verktygsfältet. Ändra vyn genom att trycka på ikonen Visa och sedan välja **[!UICONTROL Column View]**, **[!UICONTROL Card View]** eller **[!UICONTROL List View]**.

   Mer information finns i [Arbeta med väljare](/help/assets/dynamic-media/working-with-selectors.md) .

1. Fortsätt med att lägga till bilder tills du har lagt till alla bilder som du vill rotera genom i Carousel-uppsättningen.
1. (Valfritt) Gör något av följande:

   * Om det behövs drar du bildrutorna för att ändra ordning på bilderna i listan.
   * Om du vill ta bort en bild markerar du bilden och trycker sedan **[!UICONTROL Delete Slide]** på verktygsfältet.

   * Om du vill använda en förinställning trycker du på den förinställda listrutan längst upp till höger på sidan och väljer sedan en förinställning som ska användas på uppsättningen samtidigt.
   Om du vill ta bort en bildruta trycker eller klickar du på bildrutan och trycker eller klickar **[!UICONTROL Delete Slide]** i verktygsfältet. Om du vill flytta en bildruta trycker du på ikonen för att ändra ordning och håller ned och flyttar till önskad plats.

1. När du har lagt till bilderna i bildrutor kan du lägga till en aktiveringspunkt, ett bildschema eller båda delarna. Se [Lägga till aktiveringspunkter eller bildscheman](#adding-hotspots-or-image-maps-to-an-image-banner).
1. Du kan ändra den visuella designen och beteendet för karuselluppsättningar genom att trycka eller klicka på flikarna Beteende och Utseende och göra justeringar av hur karusellbanderollen ser ut eller hur specifika komponenter fungerar. Mer information om hur du använder visningsprogramredigeraren finns i [Hantera visningsförinställningar](/help/assets/dynamic-media/viewer-presets.md) .

   >[!NOTE]
   >
   >För karusellbanderoller kan följande saker behöva justeras:
   >    * Längd som en bild visas. Som standard visas varje bild i 9 sekunder.
   >    * Animering. Som standard tonas varje bildruteövergång ut. Du kan ändra det till en bildövergång.
   >    * Knapparnas format. Användarna kan rotera genom banners genom att trycka på varje punkt eller nummer. Du kan ändra var de angivna indikatorknapparna visas (och om de är numeriska eller prickade) och hur stora de är.
   >    * Ändra markeringsformatet för ett bildschema eller ikonen som används för aktiveringspunkter.
   >    * Innan du redigerar en visningsförinställning väljer du det format du vill basera förinställningen på. Om du inte gör det kommer du att förlora alla ändringar när du börjar redigera visningsförinställningen om du väljer att ändra till en annan förinställning


   Du kan också förhandsvisa hur karusellbanderollen kommer att se ut. Se [(valfritt) Förhandsgranska Carousel Banners](#optional-previewing-carousel-banners).

1. Tryck **[!UICONTROL Save]** när du är klar.

## Lägga till aktiveringspunkter eller bildscheman i en bildbanderoll {#adding-hotspots-or-image-maps-to-an-image-banner}

Du kan lägga till aktiveringspunkter eller bildscheman i en banderoll med hjälp av Carousel Set-redigeraren.

När du lägger till aktiveringspunkter eller bildscheman kan du definiera dem som en snabbvypopup-visning, som en hyperlänk eller som en upplevelsefragment.

Se [Experience Fragment](/help/sites-cloud/authoring/fundamentals/experience-fragments.md).

>[!NOTE]
>
>Observera att verktygen för delning av sociala medier i Carousel Banner inte stöds när du bäddar in visningsprogrammet i en Experience Fragment.
>
>Du kan undvika detta genom att använda eller skapa visningsförinställningar som inte har verktyg för delning av sociala medier. Med sådana visningsförinställningar kan du bädda in dem i Experience Fragments.

Kom ihåg att spara ditt arbete när du lägger till hotspot-områden eller bildscheman i en bild. Alternativen Ångra och Gör om, nära det övre högra hörnet på sidan, stöds under den aktuella skaps-/redigeringssessionen.

När du är klar med att skapa en karusellbanderoll kan du använda Förhandsgranska för att se hur karusellbanderollen kommer att se ut för kunderna.

Se [(valfritt) Förhandsgranska Carousel Banners.](#optional-previewing-carousel-banners)

>[!NOTE]
>
>När du lägger till aktiveringspunkter i en bild i en [interaktiv bild](/help/assets/dynamic-media/interactive-images.md) eller en Carousel-banderoll lagras hotspot-informationen på samma metadataplats, i förhållande till bildens plats&amp;mdashvärde, oavsett om det är en interaktiv bild eller en Carousel-banderoll. Den här funktionen innebär att du enkelt kan återanvända samma bild - tillsammans med dess definierade hotspot-data - i båda visningsprogrammen.

>Observera dock att Carousel Banners stöder bildscheman på bilder som även kan innehålla hotspot-områden. en interaktiv bild gör det inte. Tänk på detta om du tänker skapa en interaktiv bild eller en Carousel-banderoll som använder samma bild. Du kanske vill skapa interaktiva bilder och Carousel Banners med separata kopior av samma bild istället.

>[!NOTE]
>
>Om du redigerar interaktiva bilder med aktiveringspunkter och beskär bilden tas dina aktiveringspunkter bort.

<!-- See also [Adding Image Maps](/help/assets/image-maps.md). -->

**Lägga till aktiveringspunkter eller bildscheman i en bildbanderoll**

1. Navigera från Assets till karuselluppsättningen som du vill göra interaktiv.
1. Markera karusellen och tryck **[!UICONTROL Edit]**. Carousel Viewer Editor öppnas.
1. Markera den bildruta som du vill göra interaktiv.
1. I det övre vänstra hörnet av sidan trycker du på **[!UICONTROL Hotspot]** eller **[!UICONTROL Image Map]**.
1. Gör något av följande:

   * För aktiveringspunkter: Tryck på den plats i bilden där du vill att hotspot-området ska visas.
   * För bildscheman: Klicka på bilden och dra sedan från det övre vänstra hörnet till det nedre högra hörnet för att skapa bildschemaområdet. Du kan justera storleken på bildschemat genom att dra i hörnen.

   Om det behövs drar du hotspot- eller bildschemat till en ny plats. Lägg till ytterligare hotspot-områden eller bildscheman efter behov.

   Tryck på fliken **[!UICONTROL Actions]** om du vill ta bort ett hotspot-område eller bildschema. Under rubriken **[!UICONTROL Maps & Hotspots]** i listrutan **[!UICONTROL Selected Type]** väljer du namnet på det hotspot-område eller bildschema som du vill ta bort. Tryck på ikonen **[!UICONTROL Trash]** bredvid menyn och tryck sedan på **[!UICONTROL Delete]**.

1. Skriv namnet på aktiveringspunkten eller bildschemat i textfältet Namn. Det här namnet visas också i **[!UICONTROL Maps & Hotspot]** listrutan. Genom att ange ett namn blir det enkelt att identifiera hotspot-området eller bildschemat om du bestämmer dig för att göra ändringar i det i framtiden.
1. Gör något av följande på **[!UICONTROL Actions]** fliken:

   * Tryck på **[!UICONTROL Quickview]**.

      * Om du är AEM Sites <!-- and Ecommerce customer-->trycker du på produktväljarikonen (förstoringsglas) för att öppna produktsidan. Tryck på den produkt du vill använda och tryck sedan på bockmarkeringen i det övre högra hörnet av sidan för att gå tillbaka till Carousel Banner Editor.
      * Om du inte är AEM Sites <!-- or Ecommerce customer -->

         * Se [Identifiera hotspot-variabler](#identifying-hotspot-and-image-map-variables) eftersom du kanske vill definiera dessa variabler.
         * Ange sedan SKU-värdet manuellt. I textfältet SKU-värde skriver du produktens SKU (Stock Keeping Unit), som är en unik identifierare för varje separat produkt eller tjänst som du erbjuder. Det angivna SKU-värdet fyller automatiskt i variabeldelen av snabbvymallen så att systemet vet att den aktiveringspunkt som användaren går till associeras med en viss SKU-snabbvy.
         * (Valfritt) Om det finns andra variabler i snabbvyn som du behöver för att kunna identifiera en produkt ytterligare trycker du på **[!UICONTROL Add Generic Variable]**. Ange ytterligare en variabel i textfältet. Till exempel är category=Mens en tillagd variabel.

         * Mer information finns i [Arbeta med väljare](/help/assets/dynamic-media/working-with-selectors.md) .
   * Tryck på **[!UICONTROL Hyperlink]**.

      * Om du är kund hos AEM Sites trycker du på ikonen Platsväljare (mapp) för att navigera till en URL.

         >[!NOTE]
         >
         >Den URL-baserade länkningsmetoden är inte möjlig om det interaktiva innehållet har länkar till relativa URL-adresser, särskilt länkar till AEM Sites-sidor.

      * Om du är en fristående kund anger du den fullständiga URL-sökvägen till en länkad webbsida i textfältet HREF.

   Var noga med att ange om länken ska öppnas på en ny webbläsarflik (rekommenderat standardvärde) eller på samma flik.

   Mer information finns i [Arbeta med väljare](/help/assets/dynamic-media/working-with-selectors.md) .

   * Tryck på **[!UICONTROL Experience Fragment]**.

      * Om du är AEM Sites-kund trycker du på ikonen Sök (förstoringsglas) för att öppna sidan Experience Fragment. Tryck eller klicka på det Experience Fragment som du vill använda och tryck sedan på Select (Välj) längst upp till höger på sidan för att återgå till sidan för hantering av hotspot.
Se [Upplevelsefragment](/help/sites-cloud/authoring/fundamentals/experience-fragments.md).

      * Ange bredd och höjd för Experience Fragment så som det kommer att visas på banderollen.

         >[!NOTE]
         >
         >Observera att verktygen för delning av sociala medier i Carousel Banner inte stöds när du bäddar in visningsprogrammet i en Experience Fragment.
         >Du kan undvika detta genom att använda eller skapa visningsförinställningar som inte har verktyg för delning av sociala medier. Med sådana visningsförinställningar kan du bädda in dem i Experience Fragments.

   ![experience_fragment-carouselbanner](assets/experience_fragment-carouselbanner.png)

   Du kan också förhandsvisa hur karusellbanderollen kommer att se ut. Se [(valfritt) Förhandsgranska Carousel Banners](#optional-previewing-carousel-banners).

1. Tryck på **[!UICONTROL Save]**.
1. Publicera karuselluppsättningen. Publicering skapar den inbäddningskod eller URL som du kan använda på din webbsida. Om du är kund hos AEM Sites kan du lägga till karuselluppsättningen direkt på din webbsida.

   Se [Publicera resurser](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

   Se [Lägga till en karuselluppsättning på webbplatsens landningssida](#adding-a-carousel-banner-to-your-website-page)

## Redigera Carousel-uppsättningar {#editing-carousel-sets}

>[!NOTE]
>
>Icke-administrativa användare måste läggas till i **[!UICONTROL dam-users]** gruppen för att kunna skapa eller redigera karusellbanderoller. Om du har problem med att skapa eller redigera kontaktar du systemadministratören som kan lägga till dig i **[!UICONTROL dam-users]** gruppen.

Du kan utföra en mängd redigeringsuppgifter på Carousel Sets, till exempel:

* Lägg till bilder i en Carousel-uppsättning. Se även [Arbeta med väljare](/help/assets/dynamic-media/working-with-selectors.md).
* Sortera om bilderna i Carousel-uppsättningen.
* Ta bort resurser i Carousel-uppsättningen.
* Använd en visningsförinställning.
* Ta bort Carousel-uppsättningen.
* Lägg till eller redigera hotspot-områden och bildscheman. Se även [Arbeta med väljare](/help/assets/dynamic-media/working-with-selectors.md).

**Redigera en Carousel-uppsättning**

1. Gör något av följande:

   * Håll pekaren över en Carousel Set-resurs och tryck sedan på **[!UICONTROL Edit]** (pennikon).
   * Håll pekaren över en Carousel Set-resurs, tryck **[!UICONTROL Select]** (bockmarkeringsikon) och tryck sedan **[!UICONTROL Edit]** på verktygsfältet.

   * Tap on a Carousel Set asset, then in the upper-left corner of the page tap **[!UICONTROL Edit]** (pencil icon).

1. Om du vill redigera Carousel-uppsättningen gör du något av följande:

   * To add a slide, tap the **[!UICONTROL Add Slide]** icon then navigate to the asset you want to add to that slide and tap or click the checkmark.
   * Om du vill ändra ordning på bildrutorna drar du en bildruta till en ny plats (markera sorteringsikonen för att flytta objekt).
   * Om du vill lägga till ett hotspot-område eller bildschema klickar du på ikonerna för hotspot eller bildschema och ser hur du [lägger till hotspot-områden och bildscheman](#adding-hotspots-or-image-maps-to-an-image-banner).
   * To edit the appearance or behavior of the carousel set, tap the **[!UICONTROL Appearance]** tab or **[!UICONTROL Behavior]** tab, then set the options you want.
   * Om du vill redigera aktiveringspunkter eller bildscheman markerar du en aktiveringspunkt eller ett bildschema på lämplig bildruta och gör de ändringar som behövs under **[!UICONTROL Actions]** fliken.
   * Om du vill ta bort en bildruta markerar du den och trycker sedan **[!UICONTROL Delete Slide]** på verktygsfältet.
   * To apply a preset, near the upper-right corner of the page, tap the **[!UICONTROL Preset]** drop-down list, then select a viewer preset.
   * Om du vill ta bort en hel Carousel-uppsättning går du till Carousel-uppsättningen, markerar den och trycker sedan på **[!UICONTROL Delete]**.

   >[!NOTE]
   >
   >Om du redigerar interaktiva bilder med aktiveringspunkter och beskär bilden tas dina aktiveringspunkter bort.

## (Valfritt) Förhandsgranska Carousel Banners {#optional-previewing-carousel-banners}

Du kan använda Förhandsgranska för att se hur karusellbanderollen kommer att se ut för kunderna och för att testa karusellbanderollernas hotspot-områden och bildscheman för att säkerställa att de beter sig som förväntat.

När du är nöjd med karusellbanderollen kan du publicera den.
See [Embedding the Video or Image Viewer on a Web Page](/help/assets/dynamic-media/embed-code.md).
See [Linking URLs to your web application](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md). Observera att den URL-baserade länkningsmetoden inte är möjlig om det interaktiva innehållet har länkar till relativa URL-adresser, särskilt länkar till AEM Sites-sidor.
See [Adding Dynamic Media Assets to pages.](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)

Du kan förhandsgranska karusellbanderoller från Carousel Editor (önskad metod) eller från **[!UICONTROL Viewers]** listan.

**Förhandsgranska Carousel banners**

1. Navigera **[!UICONTROL Assets]** till en befintlig Carousel-banderoll som du har skapat och öppna den genom att trycka.
1. Tryck på **[!UICONTROL Edit]**.
1. I listan med visningsförinställningar i det högra hörnet av verktygsfältet väljer du ett visningsprogram för att förhandsgranska karusellbanderollen.

   ![experience_fragment-carouselbanner-viewerdropdown](assets/experience_fragment-carouselbanner-viewerdropdown.png)

1. Tryck på **[Förhandsgranska]**.
1. Tryck på hotspot-områden eller bildscheman på bilden för att testa deras associerade åtgärder.

**Förhandsgranska karusellbanners från visningslistan**

1. Navigera **[!UICONTROL Assets]** till en befintlig Carousel-banderoll som du har skapat och öppna den genom att trycka.
1. Klicka på ikonen Innehåll i det övre vänstra hörnet på sidan Förhandsvisa.
1. I listan på panelen till vänster på sidan trycker du på namnet på den visningsförinställning för Carousel banner som du vill använda. **[!UICONTROL Viewers]**
1. Tryck på hotspot-områden eller bildscheman på bilden för att testa deras associerade åtgärder.

## Publishing Carousel Banners {#publishing-carousel-banners}

Du måste publicera karusellen för att kunna använda den. När du publicerar en Carousel Set aktiveras URL:en och Bädda in kod. Carousel publiceras också i Dynamic Media Cloud, som är integrerat med ett CDN för skalbar och prestandamaterial.

>[!NOTE]
>
>Om du använder en befintlig interaktiv bild med aktiveringspunkter för din Carousel-banderoll måste du publicera den interaktiva bilden separat när du har publicerat karusellbanderollen.
>Om du ändrar en befintlig publicerad interaktiv bild som du använder i en karusellbanderoll måste du publicera den interaktiva bilden innan ändringarna återspeglas i karusellbanderollen.

Mer information om hur du publicerar karusellbanderoller finns i [Publicera dynamiska medieresurser](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md) .

## Lägga till en Carousel-banderoll på din webbplatssida {#adding-a-carousel-banner-to-your-website-page}

När du har överfört banderollbilder för att skapa en karusell, lagt till hotspot-områden och/eller bildscheman i banderollen och publicerat karuselluppsättningen är du nu redo att lägga till den på din befintliga webbsida.

>[!NOTE]
>
>Om du är kund hos AEM Sites kan du lägga till karusellbanderollen direkt på din sida genom att dra Interactive Media-komponenten till din sida. See [Adding Dynamic Media Assets to Pages.](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)

Om du är en fristående AEM kan du dock manuellt lägga till karusellbanderollen på webbplatsens landningssida enligt beskrivningen i detta avsnitt.

1. Kopiera den publicerade Carousel-uppsättningens inbäddningskod.
See [Embedding the Video or Image Viewer on a Web Page](/help/assets/dynamic-media/embed-code.md).

1. Lägg till den inbäddningskod som du kopierade från AEM Assets på din webbsida.
Den kopierade inbäddningskoden är responsiv så den bör automatiskt passa inbäddningsområdet på sidan.

## Integrera Carousel-banderollen med en befintlig snabbvy {#integrating-the-carousel-banner-with-an-existing-quickview}

Obs! det här steget gäller endast om du är en fristående AEM Assets-kund.

Det sista steget i den här processen är att integrera karusellbanderollen med en befintlig snabbvyimplementering på din webbplats. Alla snabba visningsimplementeringar är unika och det behövs ett specifikt tillvägagångssätt som sannolikt inbegriper hjälp av en IT-handläggare på frontend.

Den befintliga snabbvyimplementeringen representerar normalt en kedja av interrelaterade åtgärder som inträffar på webbsidan i följande ordning:

1. En användare utlöser ett element i användargränssnittet för webbplatsen.
1. Slutkoden hämtar en URL för snabbvyn baserat på användargränssnittselementet som utlöstes i steg 1.
1. Front-end-koden skickar en Ajax-begäran med den URL som fås i steg 2.
1. Motstående logik returnerar motsvarande snabbvydata eller innehåll tillbaka till slutkoden.
1. Slutkoden läser in snabbvydata eller -innehåll.
1. Om du vill kan du konvertera den inlästa snabbvyinformationen till en HTML-representation med koden längst fram.
1. I koden visas en modal dialogruta eller panel och HTML-innehållet återges på skärmen för slutanvändaren.

Dessa anrop kanske inte representerar oberoende offentliga API-anrop som kan anropas av webbsidans logik från ett godtyckligt steg. I stället är det ett kedjat anrop där varje steg döljs i den sista fasen (återanrop) av föregående steg.

Samtidigt som Carousel-banderollen ersätter steg 1 och delvis steg 2, när en användare klickar på en hotspot eller bildschema inuti karusellbanderollen, hanteras en sådan användarinteraktion av användaren. Visningsprogrammet returnerar en händelse till webbsidan som innehåller alla hotspot- eller bildschemadata som tidigare lagts till.

I en sådan händelsehanterare gör koden längst fram följande:

* Lyssnar på en händelse som skickas av karusellbanderollen.
* Skapar en URL för snabbvyn baserat på hotspot- eller bildschemats data.
* Startar processen att läsa in snabbvyn från backend-objektet och återge den på skärmen för visning.

Den inbäddningskod som returneras av AEM Assets har redan en färdig händelsehanterare på plats som kommenteras ut.

Därför är det bara nödvändigt att avkommentera koden och ersätta dummy-hanterarens brödtext med koden som är specifik för den aktuella webbsidan.

Processen med att skapa snabbvyns URL är i princip motsatt den process som används för att identifiera hotspot- och bildschemavariabler som beskrivs tidigare.

Se [Identifiera hotspot- och bildschemavariabler](#identifying-hotspot-and-image-map-variables).

Det sista steget för att utlösa snabbvyns URL och aktivera snabbvypanelen kräver troligen hjälp av en IT-handläggare på IT-avdelningen. De har kunskap att lära sig hur man på bästa sätt aktiverar snabbvyimplementeringen från rätt steg med en färdig snabbvywebbadress.

## Använda snabbvyer för att skapa anpassade popup-fönster {#using-quickviews-to-create-custom-pop-ups}

See [Using Quickviews to create custom pop-ups](/help/assets/dynamic-media/custom-pop-ups.md).