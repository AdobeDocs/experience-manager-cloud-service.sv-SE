---
title: Integrera Dynamic Media Viewers med Adobe Analytics och Adobe Launch
description: Med tillägget Dynamic Media Viewers för Adobe Launch, tillsammans med releasen av Dynamic Media Viewers 5.13, kan kunder som använder Dynamic Media, Adobe Analytics och Adobe Launch använda händelser och data som är specifika för Dynamic Media Viewers i Adobe Launch-konfigurationen.
translation-type: tm+mt
source-git-commit: 1713cddf713afc24103a841a7dbae923941f6322
workflow-type: tm+mt
source-wordcount: '6263'
ht-degree: 16%

---


# Integrera Dynamic Media Viewers med Adobe Analytics och Adobe Launch {#integrating-dynamic-media-viewers-with-adobe-analytics-and-adobe-launch}

## Vad är Dynamic Media Viewer-integrering med Adobe Analytics och Adobe Launch? {#what-is-dynamic-media-viewers-integration-with-adobe-analytics-and-adobe-launch}

Med det nya tillägget *Dynamic Media Viewers* för Adobe Launch, tillsammans med den senaste versionen av Dynamic Media Viewers 5.13, kan kunder som använder Dynamic Media, Adobe Analytics och Adobe Launch använda händelser och data som är specifika för Dynamic Media Viewers i sin Adobe Launch-konfiguration.

Integrationen innebär att du kan spåra användningen av dynamiska medievyer på din webbplats med Adobe Analytics. Samtidigt kan du använda de händelser och data som visas av tittarna med andra Launch-tillägg som kommer från Adobe eller en tredje part.

Mer information om tillägg finns i [Adobe Extension](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/overview.html) i användarhandboken för Experience Platform Launch.

**Vem bör läsa denna dokumentation:** Webbplatsadministratörer, utvecklare på AEM-plattformen och driftadministratörer.

### Begränsningar i integreringen {#limitations-of-the-integration}

* Adobe Launch-integrering för Dynamic Media-visningsprogram fungerar inte i AEM författarnod. Du kan inte se någon spårning från en WCM-sida förrän den har publicerats.
* Adobe Launch-integrering för Dynamic Media-visningsprogram stöds inte för &quot;popup&quot;-åtgärdsläget, där visningsprogrammets URL hämtas med knappen &quot;URL&quot; på sidan Resursinformation.
* Integrering med Adobe Launch kan inte användas samtidigt med integrering med äldre visningsprogram med Analytics (med `config2=` parametern).
* Stödet för videospårning är begränsat till enbart huvudspårning av uppspelning, vilket beskrivs i [Spårningsöversikt](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/track-av-playback/track-core-overview.html). Speciellt stöds inte QoS, Ads, Chapter/Segments eller Errors tracking.
* Konfiguration av lagringstid för dataelement stöds inte för dataelement med tillägget *Dynamiska medievyer* . Lagringsvaraktighet måste anges till **[!UICONTROL None]**.

### Användningsexempel för integreringen {#use-cases-for-the-integration}

Det viktigaste användningsområdet för integreringen med Adobe Launch är kunder som använder både AEM Assets och AEM Sites. I sådana fall kan du konfigurera en standardintegrering mellan AEM författarnod och Adobe Launch och sedan associera platsinstansen med Adobe Launch-egenskapen. Efter det kommer alla WCM-komponenter för Dynamic Media som läggs till på en Sites-sida att spåra data och händelser från tittarna.

