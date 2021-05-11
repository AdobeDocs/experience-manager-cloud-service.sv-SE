---
title: Karusellbanner
description: Lär dig hur du arbetar med Carousel Banners i Dynamic Media.
feature: Karusellbanner
role: Business Practitioner
exl-id: 34541302-6610-4f5e-af93-c95328dda910
translation-type: tm+mt
source-git-commit: 78d85d31e03d8190c086a870f2fc2ff1cb00a320
workflow-type: tm+mt
source-wordcount: '4469'
ht-degree: 3%

---

# Karusellbanner{#carousel-banners}

Carousel-banners gör det möjligt för marknadsförare att öka konverteringsgraden genom att enkelt skapa interaktivt roterande marknadsföringsmaterial och leverera det till alla skärmar.

Det kan vara tidskrävande att skapa och ändra innehåll i reklambanners, vilket begränsar möjligheten att snabbt publicera nytt innehåll eller göra det mer riktat. Med Carousel Banners kan du snabbt skapa eller ändra roterande banderoller och lägga till interaktivitet som hotspot-länkar till produktdetaljer eller relaterade resurser. Ni kan leverera dem till alla skärmar och snabbare få ut nytt marknadsföringsmaterial.

Carousel Banners betecknas med en banderoll med ordet **[!UICONTROL CAROUSELSET]**:

![chlimage_1-438](assets/chlimage_1-438.png)

På din webbplats kan en karusellbanderoll se ut så här:

![chlimage_1-439](assets/chlimage_1-439.png)

Här kan du navigera bland bilderna genom att klicka på siffrorna. Dessutom roteras bildrutorna automatiskt baserat på ett tidsintervall som du kan anpassa. Bilder i en karusellbanderoll har stöd för både aktiveringspunkter och bildscheman. Användarna kan antingen trycka eller gå till en hyperlänk eller öppna ett snabbvyfönster.

I det här exemplet har användaren tryckt på eller klickat på ett bildschema och öppnat snabbvyfönstret för handskar:

![chlimage_1-440](assets/chlimage_1-440.png)

## Se hur karusellbanderoller skapas {#watch-how-carousel-banners-are-created}

Titta på en genomgång om [hur karusellbanners skapas](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveCarouselBanner) (längd: 10 minuter och 33 sekunder). Du får också lära dig hur du förhandsgranskar, redigerar och levererar karusellbanderoller.

>[!NOTE]
>
>Icke-administrativa användare måste läggas till i **[!UICONTROL dam-users]**-gruppen för att kunna skapa eller redigera karusellbanderoller. Om du har problem med att skapa eller redigera kontaktar du systemadministratören som kan lägga till dig i gruppen **d[!UICONTROL am-users]**.

## Snabbstart: Carousel Banners {#quick-start-carousel-banners}

Så här kommer du igång snabbt:

