---
title: Interaktiva bilder
description: Lär dig hur du arbetar med interaktiva bilder i Dynamic Media
translation-type: tm+mt
source-git-commit: d992b68d4a015f8f947167b5b1d5f0a1ac5c09ec
workflow-type: tm+mt
source-wordcount: '4220'
ht-degree: 1%

---


# Interactive images{#interactive-images}

Du kan enkelt skapa statiska bilder med engagerande upplevelser för kunderna genom att dra och släppa&quot;köpbara&quot; hotspot-områden på en bild. De köpbara hotspotten kombinerar ytterligare information om en produkt eller tjänst med en direktförsäljningsfunktion,&quot;Lägg i kundvagnen&quot; eller&quot;Köp&quot;. Kunderna kan trycka eller klicka på dessa hotspot-områden och länkas direkt till produkten eller tjänsten, lägga till den i en kundvagn eller länkas till en webbsida. Direktupplevelser som dessa ökar kundernas engagemang och konverteringsgrad på er webbplats.

Här följer en köpbar banderoll med popup-fönstret QuickView. En användare aktiverar snabbvyn genom att trycka på cirkeln eller aktiveringspunkten på modellen.

![chlimage_1-152](assets/chlimage_1-368.png)

Se [interaktiva bilder in action](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion-QVzoom/index2-shoppable.html) på webbsidan som visas ovan.

## Se hur interaktiva bildbanderoller skapas {#watch-how-interactive-image-banners-are-created}

Titta på en genomgång på 10 minuter och 33 sekunder om [hur interaktiva bildbanderoller skapas](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveCarouselBanner). Du får också lära dig att förhandsgranska, redigera och leverera interaktiva bildbanderoller.

## Snabbstart: Interaktiva bilder {#quick-start-interactive-images}

Följande steg-för-steg-beskrivning av arbetsflödet hjälper dig att komma igång snabbt med interaktiva bilder i AEM Assets.

Leta efter rubriken **Exempel** i några av snabbstartsåtgärderna. Den innehåller en kort självstudiekurs som baseras på ett exempel på en [webbsida som ännu inte har Interactive Images tillagd](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html).



Självstudiekursen visar hur du integrerar interaktiva bilder på din egen webbplats.

Interactive Images:

