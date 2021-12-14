---
title: Interaktiva videoklipp
description: Lär dig hur du arbetar med interaktiv video och videor som kan köpas i Dynamic Media.
feature: Interactive Videos
role: User
exl-id: e4859223-91de-47a1-a789-c2a9447e5f71
source-git-commit: ba752888601413dd4725a7a137f8b468b92ad5c7
workflow-type: tm+mt
source-wordcount: '5919'
ht-degree: 3%

---

# Interaktiva videoklipp{#interactive-videos}

Du kan enkelt skapa interaktiva videor - även kallade videor som kan köpas - som genererar konverteringar direkt från videon. Kundens engagemang i videon äger rum i en panel bredvid videospelaren där relaterade tjänster, information eller produktminiatyrer rullas in i vyn baserat på vad som visas i videon. Kunderna kan välja miniatyrbilden och länkas direkt till tjänsten, lägga till artikeln i en kundvagn för direktköp eller länkas till en webbsida för mer information.

När videon är slut visas en visuell sammanfattning av alla erbjudanden för att skapa ett actionanrop. Kunderna har en annan möjlighet att välja önskad artikel. Användbara och specifika upplevelser som dessa ökar kundernas engagemang och konverteringar.

Se även [Interaktiva bilder](/help/assets/dynamic-media/interactive-images.md).

## Interaktiv video in action {#interactive-video-in-action}