1. [Identifiera hotspot- och bildschemavariabler](#identifying-hotspot-and-image-map-variables)  (endast för kunder som använder Adobe Experience Manager Assets + Dynamic Media)

   Börja med att identifiera dynamiska variabler som används i den befintliga snabbvyimplementeringen. Om du gör det blir det lättare att ange aktiveringspunkter och data för bildscheman korrekt när du skapar en karusellbanderoll i Experience Manager Assets.

<!-- LEAVE; COMMERCE BEING ADDED AGAIN IN THE FUTURE

   >[!NOTE]
   >
   >If you are an AEM Sites or Ecommerce customer, you can use the built-in feature to navigate to product pages and lookup the existing skus in the product catalog. You do not need to manually enter hotspot or image map variables.
   >
   >
   >If you are an AEM Assets and Dynamic Media customer, you will manually enter data for hotspots and image maps, and then integrate the published URL or Embed code with your third-party content management system.

-->

1. Valfritt: [Skapa en visningsförinställning för en karuselluppsättning](/help/assets/dynamic-media/managing-viewer-presets.md) om det behövs.

   Om du är administratör kan du anpassa karusellens beteende och utseende genom att skapa en egen förinställning för Carousel-visningsprogrammet. Den största fördelen är att du kan återanvända den här anpassade visningsförinställningen för flera bildspel. Man kan dock anpassa karusellens beteende och utseende direkt när man skapar karusellen. Detta är att föredra när du vill ha en specifik design för en viss karusell.

1. [Överför en bildbanderoll](#uploading-image-banners).

   Överför bildbanderoller som du vill göra interaktiva.

1. [Skapa en Carousel-uppsättning](#creating-carousel-sets).

   I Carousels Sets navigerar användarna genom banderollbilder och trycker på hotspot-områden eller bildscheman för att få tillgång till relevant innehåll.

   Om du vill skapa en karuselluppsättning i Assets trycker du på **[!UICONTROL Create]** och väljer sedan **[!UICONTROL Carousel Sets]**. Lägg till resurser i bilderna och tryck på **[!UICONTROL Save]**. Du kan också redigera karusellens utseende och beteende direkt i redigeraren.

1. [Lägg till aktiveringspunkter eller bildscheman i en bildbanderoll](#adding-hotspots-or-image-maps-to-an-image-banner).

   Lägg till en eller flera hotspot-områden eller bildscheman i en bildbanderoll. Koppla sedan vart och ett till en åtgärd som en länk, en snabbvy eller ett Experience Fragment. När du har lagt till aktiveringspunkter eller bildscheman avslutar du den här uppgiften genom att publicera karuselluppsättningen. Med Publicering skapas den inbäddningskod som du kan använda för att kopiera och tillämpa på webbplatsens landningssida.

   Se [(Valfritt) Förhandsgranska Carousel Banners](#optional-previewing-carousel-banners) - Valfritt. Om du vill kan du visa en representation av karuselluppsättningen och testa dess interaktivitet.

1. [Publicera Carousel Banners](#publishing-carousel-banners).

   Du publicerar en Carousel-uppsättning på samma sätt som andra resurser. Navigera till Carousel Set i Assets, markera den och tryck på **[!UICONTROL Publish]**. När du publicerar en Carousel Set aktiveras URL:en och strängen Embed.

1. Gör något av följande:

   * [Lägg till en karusellbanderoll på webbplatsens ](#adding-a-carousel-banner-to-your-website-page)sidaDu kan lägga till karusellbanderollens URL eller inbäddningskod som du har kopierat till webbplatsens sida.

      * [Integrera karusellbanderollen med en befintlig snabbvy](#integrating-the-carousel-banner-with-an-existing-quickview). Om du använder ett tredjepartssystem för hantering av webbinnehåll måste du integrera den nya Carousel-banderollen med den befintliga snabbvyimplementeringen på din webbplats.
   * [Lägg till en karusellbanderoll på Experience Manager](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md). Om du använder Experience Manager Sites kan du lägga till karuselluppsättningen direkt på sidan med hjälp av komponenten Interactive Media.


Om du måste redigera Carousel-uppsättningar läser du [redigera Carousel-uppsättningar](#editing-carousel-sets). Dessutom kan du visa och redigera [Carousel Set-egenskaper](/help/assets/manage-digital-assets.md#editing-properties).

## Identifiera aktiveringspunkt- och bildschemavariabler {#identifying-hotspot-and-image-map-variables}

Börja med att identifiera dynamiska variabler som används i den befintliga snabbvyimplementeringen. Med den här metoden kan du ange aktiveringspunkter eller data för bildscheman korrekt när du skapar Carousel-uppsättningar i Experience Manager Assets.

När du lägger till aktiveringspunkter eller bildscheman i en banderollbild tilldelar du en SKU (Stock Keeping Unit). Du kan också tilldela extra variabler till varje hotspot eller bildschema. Sådana variabler används senare för att matcha aktiveringspunkter eller bildscheman med snabbvyinnehållet.

<!-- LEAVE; COMMERCE BEING ADDED LATER

>[!NOTE]
>
>If you are an AEM Sites and/or AEM Ecommerce customer, skip this step. You do not need to manually identify hotspot or image map variables; you can use the integration with Ecommerce for product integration. See information on [setting up eCommerce](/help/sites-cloud/administering/generic.md). In addition, you can use the Interactive component and add it to your web page.
>
>If you are an AEM Assets or Media customer, you publish the URL or Embed code and then integrate with your third-party content management system and identify hotspots and image maps manually.

-->

Det är viktigt att kunna identifiera antalet och typen av variabler som ska kopplas till hotspot- eller bildschemadata. Varje hotspot eller bildschema som läggs till i en banderollbild måste innehålla tillräckligt med information för att entydigt identifiera produkten i det befintliga back-end-systemet. Se samtidigt till att varje hotspot eller bildschema inte innehåller mer data än nödvändigt. Orsaken är att det skulle göra inmatningsprocessen alltför komplex och pågående hotspot- eller bildschemahantering mer felbenägen.

Det finns olika sätt att identifiera en uppsättning variabler som ska användas för hotspot- eller bildschemaddata.

Ibland räcker det att rådfråga IT-specialister som ansvarar för den befintliga snabbvyimplementeringen. De vet troligtvis vilken minimiuppsättning data som krävs för att identifiera snabbvyn i systemet. Det är dock möjligt att helt enkelt analysera det befintliga beteendet för koden.

De flesta implementeringar av snabbvyn använder följande paradigm:

* Användaren aktiverar ett element i användargränssnittet på webbplatsen. Till exempel trycker de på en **[!UICONTROL Quick View]**-knapp.
* Webbplatsen skickar en Ajax-begäran till baksidan för att läsa in data eller innehåll i snabbvyn, om det behövs.
* Snabbvydata översätts till innehållet som förberedelse för återgivning på webbsidan.
* Slutligen återges sådant innehåll på skärmen visuellt i koden.

Då besöker man olika delar av den befintliga webbplatsen där snabbvyfunktionen används. Starta sedan snabbvyn och hämta den Ajax-URL som webbsidan skickar för att läsa in snabbvydata eller -innehåll.

Normalt behöver du inte använda några specialverktyg för felsökning. Moderna webbläsare har webbinspektörer som klarar ett bra jobb. Nedan följer några exempel på webbläsare som innehåller webbinspektörer:

* Om du vill visa alla utgående HTTP-begäranden i Google Chrome trycker du på F12 (Windows®) eller Command-Option-I (Mac) för att öppna panelen för utvecklingsverktyget. Tryck på fliken Nätverk.
* I Firefox kan du antingen aktivera plugin-programmet för Firebug genom att trycka på F12 (Windows®) eller Kommando-Alternativ-I (Mac). Använd fliken Nätverk eller det inbyggda verktyget Granska och fliken Nätverk.

När nätverksövervakning är aktiverat i webbläsaren utlöser du snabbvyn på sidan.

Nu hittar du snabbvyns Ajax-URL i nätverksloggen och kopierar den inspelade URL:en för framtida analys. Vanligtvis skickas flera begäranden till servern när du utlöser snabbvyn. Vanligtvis är snabbvyns Ajax-URL en en av de första i listan. Den har antingen en komplex frågesträngsdel eller sökväg och dess MIME-svarstyp är antingen `text/html`, `text/xml` eller `text/javascript`.

Under den här processen är det viktigt att du besöker olika delar av webbplatsen, med olika produktkategorier och typer. Anledningen är att URL:er för snabbvyn har delar som är gemensamma för en viss webbplatskategori, men som bara ändras om du besöker ett annat område på webbplatsen.

I det enklaste fallet är den enda variabeldelen i snabbvyns URL produktens SKU. I det här fallet är SKU-värdet den enda datadel som du behöver för att lägga till aktiveringspunkter eller bildscheman i banderollbilden.

I komplexa fall har dock URL:en för snabbvyn olika element förutom SKU:n. Vissa av dessa element omfattar kategori-ID, färgkod, storlekskod o.s.v. I sådana fall är varje element en separat variabel i hotspot- eller bildschemats datadefinition i karusellbanderollfunktionen.

Titta på följande exempel på URL:er för snabbvyn och deras resulterande hotspot- eller bildschemavariabler:

<table>
 <tbody>
  <tr>
   <td>En SKU, hittades i frågesträngen.</td>
   <td><p>De inspelade URL-adresserna för snabbvyn innehåller följande:</p>
    <ul>
     <li><p><code>https://server/json?productId=866558&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1196184&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1081492&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1898294&amp;source=100</code></p> </li>
    </ul> <p>Den enda variabeldelen i URL:en är värdet på frågesträngsparametern <code>productId=</code>, och det är tydligt ett SKU-värde. Därför behöver aktiveringspunkter och bildscheman bara SKU-fält med värden som <code>866558,</code> <code>1196184,</code> <code>1081492,</code> <code>1898294.</code></p> </td>
  </tr>
  <tr>
   <td>En SKU, finns i URL-sökvägen.</td>
   <td><p>De inspelade URL-adresserna för snabbvyn innehåller följande:</p>
    <ul>
     <li><p><code>https://server/product/6422350843</code></p> </li>
     <li><p><code>https://server/product/1607745002</code></p> </li>
     <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>Variabeldelen finns i den sista delen av sökvägen och blir SKU-värdet för hotspot-områden/bildscheman:<strong><code>6422350843</code>, <code>1607745002,</code> </strong><code>0086724882.</code></p> </td>
  </tr>
  <tr>
   <td>SKU och kategori-ID i frågesträngen.</td>
   <td><p>De inspelade URL-adresserna för snabbvyn innehåller följande:</p>
    <ul>
     <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
     <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
     <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>I det här fallet finns det två olika delar i URL:en. SKU:n lagras i parametern <code>prodId</code> och kategori-ID:t lagras i parametern <code>category=</code>.</p> <p>Definitionerna av hotspot/bildschema är par. Det vill säga ett SKU-värde och en extra variabel som heter <code>categoryId</code>. De resulterande paren är följande:</p>
    <ul>
     <li><p>SKU är <strong><code>305466</code></strong> och <code>categoryId</code> är <code>1100004</code>.</p> </li>
     <li><p>SKU är <strong><code>310181</code></strong> och <code>categoryId</code> är <strong><code>1100004</code></strong>.</p> </li>
     <li><p>SKU är <strong><code>308706</code></strong> och <code>categoryId</code> är <strong><code>1740148</code></strong>.</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Överför bildbanderoller {#uploading-image-banners}

Om du redan har överfört de bilder du vill använda går du vidare till nästa steg, [Skapa Carousel-uppsättningar](#creating-carousel-sets). De bilder som används i karusellen måste överföras när Dynamic Media har aktiverats.

Information om hur du överför bildbanderoller finns i [Överföra resurser](/help/assets/manage-digital-assets.md).

## Skapar Carousel-uppsättningar {#creating-carousel-sets}

>[!NOTE]
>
>Icke-administrativa användare måste läggas till i **[!UICONTROL dam-users]**-gruppen för att kunna skapa eller redigera karusellbanderoller. Om du har problem med att skapa eller redigera kontaktar du systemadministratören som kan lägga till dig i **[!UICONTROL dam-users]**-gruppen.

**Så här skapar du en Carousel-uppsättning:**

1. I Resurser navigerar du till den mapp där du vill skapa Carousel-uppsättningen och trycker på **[!UICONTROL Create > Carousel Set]**.
1. På Carousel Banner Editor-sidan trycker du på **[!UICONTROL Tap to open Asset Selector]** för att välja bilden för din första bild.

   Gör något av följande på Carousel Banner Editor-sidan:

   * I närheten av sidans övre vänstra hörn trycker du på ikonen **[!UICONTROL Add Slide]**.

   * I mitten av sidan trycker du på **[!UICONTROL Tap to open Asset Selector]**.
   Tryck här för att välja resurser som du vill inkludera i karuselluppsättningen. De markerade resurserna har en bockmarkeringsikon. När du är klar trycker du **[!UICONTROL Select]** i det övre högra hörnet på sidan.

   Med resursväljaren kan du söka efter resurser genom att skriva ett nyckelord och trycka eller klicka på **[!UICONTROL Return]**. Du kan också använda filter för att förfina sökresultatet. Du kan filtrera efter sökväg, samling, filtyp och tagg. Markera filtret och tryck sedan på ikonen **[!UICONTROL Filter]** i verktygsfältet. Ändra vyn genom att trycka på ikonen Visa och sedan välja **[!UICONTROL Column View]**, **[!UICONTROL Card View]** eller **[!UICONTROL List View]**.

   Mer information finns i [Arbeta med väljare](/help/assets/dynamic-media/working-with-selectors.md).

1. Fortsätt med att lägga till bilder tills du har lagt till alla bilder som du vill rotera genom i Carousel-uppsättningen.
1. (Valfritt) Gör något av följande:

   * Om det behövs kan du dra bildrutorna för att ändra ordning på bilderna i listan.
   * Om du vill ta bort en bild markerar du bilden och trycker sedan på **[!UICONTROL Delete Slide]** i verktygsfältet.

   * Om du vill använda en förinställning trycker du på den förinställda listrutan längst upp till höger på sidan och väljer sedan en förinställning som ska användas på uppsättningen samtidigt.
   Om du vill ta bort en bildruta trycker eller klickar du på bildrutan och trycker eller klickar på **[!UICONTROL Delete Slide]** i verktygsfältet. Om du vill flytta en bildruta trycker du på ikonen för att ändra ordning och håller ned och flyttar till önskad plats.

1. När du har lagt till bilderna i bildrutor kan du lägga till en aktiveringspunkt, ett bildschema eller båda delarna. Se [lägga till aktiveringspunkter eller bildscheman](#adding-hotspots-or-image-maps-to-an-image-banner).
1. Du kan ändra den visuella designen och beteendet för karuselluppsättningar. Tryck eller klicka på flikarna **[!UICONTROL Behavior]** och **[!UICONTROL Appearance]** och justera hur karusellbanderollen visas eller hur specifika komponenter fungerar. Mer information om hur du använder visningsprogramredigeraren finns i [hantera visningsförinställningar](/help/assets/dynamic-media/viewer-presets.md).

   >[!NOTE]
   >
   >För Carousel-banners kan du justera följande:
   >
   >* Längd som en bild visas. Som standard visas varje bild i 9 sekunder.
   >* Animering. Som standard tonas varje bildruteövergång ut. Du kan ändra det till en bildövergång.
   >* Knapparnas format. Användarna kan rotera genom banners genom att trycka på varje punkt eller nummer. Du kan ändra var de angivna indikatorknapparna visas (och om de är numeriska eller prickade) och hur stora de är.
   >* Ändra markeringsformatet för ett bildschema eller ikonen som används för aktiveringspunkter.
   >* Innan du redigerar en visningsförinställning väljer du det format som du vill basera förinställningen på. Om du inte väljer ett format förlorar du alla ändringar när du börjar redigera visningsförinställningen om du ändrar till en annan förinställning.


   Du kan också förhandsgranska karusellbanderollens utseende. Se [(Valfritt) Förhandsgranska Carousel Banners](#optional-previewing-carousel-banners).

1. Tryck på **[!UICONTROL Save]** när du är klar.

## Lägga till aktiveringspunkter eller bildscheman i en bildbanderoll {#adding-hotspots-or-image-maps-to-an-image-banner}

Du kan lägga till aktiveringspunkter eller bildscheman i en banderoll med hjälp av Carousel Set-redigeraren.

När du lägger till aktiveringspunkter eller bildscheman kan du definiera dem som en snabbvypopup-visning, som en hyperlänk eller som en upplevelsefragment.

Se [Experience Fragment](/help/sites-cloud/authoring/fundamentals/experience-fragments.md).

>[!NOTE]
>
>Delningsverktygen för sociala medier i Carousel Banner stöds inte när du bäddar in visningsprogrammet i en Experience Fragment.
>
>Du kan undvika det här problemet genom att använda eller skapa visningsförinställningar som inte har verktyg för delning av sociala medier. Med sådana visningsförinställningar kan du bädda in dem i Experience Fragments.

Kom ihåg att spara ditt arbete när du lägger till hotspot-områden eller bildscheman i en bild. Alternativen Ångra och Gör om, nära det övre högra hörnet på sidan, stöds under den aktuella skaps-/redigeringssessionen.

När du är klar med att skapa en karusellbanderoll kan du använda Förhandsgranska för att se hur karusellbanderollen ser ut för kunderna.

Se [(Valfritt) Förhandsgranska Carousel Banners](#optional-previewing-carousel-banners).

>[!NOTE]
>
>När du lägger till aktiveringspunkter i en bildbanderoll lagras hotspot-informationen på samma metadataplats, i förhållande till bildens plats. Denna punkt gäller oavsett om det är en interaktiv bild eller en Carousel-banderoll. Den här funktionen innebär att du enkelt kan återanvända samma bild tillsammans med dess definierade hotspot-data i båda visningsprogrammen.
Observera dock att Carousel Banners stöder bildscheman på bilder som även kan innehålla hotspot-områden. en interaktiv bild gör det inte. Tänk på detta om du tänker skapa en interaktiv bild eller Carousel Banner som använder samma bild. Överväg att skapa interaktiva bilder och Carousel Banners med separata kopior av samma bild istället.

>[!NOTE]
Om du redigerar interaktiva bilder med aktiveringspunkter och beskär bilden tas dina aktiveringspunkter bort.

<!-- See also [Adding Image Maps](/help/assets/image-maps.md). -->

**Så här lägger du till aktiveringspunkter eller bildscheman i en bildbanderoll:**

1. Navigera från Assets till karuselluppsättningen som du vill göra interaktiv.
1. Markera karuselluppsättningen och tryck på **[!UICONTROL Edit]**. Carousel Viewer Editor öppnas.
1. Markera den bildruta som du vill göra interaktiv.
1. I det övre vänstra hörnet av sidan trycker du på **[!UICONTROL Hotspot]** eller **[!UICONTROL Image Map]**.
1. Gör något av följande:

   * För aktiveringspunkter: Tryck på den plats i bilden där du vill att hotspot-området ska visas.
   * För bildscheman: Klicka på bilden och dra sedan från det övre vänstra hörnet till det nedre högra hörnet för att skapa bildschemaområdet. Du kan justera storleken på bildschemat genom att dra i hörnen.

   Om det behövs drar du hotspot- eller bildschemat till en ny plats. Du kan också använda piltangenterna på tangentbordet för att styra positionen för ett markerat hotspot-område. Lägg till fler hotspot-områden eller bildscheman efter behov.

   Tryck på fliken **[!UICONTROL Actions]** om du vill ta bort ett hotspot-område eller bildschema. Under rubriken **[!UICONTROL Maps & Hotspots]** väljer du namnet på den hotspot eller bildschema som du vill ta bort från listrutan **[!UICONTROL Selected Type]**. Tryck på ikonen **[!UICONTROL Trash]** bredvid menyn och tryck sedan på **[!UICONTROL Delete]**.

1. Skriv namnet på aktiveringspunkten eller bildschemat i textfältet Namn. Det här namnet visas också i listrutan **[!UICONTROL Maps & Hotspot]**. Genom att ange ett namn blir det enkelt att identifiera hotspot-området eller bildschemat om du bestämmer dig för att ändra det i framtiden.
1. Gör något av följande på fliken **[!UICONTROL Actions]**:

   * Tryck på **[!UICONTROL Quick view]**.

      * Om du använder Experience Manager Sites <!-- and Ecommerce--> trycker du på produktväljarens ikon (förstoringsglas) för att öppna produktsidan. Om du vill gå tillbaka till Carousel Banner Editor trycker du på den produkt du vill använda och sedan på bockmarkeringen i det övre högra hörnet på sidan.
      * Om du inte är kund i Experience Manager Sites <!-- or Ecommerce -->:

         * Definiera variabler. Se [Identifiera hotspot-variabler](#identifying-hotspot-and-image-map-variables).
         * Ange sedan SKU-värdet manuellt. I textfältet SKU-värde skriver du produktens SKU (Stock Keeping Unit), som är en unik identifierare för varje separat produkt eller tjänst som du erbjuder. Det angivna SKU-värdet fyller automatiskt i variabeldelen av snabbvymallen. Systemet kan nu koppla den aktiveringspunkt som användaren knackar på till en viss SKU:s snabbvy.
         * (Valfritt) Om det finns andra variabler i snabbvyn som du måste använda för att identifiera en produkt ytterligare trycker du på **[!UICONTROL Add Generic Variable]**. Ange en extra variabel i textfältet. Till exempel är category=Mens en tillagd variabel.

         * Mer information finns i [Arbeta med väljare](/help/assets/dynamic-media/working-with-selectors.md).
   * Tryck på **[!UICONTROL Hyperlink]**.

      * Om du är kund hos AEM Sites trycker du på ikonen Platsväljare (mapp) för att navigera till en URL.

         >[!NOTE]
         Den URL-baserade länkningsmetoden är inte möjlig om det interaktiva innehållet har länkar till relativa URL-adresser, särskilt länkar till AEM Sites-sidor.

      * Om du är en fristående kund anger du den fullständiga URL-sökvägen till en länkad webbsida i href-textfältet.

   Var noga med att ange om länken ska öppnas på en ny webbläsarflik (rekommenderat standardvärde) eller på samma flik.

   Mer information finns i [Arbeta med väljare](/help/assets/dynamic-media/working-with-selectors.md).

   * Tryck på **[!UICONTROL Experience Fragment]**.

      * Om du är AEM Sites-kund trycker du på ikonen Sök (förstoringsglas) för att öppna sidan Experience Fragment. Om du vill gå tillbaka till sidan för hantering av hotspot trycker du på det Experience Fragment du vill använda och sedan på Select (Välj) längst upp till höger på sidan.
Se [Upplevelsefragment](/help/sites-cloud/authoring/fundamentals/experience-fragments.md).

      * Ange bredd och höjd för Experience Fragment så som det visas på banderollen.

         >[!NOTE]
         Delningsverktygen för sociala medier i Carousel Banner stöds inte när du bäddar in visningsprogrammet i en Experience Fragment.
         Om du vill kringgå den här punkten kan du använda eller skapa visningsförinställningar som inte har verktyg för delning av sociala medier. Med sådana visningsförinställningar kan du bädda in dem i Experience Fragments.
   ![experience_fragment-carouselbanner](assets/experience_fragment-carouselbanner.png)

   Du kan också förhandsgranska karusellbanderollens utseende. Se [(Valfritt) Förhandsgranska Carousel Banners](#optional-previewing-carousel-banners).

1. Tryck på **[!UICONTROL Save]**.
1. Publicera karuselluppsättningen. Publicering skapar den inbäddningskod eller URL som du kan använda på din webbsida. Om du är kund på Experience Manager Sites lägger du till karuselluppsättningen direkt på din webbsida.

   Se [Publicera resurser](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

   Se [Lägga till en Carousel-uppsättning på webbplatsens landningssida](#adding-a-carousel-banner-to-your-website-page)

## Redigera Carousel-uppsättningar {#editing-carousel-sets}

>[!NOTE]
Icke-administrativa användare måste läggas till i **[!UICONTROL dam-users]**-gruppen för att kunna skapa eller redigera karusellbanderoller. Om du har problem med att skapa eller redigera kontaktar du systemadministratören som kan lägga till dig i **[!UICONTROL dam-users]**-gruppen.

Du kan utföra olika redigeringsåtgärder på Carousel Sets, till exempel:

* Lägg till bilder i en Carousel-uppsättning. Se även [Arbeta med väljare](/help/assets/dynamic-media/working-with-selectors.md).
* Ändra ordning på bilderna i Carousel Set.
* Ta bort resurser i Carousel-uppsättningen.
* Använd en visningsförinställning.
* Ta bort Carousel-uppsättningen.
* Lägg till eller redigera hotspot-områden och bildscheman. Se även [Arbeta med väljare](/help/assets/dynamic-media/working-with-selectors.md).

**Så här redigerar du en Carousel-uppsättning:**

1. Gör något av följande:

   * Håll pekaren över en Carousel Set-resurs och tryck sedan på **[!UICONTROL Edit]** (pennikon).
   * Håll pekaren över en Carousel Set-resurs, tryck på **[!UICONTROL Select]** (bockmarkeringsikon) och tryck sedan på **[!UICONTROL Edit]** i verktygsfältet.

   * Tryck på en Carousel Set-resurs och tryck sedan på **[!UICONTROL Edit]** (pennikon) i det övre vänstra hörnet av sidan.

1. Om du vill redigera Carousel-uppsättningen gör du något av följande:

   * Om du vill lägga till en bildruta trycker du på ikonen **[!UICONTROL Add Slide]**. Navigera till den resurs som du vill lägga till i bildrutan och tryck eller klicka på bockmarkeringen.
   * Om du vill ändra ordning på bildrutorna drar du en bildruta till en ny plats (markera sorteringsikonen för att flytta objekt).
   * Om du vill lägga till ett hotspot- eller bildschema klickar du på ikonerna för hotspot eller bildschema och läser [lägga till hotspot-områden och bildscheman](#adding-hotspots-or-image-maps-to-an-image-banner).
   * Om du vill redigera karuselluppsättningens utseende eller beteende trycker du på fliken **[!UICONTROL Appearance]** eller **[!UICONTROL Behavior]** och anger sedan önskade alternativ.
   * Om du vill redigera aktiveringspunkter eller bildscheman markerar du ett hotspot-område eller bildschema på lämplig bildruta. Gör ändringarna på fliken **[!UICONTROL Actions]**.
   * Om du vill ta bort en bildruta markerar du den och trycker sedan på **[!UICONTROL Delete Slide]** i verktygsfältet.
   * Om du vill använda en förinställning trycker du på listrutan **[!UICONTROL Preset]** längst upp till höger på sidan och väljer sedan en visningsförinställning.
   * Om du vill ta bort en hel Carousel-uppsättning går du till Carousel-uppsättningen, markerar den och trycker sedan på **[!UICONTROL Delete]**.

   >[!NOTE]
   Om du redigerar interaktiva bilder med aktiveringspunkter och beskär bilden tas dina aktiveringspunkter bort.

## (Valfritt) Förhandsgranska Carousel Banners {#optional-previewing-carousel-banners}

Du kan använda Förhandsgranska för att se hur karusellbanderollen ser ut för kunderna. Med Förhandsgranska kan du också testa karusellbanderollens hotspot-områden och bildscheman för att se om de fungerar som förväntat.

När du är nöjd med karusellbanderollen kan du publicera den.
Se [Bädda in video- eller bildvisningsprogrammet på en webbsida](/help/assets/dynamic-media/embed-code.md).
Se [Länka URL:er till ditt webbprogram](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md). Den URL-baserade länkningsmetoden är inte möjlig om det interaktiva innehållet har länkar till relativa URL-adresser, särskilt länkar till AEM Sites-sidor.
Se [Lägga till Dynamic Media Assets på sidor](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

Du kan förhandsgranska karusellbanners i Carousel Editor (föredragen metod) eller i **[!UICONTROL Viewers]**-listan.

**Så här förhandsgranskar du Carousel banners:**

1. I **[!UICONTROL Assets]** navigerar du till en befintlig Carousel-banderoll som du har skapat och trycker för att öppna den.
1. Tryck på **[!UICONTROL Edit]**.
1. I listan med visningsförinställningar i det högra hörnet av verktygsfältet väljer du ett visningsprogram för att förhandsvisa karusellbanderollen.

   ![experience_fragment-carouselbanner-viewerdropdown](assets/experience_fragment-carouselbanner-viewerdropdown.png)

1. Tryck på **[!UICONTROL Preview]**.
1. Tryck på hotspot-områden eller bildscheman på bilden för att testa deras associerade åtgärder.

**Så här förhandsgranskar du Carousel banners från visningslistan:**

1. I **[!UICONTROL Assets]** navigerar du till en befintlig Carousel-banderoll som du har skapat och trycker för att öppna den.
1. Klicka på ikonen Innehåll i det övre vänstra hörnet på sidan Förhandsvisa.
1. I listan **[!UICONTROL Viewers]** på panelen till vänster på sidan trycker du på namnet på den visningsförinställning för Carousel banner som du vill använda.
1. Tryck på hotspot-områden eller bildscheman på bilden för att testa deras associerade åtgärder.

## Publishing Carousel Banners {#publishing-carousel-banners}

Om du vill använda karusellen måste du publicera den. När du publicerar en Carousel Set aktiveras URL:en och Bädda in kod. Carousel publiceras också i Dynamic Media Cloud, som är integrerat med ett CDN för skalbar och högpresterande leverans.

>[!NOTE]
Om du använder en befintlig interaktiv bild med aktiveringspunkter för din Carousel-banderoll måste du publicera den interaktiva bilden separat när du har publicerat karusellbanderollen.
Om du ändrar en befintlig publicerad interaktiv bild som du använder i en karusellbanderoll publicerar du den interaktiva bilden så att ändringarna återspeglas i karusellbanderollen.

Se [Publicera Dynamic Media Assets](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md) för mer information om hur du publicerar Carousel-banners.

## Lägga till en Carousel-banderoll på din webbplatssida {#adding-a-carousel-banner-to-your-website-page}

När du har överfört banderollbilder för att skapa en karusell, tillagda hotspot-områden eller bildscheman, eller båda, till banderollen. Carousel-uppsättningen publicerades. Nu kan du lägga till den på din befintliga webbsida.

>[!NOTE]
Om du är kund hos AEM Sites kan du lägga till karusellbanderollen direkt på din sida genom att dra Interactive Media-komponenten till din sida. Se [Lägga till Dynamic Media-resurser på sidor](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

Om du däremot är en fristående kund som använder Experience Manager Assets kan du lägga till karusellbanderollen manuellt på webbplatsens landningssida.

1. Kopiera den publicerade Carousel-uppsättningens inbäddningskod.
Se [Bädda in video- eller bildvisningsprogrammet på en webbsida](/help/assets/dynamic-media/embed-code.md).

1. Lägg till den inbäddningskod som du kopierade från Experience Manager Assets på webbsidan.
Den kopierade inbäddningskoden är responsiv så den passar automatiskt sidans inbäddningsområde.

## Integrera Carousel Banner med en befintlig snabbvy {#integrating-the-carousel-banner-with-an-existing-quickview}

Obs! det här steget gäller endast om du är en fristående AEM Assets-kund.

Det sista steget i den här processen är att integrera karusellbanderollen med en befintlig snabbvyimplementering på din webbplats. Varje implementering av snabbvyn är unik och det behövs ett specifikt tillvägagångssätt som vanligtvis inbegriper hjälp av en IT-handläggare.

Den befintliga snabbvyimplementeringen representerar normalt en kedja av interrelaterade åtgärder som inträffar på webbsidan i följande ordning:

1. En användare utlöser ett element i användargränssnittet för webbplatsen.
1. Slutkoden hämtar en URL för snabbvyn baserat på användargränssnittselementet som utlöstes i steg 1.
1. Front-end-koden skickar en Ajax-begäran med den URL som fås i steg 2.
1. Bakgrundslogiken returnerar motsvarande snabbvydata eller innehåll tillbaka till slutkoden.
1. Slutkoden läser in snabbvydata eller -innehåll.
1. Om du vill kan du konvertera den inlästa snabbvyinformationen till en HTML-representation med koden längst fram.
1. I koden visas en modal dialogruta eller panel och HTML-innehållet återges på skärmen för slutanvändaren.

Dessa anrop representerar inte oberoende offentliga API-anrop som kan anropas av webbsidans logik från ett godtyckligt steg. I stället är det ett kedjat anrop där varje steg döljs i den sista fasen (återanrop) av föregående steg.

Samtidigt som Carousel-banderollen ersätter steg 1 och delvis steg 2, när en användare klickar på en hotspot eller bildschema, hanteras sådan interaktion av användaren. Visningsprogrammet returnerar en händelse till webbsidan som innehåller alla hotspot- eller bildschemadata som tidigare lagts till.

I en sådan händelsehanterare gör koden längst fram följande:

* Lyssnar på en händelse som skickas av karusellbanderollen.
* Skapar en URL för snabbvyn baserat på hotspot- eller bildschemats data.
* Startar processen att läsa in snabbvyn från bakänden och återge den på skärmen för visning.

Den inbäddningskod som returneras av AEM Assets har redan en färdig händelsehanterare på plats som kommenteras ut.

Därför är det bara nödvändigt att avkommentera koden och ersätta dummy-hanterarens brödtext med koden som är specifik för den aktuella webbsidan.

Processen med att skapa snabbvyns URL är motsatt den process som används för att identifiera hotspot- och bildschemavariabler som beskrivs tidigare.

Se [Identifiera hotspot- och bildschemavariabler](#identifying-hotspot-and-image-map-variables).

Det sista steget för att utlösa snabbvyns URL-adress och aktivera snabbvypanelen kräver troligen hjälp av en IT-handläggare på IT-avdelningen. De har kunskap att lära sig hur man på bästa sätt aktiverar snabbvyimplementeringen från rätt steg med en färdig snabbvywebbadress.

## Använda snabbvyer för att skapa anpassade popup-fönster® {#using-quickviews-to-create-custom-pop-ups}

Se [Använda snabbvyer för att skapa anpassade popup-fönster®](/help/assets/dynamic-media/custom-pop-ups.md).