1. **(Valfritt) Identifiera hotspot-variabler** - Om du använder fristående AEM Assets och Dynamic Media börjar du med att identifiera dynamiska variabler som används i den befintliga QuickView-implementeringen så att du kan ange hotspot-data när du skapar den interaktiva bilden. Se [(Valfritt) Identifiera hotspot-variabler](#optional-identifying-hotspot-variables).
Men om du använder AEM Sites, eller AEM e-handel, eller båda, är det här steget inte nödvändigt.

1. **(Valfritt) Skapa en förinställning** för Interactive Image Viewer - Anpassa den grafiska bild som används för att representera aktiveringspunkter. Du behöver inte skapa en egen förinställning för Interactive Image Viewer om du tänker använda den färdiga Interactive Image Viewer-förinställningen med namnet `Shoppable_Banner` .
Se [(Valfritt) Skapa en förinställning](/help/assets/dynamic-media/managing-viewer-presets.md#creating-a-new-viewer-preset)för visningsprogrammet för interaktiva bilder.

1. **Överför en bildbanderoll** - Överför bildbanderoller som du vill göra interaktiva.
Se [Överföra en bildbanderoll](#uploading-an-image-banner).

1. **Lägga till aktiveringspunkter i en bildbanderoll** - Lägg till en eller flera hotspot-områden i en bildbanderoll och koppla dem till en åtgärd som en hyperlänk, en snabbvy eller ett Experience Fragment. När du har lagt till aktiveringspunkter avslutar du den här uppgiften genom att publicera den interaktiva bilden.
Se [Lägga till aktiveringspunkter i en bildbanderoll](#adding-hotspots-to-an-image-banner).
Se [Förhandsvisa interaktiva bilder](#optional-previewing-interactive-images) - valfritt. Om du vill kan du visa en representation av din köpbara banner och testa dess interaktivitet.
Mer information om hur du publicerar interaktiva bildresurser finns i [Publicera resurser](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md) .

1. **Lägga till en interaktiv bild till din webbplats eller till din webbplats i AEM** Om du använder AEM Sites eller AEM e-handel, eller båda, kan du lägga till den interaktiva bilden direkt på en webbsida i AEM genom att dra komponenten Interactive Media till sidan. See [Adding Dynamic Media Assets to Pages.](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)
Om du använder fristående AEM Assets och Dynamic Media måste du kopiera den inbäddade koden på webbplatsen och sedan integrera den med din befintliga QuickView. Se [Integrera en interaktiv bild med webbplatsen](#integrating-an-interactive-image-with-your-website).
Om du använder en WCM-fil (Web Content Manager) från tredje part måste du integrera den nya interaktiva videon med den befintliga QuickView-implementeringen som används på webbplatsen. Se [Integrera en interaktiv bild med en befintlig snabbvy](#integrating-an-interactive-image-with-an-existing-quickview).

## (Valfritt) Identifiera hotspot-variabler {#optional-identifying-hotspot-variables}

>[!NOTE]
>
>Den här aktiviteten krävs bara om följande är sant:
>
>* Du vill lägga till interaktivitet i bilden genom att aktivera snabbvyer.
>* Er implementering av AEM använder *inte* ett ramverk för e-handelsintegration för att hämta in produktdata till AEM från någon e-handelslösning som IBM Websphere Commerce, Elastic Path, hybris eller Intershop.

>
>
Om din implementering av AEM använder e-handel kan du hoppa över den här uppgiften och fortsätta med nästa uppgift.

Börja med att identifiera dynamiska variabler som används i den befintliga QuickView-implementeringen så att du kan ange hotspot-data för att skapa den interaktiva bilden.

När du lägger till aktiveringspunkter i en banderollbild i AEM Assets måste du tilldela en SKU (Stock Keeping Unit) en unik identifierare för varje enskild produkt eller tjänst som du erbjuder) och valfria ytterligare variabler för varje hotspot. Sådana hotspot-variabler används senare för att matcha hotspot-områden med Quickview-innehåll.

Det är viktigt att kunna identifiera antalet och typen av variabler som ska kopplas till hotspot-data. Varje hotspot som läggs till i en banderollbild måste innehålla tillräckligt med information för att entydigt identifiera produkten i det befintliga backend-systemet.

Det finns olika sätt att identifiera en uppsättning variabler som ska användas för hotspot-data.

Ibland kan det räcka att rådfråga IT-specialister som är ansvariga för den befintliga QuickView-implementeringen, eftersom de troligen vet vilken minimiuppsättning data som behövs för att identifiera Quickview i systemet. I de flesta fall går det dock även att bara analysera den befintliga beteendet för koden.

De flesta QuickView-implementeringar använder följande paradigm:

* Användaren aktiverar ett element i användargränssnittet på webbplatsen. Om du till exempel klickar på en snabbvyknapp.
* Webbplatsen skickar en Ajax-begäran till serverdelen för att läsa in QuickView-data eller -innehåll vid behov.
* Quickview-data översätts till innehållet som förberedelse för återgivning på webbsidan.
* Slutligen återges sådant innehåll på skärmen visuellt i koden.

Sedan besöker man olika delar av den befintliga webbplatsen där QuickView-funktionen används, startar QuickView och hämtar den Ajax-URL som skickats från webbsidan för att läsa in QuickView-data eller -innehåll.

Normalt behöver du inte använda några specialverktyg för felsökning. Moderna webbläsare har webbinspektörer som klarar ett bra jobb. Nedan följer några exempel på webbläsare som innehåller webbinspektörer:

* Om du vill visa alla utgående HTTP-begäranden i Google Chrome trycker du på F12 för att öppna panelen Utvecklarverktyg och klickar sedan på fliken Nätverk.
På Mac trycker du på Command+Option+I för att öppna panelen Utvecklarverktyg och klickar sedan på fliken Nätverk.

* I Firefox kan du antingen aktivera plugin-programmet för Firebug genom att trycka på F12 och använda fliken Net. Du kan också använda det inbyggda Inspector-verktyget och fliken Nätverk.
Tryck på Kommando+Alt+I på en Mac för att öppna panelen Utvecklarverktyg och klicka sedan på fliken Granska.

När nätverksövervakning är aktiverat i webbläsaren utlöser du snabbvyn på sidan.

Nu kan du hitta Quickview Ajax-URL:en i nätverksloggen och kopiera den inspelade URL:en för framtida analys. I de flesta fall när du utlöser snabbvyn skickas flera begäranden till servern. Vanligtvis är Quickview Ajax-URL en en av de första i listan. Den har antingen en komplex frågesträngsdel eller -sökväg och dess MIME-svarstyp är antingen `text/html`, `text/xml`eller `text/javascript`.

Under den här processen är det viktigt att du besöker olika delar av webbplatsen, med olika produktkategorier och typer. Anledningen är att URL:er för snabbvyn kan ha delar som är gemensamma för en viss webbplatskategori, men bara ändras om du besöker ett annat område på webbplatsen.

I det enklaste fallet är den enda variabeldelen i snabbvyns URL produktens SKU. I det här fallet är SKU-värdet den enda datadel som du behöver för att lägga till aktiveringspunkter i banderollbilden.

I komplexa fall har emellertid QuickView-webbadressen olika element utöver SKU:n, till exempel kategori-ID, färgkod, storlekskod osv. I sådana fall är varje element en separat variabel i hotspot-datadefinitionen i den interaktiva bildfunktionen som kan köpas i AEM Assets.

Titta på följande exempel på QuickView-URL:er och deras resulterande hotspot-variabler:

<table>
  <tbody>
  <tr>
    <td><p>En SKU, hittades i frågesträngen.</p> </td>
    <td><p>De inspelade URL:erna för snabbvyn är bland annat följande:</p>
    <ul>
      <li><p><code>https://server/json?productId=866558&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1196184&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1081492&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1898294&amp;source=100</code></p> </li>
    </ul> <p>Den enda variabeldelen i URL:en är värdet på strängparametern productId= och det är tydligt ett SKU-värde. Därför behöver våra aktiveringspunkter bara SKU-fält med värden som <strong><code>866558</code></strong>, <strong><code>1196184</code></strong>, <strong><code>1081492</code></strong>, <strong><code>1898294</code></strong>.</p> </td>
  </tr>
  <tr>
    <td><p>En SKU, finns i URL-sökvägen.</p> </td>
    <td><p>De inspelade URL:erna för snabbvyn är bland annat följande:</p>
    <ul>
      <li><p><code>https://server/product/6422350843</code></p> </li>
      <li><p><code>https://server/product/1607745002</code></p> </li>
      <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>Variabeldelen finns i den sista delen av banan och blir SKU-värdet för aktiveringspunkterna: <strong><code>6422350843</code></strong>, <strong><code>1607745002</code></strong>, <strong><code>0086724882</code></strong>.</p> </td>
  </tr>
  <tr>
    <td><p>SKU och kategori-ID i frågesträngen.</p> </td>
    <td><p>De inspelade URL:erna för snabbvyn är bland annat följande:</p>
    <ul>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>I det här fallet finns det två olika delar i URL:en. SKU:n lagras i <code>prodId</code> parametern och kategori-ID<code></code> lagras i <code>category=</code> -parametern.</p> <p>Därför är hotspot-definitionerna par. Det vill säga ett SKU-värde och ytterligare en variabel som kallas <code>categoryId</code>. De resulterande paren är följande:</p>
    <ul>
      <li><p>SKU är <strong><code>305466</code></strong> och <code>categoryId</code> är <code>1100004</code>.</p> </li>
      <li><p>SKU är <strong><code>310181</code></strong> och <code>categoryId</code> är <strong><code>1100004</code></strong>.</p> </li>
      <li><p>SKU är <strong><code>308706</code></strong> och <code>categoryId</code> är <strong><code>1740148</code></strong>.</p> </li>
    </ul> <p> </p> </td>
  </tr>
  </tbody>
</table>

**Exempel**

Du kan använda samma metod som i de tre exemplen ovan på [demowebbsidan](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html).

Demonstrationswebbsidan innehåller flera produktminiatyrbilder med en QuickView-knapp med etiketten&quot;See More&quot;. Med webbläsarens felsökningsverktyg fortfarande aktiverat klickar du på varje knapp och noterar de inspelade URL:erna för snabbvyn. När du har aktiverat alla fyra snabbvyerna för produkten som finns på sidan, finns följande lista över snabbvybegäranden som gjorts i bakgrunden:

* `/datafeed/Men-Windbreaker.json`
* `/datafeed/Men-SimpleHenley.json`
* `/datafeed/Men-CamoPullover.json`
* `/datafeed/Women-QuiltedDownJacket.json`

Om du tittar på de här serversamtalen ser du att produktspecifik information bara finns i sökvägen för begäran. Du observerar också att frågesträngen inte används alls och att det finns två olika typer av datadelar:

* Den första typen är Män eller Kvinnor. Du kan kalla den här&quot;produktkategorin&quot;.
* Den andra typen är produktnamn, till exempel CamoPullover. Du kan anta att det här är SKU:n för produkten.

Med hjälp av den här informationen har hela snabbvyns URL följande mönster:

`/datafeed/$categoryId$-$SKU$.json`

Baserat på en sådan analys skulle ni använda `categoryId` och `SKU` för aktiveringspunkter.

Du är nu redo att ladda upp en bildbanderoll och lägga till hotspot-områden i den med funktionen för interaktiv bild i AEM Assets.

## (Valfritt) Skapa en förinställning för Interactive Image Viewer {#optional-creating-an-interactive-image-viewer-preset}

Du kan välja att använda standardförinställningen för interaktiv bildvisning, som kallas `Shoppable_Banner` för AEM Assets. Du kan också skapa en egen förinställning för visningsprogrammet som kan användas med interaktiva bilder.

När du skapar en anpassad förinställning för Interactive Image Viewer kan du bestämma utseendet på aktiveringspunkter i bildbanderollen. När du skapar visningsförinställningen kan du välja att använda en aktiveringspunktsbild från ett galleri med fördefinierade bilder.

När du har sparat visningsförinställningen aktiveras den automatiskt (aktiveras) på listsidan för visningsförinställningar i AEM Assets. Den här funktionen innebär att den är synlig i komponenten Interactive Media och när du visar en resurs. Om du vill *leverera *en interaktiv banderoll med den här visningsförinställningen måste du även *publicera *din visningsförinställning (detta gäller anpassade visningsprogramförinställningar eller förinställda visningsprograminställningar som inte är installerade).

**Skapa en förinställning för Interactive Image Viewer**

1. Tryck på vänster spår **[!UICONTROL Tools > Assets > Viewer Presets]**.
1. Near the upper-right corner of the page, tap **[!UICONTROL Create]**.
1. I dialogrutan Ny visningsförinställning för visningsprogrammet skriver du ett namn som beskriver förinställningen för det interaktiva visningsprogrammet för banderollen.

   Det här är titeln som visas på listsidan för visningsförinställningar när du har sparat.

1. I listrutan Multimedietyp väljer du **[!UICONTROL Interactive Image]**.
1. Tryck på **[!UICONTROL Create]**.
1. On the Edit Viewer Preset page, tap the **[!UICONTROL Appearance]** tab.
1. Gör något av följande:

   * Om du vill överföra en egen hotspot-bild som du vill använda på bilder trycker du på ikonen Resursväljaren. Gå till den hotspot-bild som du vill använda på sidan Välj innehåll, markera den och tryck sedan på ikonen Markera i det övre högra hörnet.
   * Om du vill välja en fördefinierad hotspot-bild trycker du på ikonen för Hotspot-galleriet. Tryck på den hotspot-bild som du vill använda på paletten för klickbara områden.

1. Near the upper-right corner of the page, tap **[!UICONTROL Save]**.

   Var noga med att publicera den nya visningsförinställningen.

   Se [Publicera förinställningar](/help/assets/dynamic-media/managing-viewer-presets.md#publishing-viewer-presets)för visningsprogram.

   Du kan nu ladda upp en bildbanderoll.

## Överföra en bildbanderoll {#uploading-an-image-banner}

Om du redan har överfört de bilder du vill använda går du vidare till nästa steg, [Lägga till aktiveringspunkter i en bildbanderoll](#adding-hotspots-to-an-image-banner).

**Så här överför du en bildbanderoll**

1. Överför bildbanderoller som du vill göra interaktiva.

   Se [Överföra resurser](/help/assets/manage-digital-assets.md#uploading-assets).

   Nu kan du lägga till hotspot-områden i bildbanderollen; se nästa uppgift nedan.

## Lägga till aktiveringspunkter i en bildbanderoll {#adding-hotspots-to-an-image-banner}

Du kan lägga till aktiveringspunkter i en bildbanderoll med redigeraren på sidan Hantering av aktiveringspunkter.

När du lägger till aktiveringspunkter kan du definiera dem som en snabbvypopup-visning, som en hyperlänk eller som en upplevelsefragment.

Se [Upplevelsefragment](/help/sites-cloud/authoring/fundamentals/experience-fragments.md).

>[!NOTE]
>
>Tänk på att verktygen för delning av sociala medier i interaktiv bild inte stöds när du bäddar in visningsprogrammet i ett Experience Fragment. Du kan undvika detta genom att använda eller skapa visningsförinställningar som inte har verktyg för delning av sociala medier. Med sådana visningsförinställningar kan du bädda in dem i Experience Fragments.

Alternativen Ångra och Gör om, nära det övre högra hörnet på sidan, stöds under den aktuella skaps-/redigeringssessionen.

När du är klar med att skapa en interaktiv bild kan du använda Förhandsgranska för att se hur den interaktiva bilden kommer att se ut för kunderna.

Se [(Valfritt) Förhandsvisa interaktiva bilder](#optional-previewing-interactive-images).

>[!NOTE]
>
>När du lägger till aktiveringspunkter i en bild i en interaktiv bild eller en Carousel-banderoll lagras hotspot-informationen på samma metadataplats - i förhållande till bildens plats - oavsett om det är en interaktiv bild eller en Carousel-banderoll. Den här funktionen innebär att du enkelt kan återanvända samma bild - tillsammans med dess definierade hotspot-data - i båda visningsprogrammen.
>
>Observera dock att Carousel Banners stöder bildscheman på bilder som även kan innehålla hotspot-områden. en interaktiv bild gör det inte. Tänk på detta om du tänker skapa en interaktiv bild eller en Carousel-banderoll som använder samma bild. Du kanske vill skapa interaktiva bilder och Carousel Banners med separata kopior av samma bild istället.
>
>Se även [Carousel Banners](/help/assets/dynamic-media/carousel-banners.md).

>[!NOTE]
>
>Om du redigerar interaktiva bilder med aktiveringspunkter och beskär bilden tas dina aktiveringspunkter bort.

**Lägga till aktiveringspunkter i en bildbanderoll**

1. I resursvyn navigerar du till den bildbanderoll som du vill göra interaktiv.
1. Gör något av följande:

   * Hover on the image, then tap **[!UICONTROL Select]** (checkmark icon). Tryck på i verktygsfältet **[!UICONTROL Edit]**.

   * Håll pekaren över bilden och tryck sedan på **[!UICONTROL More actions]** (ikonen med tre punkter) **[!UICONTROL > Edit]**.

   * Tryck på bilden för att öppna den på sidan Detaljvy. Tryck på i verktygsfältet **[!UICONTROL Edit]**.

1. I närheten av sidans övre vänstra hörn trycker du på **[!UICONTROL Add Hotspot]** (pekaren) för att öppna sidan för hantering av hotspot-områden.
1. Near the upper-left corner of the page, tap **[!UICONTROL Hotspot]**.

   1. Tryck på i det övre vänstra hörnet av sidan Hantering av hotspot **[!UICONTROL Hotspot]**.
   1. Tryck på den plats i bilden där du vill att hotspot-området ska visas. Dra hotspot-området om det behövs för att justera dess placering. Du kan också använda piltangenterna på tangentbordet för att styra positionen för en markerad aktiveringspunkt.
   1. Lägg till ytterligare hotspot-områden efter behov genom att upprepa steg a och b.
   1. (Valfritt) Om du vill ta bort en aktiveringspunkt markerar du den i bilden och trycker sedan på **[!UICONTROL Delete]** (skräpburkikonen) under **[!UICONTROL Hotspots]** rubriken.

1. Skriv namnet på aktiveringspunkten i textfältet Namn. Det här namnet visas också i listrutan Markerad aktiveringspunkt.
1. Gör något av följande:

   * Tryck på **[!UICONTROL Quickview]**.

      * Om du är AEM Sites- eller e-handelskund trycker eller klickar du på produktväljarens ikon (förstoringsglas) för att öppna sidan Select Product (Välj produkt). Tryck eller klicka på den produkt du vill använda och tryck sedan på **Select **i det övre högra hörnet av sidan för att gå tillbaka till sidan för hantering av hotspot.
      * Om du *inte* är AEM Sites- eller e-handelskund

         * Se [Identifiera hotspot-variabler](#optional-identifying-hotspot-variables). måste du definiera dessa variabler.
         * Ange sedan SKU-värdet manuellt. I textfältet SKU-värde skriver du produktens SKU (Stock Keeping Unit), som är en unik identifierare för varje separat produkt eller tjänst som du erbjuder. Det angivna SKU-värdet fyller automatiskt i variabeldelen av QuickView-mallen så att systemet vet att den aktiveringspunkt som användaren går till associeras med en viss SKU:s snabbvy.
         * (Valfritt) Om det finns andra variabler i snabbvyn som du behöver för att identifiera en produkt ytterligare trycker du **[!UICONTROL Add Generic Variable]**. Ange ytterligare en variabel i textfältet. Till exempel `category=Mens` är en tillagd variabel.
   * Tryck på **[!UICONTROL Hyperlink]**.

      * Om du är kund hos AEM Sites trycker eller klickar du på ikonen Platsväljare (mapp) för att navigera till en URL. Observera att den URL-baserade länkningsmetoden inte är möjlig om det interaktiva innehållet har länkar till relativa URL-adresser, särskilt länkar till AEM Sites-sidor.
      * Om du är en fristående kund anger du den fullständiga URL-sökvägen till en länkad webbsida i textfältet HREF.

   Var noga med att ange om länken ska öppnas på en ny webbläsarflik (rekommenderat standardvärde) eller på samma flik.

   Mer information finns i [Arbeta med väljare](/help/assets/dynamic-media/working-with-selectors.md) .

   * Tryck på **[!UICONTROL Experience Fragment]**.

      * Om du är AEM Sites-kund trycker eller klickar du på ikonen Sök (förstoringsglas) för att öppna sidan Experience Fragment. Tryck eller klicka på det Experience Fragment som du vill använda och tryck sedan på Select (Välj) längst upp till höger på sidan för att återgå till sidan för hantering av hotspot.
Se [Upplevelsefragment](/help/sites-cloud/authoring/fundamentals/experience-fragments.md).

      * Ange bredd och höjd för Experience Fragment så som det kommer att visas på banderollen.

         >[!NOTE]
         >
         >Tänk på att verktygen för delning av sociala medier i interaktiv bild inte stöds när du bäddar in visningsprogrammet i ett Experience Fragment. Du kan undvika detta genom att använda eller skapa visningsförinställningar som inte har verktyg för delning av sociala medier. Med sådana visningsförinställningar kan du bädda in dem i Experience Fragments.



1. Tryck för **[!UICONTROL Save]** att spara ditt arbete och återgå till sidan Bläddra.
1. Publicera den interaktiva bilden. Med publicering kan banderollen levereras via molnet och även generera inbäddningskod om du behöver integrera med en tredjepartswebbplats.

   Se [Publicera resurser](/help/assets/manage-digital-assets.md#publish-assets).

   När du har lagt till aktiveringspunkter och publicerat den interaktiva bilden kan du nu lägga till den på din befintliga webbplats.

   Se [Integrera en interaktiv bild med webbplatsen](#integrating-an-interactive-image-with-your-website).

   >[!NOTE]
   >
   >Om du redigerar interaktiva bilder med aktiveringspunkter och beskär bilden tas dina aktiveringspunkter bort.

### (Valfritt) Förhandsgranska interaktiva bilder {#optional-previewing-interactive-images}

Du kan använda Förhandsgranska för att se hur den interaktiva bilden kommer att se ut för kunderna och för att testa hur hotspot-områden i bilden beter sig som förväntat.

När du är nöjd med den interaktiva bilden kan du publicera den.
See [Embedding the Video or Image Viewer on a Web Page](/help/assets/dynamic-media/embed-code.md).
See [Linking URLs to your web application](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md). Observera att den URL-baserade länkningsmetoden inte är möjlig om det interaktiva innehållet har länkar till relativa URL-adresser, särskilt länkar till AEM Sites-sidor.
See [Adding Dynamic Media Assets to Pages.](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)

**Förhandsgranska interaktiva bilder**

1. Navigera till en befintlig interaktiv bild som du har skapat i resursvyn och öppna den i förhandsvisningen genom att trycka.
1. I det övre vänstra hörnet av förhandsvisningssidan trycker du på **[!UICONTROL Viewers]**.
1. Tryck på **[!UICONTROL Shoppable_Banner]** eller ange namnet på den förinställning för visningsprogram för interaktiva bilder som du har skapat i listan Visningsprogram.
1. Tryck på hotspot-områden på bilden för att testa deras associerade åtgärder.

## Publicera interaktiva bildresurser {#publishing-interactive-image-assets}

Mer information om hur du publicerar interaktiva bildresurser finns i [Publicera resurser](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md) .

## Integrera en interaktiv bild med webbplatsen {#integrating-an-interactive-image-with-your-website}

När du har överfört en banderollbild, lagt till aktiveringspunkter i bilden och publicerat den interaktiva bilden kan du nu lägga till den på din webbsida.

Om du är kund hos AEM Sites kan du lägga till den interaktiva bilden genom att dra Interactive Media-komponenten till din sida. See [Adding Dynamic Media Assets to Pages.](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)

Om du är en fristående AEM Assets-kund kan du lägga till den interaktiva bilden manuellt på din webbplats enligt beskrivningen i det här avsnittet.

1. Kopiera den publicerade interaktiva bildens inbäddningskod.
See [Embedding the Video or Image Viewer on a Web Page](/help/assets/dynamic-media/embed-code.md).

1. Lägg till den kopierade inbäddningskoden på önskad plats på webbsidan.
Den kopierade inbäddningskoden ställs in för en responsiv miljö så att den automatiskt passar det tilldelade området.

**Exempel**

Lägg märke till att bilden på de tre männen är en statisk [tagg med hjälp av demowebbplatsen som exempel](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html)`IMG` :

```xml
<img class="img-responsive" width="100%" title="Hero Image 2" alt="Hero Image 2" src="images/shoppable-banner.jpg">
```

Integrationen är lika enkel som att ta bort `IMG` taggen och ersätta den med den kopierade inbäddningskoden från AEM Assets. Resultatet [visar den interaktiva bilden på sidan med tre cirkelaktiveringspunkter](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-1.html).

>[!NOTE]
>
>Så här långt är de hotspots som finns på den interaktiva bilden av demowebbplatsen endast avsedda för webben. de är ännu inte integrerade med de befintliga snabbvyerna.

Om du vill tillämpa en beskärning på en interaktiv bild för en responsiv miljö kan du inkludera konfigurationsattributet Interactive Image `ZoomView.iscommand` på sökvägen, där `ZoomView` är den komponent som ska anropas och `iscommand` är det beskärningsbildserverkommando som du använder.

Se [Konfigurationsattribut för ZoomView.iscommand](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/command-reference-configuration-attributes-interactive-images/r-html5-aem-interactive-image-config-attrib-zoomview-iscommand.html) .

Se [kommandot för att beskära](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-crop.html) bilder.

Nu kan du integrera den interaktiva bilden med en befintlig Quickview på webbplatsen.

## Integrera en interaktiv bild med en befintlig snabbvy {#integrating-an-interactive-image-with-an-existing-quickview}

>[!NOTE]
>
>Detta gäller endast om du är en fristående AEM Assets-kund.

Det sista steget i den här processen är att integrera den interaktiva bilden med en befintlig Quickview-implementering på din webbplats. Det finns ingen lösning på integreringen som fungerar i alla fall. Alla QuickView-implementeringar är unika och det behövs ett specifikt tillvägagångssätt som troligen inbegriper hjälp av en IT-handläggare på frontend.

Den befintliga Quickview-implementeringen representerar normalt en kedja av interrelaterade åtgärder som inträffar på webbsidan i följande ordning:

1. En användare utlöser ett element i användargränssnittet för webbplatsen.
1. FrontEnd-koden hämtar en QuickView-URL som baseras på användargränssnittselementet som utlöstes i steg 1.
1. Front-end-koden skickar en Ajax-begäran med den URL som fås i steg 2.
1. Bakåtlogiken returnerar motsvarande QuickView-data eller -innehåll tillbaka till slutkoden.
1. Slutkoden läser in QuickView-data eller -innehåll.
1. Om du vill kan du konvertera den inlästa QuickView-informationen till en HTML-representation med hjälp av koden längst fram.
1. I koden visas en modal dialogruta eller panel och HTML-innehållet återges på skärmen för slutanvändaren.

Dessa anrop kanske inte representerar oberoende offentliga API-anrop som kan anropas av webbsidans logik från ett godtyckligt steg. I stället är det ett kedjat anrop där varje steg döljs i den sista fasen (återanrop) av föregående steg.

Samtidigt som den interaktiva bilden som kan köpas ersätter steg 1, och delvis steg 2, när en användare klickar på en hotspot i bilden som kan köpas, hanteras den här användarinteraktionen av användaren. Visningsprogrammet returnerar en händelse till webbsidan som innehåller alla hotspot-data som tidigare lagts till i AEM Assets.

I en sådan händelsehanterare gör koden längst fram följande:

* Lyssnar på en händelse som skickas av den interaktiva bilden som kan köpas.
* Skapar en URL för snabbvyn baserat på hotspot-data.
* Startar processen att läsa in snabbvyn från serverdelen och återge den på skärmen för visning.

Den inbäddningskod som returneras av AEM Assets har redan en färdig händelsehanterare på plats som kommenteras ut, vilket visas i följande markerade kodfragment:

```xml
        var s7interactiveimageviewer = new s7viewers.InteractiveImage({
            "containerId" : "s7interactiveimage_div",
            "params" : {
                "serverurl" : "https://aodmarketingna.assetsadobe.com/is/image",
                "contenturl" : "https://aodmarketingna.assetsadobe.com/",
                "config" : "/etc/dam/presets/viewer/Shoppable_Media",
                "asset" : "/content/dam/mac/aodmarketingna/shoppable-banner/shoppable-banner.jpg" }
        })
        /* // Example of interactive image event for Quickview.
             s7interactiveimageviewer.setHandlers({
                "quickViewActivate": function(inData) {
                    var sku=inData.sku; //SKU for product ID
                    //To pass other parameter from the hotspot, you will need to add custom parameter during the hotspot setup as parameterName=value
                    loadQuickView(sku); //Replace this call with your Quickview plugin
                    //Please refer to your Quickviewer plugin for the Quickview call
                 },
             });
        */
        s7interactiveimageviewer.init();
```

Därför är det bara nödvändigt att avkommentera koden och ersätta dummy-hanterarens brödtext med koden som är specifik för den aktuella webbsidan.

Processen med att konstruera en Quickview-URL är i stort sett annorlunda än den process som användes för att identifiera hotspot-variabler som beskrivs tidigare.

Se [Identifiera hotspot-variabler](#optional-identifying-hotspot-variables).

Med hjälp av våra tidigare exempel på QuickView-webbadresser kan du i följande exempel se hur snabbvyns webbadress är uppbyggd i varje fall:

<table>
 <tbody>
  <tr>
   <td><p>En SKU, som finns i frågesträngen</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/json?productId=" + inData.sku + "&amp;amp;source=100";
      },
      });</code></td>
  </tr>
  <tr>
   <td><p>En SKU, finns i URL-sökvägen</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/product/" + inData.sku;
      },
      });</code></td>
  </tr>
  <tr>
   <td><p>SKU och kategori-ID i frågesträngen</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/quickView/product/?category=" + inData.categoryId + "&amp;amp;prodId=" + inData.sku;
      },
      });</code></td>
  </tr>
 </tbody>
</table>

Det sista steget för att utlösa snabbgransknings-URL:en och aktivera snabbvypanelen kräver troligen hjälp av en IT-handläggare på IT-avdelningen. De har kunskap om hur de bäst kan utlösa QuickView-implementeringen från rätt steg med en färdig QuickView-URL.

Du kan se hur dessa steg tillämpas på demowebbplatsen för att helt integrera en interaktiv bild som kan köpas med QuickView-koden. Tidigare identifierades strukturen för snabbvyns URL som följande:

```xml
/datafeed/$categoryId$-$SKU$.json
```

Om du vill rekonstruera den här URL:en inuti `quickViewActivate` hanteraren kan du använda de `categoryId` - och `SKU` -fält som är tillgängliga i det `inData` objekt som skickas till hanteraren av användarens kod:

```xml
var sku=inData.sku;
var categoryId=inData.categoryId;
var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
```

Demonstrationswebbplatsen utlöser dialogrutan Snabbvisning med ett enkelt `loadQuickView()` funktionsanrop. Den här funktionen har bara ett argument, vilket är snabbvydata-URL:en. Det sista steget som krävs för att integrera den interaktiva bilden för köpare är att lägga till följande kodrad i `quickViewActivate` hanteraren:

```xml
loadQuickView(quickViewUrl);
```

Här följer den fullständiga källkoden:

```xml
 var s7interactiveimageviewer = new s7viewers.InteractiveImage({
  "containerId" : "s7interactiveimage_div",
  "params" : {
   "serverurl" : "https://aodmarketingna.assetsadobe.com/is/image",
   "contenturl" : "https://aodmarketingna.assetsadobe.com/",
   "config" : "/etc/dam/presets/viewer/Shoppable_Media",
   "asset" : "/content/dam/mac/aodmarketingna/shoppable-banner/shoppable-banner.jpg" }
 })
   s7interactiveimageviewer.setHandlers({
   "quickViewActivate": function(inData) {
     var sku=inData.sku;
     var categoryId=inData.categoryId;
    var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
    loadQuickView(quickViewUrl);
    },
   });
 s7interactiveimageviewer.init();
```

Den [slutliga demowebbplatsen med den helt integrerade interaktiva bilden](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-3.html).

## Använda snabbvyer för att skapa anpassade popup-fönster {#using-quickviews-to-create-custom-pop-ups}

See [Using Quickviews to create custom pop-ups](/help/assets/dynamic-media/custom-pop-ups.md).