Se [Om spårning av dynamiska medievyer i AEM Sites](https://wiki.corp.adobe.com/display/~oufimtse/Dynamic+Media+Viewers+integration+with+Adobe+Launch#DynamicMediaViewersintegrationwithAdobeLaunch-TrackingDynamicMediaViewersinAEMSites).

Ett sekundärt användningsfall som integreringen stöder är kunder som bara använder AEM Assets eller Dynamic Media Classic. I så fall får du inbäddningskoden för ditt visningsprogram och lägger till den på webbplatssidan. Hämta sedan Adobe Launch-bibliotekets produktions-URL från Adobe Launch och lägg till den manuellt i webbsideskoden.

Se [Om spårning av Dynamic Media-visningsprogram med hjälp av inbäddningskod](https://wiki.corp.adobe.com/display/~oufimtse/Dynamic+Media+Viewers+integration+with+Adobe+Launch#DynamicMediaViewersintegrationwithAdobeLaunch-TrackingDynamicMediaViewersusingEmbedcode).

## Hur data- och händelsespårning fungerar i integreringen {#how-data-and-event-tracking-works-in-the-integration}

Integreringen utnyttjar två separata och oberoende typer av spårning av dynamiska medievyer: *Adobe Analytics* och *Adobe Analytics för ljud och video*.

### Om spårning med Adobe Analytics  {#about-tracking-using-adobe-analytics}

Med Adobe Analytics kan du spåra åtgärder som slutanvändaren utför när de interagerar med dynamiska medievyer på webbplatsen. Med Adobe Analytics kan du också spåra visningsprogramspecifika data. Du kan till exempel spåra och spela in inläsningshändelser tillsammans med resursnamnet, eventuella zoomåtgärder som har utförts, videouppspelningsåtgärder och så vidare.

I Adobe Launch fungerar koncepten med *dataelement* och *regler* tillsammans för att möjliggöra Adobe Analytics-spårning.

#### Om dataelement i Adobe Launch {#about-data-elements-in-adobe-launch}

Ett dataelement i Adobe Launch är en namngiven egenskap vars värde antingen är statiskt definierat eller dynamiskt beräknat baserat på statusen för en webbsida eller dynamiska medievydata.

Vilka alternativ som är tillgängliga för en dataelementsdefinition beror på listan med tillägg som är installerade i Adobe Launch-egenskapen. Tillägget &quot;Core&quot; är förinstallerat och finns tillgängligt direkt i alla konfigurationer. Med det här tillägget Core kan du definiera ett dataelement som kommer från cookie, JavaScript-kod, frågesträng och många andra källor.

För Adobe Analytics tracking måste ytterligare tillägg installeras, vilket beskrivs i [Installera och konfigurera tillägg](#installing-and-setup-of-extensions). Tillägget Dynamic Media Viewer ger möjlighet att definiera ett dataelement som är ett argument i Dynamic Viewer-händelsen. Det är till exempel möjligt att referera till visningsprogramtypen, eller resursnamnet som rapporteras av visningsprogrammet vid inläsning, den zoomnivå som rapporteras när användaren zoomar och mycket annat.

Tillägget Dynamic Media Viewer håller automatiskt värdena för Data Elements uppdaterad.

När du har definierat det kan ett dataelement användas på andra platser i användargränssnittet för Adobe-start med hjälp av väljarwidgeten för dataelement. Dataelement som definieras för spårning av dynamiska medievyer kommer att refereras av tillägget Ange variabelåtgärd för Adobe Analytics i regeln (se nedan).

Mer information finns i [Dataelement](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/data-elements.html) i användarhandboken för Experience Platform Launch.

#### Om regler i Adobe Launch {#about-rules-in-adobe-launch}

En regel i Adobe Launch är en agnostisk konfiguration som definierar tre områden som utgör en regel: *Händelser*, *villkor* och *åtgärder*:

* *Händelser* (if) anger för Adobe Launch när en regel ska aktiveras.
* *Villkor* (if) anger för Adobe Launch vilka ytterligare begränsningar som ska tillåtas eller inte när en regel aktiveras.
* *Åtgärder* (sedan) anger för Adobe Launch vad som ska göras när en regel aktiveras.

Vilka alternativ som är tillgängliga i avsnittet Händelser, Villkor och Åtgärder beror på vilka tillägg som är installerade i Adobe Launch Property. Tillägget *Core* är förinstallerat och kan användas direkt i alla konfigurationer. Tillägget innehåller flera alternativ för Händelser, t.ex. grundläggande åtgärder på webbläsarnivå som inkluderar fokusändring, tangenttryckningar, formulärskickning osv. Den innehåller även alternativ för Villkor, som cookie-värde, webbläsartyp och mycket annat. För Åtgärder är endast alternativet Anpassad kod tillgängligt.

För Adobe Analytics tracking måste flera tillägg installeras, vilket beskrivs i [Installera och konfigurera tillägg](#installing-and-setup-of-extensions). Särskilt:

* Tillägget Dynamic Media Viewer utökar listan med händelser som stöds till händelser som är specifika för Dynamic Media-visningsprogram, t.ex. inläsning av visningsprogram, resursväxling, inzoomning och videouppspelning.
* Adobe Analytics-tillägget utökar listan över åtgärder som stöds med två åtgärder som krävs för att skicka data till spårningsservrar: *Ange variabler* och *skicka fyr*.

Om du vill spåra Dynamic Media-visningsprogram kan du använda någon av följande typer:

* Händelser från tillägget Dynamic Media Viewer, Core-tillägget eller något annat tillägg.
* Villkor i regeldefinitionen. Du kan också lämna villkorsområdet tomt.

I avsnittet Åtgärder måste du ha en *Ange variabler* -åtgärd. Den här åtgärden anger för Adobe Analytics hur spårningsvariabler ska fyllas i med data. Samtidigt skickar inte åtgärden *Ange variabler* något till spårningsservern.

Åtgärden *Ange variabler* måste följas av en *Skicka Beacon* -åtgärd. Åtgärden *Send Beacon* skickar data till analysspårningsservern. Båda åtgärderna, *Ange variabler* och *Skicka Beacon*, kommer från Adobe Analytics-tillägget.

Mer information finns i [Regler](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/rules.html) i användarhandboken för Experience Platform Launch.

#### Exempelkonfiguration {#sample-configuration}

I följande exempelkonfiguration i Adobe Launch visas hur du spårar ett resursnamn när visningsprogrammet läses in.

1. På **[!UICONTROL Data Elements]** fliken definierar du ett dataelement `AssetName` som refererar till `asset` parametern för `LOAD` händelsen från tillägget Dynamiska medievyer.

   ![image2019-11](assets/image2019-11.png)

1. På **[!UICONTROL Rules]** fliken definierar du en regel *TrackAssetOnLoad*.

   I den här regeln använder **[!UICONTROL Event]** fältet händelsen **[!UICONTROL LOAD]** från tillägget Dynamiska medievyer.

   ![image2019-22](assets/image2019-22.png)

1. Åtgärdskonfigurationen har två åtgärdstyper från Adobe Analytics-tillägget:

   *Ange variabler*, som mappar en analysvariabel som du väljer till värdet för `AssetName` dataelementet.

   *Skicka Beacon* som skickar spårningsinformation till Adobe Analytics.

   ![image2019-3](assets/image2019-3.png)

1. Den resulterande regelkonfigurationen ser ut så här:

   ![image2019-4](assets/image2019-4.png)

### Om Adobe Analytics för ljud och video {#about-adobe-analytics-for-audio-and-video}

När ett Experience Cloud-konto prenumererar på Adobe Analytics för ljud och video räcker det att aktivera videospårning i tilläggsinställningarna för *dynamiska medievyer* . Videomått blir tillgängligt i Adobe Analytics. Videospårning beror på att det finns Adobe Media Analytics för ljud- och videotillägg.

Se [Installera och konfigurera tillägg](#installing-and-setup-of-extensions).

För närvarande är stödet för videospårning begränsat till&quot;huvuduppspelningsspårning&quot;, vilket beskrivs i [Spårningsöversikt](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/track-av-playback/track-core-overview.html). Speciellt stöds inte QoS, Ads, Chapter/Segments eller Errors tracking.

## Använda tillägget Dynamic Media Viewer {#using-the-dynamic-media-viewers-extension}

Som nämndes i [Användningsexempel för integreringen](#use-cases-for-the-integration)är det möjligt att spåra Dynamic Media-visningsprogram med den nya Adobe Launch-integrationen i AEM Sites och genom att använda inbäddningskod.

### Spåra Dynamic Media-visningsprogram i AEM Sites {#tracking-dynamic-media-viewers-in-aem-sites}

Om du vill spåra Dynamic Media-visningsprogram i AEM Sites måste du utföra alla steg som listas under [Konfigurera alla integrationsdelar](#configuring-all-the-integration-pieces) . Du måste skapa IMS-konfigurationen och konfigurationen för Adobe Launch Cloud.

Om du använder en WCM-komponent som stöds av Dynamic Media, spåras data automatiskt till Adobe Analytics, Adobe Analytics for Video eller båda, efter rätt konfiguration.

Se [Lägga till dynamiska medieresurser på sidor med hjälp av Adobe-platser](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

### Spåra Dynamic Media-visningsprogram med hjälp av inbäddningskod {#tracking-dynamic-media-viewers-using-embed-code}

Kunder som inte använder AEM Sites, eller bäddar in Dynamic Media-visningsprogram på webbsidor utanför AEM Sites, eller båda, kan fortfarande använda Adobe Launch-integrering.

Du måste slutföra konfigurationsstegen i avsnitten [Konfigurera Adobe Analytics](#configuring-adobe-analytics-for-the-integration) och [Konfigurera Adobe Launch](#configuring-adobe-launch-for-the-integration). AEM-relaterade konfigurationssteg behövs dock inte.

Om konfigurationen är korrekt kan du lägga till stöd för Adobe Launch på en webbsida med ett dynamiskt mediavisningsprogram.

Mer information om hur du använder inbäddningskoden för Adobe Launch-biblioteket finns i [Lägga till koden](https://docs.adobe.com/content/help/en/launch/using/implement/configure/implement-the-launch-install-code.html) för Starta inbäddning.

Mer information om hur du använder inbäddningsfunktionen i AEM Dynamic Media finns i [Bädda in video- eller bildvisningsprogrammet på en webbsida](/help/assets/dynamic-media/embed-code.md) .

**Spåra Dynamic Media-visningsprogram med hjälp av inbäddningskod**

1. Ha en webbsida redo för inbäddning av ett dynamiskt medievisningsprogram.
1. Hämta inbäddningskoden för Adobe Launch-biblioteket genom att först logga in på Adobe Launch (se [Konfigurera Adobe Launch](#configuring-adobe-launch-for-the-integration)).
1. Click **[!UICONTROL Property]**, then click the **[!UICONTROL Environments]** tab.
1. Plocka upp den miljönivå som är relevant för webbsidans miljö. Klicka sedan på ruteikonen i **[!UICONTROL Install]** kolumnen.
1. **[!UICONTROL In the Web Install Instructions]** kopierar den fullständiga inbäddningskoden för Adobe-startbiblioteket tillsammans med de omgivande `<script/>` taggarna.

## Referenshandbok för tillägget Dynamic Media Viewers {#reference-guide-for-the-dynamic-media-viewers-extension}

### Om konfigurationen för Dynamic Media Viewer {#about-the-dynamic-media-viewers-configuration}

Tillägget Dynamic Media Viewer integreras automatiskt med startbiblioteket i Adobe om alla följande villkor nedan är uppfyllda:

* Adobe Launch-bibliotekets globala objekt ( `_satellite`) finns på sidan.
* Tilläggsfunktionen för dynamiska medievyer `_dmviewers_v001()` är definierad för `_satellite`.

* `config2=` Ingen visningsprogramparameter har angetts, vilket innebär att visningsprogrammet inte använder äldre Analytics-integrering.

Dessutom finns det ett alternativ för att uttryckligen inaktivera Adobe Launch-integrering i visningsprogrammet genom att ange `launch=0` parameter i visningsprogrammets konfiguration. Standardvärdet för den här parametern är `1`.

### Konfigurera tillägget för dynamiska medievyer {#configuring-the-dynamic-media-viewers-extension}

Det enda konfigurationsalternativet för tillägget Dynamiska medievyer är **[!UICONTROL Enable Adobe Media Analytics for Audio and Video]**.

När du markerar (aktiverar eller&quot;aktiverar&quot;) det här alternativet och om Adobe Media Analytics för ljud- och videotillägg är installerat och korrekt konfigurerat skickas videouppspelningsstatistik till Adobe Analytics för ljud- och videolösning. Om du inaktiverar det här alternativet inaktiveras videospårning.

Observera att om du aktiverar det här alternativet *utan* att ha Adobe Media Analytics för ljud- och videotillägg installerat, har alternativet ingen effekt.

![image2019-7-22_12-4-23](assets/image2019-7-22_12-4-23.png)

### Om dataelement i tillägget Dynamiska medievisningsprogram {#about-data-elements-in-the-dynamic-media-viewers-extension}

Den enda dataelementtypen som tillägget Dynamic Media-visningsprogram tillhandahåller är **[!UICONTROL Viewer Event]** i listrutan **[!UICONTROL Data Element Type]**.

När du väljer det här alternativet återges ett formulär med två fält i dataelementsredigeraren:

* **[!UICONTROL DM viewers event data type]** – en listruta som identifierar alla visningsprogramhändelser som stöds av tillägget Dynamic Media-visningsprogrammet och som har argument, plus ett särskilt **[!UICONTROL COMMON]**-objekt. Objektet **[!UICONTROL COMMON]** representerar en lista med händelseparametrar som är gemensamma för alla typer av händelser som skickas av visningsprogrammen.
* **[!UICONTROL Tracking parameter]** - ett argument för den valda Dynamic Media Viewer-händelsen.

![image2019-7-22_12-5-46](assets/image2019-7-22_12-5-46.png)

I referenshandboken [för](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/c-html5-s7-aem-asset-viewers.html) dynamiska mediavisare finns en lista över händelser som stöds av varje visningsprogramtyp. Gå till ett specifikt visningsprogramavsnitt och klicka sedan på Support för underavsnittet Adobe Analytics tracking. För närvarande dokumenterar inte referenshandboken för Dynamic Media Viewer händelseargument.

Nu ska vi titta på livscykeln för Dynamic Media Viewer *Data Element*. Värdet för det dataelementet fylls i efter att motsvarande Dynamic Media Viewer-händelse inträffar på sidan. Om dataelementet till exempel pekar på **[!UICONTROL LOAD]** händelsen och dess &quot;asset&quot;-argument, kommer värdet för det dataelementet att få giltiga data när visningsprogrammet kör LOAD-händelsen för första gången. Om dataelementet pekar på **[!UICONTROL ZOOM]** händelsen och dess &quot;scale&quot;-argument, kommer värdet för det dataelementet att vara tomt tills användaren skickar en **[!UICONTROL ZOOM]** händelse för första gången.

På samma sätt uppdateras värdena för dataelement automatiskt när visningsprogrammet skickar en motsvarande händelse på sidan. Värdeuppdateringen sker även om den särskilda händelsen inte har angetts i regelkonfigurationen. Om till exempel dataelementet **[!UICONTROL ZoomScale]** har definierats för parametern ”scale” i ZOOM-händelsen, men den enda regeln som finns i Regelkonfigurationen aktiveras av händelsen **[!UICONTROL LOAD]**, kommer värdet **[!UICONTROL ZoomScale]** ändå att uppdateras varje gång en användare kör zoomning inuti visningsprogrammet.

Alla Dynamic Media-visningsprogram har en unik identifierare på webbsidan. Dataelementet håller reda på själva värdet och det visningsprogram som har fyllt i värdet. Det innebär att om det finns flera visningsprogram på samma sida, och det finns ett **[!UICONTROL AssetName]** dataelement som pekar på händelsen **[!UICONTROL LOAD]** och dess ”asset”-argument, så behåller dataelementet **[!UICONTROL AssetName]** en samling med resursnamn som är associerade med de visningsprogram som är inlästa på sidan.

Det exakta värdet som returneras av dataelementet beror på sammanhanget. Om dataelementet begärs i en regel som utlöstes av en Dynamic Media Viewer-händelse, returneras Data Element-värdet för det visningsprogram som initierade regeln. Och om dataelementet begärs i en regel som utlöstes av en händelse från något annat Adobe Launch-tillägg, är värdet för dataelementet värdet från det visningsprogram som var det sista som uppdaterade det här dataelementet.

**Se följande exempeluppsättning**:

* En webbsida med två zoomningsvisningsprogram för Dynamic Media. vi kallar dem *viewer1* och *viewer2*.

* **[!UICONTROL ZoomScale]** Dataelementet pekar på **[!UICONTROL ZOOM]** händelsen och dess &quot;scale&quot;-argument.
* **[!UICONTROL TrackPan]** Regel med följande:

   * Använder Dynamic Media Viewer- **[!UICONTROL PAN]** händelsen som utlösare.
   * Skickar värdet för **[!UICONTROL ZoomScale]** Data Element till Adobe Analytics.

* 
   * **[!UICONTROL TrackKey]** Regel med följande:

   * Använder knapptryckningshändelsen från Core Adobe Launch-tillägget som utlösare.
   * Skickar värdet för **[!UICONTROL ZoomScale]** Data Element till Adobe Analytics.

Anta nu att slutanvändaren läser in webbsidan med de två visningsprogrammen. I *visningsprogram1* zoomas de in till en skala på 50 %. i *visningsprogrammet2* zoomas de sedan in till 25 % skala. I *visningsprogrammet1* panorerar de bilden och trycker slutligen på en tangent på tangentbordet.

Slutanvändarens aktivitet resulterar i följande två spårningsanrop till Adobe Analytics:

* Det första anropet sker eftersom **[!UICONTROL TrackPan]** regeln aktiveras när användaren panorerar i *visningsprogrammet1*. Anropet skickar 50 % som värde för **[!UICONTROL ZoomScale]** dataelementet eftersom dataelementet vet att regeln aktiveras av *viewer1* och hämtar motsvarande skalvärde.
* Det andra anropet sker eftersom **[!UICONTROL TrackKey]** regeln aktiveras när användaren trycker på en tangent på tangentbordet. Det anropet skickar 25 % som ett värde för **[!UICONTROL ZoomScale]** dataelementet eftersom regeln inte utlöstes av användaren. Därför returnerar dataelementet det senaste värdet.

Samplingsuppsättningen ovan påverkar också dataelementvärdets livslängd. Värdet för dataelementet som hanteras av Dynamic Media Viewer lagras i bibliotekskoden för Adobe Launch även efter att visningsprogrammet har tagits bort från webbsidan. Det innebär att om det finns en regel som aktiveras av ett icke-dynamiskt visningsprogramtillägg och refererar till ett sådant dataelement, returnerar dataelementet det senast kända värdet, även om visningsprogrammet inte längre finns på webbsidan.

Värdena för dataelement som drivs av dynamiska medievyer lagras inte i den lokala lagringen eller på servern. i stället finns de bara i Adobe Launch-biblioteket på klientsidan. Värdena för sådana dataelement försvinner när webbsidan läses in igen.

I allmänhet har dataelementsredigeraren stöd för val av [lagringstid](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/data-elements.html#create-a-data-element). Dataelement som använder tillägget för dynamiska medievisningsprogram har dock bara stöd för alternativet för lagringstid i **[!UICONTROL None]**. Det går att ange andra värden i användargränssnittet, men i det här fallet är dataelementets beteende inte definierat. Tillägget hanterar värdet för dataelementet separat: Data-elementet som behåller värdet för visningsprogrammets händelseargument under hela visningsprogrammets livscykel.

### Regler i tillägget Dynamiska medievyer {#about-rules-in-the-dynamic-media-viewers-extension}

I regelredigeraren lägger tillägget till nya konfigurationsalternativ för händelseredigeraren. I finns också ett alternativ för att manuellt referera till händelseparametrar i Action Editor som ett kortvarigt alternativ i stället för att använda förkonfigurerade dataelement.

#### Om händelseredigeraren {#about-the-events-editor}

I händelseredigeraren lägger tillägget för Dynamic Media-visningsprogrammet till en ny **[!UICONTROL Event Type]** med namnet **[!UICONTROL Viewer Event]**.

När du väljer det här alternativet återges listrutan **[!UICONTROL Dynamic Media Viewer events]** med alla tillgängliga händelser som stöds av visningsprogram för dynamiska media.

![image2019-8-2_15-13-1](assets/image2019-8-2_15-13-1.png)

#### Om funktionsmakroredigeraren {#about-the-actions-editor}

Med tillägget Dynamic Media Viewer kan du använda händelseparametrar för Dynamic Media-visningsprogram för att mappa till analysvariabler i Adobe Analytics-tilläggets Set Variables-redigerare.

Det enklaste sättet att göra detta är att slutföra följande tvåstegsprocess:

* Börja med att definiera ett eller flera dataelement, där varje dataelement representerar en parameter för en Dynamic Media Viewer-händelse.
* I redigeraren Ange variabler för Adobe Analytics-tillägget klickar du slutligen på väljarikonen för dataelement (tre skiktade skivor) för att öppna dialogrutan Markera dataelement och väljer sedan ett dataelement.

![image2019-7-10_20-41-52](assets/image2019-7-10_20-41-52.png)

Det är dock möjligt att använda en alternativ metod och åsidosätta skapande av dataelement. Du kan direkt referera till ett argument från en händelse i Dynamic Media-visningsprogrammet genom att ange det fullständiga, kvalificerade namnet på händelseargumentet i indatafältet **[!UICONTROL value]** för variabeltilldelningen i Analytics, omgivet av procenttecken (%). Till exempel,

`%event.detail.dm.LOAD.asset%`

![image2019-7-12_19-2-35](assets/image2019-7-12_19-2-35.png)

Observera att det finns en viktig skillnad mellan att använda dataelement och argumentreferens för direkt händelse. För dataelement spelar det ingen roll vilken händelse som utlöser åtgärden Ange variabler. Den händelse som utlöser regeln kan vara orelaterad till Dynamic Viewer (som ett musklick på webbsidan från tillägget Core). Men när du använder en referens för ett direkt argument är det viktigt att se till att händelsen som utlöser regeln motsvarar händelseargumentet som den refererar till.

Om du till exempel refererar till `%event.detail.dm.LOAD.asset%` returneras rätt resursnamn om regeln aktiveras av händelsen **[!UICONTROL LOAD]** för tillägget Dynamic Media-visningsprogrammet. Det returnerar dock ett tomt värde för alla andra händelser.

I följande tabell visas Dynamic Media Viewer-händelser och deras argument som stöds:

<table>
 <tbody>
  <tr>
   <td>Namn på visningsprogramhändelse</td>
   <td>Argumentreferens</td>
  </tr>
  <tr>
   <td><code>COMMON</code></td>
   <td><code>%event.detail.dm.objID%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.compClass%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.instName%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.timeStamp%</code></td>
  </tr>
  <tr>
   <td><code>BANNER</code> </td>
   <td><code>%event.detail.dm.BANNER.asset%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.BANNER.frame%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.BANNER.label%</code></td>
  </tr>
  <tr>
   <td><code>HREF</code></td>
   <td><code>%event.detail.dm.HREF.rollover%</code></td>
  </tr>
  <tr>
   <td><code>ITEM</code></td>
   <td><code>%event.detail.dm.ITEM.rollover%</code></td>
  </tr>
  <tr>
   <td><code>LOAD</code></td>
   <td><code>%event.detail.dm.LOAD.applicationname%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.asset%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.company%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.sdkversion%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.viewertype%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.viewerversion%</code></td>
  </tr>
  <tr>
   <td><code>METADATA</code></td>
   <td><code>%event.detail.dm.METADATA.length%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.METADATA.type%</code></td>
  </tr>
  <tr>
   <td><code>MILESTONE</code></td>
   <td><code>%event.detail.dm.MILESTONE.milestone%</code></td>
  </tr>
  <tr>
   <td><code>PAGE</code></td>
   <td><code>%event.detail.dm.PAGE.frame%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.PAGE.label%</code></td>
  </tr>
  <tr>
   <td><code>PAUSE</code></td>
   <td><code>%event.detail.dm.PAUSE.timestamp%</code></td>
  </tr>
  <tr>
   <td><code>PLAY</code></td>
   <td><code>%event.detail.dm.PLAY.timestamp%</code></td>
  </tr>
  <tr>
   <td><code>SPIN</code></td>
   <td><code>%event.detail.dm.SPIN.framenumber%</code></td>
  </tr>
  <tr>
   <td><code>STOP</code></td>
   <td><code>%event.detail.dm.STOP.timestamp%</code></td>
  </tr>
  <tr>
   <td><code>SWAP</code></td>
   <td><code>%event.detail.dm.SWAP.asset%</code></td>
  </tr>
  <tr>
   <td><code>SWATCH</code></td>
   <td><code>%event.detail.dm.SWATCH.frame%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.SWATCH.label%</code></td>
  </tr>
  <tr>
   <td><code>TARG</code></td>
   <td><code>%event.detail.dm.TARG.frame%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.TARG.label%</code></td>
  </tr>
  <tr>
   <td><code>ZOOM</code></td>
   <td><code>%event.detail.dm.ZOOM.scale%</code></td>
  </tr>
 </tbody>
</table>

## Konfigurera alla integreringsdelar {#configuring-all-the-integration-pieces}

**INNAN DU BÖRJAR**

Om du inte redan har gjort det rekommenderar Adobe att du noggrant granskar all dokumentation innan det här avsnittet så att du förstår den fullständiga integreringen.

I det här avsnittet beskrivs de konfigurationssteg som krävs för att integrera dynamiska medievyer med Adobe Analytics och Adobe Analytics för ljud och video. Även om det går att använda tillägget Dynamic Media Viewer för andra syften i Adobe Launch, omfattas sådana scenarier inte av den här dokumentationen.

Du konfigurerar integreringen i följande Adobe-produkter:

* Adobe Analytics - du konfigurerar spårningsvariabler och rapporter.
* Starta Adobe - du definierar en egenskap, en eller flera regler och ett eller flera dataelement för att aktivera spårning av visningsprogram.

Om den här integrationslösningen används med AEM Sites måste dessutom följande konfiguration göras:

* Adobe I/O Console - integrering skapas för Adobe Launch.
* AEM författarnod - IMS-konfiguration och Adobe Launch-molnkonfiguration.

Som en del av konfigurationen bör du kontrollera att du har tillgång till ett företag i Adobe Experience Cloud som redan har Adobe Analytics och Adobe Launch aktiverat.

## Konfigurera Adobe Analytics för integrering {#configuring-adobe-analytics-for-the-integration}

När du har konfigurerat Adobe Analytics kommer följande att konfigureras för integreringen:

* En rapportsvit finns på plats och har valts.
* Analysvariabler är tillgängliga för att ta emot spårningsdata.
* Det finns rapporter för att visa insamlade data i Adobe Analytics.

Se även [implementeringshandboken](https://docs.adobe.com/content/help/en/analytics/implementation/home.html)för analyser.

**Så här konfigurerar du Adobe Analytics för integreringen**:

1. Börja med att gå till Adobe Analytics från Experience Cloud [hemsida](https://exc-home.experiencecloud.adobe.com/exc-home/home.html#/). På menyraden klickar du på ikonen Lösningar (en tabell med tre punkter) i det övre högra hörnet av sidan och sedan på **[!UICONTROL Analytics]**.

   ![2019-07-22_18-08-47](assets/2019-07-22_18-08-47.png)

   Nu ska du välja en rapportserie.

### Välja en rapportsvit {#selecting-a-report-suite}

1. I det övre högra hörnet av Adobe Analytics-sidan, till höger om fältet **[!UICONTROL Search Reports]**, väljer du rätt rapportsvit i listrutan. Om det finns flera rapportsviter och du är osäker på vilken du ska använda kontaktar du Adobe Analytics-administratören, som kan hjälpa dig att välja rätt rapportsvit.

   I bilden nedan skapade en användare en rapportsserie med namnet *DynamicMediaViewersExtensionDoc* och markerade den i listrutan. Rapportsvitens namn är avsett endast som illustration. namnet på den rapportsvit som du väljer skiljer sig åt.

   Om ingen rapportsvit är tillgänglig måste du eller Adobe Analytics-administratören skapa en innan du kan fortsätta med konfigurationen.

   Se [Rapporter och Rapportsviter](https://docs.adobe.com/content/help/en/analytics/implementation/analytics-basics/ref-reports-report-suites.html) och [Skapa en rapportserie](https://docs.adobe.com/content/help/en/analytics/admin/admin-console/create-report-suite.html).

   I Adobe Analytics hanteras rapportsviter under **[!UICONTROL Admin > Report Suites]**.

   ![2019-07-22_18-09-49](assets/2019-07-22_18-09-49.png)

   Nu kommer du att ställa in Adobe Analytics-variabler.

### Konfigurera Adobe Analytics-variabler {#setting-up-adobe-analytics-variables}

1. Du kommer nu att ange en eller flera Adobe Analytics-variabler som du vill använda för att spåra beteendet hos dynamiska mediavisare på webbsidan.

   Det går att använda alla typer av variabler som stöds av Adobe Analytics. Beslutet om variabeltypen (som Custom Traffic [Props], Conversion [eVar]) ska styras av specifika behov i er Analytics-implementering.

   Se [Översikt över utkast och eVars](https://docs.adobe.com/content/help/en/analytics/implementation/analytics-basics/traffic-props-evars/props-evars.html).

   I den här dokumentationen kommer endast en anpassad trafikvariabel (props) att användas eftersom de blir tillgängliga i en analysrapport inom några minuter efter att en åtgärd har utförts på en webbsida.

   Om du vill aktivera en ny anpassad trafikvariabel i Adobe Analytics klickar du på i verktygsfältet **[!UICONTROL Admin > Report Suites]**.

1. Markera rätt rapport på sidan **[!UICONTROL Report Suite Manager]** och klicka sedan på **[!UICONTROL Edit Settings > Traffic > Traffic Variables]** i verktygsfältet.
1. Där hämtar du en variabel som inte används, ger den ett beskrivande namn ( **[!UICONTROL Viewer asset (prop 30)]**) och ändrar kombinationsrutan till &quot;Aktiverad&quot; i kolumnen Aktiverad.

   Följande skärmbild är ett exempel på en anpassad trafikvariabel ( **[!UICONTROL prop30]**) för att spåra ett resursnamn som används av visningsprogrammet:

   ![image2019-6-26_23-6-59](/help/assets/dynamic-media/assets/image2019-6-26_23-6-59.png)

1. Klicka på längst ned i variabellistan **[!UICONTROL Save]**.

### Konfigurera en rapport {#setting-up-a-report}

1. Vanligtvis styrs skapandet av en rapport i Adobe Analytics av specifika projektbehov. Därför ligger detaljerad rapportkonfiguration utanför den här integreringens räckvidd.

   Det räcker dock att känna till att rapporter om anpassad trafik automatiskt blir tillgängliga i Adobe Analytics när du har konfigurerat anpassade trafikvariabler i **[Konfigurera Adobe Analytics-variabler](#setting-up-adobe-analytics-variables)**.

   Till exempel finns rapporten för variabeln **[!UICONTROL Viewer asset (prop 30)]** på menyn Rapporter under **[!UICONTROL Custom Traffic > Custom Traffic 21-30 > Viewer asset (prop 30)]**.

   Inga data visas när du besöker den här rapporten direkt efter att **[!UICONTROL Viewer asset (prop 30)]** har skapats, vilket är som väntat vid den här tidpunkten i integreringen.

   ![image2019-6-26_23-12-49](/help/assets/dynamic-media/assets/image2019-6-26_23-12-49.png)

## Konfigurera Adobe Launch för integrering {#configuring-adobe-launch-for-the-integration}

När du har konfigurerat Adobe Launch kommer följande att konfigureras för integreringen:

* Skapandet av en ny egenskap som håller ihop alla dina konfigurationer.
* Installation och installation av tillägg. Klientkoden för alla tillägg som är installerade i egenskapen kompileras tillsammans till ett bibliotek. Det här biblioteket används av webbsidan senare.
* Konfiguration av dataelement och regler. Den här konfigurationen definierar vilka data som ska hämtas från de dynamiska medievyn, när spårningslogiken ska utlösas och var data ska skickas i Adobe Analytics.
* Publicering av biblioteket.

**Så här konfigurerar du Adobe Launch för integreringen**:

1. Börja med att gå till Adobe Launch från Experience Cloud [hemsida](https://exc-home.experiencecloud.adobe.com/exc-home/home.html#/). På menyraden klickar du på ikonen Lösningar (tre gånger tre punkter) i det övre högra hörnet av sidan och sedan på **[!UICONTROL Launch]**.

   Du kan också [öppna Adobe Launch direkt](https://launch.adobe.com/).

   ![image2019-7-8_15-38-44](assets/image2019-7-8_15-38-44.png)

### Skapa en egenskap i Adobe Launch {#creating-a-property-in-adobe-launch}

En egenskap i Adobe Launch är en namngiven konfiguration som håller ihop alla inställningar. Ett bibliotek med konfigurationsinställningarna genereras och publiceras på olika miljönivåer (utveckling, mellanlagring och produktion).

Se även [Skapa en egenskap](https://docs.adobe.com/content/help/en/launch/using/implement/configure/create-a-property.html).

1. I Adobe Launch klickar du på **[!UICONTROL New Property]**.
1. I dialogrutan **[!UICONTROL Create Property]** anger du ett beskrivande namn, till exempel webbplatsens titel, i fältet **[!UICONTROL Name]**. Till exempel, `DynamicMediaViewersProp.`
1. Ange webbplatsens domän i **[!UICONTROL Domains]** fältet.
1. Aktivera **[!UICONTROL Configure for extension development (cannot be modified later)]** i listrutan **[!UICONTROL Advanced Options]** om det tillägg som du vill använda – i det här fallet *Dynamic Media-visningsprogram* – inte släppts än.

   ![image2019-7-8_16-3-47](assets/image2019-7-8_16-3-47.png)

1. Klicka på **[!UICONTROL Save]**.

   Klicka på den nya egenskapen och fortsätt sedan till *Installation och konfiguration av tillägg*.

### Installera och konfigurera tillägg {#installing-and-setup-of-extensions}

Alla tillgängliga tillägg i Adobe Launch visas under **[!UICONTROL Extensions > Catalog]**.

Klicka på **[!UICONTROL Install]** om du vill installera ett tillägg. Utför vid behov en engångskonfiguration och klicka sedan på **[!UICONTROL Save]**.

Om det behövs måste följande tillägg installeras och konfigureras:

* (Obligatoriskt) *Experience Cloud ID-tjänsttillägg*

Ingen ytterligare konfiguration behövs. Godkänn för föreslagna värden. När du är klar ska du klicka **[!UICONTROL Save]**.

Se [Experience Cloud ID-tjänsttillägg](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/id-service-extension/overview.html).

* (Obligatoriskt) *Adobe Analytics* -tillägg

Om du vill konfigurera det här tillägget behöver du först det rapportsvit-ID som finns i Adobe Analytics, under **[!UICONTROL Admin > Report Suite]** under kolumnrubriken **[!UICONTROL Report Suite ID]**.

(Rapportsvit-ID:t för rapportsviten **[!UICONTROL DynamicMediaViewersExtensionDoc]** används endast i demonstrationssyfte i följande skärmbilder. Detta ID skapades och användes tidigare när du [valde en rapportsvit](#selecting-a-report-suite).)

![image2019-7-8_16-45-34](assets/image2019-7-8_16-45-34.png)

På sidan Installera tillägg anger du rapportsvits-ID:t i fälten **[!UICONTROL Development Report Suites]**, **[!UICONTROL Staging Report Suites]** och **[!UICONTROL Production Report Suites]**.

![image2019-7-8_16-47-40](assets/image2019-7-8_16-47-40.png)

*Konfigurera endast följande objekt om du tänker använda videospårning:*

Expandera på **[!UICONTROL Install Extension]** sidan **[!UICONTROL General]** och ange sedan spårningsservern. Spårningsservern följer mallen `<trackingNamespace>.sc.omtrdc.net`, där `<trackingNamespace>` är informationen som hämtas i e-postmeddelandet om etablering.

Klicka på **[!UICONTROL Save]**.

Se [Adobe Analytics Extension](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/analytics-extension/overview.html).

* (Valfritt. Krävs endast om videospårning behövs) *Adobe Media Analytics för ljud- och videotillägg*

Fyll i spårningsserverfältet. Spårningsservern för *Adobe Media Analytics för ljud och video* skiljer sig från spårningsservern som används för Adobe Analytics. Den följer mallen `<trackingNamespace>.hb.omtrdc.net`där `<trackingNamespace>` är informationen från e-postmeddelandet om etablering.

Alla andra fält är valfria.

Se [Adobe Media Analytics för ljud- och videotillägg](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html).

* (Obligatoriskt) *Dynamic Media Viewers* -tillägg

Välj **[!UICONTROL enable Adobe Analytics for Video]** om du vill aktivera (starta) spårning av pulsslag för video.

Observera att tillägget *Dynamiska medievyer* endast är tillgängligt när du skriver det om Adobe Launch-egenskapen har skapats för utveckling.

Se [Skapa en egenskap i Adobe Launch](#creating-a-property-in-adobe-launch).

När tilläggen har installerats och konfigurerats visas minst följande fem tillägg (fyra om du inte spårar video) under Tillägg > Installerat.

![image2019-7-22_12-7-36](assets/image2019-7-22_12-7-36.png)

### Konfigurera dataelement och regler {#setting-up-data-elements-and-rules}

I Adobe Launch skapar du dataelement och regler som behövs för att spåra Dynamic Media-visningsprogram.

Se [Hur data- och händelsespårning fungerar i integreringen](#how-data-and-event-tracking-works-in-the-integration) för en översikt över spårning med Adobe Launch.

Se [Exempelkonfiguration](#sample-configuration) för en exempelkonfiguration i Adobe Launch som visar hur du spårar ett resursnamn när visningsprogrammet läses in.

Se [Konfigurera tillägget](#configuring-the-dynamic-media-viewers-extension) Dynamic Media Viewer för detaljerad information om tilläggets funktioner.

### Publicera ett bibliotek {#publishing-a-library}

Om du vill göra ändringar i startkonfigurationen för Adobe (inklusive inställningar för egenskaper, tillägg, regler och dataelement) måste du *publicera* sådana ändringar. Publicering i Adobe Launch görs från fliken Publishing under egenskapskonfigurationen.

Adobe Launch kan ha flera utvecklingsmiljöer, en mellanlagringsmiljö och en produktionsmiljö. Som standard pekar konfigurationen för Adobe Launch Cloud i AEM författarnoden till scenmiljön i Adobe Launch och AEM publiceringsnod till produktionsmiljön i Adobe Launch. Detta betyder att med standardinställningarna för AEM måste du publicera Adobe Launch-biblioteket till mellanlagringsmiljön så att du kan använda det i AEM författare och sedan publicera det i produktionsmiljön så att det kan användas i AEM publicering.

Mer information om Adobe Launch-miljöer finns i [Miljöer](https://docs.adobe.com/content/help/en/launch/using/reference/publish/environments.html) .

Publicering av ett bibliotek omfattar följande två steg:

* Lägga till och skapa ett nytt bibliotek genom att inkludera alla nödvändiga ändringar (nya och uppdateringar) i biblioteket.
* Flytta biblioteket uppåt mellan olika miljönivåer (från utveckling till mellanlagring och produktion)

#### Lägga till och skapa ett nytt bibliotek {#adding-and-building-a-new-library}

1. Första gången du öppnar fliken Publicering i Adobe Launch är bibliotekslistan tom.

   Klicka i den vänstra kolumnen **[!UICONTROL Add New Library]**.

   ![image2019-7-15_14-43-17](assets/image2019-7-15_14-43-17.png)

1. På sidan Skapa nytt bibliotek anger du ett beskrivande namn för det nya biblioteket i **[!UICONTROL Name]** fältet. Till exempel,

   *DynamicMediaViewersLib*

   Välj miljönivå i listrutan Miljö. Till att börja med är bara utvecklingsnivån tillgänglig för val. Near the lower-left side of the page, click **[!UICONTROL Add All Changed Resources]**.

   ![image2019-7-15_14-49-41](assets/image2019-7-15_14-49-41.png)

1. Klicka på **[!UICONTROL Save & Build for Development]** i det övre högra hörnet på sidan.

   På några minuter är biblioteket klart att användas.

   ![image2019-7-15_15-3-34](assets/image2019-7-15_15-3-34.png)

   >[!NOTE]
   >
   >Nästa gång du ändrar i Adobe Launch-konfigurationen går du till fliken **[!UICONTROL Publishing]** under konfigurationen **[!UICONTROL Property]** och klickar sedan på det bibliotek du skapade tidigare.
   >
   >
   >På bibliotekets publiceringsskärm klickar du på **[!UICONTROL Add All Changed Resources]** och sedan på **[!UICONTROL Save & Build for Development]**.

#### Flytta ett bibliotek uppåt på miljönivåer {#moving-a-library-up-through-environment-levels}

1. När ett nytt bibliotek har lagts till är det från början placerat i utvecklingsmiljön. Om du vill flytta den till nivån Mellanlagringsmiljö (som motsvarar kolumnen Skickat) går du till bibliotekets nedrullningsbara meny och klickar på **[!UICONTROL Submit for Approval]**.

   ![image2019-7-15_15-52-37](assets/image2019-7-15_15-52-37.png)

1. In the confirmation dialog box, click **[!UICONTROL Submit]**.

   När biblioteket har flyttats till kolumnen Skickat går du till bibliotekets nedrullningsbara meny och klickar på **[!UICONTROL Build for Staging]**.

   ![image2019-7-15_15-54-37](assets/image2019-7-15_15-54-37.png)

1. Följ en liknande process för att flytta biblioteket från mellanlagringsmiljön till produktionsmiljön (kolumnen Publicerad).

   Klicka först på i listrutan **[!UICONTROL Approve for Publishing]**.

   ![image2019-7-15_16-7-39](assets/image2019-7-15_16-7-39.png)

1. Klicka på i listrutan **[!UICONTROL Build & Publish to Production]**.

   ![image2019-7-15_16-8-9](assets/image2019-7-15_16-8-9.png)

   Mer information om publiceringsprocessen i Adobe Launch finns i [Publicering](https://docs.adobe.com/content/help/en/launch/using/reference/publish/overview.html) .

## Konfigurera Adobe Experience Manager för integrering {#configuring-adobe-experience-manager-for-the-integration}

<!-- Prerequisites lost below should be verified by Sasha -->

Förutsättningar:

* AEM kör både Author- och Publish-instanser.
* AEM författarnod är konfigurerad i Dynamic Media. <!-- Scene7 run mode (dynamicmedia_s7) -->
* Dynamic Media WCM-komponenter är aktiverade i AEM Sites.

Den AEM konfigurationen består av följande två huvudsteg:

* Konfiguration av AEM IMS.
* Konfiguration av Adobe Launch Cloud.

### Konfigurera AEM IMS {#configuring-aem-ims}

1. Klicka på ikonen Verktyg (hammer) i AEM författare och klicka sedan på **[!UICONTROL Security > Adobe IMS Configurations]**.

   ![2019-07-25_11-52-58](assets/2019-07-25_11-52-58.png)

1. På konfigurationssidan för Adobe IMC klickar du på **[!UICONTROL Create]**.
1. På sidan **[!UICONTROL Adobe IMS Technical Account Configuration]** går du till listrutan **[!UICONTROL Cloud Solution]** och klickar på **[!UICONTROL Adobe Launch]**.
1. Aktivera **[!UICONTROL Create new certificate]** och ange sedan ett meningsfullt värde för certifikatet i textfältet. Till exempel *AdobeLaunchIMSCert*. Klicka på **[!UICONTROL Create certificate]**.

   Följande informationsmeddelande visas:

   *Om du vill hämta en giltig åtkomsttoken måste det nya certifikatets offentliga nyckel läggas till i det tekniska kontot på Adobe I/O!*.

   Klicka **[!UICONTROL OK]** för att stänga dialogrutan Info.

   ![2019-07-25_12-09-24](assets/2019-07-25_12-09-24.png)

1. Klicka **[!UICONTROL Download Public Key]** för att hämta en fil med en offentlig nyckel (`*.crt`) till ditt lokala system.

   >[!NOTE]
   >
   >Nu: ***låt*** sidan **[!UICONTROL Adobe IMS Technical Account Configuration]** vara öppen; stäng ***inte*** sidan och klicka ***inte*** på Nästa. Du kommer tillbaka till den här sidan längre fram.

   ![2019-07-25_12-52-24](assets/2019-07-25_12-52-24.png)

1. Gå till [Adobe I/O Console](https://console.adobe.io/integrations)på en ny flik i webbläsaren.

1. Klicka på på **[!UICONTROL Adobe I/O Console Integrations]** sidan i det övre högra hörnet **[!UICONTROL New integration]**.
1. I dialogrutan **[!UICONTROL Create a new integration]** kontrollerar du att alternativknappen **[!UICONTROL Access an API]** är markerad och sedan klickar du på **[!UICONTROL Continue]**.

   ![2019-07-25_13-04-20](assets/2019-07-25_13-04-20.png)

1. På den andra **[!UICONTROL Create a new integration]**-sidan aktiverar du (sätter på) alternativknappen **[!UICONTROL Experience Platform Launch API]**. I sidans nedre högra hörn klickar du på **[!UICONTROL Continue]**.

   ![2019-07-25_13-13-54](assets/2019-07-25_13-13-54.png)

1. Gör följande på den tredje **[!UICONTROL Create a new integration]** sidan:

   * Ange ett beskrivande namn i **[!UICONTROL Name]** fältet. Exempel: *DynamicMediaViewersIO*.

   * I **[!UICONTROL Description]** fältet anger du en beskrivning av integreringen.

   * Ladda upp din offentliga nyckelfil ( **[!UICONTROL Public key certificates]** ) som du laddat ned tidigare i dessa steg i`*.crt`området.

   * Välj under **[!UICONTROL Select a role for Experience Platform Launch API]** rubriken **[!UICONTROL Admin]**.

   * Under **[!UICONTROL Select one or more product profiles for Experience Platform Launch API]** rubriken väljer du produktprofilen **[!UICONTROL Launch - <your_company_name>]**.

   ![2019-07-25_13-49-18](assets/2019-07-25_13-49-18.png)

1. Klicka på **[!UICONTROL Create integration]**.
1. På sidan **[!UICONTROL Integration created]** klickar du på **[!UICONTROL Continue to integration details]**.

   ![2019-07-25_14-16-33](assets/2019-07-25_14-16-33.png)

1. En integreringsinformationssida visas, som i följande exempel:

   >[!NOTE]
   >
   >***Låt den här sidan med integreringsinformation vara öppen.*** Du behöver snart olika uppgifter från flikarna **[!UICONTROL Overview]** och **[!UICONTROL JWT]**.

   ![2019-07-25_14-35-30](assets/2019-07-25_14-35-30.png)
   _Sidan med integreringsinformation_

1. Gå tillbaka till sidan **[!UICONTROL Adobe IMS Technical Account Configuration]** som du öppnade tidigare. Klicka på **[!UICONTROL Next]** i det övre högra hörnet av sidan för att öppna sidan **[!UICONTROL Account]** i fönstret **[!UICONTROL Adobe IMS Technical Account Configuration]**.

   (Om du stängde sidan av misstag tidigare går du tillbaka till AEM-redigeraren och klickar sedan på **[!UICONTROL Tools > Security > Adobe IMS Configurations]**. Klicka på **[!UICONTROL Create]**. I listrutan **[!UICONTROL Cloud Solution]** väljer du **[!UICONTROL Adobe Launch]**. I listrutan **[!UICONTROL Certificate]** markerar du namnet på det tidigare skapade certifikatet.

   ![2019-07-25_20-57-50](assets/2019-07-25_20-57-50.png)
   _Adobe IMS Technical Account Configuration - certifikatsida_

1. Sidan innehåller fem fält som du måste fylla i med information från sidan Integreringsinformation från föregående steg. **[!UICONTROL Account]**

   ![2019-07-25_20-42-45](assets/2019-07-25_20-42-45.png)
   _Adobe IMS Technical Account Configuration - kontosida_

1. På **[!UICONTROL Account]** sidan fyller du i följande fält:

   * **[!UICONTROL Title]** - Ange en beskrivande kontotitel.
   * **[!UICONTROL Authorization Server]** - Gå tillbaka till sidan Integreringsinformation som du öppnade tidigare. Click the **[!UICONTROL JWT]** tab. Kopiera servernamnet - utan sökvägen - enligt markeringen nedan.

(exempelservernamnet är endast för illustrationsändamål)   Gå tillbaka till sidan **[!UICONTROL Account]** och klistra sedan in namnet i respektive fält.
Exempelservernamnet `https://ims-na1.adobelogin.com/`(är till exempel endast för illustrationsändamål)

   ![2019-07-25_15-01-53](assets/2019-07-25_15-01-53.png)
   _Detaljsida för integrering - fliken JWT_

1. **[!UICONTROL API Key]** – Gå tillbaka till sidan med integreringsinformation. Klicka på fliken **[!UICONTROL Overview]** och sedan till höger om fältet **[!UICONTROL API Key (Client ID)]** klickar du på **[!UICONTROL Copy]**.

   Gå tillbaka till sidan **[!UICONTROL Account]** och klistra sedan in nyckeln i respektive fält.

   ![2019-07-25_14-35-333](assets/2019-07-25_14-35-333.png)
   _Sidan med integreringsinformation_

1. **[!UICONTROL Client Secret]**– Gå tillbaka till sidan med integreringsinformation. Klicka på **[!UICONTROL Retrieve Client Secret]** på fliken **[!UICONTROL Overview]**. Till höger om fältet **[!UICONTROL Client secret]** klickar du på **[!UICONTROL Copy]**.

   Gå tillbaka till sidan **[!UICONTROL Account]** och klistra sedan in nyckeln i respektive fält.

1. **[!UICONTROL Payload]** – Gå tillbaka till sidan med integreringsinformation. Kopiera hela JSON-objektkoden från fliken JWT-nyttolastfält **[!UICONTROL JWT]** .

   Gå tillbaka till sidan **[!UICONTROL Account]** och klistra sedan in koden i respektive fält.

   ![2019-07-25_21-59-12](assets/2019-07-25_21-59-12.png)
   _Integrationsinformationssida - JWT-flik_

   Kontosidan, med alla fält ifyllda, ser ut ungefär så här:

   ![2019-07-25_22-08-30](assets/2019-07-25_22-08-30.png)

1. Near the upper-right corner of the **[!UICONTROL Account]** page, click **[!UICONTROL Create]**.

   Med AEM IMS konfigurerat har du nu ett nytt IMSAccount som visas under **[!UICONTROL Adobe IMS Configurations]**.

   ![image2019-7-15_14-17-54](assets/image2019-7-15_14-17-54.png)

## Konfigurera Adobe Launch Cloud för integrering {#configuring-adobe-launch-cloud-for-the-integration}

1. I AEM författare klickar du på verktygsikonen (hammaren) i det övre vänstra hörnet och sedan på **[!UICONTROL Cloud Services > Adobe Launch Configurations]**.

   ![2019-07-26_12-10-38](assets/2019-07-26_12-10-38.png)

1. På **[!UICONTROL Adobe Launch Configurations]** sidan i den vänstra panelen väljer du en AEM plats som du vill använda startkonfigurationen för Adobe.

   Endast i illustrationssyfte är **[!UICONTROL We.Retail]** Webbplatsen markerad i skärmbilden nedan.

   ![2019-07-26_12-20-06](assets/2019-07-26_12-20-06.png)

1. Klicka på **[!UICONTROL Create]** i det övre vänstra hörnet av sidan.
1. På sidan **[!UICONTROL General]** (sida 1/3) i fönstret **[!UICONTROL Create Adobe Launch Configuration]** fyller du i följande fält:

   * **[!UICONTROL Title]** - Ange en beskrivande konfigurationstitel. Till exempel, `We.Retail Launch cloud configuration`.

   * **[!UICONTROL Associated Adobe IMS Configuration]** - Välj den IMS-konfiguration som du skapade tidigare i [Konfigurera AEM IMS](#configuring-aem-ims).

   * **[!UICONTROL Company]** - I **[!UICONTROL Company]** listrutan väljer du ditt Experience Cloud-företag. Listan fylls i automatiskt.

   * **[!UICONTROL Property]** - I listrutan Egenskap väljer du Adobe-startegenskapen som du skapade tidigare. Listan fylls i automatiskt.
   När du har fyllt i alla fält ser din **[!UICONTROL General]** sida ut ungefär så här:

   ![image2019-7-15_14-34-23](assets/image2019-7-15_14-34-23.png)

1. Klicka i det övre vänstra hörnet **[!UICONTROL Next]**.
1. På sidan **[!UICONTROL Staging]** (sida 2/3) i fönstret **[!UICONTROL Create Adobe Launch Configuration]** fyller du i följande fält:

   I fältet **[!UICONTROL Library URI]** kontrollerar du var mellanlagringsversionen av ditt Adobe Launch-bibliotek finns. Det här fältet fylls i automatiskt i AEM.

   I det här steget används endast bibliotek för Adobe Launch som distribueras till Adobe CDN.

   >[!NOTE]
   >
   >Kontrollera att den automatiskt ifyllda biblioteks-URI:n (Uniform Resource Identifier) inte har fel format. Om det behövs kan du åtgärda det så att URI:n representerar en protokollrelativ URI. Det vill säga, det börjar med ett dubbelt snedstreck.
   >
   >
   >Till exempel: `//assets.adobetm.com/launch-xxxx`.

   Sidan **[!UICONTROL Staging]** ska se ut ungefär så här: Observera att alternativen **[!UICONTROL Archive]** och **[!UICONTROL Load Library Asynchronously]** ***inte*** har angetts:

   ![image2019-7-15_15-21-8](assets/image2019-7-15_15-21-8.png)

1. Klicka i det övre högra hörnet **[!UICONTROL Next]**.
1. På sidan **[!UICONTROL Production]** (sida 3/3) i fönstret **[!UICONTROL Create Adobe Launch Configuration]** korrigerar du (vid behov) den automatiskt ifyllda produktions-URI:n på samma sätt som på föregående **[!UICONTROL Staging]**-sida.
1. Klicka i det övre högra hörnet **[!UICONTROL Create]**.

   Din nya konfiguration för Adobe Launch Cloud skapas nu och visas bredvid din webbplats.

1. Markera din nya konfiguration för Adobe Launch Cloud (en bock visas till vänster om konfigurationstiteln när den har valts). On the toolbar, click **[!UICONTROL Publish]**.

   ![image2019-7-15_15-47-6](assets/image2019-7-15_15-47-6.png)

För närvarande stöder AEM inte integrering av dynamiska medievyer med Adobe Launch.

Det stöds dock i AEM publiceringsnod. Med standardinställningarna i Adobe Launch Cloud Configuration används produktionsmiljön i Adobe Launch AEM publiceringen. Därför är det nödvändigt att varje gång under testet push-överföra biblioteksuppdateringar för Adobe Launch från Development till produktionsmiljön.

Det går att kringgå den här begränsningen genom att ange utvecklings- eller mellanlagrings-URL för Adobe Launch-biblioteket i Adobe Launch Cloud-konfigurationen för AEM publicering ovan. Detta gör att AEM publiceringsnod använder utvecklingsversionen eller mellanlagringsversionen av Adobe Launch-biblioteket.

Se [Integrera AEM med Adobe Launch via Adobe I/O](https://helpx.adobe.com/experience-manager/using/aem_launch_adobeio_integration.html) för mer information om hur du konfigurerar Adobe Launch Cloud Configuration.