Om du vill se en interaktiv videoklipp i praktiken väljer du [Live Demos](https://landing.adobe.com/en/na/dynamic-media/ctir-2755/live-demos.html), bläddra till **[!UICONTROL Shoppable Media]** på sidan och välj sedan den köpbara videon för att påbörja uppspelningen.

* Under uppspelningen, när produkterna används i videon, visas den identiska produkten till höger som en miniatyrbild.

* Om du vill pausa videon och öppna snabbvyn för produkten väljer du miniatyrbilden. Välj till exempel miniatyrbilden Kitchenaid i videon om du vill se en 360-graderssnurra över blandaren, eller zooma in om du vill se blandningsinformationen.

Se även [Använd interaktiv video med Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-interactive-video-feature-video-use.html#dynamic-media)

<!-- 

There was a link here that showed the video frame of an interactive video and when the reader selected the frame the video would play https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/AXIS/index.html. This now needs to call a new interactive video

-->

<!-- 

[A frame from an interactive, shoppable video](assets/chlimage_1-126.png) *A video frame capture from an interactive, shoppable video.*

-->

>[!NOTE]
>
>Om du skapar en interaktiv video för att starta en webbsida när en användare väljer en miniatyrbild blockerar vissa enheter popup-webbsidan från att öppnas. I så fall ändrar du inställningen för blockering av popup-fönster på enheten. På en Apple iPhone 6 går du till exempel till **[!UICONTROL Settings]** > **[!UICONTROL Safari]** > **[!UICONTROL Block Pop-ups]** och sedan flytta kontrollen till **[!UICONTROL Off]**. När du spelar upp en interaktiv video och väljer en miniatyrbild blir du nu tillfrågad om du vill öppna popup-fönstret. Om du accepterar öppnas webbsidan.

### Se hur interaktiva videor skapas {#watch-how-interactive-videos-are-created}

Se en genomgång på [hur interaktiva videor skapas](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveVideo)(7 minuter och 30 sekunder).
(Även om videogenomgången är märkt med Assets on Demand gäller fortfarande principerna och stegen för Interactive Video i Adobe Experience Manager Assets.)

### Adobe Customer Success Webinar {#adobe-customer-success-webinar}

The [Använd interaktiv video, länkdelning och YouTube-delning i Experience Manager Assets](https://adobecustomersuccess.adobeconnect.com/p1yxzdo4aec/) webbinariet visar hur du använder interaktiv video och andra funktioner för att knyta konverteringsdrivna händelser till ert videomarknadsföringsmaterial.

## Snabbstart: Interaktiva videoklipp {#quick-start-interactive-videos}

Följande steg-för-steg-beskrivning av arbetsflödet hjälper dig att komma igång snabbt med interaktiva videor i Dynamic Media.

Leta efter **Exempel** i vissa snabbstartsåtgärder. Det innehåller en kort självstudiekurs som bygger på detta [starta en demowebbsida som *inte* har lagt till interaktivitet i den ännu](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-0.html).

**Exemplen** visar hur du integrerar interaktiva videofilmer på en webbplats.

När du är klar med självstudiekursen i det sista exempelavsnittet [den färdiga demowebbsidan med helt integrerad interaktiv video visas på det här sättet](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-3.html).

Interaktiva videosteg:

1. **(Valfritt) Identifiera QuickView-variabler** - Börja med att identifiera dynamiska variabler som används i den befintliga QuickView-implementeringen. Du använder variablerna för att mappa produktminiatyrbilder till deras motsvarande produkt-snabbvyn när du skapar en interaktiv video. Se [(Valfritt) Identifiera Quickview-variabler](#optional-identifying-quickview-variables).
   **Det här steget är bara obligatoriskt om alla följande är uppfyllda:**
・ Du vill lägga till interaktivitet i videon genom att aktivera snabbvyer.
・ Er implementering av Experience Manager gör det 
*not* använda ett ramverk för e-handelsintegrering för att hämta produktdata till Experience Manager från alla e-handelslösningar som IBM® WebSphere® Commerce, Elastic Path, SAP Hybris eller Intershop.

1. **(Valfritt) Skapa en förinställning för Interactive Video Viewer** - Anpassa utseendet och beteendet för olika komponenter som utgör spelaren, t.ex. videobandspelaren och de interaktiva miniatyrbilderna.
Det är inte nödvändigt att skapa en egen förinställning för Interactive Video Viewer om du tänker använda förinställningarna för Interactive Video Viewer `Shoppable_Video_Light` eller `Shoppable_Video_Dark` i stället.
Se [Skapa en visningsförinställning](/help/assets/dynamic-media/managing-viewer-presets.md#creating-a-new-viewer-preset) (valfritt) och [Specialöverväganden när du skapar en interaktiv visningsförinställning](/help/assets/dynamic-media/managing-viewer-presets.md#special-considerations-for-creating-an-interactive-viewer-preset).

1. **Överföra en video och dess associerade bildresurser** - Ladda upp en video och tillhörande bilder som du vill göra interaktiva.
Se [Överföra en video och dess tillhörande miniatyrbilder](#uploading-a-video-and-its-associated-thumbnail-assets).

   >[!NOTE]
   >
   >MXF-videoformatet stöds ännu inte för användning med interaktiva videoklipp i Dynamic Media.

1. **Lägg till interaktivitet i videon** - Lägg till ett eller flera tidssegment i videon. Associera sedan bildminiatyrer inom dessa tidssegment. Tilldela varje miniatyrbild till en åtgärd som en hyperlänk, en snabbvy eller ett Experience Fragment.
(Den URL-baserade länkningsmetoden är inte möjlig om det interaktiva innehållet har länkar till relativa URL-adresser, särskilt länkar till Experience Manager Sites-sidor.)
Slutför genom att publicera det interaktiva videomaterialet. Publicering skapar den inbäddningskod eller URL som du så småningom kopierar och använder på webbplatsens landningssida. Se [Lägg till interaktivitet i videon](#adding-interactivity-to-your-video).
Se [Publicera resurser](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

1. **Lägga till en interaktiv video på din webbplats eller på din webbplats i Experience Manager** - Om du använder Experience Manager Sites eller e-handel, eller båda, lägger du till den interaktiva videon på en webbsida i Experience Manager. Dra Interactive Media-komponenten till sidan. Se [Lägga till Dynamic Media-resurser på sidor](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).
Använd inbäddningskoden eller URL-adressen för att integrera interaktiv video med webbplatsupplevelserna. Se [Integrera en interaktiv video med webbplatsen](#integrating-an-interactive-video-with-your-website).
Om du använder en WCM-fil (Web Content Manager) från tredje part måste du integrera den nya interaktiva videon med den befintliga QuickView-implementeringen som används på webbplatsen. Se [Integrera en interaktiv video med en befintlig QuickView](#integrating-an-interactive-video-with-an-existing-quickview).
   [Lägga till Dynamic Media-resurser på sidor](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)

## (Valfritt) Identifiera QuickView-variabler {#optional-identifying-quickview-variables}

>[!NOTE]
>
>Den här aktiviteten krävs bara om följande är sant:
>
>* Du vill lägga till interaktivitet i videon genom att aktivera snabbvyer.
>* Er implementering av Experience Manager gör *not* använda ett ramverk för e-handelsintegrering för att hämta produktdata till Experience Manager från alla e-handelslösningar som IBM® WebSphere® Commerce, Elastic Path, SAP Hybris eller Intershop. <!-- See [eCommerce concepts in Experience Manager Assets](/help/sites-administering/concepts.md).-->

>
>Om din implementering av Experience Manager använder e-handel kan du hoppa över den här uppgiften och fortsätta med nästa uppgift.

Börja med att identifiera dynamiska variabler som används i den befintliga QuickView-implementeringen, så att du kan mappa produktminiatyrbilder till deras motsvarande produkt i QuickView när du skapar interaktiva videofilmer.

När du lägger till tidssegment i en video tilldelar du en SKU (Stock Keeping Unit) och eventuella ytterligare variabler till varje miniatyrbild som du lägger till i ett segment. Sådana variabler används senare för att visa rätt Quickview-produkt.

Det är viktigt att kunna identifiera vilka variabler som krävs för att utlösa en produktsnabbvy på ett unikt sätt.

Ibland räcker det att rådfråga IT-specialister som är ansvariga för din befintliga QuickView-implementering. De känner troligtvis till den minsta datauppsättning som identifierar snabbvyn i systemet. Det är dock möjligt att helt enkelt analysera det befintliga beteendet för koden.

De flesta QuickView-implementeringar använder följande paradigm:

* Användaren aktiverar ett element i användargränssnittet på webbplatsen. Du kan till exempel välja en snabbvyknapp.
* Webbplatsen skickar en Ajax-begäran till serverdelen för att läsa in QuickView-data eller -innehåll vid behov.
* Quickview-data översätts till innehållet som förberedelse för återgivning på webbsidan.
* Slutligen återges sådant innehåll på skärmen visuellt i koden.

Du bör därför besöka olika delar av din befintliga webbplats där Quickview används. Starta sedan Quickview och hämta den Ajax-URL som webbsidan skickade för att läsa in QuickView-data eller -innehåll.

Normalt behöver du inte använda några specialverktyg för felsökning. Moderna webbläsare har webbinspektörer som klarar ett bra jobb. Nedan följer några exempel på webbläsare som innehåller webbinspektörer:

* Om du vill se alla utgående HTTP-begäranden i Google Chrome trycker du på **F12** (Windows®) eller **Kommando+Alternativ+I** (Mac) för att öppna panelen Utvecklingsverktyg och sedan välja **Nätverk** -fliken.

* I Firefox kan du antingen aktivera plugin-programmet för Firebug genom att trycka på **F12** (Windows®) eller **Kommando+Alt+I** (Mac) och använda **[!UICONTROL Net]** eller så kan du använda det inbyggda verktyget Granska och fliken Nätverk.

* Aktivera felsökningsverktyget i Internet Explorer genom att trycka på **F12**.

När nätverksövervakning är aktiverat i webbläsaren utlöser du snabbvyn på sidan.

Nu kan du hitta Quickview Ajax-URL:en i nätverksloggen och kopiera den inspelade URL:en för framtida analys. Vanligtvis skickas flera begäranden till servern när du utlöser snabbvyn. Vanligtvis är Quickview Ajax-URL en en av de första i listan. Den har antingen en komplex frågesträngsdel eller sökväg och dess MIME-svarstyp är antingen `text/html`, `text/xml`, eller `text/javascript`.

Under den här processen är det viktigt att du besöker olika delar av webbplatsen, med olika produktkategorier och typer. Anledningen är att URL:er för snabbvyn har delar som är gemensamma för en viss webbplatskategori, men som bara ändras om du besöker ett annat område på webbplatsen.

I det enklaste fallet är den enda variabeldelen i snabbvyns URL produktens SKU. I det här fallet är produktens SKU-värde den enda datadel som behövs för att lägga till miniatyrbilder i ett tidssegment i den interaktiva videon i Experience Manager.

I komplexa fall har dock QuickView-URL:en olika element förutom produkt-SKU:n, till exempel kategori-ID och färgkod. I sådana fall blir varje sådant element en separat variabel i definitionen av miniatyrbildsdata i Experience Manager.

Titta på följande exempel på QuickView-URL:er och deras resulterande miniatyrbildsvariabler:

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
    </ul> <p>Den enda variabeldelen i URL:en är värdet på <code>productId=</code> frågesträngsparameter, och det är tydligt ett SKU-värde. Därför behöver miniatyrbilderna bara SKU-fält med värden som <strong><code>866558</code></strong>, <strong><code>1196184</code></strong>, <strong><code>1081492</code></strong>, <strong><code>1898294</code></strong>.</p> </td>
  </tr>
  <tr>
    <td><p>En SKU, finns i URL-sökvägen.</p> </td>
    <td><p>De inspelade URL:erna för snabbvyn är bland annat följande:</p>
    <ul>
      <li><p><code>https://server/product/6422350843</code></p> </li>
      <li><p><code>https://server/product/1607745002</code></p> </li>
      <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>Variabeldelen finns i den sista delen av banan och blir SKU-värdet för miniatyrbilder i Experience Manager: <strong><code>6422350843</code></strong>, <strong><code>1607745002</code></strong>, <strong><code>0086724882</code></strong>.</p> </td>
  </tr>
  <tr>
    <td><p>SKU och kategori-ID i frågesträngen.</p> </td>
    <td><p>De inspelade URL:erna för snabbvyn är bland annat följande:</p>
    <ul>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>I det här fallet finns det två olika delar i URL:en. SKU:n lagras i <code>prodId</code> -parametern och kategori-ID:t lagras i <code>category=</code> parameter.</p> <p>Miniatyrbildsdefinitionerna är par. Det vill säga ett SKU-värde och en extra variabel som kallas <code>categoryId</code>. De resulterande paren är följande:</p>
    <ul>
      <li>SKU är <code>305466</code> och <code>categoryId</code> är <code>1100004</code></li>
      <li>SKU är <code>310181</code> och <code>categoryId</code> är <code>1100004</code></li>
      <li>SKU är <code>308706</code> och <code>categoryId</code> är <code>1740148</code></li>
    </ul> <p> </p> </td>
  </tr>
  </tbody>
</table>

**Exempel**

När ovanstående metod används på exempelwebbplatsen har du en webbsida med flera produktminiatyrbilder där var och en har knappen &quot;SE MER&quot;:

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-0.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-0.html)

När du har aktiverat alla snabbvyer för produkter som är tillgängliga på sidan visas följande lista över snabbvybegäranden som gjorts i serverdelen:

* datafeed/candles-233396346.json
* datafeed/candles-233978050.json
* datafeed/candles-234024346.json
* datafeed/candles-234024356.json
* datafeed/candles-234024359.json
* datafeed/cushions-233939848.json
* datafeed/cushions-234019477.json
* datafeed/cushions-234019483.json
* datafeed/furniture-231747479.json
* datafeed/furniture-232625621.json
* datafeed/furniture-232625626.json
* datafeed/furniture-233939810.json
* datafeed/furniture-233939825.json
* datafeed/furniture-233939828.json
* datafeed/furniture-233939853.json
* datafeed/furniture-233940334.json
* datafeed/glassware-000064007.json
* datafeed/glassware-230722193.json
* datafeed/glassware-233916550.json
* datafeed/glassware-233916597.json

Om du tittar på serveranropen finns produktspecifik information bara i sökvägen för begäran. Du observerar också att frågesträngen inte används alls och att det finns två olika typer av datadelar:

* Den första typen är ljus, kuddar, möbler och glasvaror. Du kan kalla den här&quot;produktkategorin&quot;.
* Den andra typen är produktkod, till exempel 233916597. Du kan anta att det är&quot;produkt-SKU&quot;.

Med hjälp av den här informationen har hela snabbvyns URL följande mönster:

`/datafeed/$categoryId$-$SKU$.json`

Utifrån en sådan analys kan du dra slutsatsen att du kan använda följande två variabler för miniatyrbilderna: `categoryId` och `SKU`.

Du är nu redo att överföra en video och dess associerade miniatyrbildsresurser.

## (Valfritt) Skapa en förinställning för Interactive Video Viewer {#optional-creating-an-interactive-video-viewer-preset}

Du kan hoppa över den här uppgiften och fortsätta till nästa om du tänker använda någon av de förinställda standardtyperna i det interaktiva visningsprogrammet `Shoppable_Video_dark` eller `Shoppable_Video_light`.

När en miniatyrbild är markerad i redigeringsmiljön visas en förhandsvisning av dialogrutan Snabbvy.

![chlimage_1-21](assets/chlimage_1-127.png)

Du kan också skapa en egen förinställning för Interactive Video Viewer. Du kan bland annat bestämma hur videospelaren, de interaktiva miniatyrbilderna och miniatyrbildsvyn som visas i slutet av videon ska se ut.

En förinställning för Interactive Video Viewer återger videon och alla tidslinjesegment som du har lagt till. I förhandsvisningsläget används dessutom ett standardexempel för snabbvyn när du väljer en miniatyrbild av en produkt, så att du kan testa dess interaktivitet innan du publicerar den.

När du har sparat visningsförinställningen ställs dess läge automatiskt in på **På ** på sidan Visningsförinställningar. Det här läget innebär att den är synlig i komponenten Dynamic Media och när du förhandsgranskar en video med den. Se också till att du publicerar den nya visningsförinställningen manuellt.

Se [Skapa en visningsförinställning](/help/assets/dynamic-media/managing-viewer-presets.md#creating-a-new-viewer-preset) för att skapa en egen förinställning för Interactive Video Viewer.

## Överföra en video och dess tillhörande miniatyrbilder {#uploading-a-video-and-its-associated-thumbnail-assets}

Om du redan har laddat upp videoklipp och miniatyrbilder går du vidare till [Lägg till interaktivitet i videon](#adding-interactivity-to-your-video).

>[!NOTE]
>
>MXF-videoformatet stöds ännu inte för användning med interaktiva videoklipp i Dynamic Media.

Om du har överfört fel videoklipp eller bilder, eller om du vill ta bort överförda videoklipp eller bilder som du inte längre behöver, se [Ta bort resurser](/help/assets/manage-digital-assets.md#delete-assets).

Så här överför du en video och dess associerade miniatyrbildsresurser:

1. Överför videon och tillhörande miniatyrbilder till den eller de mappar du vill använda.

   Se [Överför resurser](/help/assets/manage-digital-assets.md).
Se [Överför resurser med FTP-jobbplanering](/help/assets/manage-digital-assets.md).

   Nu kan du lägga till interaktivitet i videon.

## Lägg till interaktivitet i videon {#adding-interactivity-to-your-video}

Du lägger till tidslinjesegment i en video med den visuella redigeraren på sidan Skapa interaktiv video.

När du har lagt till tidslinjesegment lägger du till miniatyrbilder i varje segment. För varje miniatyrbild som du lägger till tillämpar du en åtgärd på den. Du kan t.ex. använda en snabbvy för miniatyrbilden eller tilldela en hyperlänk till den eller ett Experience Fragment.

Se [Upplevelsefragment](/help/sites-cloud/authoring/fundamentals/experience-fragments.md).

>[!NOTE]
>
>Delningsverktyg för sociala medier i interaktiv video stöds inte när du bäddar in visningsprogrammet i ett Experience Fragment. I stället kan du använda eller skapa visningsförinställningar som inte har verktyg för delning av sociala medier. Med sådana visningsförinställningar kan du bädda in dem i Experience Fragments.

>[!NOTE]
>
>Den URL-baserade länkningsmetoden är inte möjlig om det interaktiva innehållet har länkar till relativa URL-adresser, särskilt länkar till Experience Manager Sites-sidor.

Alternativen Ångra och Gör om, nära det övre högra hörnet på sidan, stöds under den aktuella skaps-/redigeringssessionen.

När du har sparat den interaktiva videon öppnas videon direkt i förhandsvisningen. Därifrån kan du välja en förinställning för Interactive Video Viewer och spela upp videon för att se en ungefärlig representation av hur den ser ut för kunderna.

**Så här lägger du till interaktivitet i videon:**

1. I resursvyn navigerar du till videon som du överförde och vill göra interaktiv.
1. Gör något av följande:

   * Hovra över bilden och välj sedan **[!UICONTROL Select]** (bockmarkeringsikon). I verktygsfältet väljer du **[!UICONTROL Edit]**.

   * Hovra över bilden och välj sedan **[!UICONTROL More actions]** (ikon med tre punkter) **[!UICONTROL > Edit]**.

   * Markera bilden om du vill öppna den på sidan Detaljvy. I verktygsfältet väljer du **[!UICONTROL Edit]**.

1. Gör något av följande på sidan Skapa interaktiv video:

   * För att börja spela upp videon väljer du **[!UICONTROL Play]** -knappen. När en viss produkt, tjänst eller detalj som du vill markera visas, väljer du **[!UICONTROL Add Segment]** i verktygsfältet. Upprepa tills du har nått slutet av videon.

      För varje tidssegment som du lägger till kan du tilldela det en eller flera miniatyrbilder. Du kan sedan länka dessa miniatyrbilder till QuickView-produktsidor som kunderna kan köpa eller till webbsidor för mer information.

   * För att börja spela upp videon väljer du **[!UICONTROL Play]** -knappen. När en viss produkt, tjänst eller detalj som du vill markera visas, väljer du **[!UICONTROL Pause]**. Välj **[!UICONTROL Add Segment]**.

      Fortsätt spela upp och pausa videon vid punkter längs tidslinjen där du vill lägga till ett segment tills du når slutet av videon.

1. (Valfritt) Dra fältet till vänster **[!UICONTROL Timeline Scale Slider]** vänster för att zooma in eller höger för att zooma ut. Med den här åtgärden kan du styra hur mycket detaljrikedom du ser på de segment som du har lagt till.

   ![chlimage_1-22](assets/chlimage_1-128.png)

   Beroende på videons längd är standardvärdet för Segmentvaraktighet följande värden:

   <table>
      <tbody>
        <tr>
        <td><strong>Om videolängden är ...</strong></td>
        <td><strong>Inställningen för segmentvaraktighet är som standard..</strong></td>
        </tr>
        <tr>
        <td>3 minuter eller mer</td>
        <td>60 sekunder</td>
        </tr>
        <tr>
        <td>2-3 minuter</td>
        <td>30 sekunder</td>
        </tr>
        <tr>
        <td>1-2 minuter</td>
        <td>20 sekunder<br /> </td>
        </tr>
        <tr>
        <td>30-60 sekunder</td>
        <td>10 sekunder</td>
        </tr>
        <tr>
        <td>30 sekunder eller mindre</td>
        <td>5 sekunder</td>
        </tr>
      </tbody>
    </table>

   Videons tidslinje använder så mycket skärmutrymme som det som finns tillgängligt för den. När du ändrar storlek på webbläsaren behåller segmenten som du lade till sin korrekta bredd.

   Följande tre skärmbilder använder samma video. Observera att bredden på varje segment ändras beroende på inställningen för tidslinjens skala.

   ![chlimage_1-23](assets/chlimage_1-129.png)

   Skärmbild A

   Skärmbild A ovan visar standardvyn för en 29-sekunders produktvideo. Tidslinjens skala är inställd på 5 sekunder som standard.

   ![chlimage_1-130](assets/chlimage_1-130.png)

   Skärmbild B

   I skärmbild B ovan har reglaget för tidslinjeskala dragits från standardvärdet 5 sekunder till 3 sekunder. Observera att tidstämplarna för den enskilda tidslinjens skala nu är inställda med 3-sekundersintervall.

   ![chlimage_1-25](assets/chlimage_1-131.png)

   Skärmbild C

   I skärmbild C ovan flyttades inställningen för tidslinjeskala till 8 sekunder. Lägg märke till hur segmenten som innehåller produktminiatyrer har krympt. Det är praktiskt att zooma ut på det här sättet om du har en lång video och vill kunna se en översikt över fler segment som normalt passar in på sidbredden.

1. (Valfritt) Gör något av följande:

   * Justera ett segments starttid och sluttid.

      Markera ett segment och dra sedan den inledande eller avslutande blå ovalen för att justera start- respektive sluttiden. Den videobildruta som visas flyttas till lämplig tid i videon, baserat på dina justeringar. Tidslinjesegmentets rörelse begränsas baserat på intilliggande segment i tidslinjen. Den minsta tillåtna segmenttiden är en sekund.

      Använd följande kortkommandon för att snabbt kontrollera och finjustera videosegmenten:

      * Om du vill söka efter videon direkt till början av det segmentet väljer du den blå inledande ovalen.
      * Om du vill söka efter videon direkt i slutet av det segmentet markerar du den efterföljande blå ovalen.
      * Om du vill återställa videouppspelningen till början av det segmentet markerar du hela segmentet.

   ![chlimage_1-26](assets/chlimage_1-132.png)

   Flytta slutet av ett tidslinjesegment

   * Ta bort ett segment

      Markera det sista segmentet på tidslinjen och välj sedan i verktygsfältet **[!UICONTROL Delete Segment]**. Om två eller flera segment är markerade är funktionen Ta bort segment inaktiverad.

      Du kan bara ta bort det sista segmentet. Om du till exempel vill ta bort alla segment på tidslinjen måste du alltid markera det sista och sedan markera **[!UICONTROL Delete Segment]**.


1. Markera ett tidssegment som du vill associera en eller flera miniatyrbilder till.
1. Till höger om videon väljer du **[!UICONTROL Content]** -fliken.
1. Under fliken Innehåll väljer du **[!UICONTROL Select Assets]**, bläddra sedan bland och markera alla bildresurser som du vill använda med videon. De markerade resurserna läggs till på panelen Resursväljare på fliken Innehåll.

1. Gör något av följande i resursväljaren under fliken Innehåll:

   <table>
      <tbody>
        <tr>
        <td>Associera en miniatyrbild med det markerade tidslinjesegmentet</td>
        <td><p>Markera bilden på resurssväljarpanelen till höger.</p> <p>Du kan lägga till så många miniatyrbilder du vill i ett tidslinjesegment. För varje bild som du väljer visas en bock över bilden i resursväljaren.</p> </td>
        </tr>
        <tr>
        <td>Ta bort en miniatyrbild från det markerade tidslinjesegmentet</td>
        <td><p>Gör något av följande:</p>
          <ul>
          <li>Avmarkera en bild med en bockmarkering på resurssväljarpanelen. Bildresursen tas bort från tidslinjesegmentet.<br /> </li>
          <li>Markera en bild i det markerade tidslinjesegmentet och välj sedan en bild i verktygsfältet <strong>Ta bort produkt</strong>.</li>
          </ul> </td>
        </tr>
      </tbody>
    </table>

   ![Resursväljaren](assets/chlimage_1-133.png)

   Om du väljer en bild på resurssväljarpanelen läggs den till i det valda tidslinjesegmentet.

1. Markera en miniatyrbild i ett av tidslinjesegmenten och välj sedan **[!UICONTROL Actions]** -fliken.
1. Gör något av följande:
   <table> 
    <tbody> 
      <tr> 
      <td>Associera den markerade miniatyrbilden med en snabbvy</td> 
      <td><p>Under Åtgärdstyp väljer du <strong>Snabbvy</strong>.</p> <p>Om du är kund inom Experience Manager Sites och e-handel:</p> 
       <ul> 
       <li>Observera att textfältet SKU-värde är förifyllt med den valda produktens SKU (Stock Keeping Unit). SKU:n är en unik identifierare för varje enskild produkt eller tjänst som du erbjuder. Det här fältet fylls i automatiskt när bilden är kopplad till en produkt i Experience Manager Commerce.</li> 
       <li>Om den i förväg ifyllda SKU:n är felaktig väljer du produktväljarens ikon (förstoringsglas) för att öppna sidan Välj produkt. Markera den produkt du vill använda och markera sedan bockmarkeringen i det övre högra hörnet på sidan. Du återgår till den interaktiva videoredigeraren.</li> 
       </ul> <p> Om du <em>not</em> en Experience Manager Sites- eller e-handelskund</p> 
       <ul> 
       <li>Se <a href="/help/assets/dynamic-media/carousel-banners.md#identifying-hotspot-and-image-map-variables">Identifiera hotspot-variabler</a>. Dessa variabler måste definieras.</li> 
       <li>Som standard använder det här SKU-fältet bildresursens filnamn utan tillägget. Om du använder en standardnamnkonvention för dina filer som baseras på SKU, behöver fältet vanligtvis inte redigeras ytterligare. </li> 
       <li>I annat fall redigerar du standardvärdet och anger rätt SKU-värde. I textfältet SKU-värde skriver du produktens SKU (Stock Keeping Unit), som är en unik identifierare för varje separat produkt eller tjänst som du erbjuder. Det angivna SKU-värdet fyller automatiskt i variabeldelen av QuickView-mallen så att systemet vet att den valda bilden associeras med en viss SKU:s snabbvy.</li> 
       </ul> <p>(Valfritt) Om det finns andra variabler i snabbvyn som du måste använda för att identifiera en produkt ytterligare väljer du <strong>Lägg till allmän variabel</strong>. Ange en extra variabel i textfältet. Till exempel: <code>category=Womens</code> är en tillagd variabel.</p> <p> </p> </td> 
      </tr> 
      <tr> 
      <td>Associera den markerade miniatyrbilden med en hyperlänk</td> 
      <td><p>Under Åtgärdstyp väljer du <strong>Hyperlänk</strong>gör du något av följande:</p> 
       <ul> 
       <li>Om du är kund hos Experience Manager Sites väljer du ikonen Platsväljare (mapp) för att navigera till en webbsida. Den URL-baserade länkningsmetoden är inte möjlig om det interaktiva innehållet har länkar till relativa URL-adresser, särskilt länkar till Experience Manager Sites-sidor.</li> 
       <li>Om du är en fristående Dynamic Media-kund anger du den fullständiga URL-sökvägen till en länkad webbsida i textfältet HREF.</li> 
       </ul> <p>Var noga med att ange om länken ska öppnas på en ny flik i webbläsaren eller på den aktuella fliken.</p> </td> 
      </tr> 
      <tr> 
      <td>Associera den markerade miniatyrbilden med ett Experience Fragment</td> 
      <td><p>Under Åtgärdstyp väljer du <strong>Experience Fragment</strong>gör du följande:<p> 
       <ul> 
       <li>Om du är Experience Manager Sites-kund väljer du sökikonen (förstoringsglas) för att öppna sidan Experience Fragment. Välj det Experience Fragment som du vill använda och välj sedan <strong>Om du vill gå tillbaka till åtgärdspanelen på föregående sida väljer du </strong>i det övre högra hörnet på sidan.<br /> Se <a href="/help/sites-cloud/authoring/fundamentals/experience-fragments.md">Upplevelsefragment</a>.</li> 
      </ul> 
       <ul> 
       <li>Ange bredd och höjd för Experience Fragment så som det visas på videon.</li>
       </ul><strong>Anteckning</strong>: Delningsverktygen för sociala medier i interaktiv video stöds inte när du bäddar in visningsprogrammet i ett Experience Fragment. I stället kan du använda eller skapa visningsförinställningar som inte har verktyg för delning av sociala medier. Med sådana visningsförinställningar kan du bädda in dem i Experience Fragments.</p></tr>&lt; 
      <tr> 
      <td>Redigera en åtgärd som redan har tilldelats en miniatyrbild</td> 
      <td>Markera en miniatyrbild som har en kedjelänk till höger om textetiketten i ett tidslinjesegment. Länken kedja anger att en åtgärd har tilldelats den. Om du vill göra ändringarna väljer du <strong>Åtgärder</strong> -fliken.</td> 
      </tr> 
      <tr> 
      <td>Ändra textetiketten för en miniatyrbild</td> 
      <td><p>Som standard använder textetiketten miniatyrbildernas <code>Title</code> metadatafält. If <code>Title</code> finns inte, används miniatyrbildens filnamn i stället, men utan filnamnstillägget.</p> <p>Ändra textetiketten för en miniatyrbild under <strong>Åtgärder </strong>anger du den önskade texten direkt under bildresursen som visas. Se bilden nedan.</p> <p>Den nya textetiketten används bara av själva videospelaren och den miniatyrtext som visas i tidslinjesegmentet. Etikettändringen påverkar inte miniatyrbildens metadatafält Titel eller dess filnamn.</p> </td> 
      </tr> 
      <tr> 
      <td>Återställa en ändring</td> 
      <td>I sidans övre högra hörn väljer du <strong>Ångra</strong> eller <strong>Gör om</strong>.</td> 
      </tr> 
    </tbody> 
   </table>

   ![experience_efragment_interactiveVideos](assets/experiencefragment_interactivevideos.png)

   En ny textetikett läggs till i miniatyrbilden.

1. Gör något av följande:

   * Upprepa steg 6-11 om du vill lägga till fler miniatyrbilder i tidslinjesegment i videon.
   * Fortsätt till det valfria steget 13.

1. (Valfritt) Gör något av följande:

   * **[!UICONTROL Merge Segment]** - Du kan kombinera två intilliggande segment (med eller utan produktminiatyrer tilldelade till dem) till ett segment.

      Markera på tidslinjen två eller flera sammanhängande segment som du vill sammanfoga till ett. Det finns inga blå ovala draghandtag för de två valda segmenten i bilden nedan.

      Välj **[!UICONTROL Merge Segment]** i verktygsfältet.
   ![chlimage_1-134](assets/chlimage_1-134.png)

   Sammanfoga två valda femsekunderssegment till ett segment på tio sekunder.

   * **[!UICONTROL Split Segment]** - Du kan dela upp ett enskilt segment i två segment med samma tidsindelning. Om det redan finns produktminiatyrer för segmentet kombineras miniatyrbilderna till det vänstra segmentet.

      Markera det segment som du vill dela upp i halva på tidslinjen och markera sedan **[!UICONTROL Split Segment]** i verktygsfältet.

      Om du markerar två eller flera segment inaktiveras **[!UICONTROL Split Segment]** -funktion.
   ![chlimage_1-135](assets/chlimage_1-135.png)

   Dela upp ett markerat segment på tio sekunder i två segment på fem sekunder vardera.

1. Nära det övre högra hörnet av **[!UICONTROL Create Interactive Video]** visas namnet på den valda visningsförinställningen som används för videon. Markera namnet om du vill välja en annan visningsförinställning.

   Till exempel `Shoppable_Video_light` Med visningsförinställningen kan du spela upp videon med ett vitt visningsområde bredvid videon. Visningsområdet är där de valda miniatyrbilderna visas under uppspelning. The `Shoppable_Video_dark` Med visningsförinställningen kan du spela upp videon med ett svart visningsområde bredvid videon.

   Om du har skapat en egen förinställning för Interactive Video Viewer kan du se den i listan med förinställningar som du kan välja mellan.

   När du är klar väljer du **[!UICONTROL Save]**.

   >[!NOTE]
   >
   >När du sparar den interaktiva videon sparas en associerad `.vtt`-fil automatiskt med den. The `.vtt` filen sparas i `_VTT` mapp i roten av **[!UICONTROL Assets]**. Filen och mappen är nödvändiga för att den interaktiva videon ska kunna spelas upp korrekt på webbplatsen. Därför ska du inte flytta, redigera eller ta bort mappen `_VTT` eller dess innehåll.

1. Publicera den interaktiva videon. Publicering skapar den inbäddningskod eller URL som du så småningom kopierar och klistrar in på webbplatsupplevelserna.

   Om du har lagt till interaktivitet med snabbvyer ska du bara använda inbäddningskoden; om du har lagt till interaktivitet med hyperlänkade webbsidor kan du även använda den publicerade webbadressen. Observera dock att den URL-baserade länkningsmetoden inte är möjlig om ditt interaktiva innehåll har länkar till relativa URL-adresser, särskilt länkar till Experience Manager Sites-sidor.

   Se [Publicera resurser](publishing-dynamicmedia-assets.md).

   >[!NOTE]
   >
   >Om du vill publicera en videoklipp som kan köpas med snabbvyer måste du även publicera videons relaterade bildresurser separat från din e-handelsplats.

   När du har lagt till tidslinjesegment och publicerat den interaktiva videon kan du lägga till den på din befintliga startsida för webbplatsen. Se [Integrera en interaktiv video med webbplatsen](#integrating-an-interactive-video-with-your-website).

## Publicera interaktivt videomaterial {#publishing-interactive-video-assets}

Se [Publicera resurser](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md) om du vill ha mer information om hur du publicerar interaktiva videoresurser.

## Integrera en interaktiv video med webbplatsen {#integrating-an-interactive-video-with-your-website}

När du har överfört en video, lagt till tidslinjesegment i den och publicerat den interaktiva videon är du nu redo att lägga till den på din befintliga webbplats.

Om du är kund hos Experience Manager Sites kan du lägga till den interaktiva videon genom att dra Interactive Media-komponenten till din sida. Se [Lägga till Dynamic Media-resurser på sidor](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

Om du är en fristående Experience Manager Assets-kund kan du lägga till den interaktiva videon manuellt på din webbplats enligt beskrivningen i det här avsnittet.

1. Kopiera den publicerade interaktiva videons inbäddningskod eller URL.
Se [Bädda in video- eller bildvisningsprogrammet på en webbsida](/help/assets/dynamic-media/embed-code.md).
Om du har lagt till interaktivitet med snabbvyer ska du bara använda inbäddningskoden; om du har lagt till interaktivitet med hyperlänkade webbsidor kan du även använda den publicerade webbadressen. Observera dock att den URL-baserade länkningsmetoden inte är möjlig om ditt interaktiva innehåll har länkar till relativa URL-adresser, särskilt länkar till Experience Manager Sites-sidor.

1. Identifiera var den statiska videon finns i målets webbsideskod.
1. Ta bort den statiska videon och ersätt koden med den inbäddade koden eller URL-adressen som du kopierade från Experience Manager Assets, som den är.
Den kopierade inbäddningskoden ställs in för en responsiv miljö så att den automatiskt passar det område som den statiska videon tidigare upptog.

>[!NOTE]
>
>Nu är du klar om du har lagt till interaktivitet med endast hyperlänkade webbsidor.
>
>Om du har lagt till någon interaktivitet för att aktivera en snabbvy är miniatyrbilderna bredvid den interaktiva videon endast avsedda för visning. de är ännu inte integrerade med dina befintliga snabbvyer. I så fall måste du integrera den interaktiva videon med befintliga snabbvyer på webbplatsen.

**Exempel**

Använda demowebbplatsen som exempel:

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-0.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-0.html)

Observera att koden för videoinbäddning är standard:

```xml
<style type="text/css">
 #s7video_div.s7videoviewer{
   width:100%;
   height:auto;
 }
</style>

<script type="text/javascript" src="https://demos-pub.assetsadobe.com/etc/dam/viewers/s7viewers/html5/js/VideoViewer.js"></script>
<div id="s7video_div"></div>
<script type="text/javascript">
 var s7videoviewer = new s7viewers.VideoViewer({
  "containerId" : "s7video_div",
  "params" : {
   "serverurl" : "https://adobedemo62-h.assetsadobe.com/is/image",
   "contenturl" : "https://demos-pub.assetsadobe.com/",
   "config" : "/etc/dam/presets/viewer/Video",
   "config2": "/etc/dam/presets/analytics",
   "videoserverurl": "https://gateway-na.assetsadobe.com/DMGateway/public/demoCo",
   "posterimage": "/content/dam/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4",
   "asset" : "/content/dam/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4" }
 }).init();
</script>
```

Integrationen är lika enkel som att ta bort inbäddningskoden för video och ersätta den med den interaktiva inbäddningskoden för video från Experience Manager. Resultatet visas på följande URL. Även om det visar en interaktiv video på sidan är den ännu inte integrerad med de befintliga snabbvyerna:

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-1.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-1.html)

## Integrera en interaktiv video med en befintlig QuickView {#integrating-an-interactive-video-with-an-existing-quickview}

>[!NOTE]
>
>Detta gäller endast om du är en fristående Experience Manager Assets-kund.

Det sista steget i den här processen är att integrera din interaktiva video med en befintlig QuickView-implementering som används på din webbplats. Det finns ingen lösning på integreringen som fungerar i alla fall. Alla QuickView-implementeringar är unika. Därför behövs ett specifikt tillvägagångssätt som innebär att IT-personal på frontend får hjälp.

Den befintliga Quickview-implementeringen representerar normalt en kedja av interrelaterade åtgärder som inträffar på webbsidan i följande ordning:

1. En användare utlöser ett element i användargränssnittet för webbplatsen.
1. FrontEnd-koden hämtar en QuickView-URL som baseras på användargränssnittselementet som utlöstes i steg 1.
1. Slutkoden skickar en AJAX med den URL som du får i steg 2.
1. Bakåtlogiken returnerar motsvarande QuickView-data eller -innehåll tillbaka till slutkoden.
1. Slutkoden läser in QuickView-data eller -innehåll.
1. Om du vill kan du konvertera den inlästa QuickView-informationen till en HTML-representation med hjälp av koden.
1. I slutkoden visas en modal dialogruta eller panel och HTML-innehållet på skärmen återges för slutanvändaren.

Dessa anrop representerar inte oberoende offentliga API-anrop som kan anropas av webbsidans logik från ett godtyckligt steg. I stället är det ett kedjat anrop där varje steg döljs i den sista fasen (återanrop) av föregående steg.

Samtidigt som den interaktiva videon ersätter steg 1, och delvis steg 2, när en användare väljer en miniatyrbild i den interaktiva videon, hanteras denna användarinteraktion av användaren. Visningsprogrammet returnerar en händelse till webbsidan som innehåller alla miniatyrbildsdata som tidigare lagts till i Experience Manager.

I en sådan händelsehanterare gör koden längst fram följande:

* Lyssnar på en händelse som skickas av den interaktiva videon.
* Skapar en QuickView-URL som baseras på miniatyrbildsdata.
* Startar processen att läsa in snabbvyn från serverdelen och återge den på skärmen för visning.

Dessutom har Interactive Video Viewer stöd för helskärmsläge. Slutanvändaren aktiverar snabbvyer genom att välja en miniatyrbild utan att lämna helskärmsläget. För att uppnå den här funktionen ändrar du frontdelskoden så att den modala dialogrutan för snabbvyn bifogas till visningsprogrammets behållare. Lägg inte till dokument-BODY eller något annat webbsideselement som inte är tillgängligt när visningsprogrammet är i helskärmsläge. Koden som utför det här jobbet lyssnar på ett till återanrop till visningsprogrammet som skickas när visningsprogrammet har lästs in på sidan.

Den inbäddningskod som returneras av Experience Manager har redan en färdig händelsehanterare på plats. Den kommenteras ut enligt följande markerade kodfragment:

```xml
<style type="text/css">
 #s7interactivevideo_div.s7interactivevideoviewer{
   width:100%;
   height:auto;
 }
</style>
<script type="text/javascript" src="https://demos-pub.assetsadobe.com/etc/dam/viewers/s7viewers/html5/js/InteractiveVideoViewer.js"></script>

<div id="s7interactivevideo_div"></div>
<script type="text/javascript">
 var s7interactivevideoviewer = new s7viewers.InteractiveVideoViewer({
  "containerId" : "s7interactivevideo_div",
  "params" : {
   "serverurl" : "https://adobedemo62-h.assetsadobe.com/is/image",
   "contenturl" : "https://demos-pub.assetsadobe.com/",
   "config" : "/etc/dam/presets/viewer/Shoppable_Video_light",
   "config2": "/etc/dam/presets/analytics",
   "videoserverurl": "https://gateway-na.assetsadobe.com/DMGateway/public/demoCo",
   "interactivedata": "content/dam/_VTT/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4.svideo.vtt",
   "VideoPlayer.contenturl": "https://adobedemo62-h.assetsadobe.com/is/content",
   "asset" : "/content/dam/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4" }
 })
 /* // Example of interactive video event for quickview.
   s7interactivevideoviewer.setHandlers({
   "quickViewActivate": function(inData) {
     var sku=inData.sku; //SKU for product ID
    //To pass other parameter from the hotspot, you need to add custom parameter during the hotspot setup as parameterName=value
    loadQuickView(sku); //Replace this call with your quickview plugin
    //Please refer to your quickviewer plugin for the quickview call
    },
"initComplete":function() {
    //--- Attach quickview popup to viewer container so popup will work in fullscreen mode ---
    var popup = document.getElementById('quickview_div'); // get custom quickview container
    popup.parentNode.removeChild(popup); // remove it from current DOM
    var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId(); // get viewer container component
    var inner_container = document.getElementById(sdkContainerId);
    inner_container.appendChild(popup); //Attach custom quickview container to viewer
    }
   });
 */
 s7interactivevideoviewer.init();
</script>
```

Därför är det bara nödvändigt att avkommentera det markerade kodfragmentet ovan och ersätta dummy-hanterarbrödtexten med kod som är specifik för den aktuella webbsidan.

Det finns två standardhanterare för återanrop i standardkoden för inbäddning: `quickViewActivate` och `initComplete`. The `quickViewActivate` hanteraren aktiveras när en miniatyrbild är markerad i visningsprogrammet. Integrera visningsprogrammet med QuickView-aktiveringslogiken. The `initComplete` hanteraren utlöses bara en gång när användaren läser in på sidan. Den här hanteraren används för att justera platsen för dialogrutan Snabbvy i webbsidans DOM.

Processen med att skapa en URL för snabbvyn är motsatt till processen att identifiera miniatyrbildsvariabler som beskrivs tidigare i det här avsnittet. Med hjälp av de tidigare identifierade exemplen på snabbvyns URL kan du se hur snabbvyns URL är uppbyggd i varje fall:

<table>
  <tbody>
  <tr>
    <td><p>En SKU, som finns i frågesträngen</p> </td>
    <td><code class="code">s7interactivevideoviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/json?productId=" + inData.sku + "&amp;source=100";
      },
      });</code></td>
  </tr>
  <tr>
    <td>En SKU, finns i URL-sökvägen</td>
    <td><code class="code">s7interactivevideoviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/product/" + inData.sku;
      },
      });</code></td>
  </tr>
  <tr>
    <td><p>SKU och kategori-ID i frågesträngen</p> </td>
    <td><code class="code">s7interactivevideoviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/quickView/product/?category=" + inData.categoryId + "&amp;prodId=" + inData.sku;
      },
      });</code></td>
  </tr>
  </tbody>
</table>

Det sista steget för att utlösa snabbgransknings-URL:en och aktivera snabbvypanelen kräver troligen hjälp av en IT-handläggare på IT-avdelningen. De har kunskap om hur de bäst kan utlösa QuickView-implementeringen från rätt steg med en färdig QuickView-URL.

Du kan se hur dessa steg tillämpas på demowebbplatsen för att helt integrera en interaktiv video med QuickView-koden. Tidigare i det här avsnittet identifierades strukturen för snabbvyns URL som följande:

```xml
/datafeed/$CategoryId$-$SKU$.json
```

Det är enkelt att rekonstruera URL:en i `quickViewActivate` hanterare använda `categoryId` och `sku` fält som är tillgängliga i `inData` objekt som skickas till hanteraren via visningsprogrammets kod enligt följande:

```xml
var sku=inData.sku;
var categoryId=inData.categoryId;
var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
```

Demonstrationswebbplatsen utlöser dialogrutan Snabb visning med en enkel `loadQuickView()` funktionsanrop. Den här funktionen har bara ett argument, vilket är snabbvydata-URL:en. Så det sista steget för att integrera den interaktiva videon är att lägga till följande kodrad i `quickViewActivate` hanterare:

```xml
loadQuickView(quickViewUrl);
```

Kontrollera slutligen att dialogrutan Snabbvy är kopplad till visningsprogrammets behållarelement. Standardinställningen för inbäddningskod innehåller exempelsteg för att uppnå den här funktionen. Om du vill få en referens till visningsprogrammets behållarelement kan du använda följande kodrader:

```xml
var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId(); // get viewer container component
var inner_container = document.getElementById(sdkContainerId);
```

Plats `inner_container` är en referens till `DIV` -element som hanteras av visningsprogrammet. Du vill att dialogrutan ska vara underordnad den `DIV`.

Stegen för att hitta det modala dialogruteelementet och bifoga det till behållaren ovan är skiftlägeskänsliga. Återigen kan du få hjälp av den som är bekant med den QuickView-implementering som behövs.

För exempelwebbplatsen implementeras den modala dialogrutan för snabbvyn som en `DIV` med det spärra/knipa-ID som är kopplat direkt till dokumentet `BODY`. Koden som flyttar dialogrutan till visningsprogrammets behållare är därför så enkel som följande:

```xml
var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId(); // get viewer container component
var inner_container = document.getElementById(sdkContainerId);
inner_container.appendChild(document.getElementById("quickview-modal"));
```

Den fullständiga källkoden är följande:

```xml
<style type="text/css">
 #s7interactivevideo_div.s7interactivevideoviewer{
   width:100%;
   height:auto;
 }
</style>
<script type="text/javascript" src="https://demos-pub.assetsadobe.com/etc/dam/viewers/s7viewers/html5/js/InteractiveVideoViewer.js"></script>

<div id="s7interactivevideo_div"></div>
<script type="text/javascript">
 var s7interactivevideoviewer = new s7viewers.InteractiveVideoViewer({
  "containerId" : "s7interactivevideo_div",
  "params" : {
   "serverurl" : "https://adobedemo62-h.assetsadobe.com/is/image",
   "contenturl" : "https://demos-pub.assetsadobe.com/",
   "config" : "/etc/dam/presets/viewer/Shoppable_Video_light",
   "videoserverurl": "https://gateway-na.assetsadobe.com/DMGateway/public/demoCo",
   "interactivedata": "content/dam/_VTT/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4.svideo.vtt",
   "VideoPlayer.contenturl": "https://adobedemo62-h.assetsadobe.com/is/content",
   "asset" : "/content/dam/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4" }
 })
 // Example of interactive video event for quickview.
   s7interactivevideoviewer.setHandlers({
   "quickViewActivate": function(inData) {
     var sku=inData.sku; //SKU for product ID
     var categoryId=inData.categoryId; //categoryId
    var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
    loadQuickView(quickViewUrl);
    },
   "initComplete":function() {
    //--- Attach quickview popup to viewer container so popup will work in fullscreen mode ---
    var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId(); // get viewer container component
    var inner_container = document.getElementById(sdkContainerId);
    inner_container.appendChild(document.getElementById("quickview-modal"));
    }
   });
 s7interactivevideoviewer.init();
</script>
```

Den färdiga demowebbplatsen med den helt integrerade interaktiva videon ser ut så här:

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-3.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-3.html)

## Skapa anpassade popup-fönster® med QuickView {#using-quickviews-to-create-custom-pop-ups}

Se [Skapa anpassade popup-fönster® med QuickView](/help/assets/dynamic-media/custom-pop-ups.md). —>
