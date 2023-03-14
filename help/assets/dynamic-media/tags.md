---
title: Integrera Dynamic Media-visningsprogram med taggar från Adobe Analytics och Experience Platform
description: Läs mer om Dynamic Media Viewer-tillägget för Experience Platform Tags och Dynamic Media Viewer 5.13. Det gör att kunder som använder Adobe Analytics- och plattformstaggar kan använda händelser och data som är specifika för Dynamic Media-visningsprogram i sina taggar för Experience Platform.
contentOwner: Rick Brough
feature: Asset Reports
role: Admin,User
exl-id: a71fef45-c9a4-4091-8af1-c3c173324b7a
source-git-commit: b37ff72dbcf85e5558eb3421b5168dc48e063b47
workflow-type: tm+mt
source-wordcount: '6287'
ht-degree: 8%

---

# Integrera Dynamic Media-visningsprogram med taggar från Adobe Analytics och Experience Platform {#integrating-dynamic-media-viewers-with-adobe-analytics-and-adobe-launch}

## Vad är Dynamic Media Viewer integrerat med Adobe Analytics och Experience Platform Tags? {#what-is-dynamic-media-viewers-integration-with-adobe-analytics-and-adobe-launch}

<!-- Leave this hidden path here; it points to the topic source from Sasha https://wiki.corp.adobe.com/pages/viewpage.action?spaceKey=~oufimtse&title=Dynamic+Media+Viewers+integration+with+Adobe+Launch 

name used to be Experience Platform Launch. Changed to Experience Platform Data Collection-->

*Dynamic Media Viewers* för Experience Platform Tags och Dynamic Media Viewer 5.13, så att Adobe Analytics- och Experience Platform Tags-kunder kan använda händelser och data som är specifika för Dynamic Media Viewer i sina Experience Platform Tags-konfigurationer.

Integrationen innebär att du kan spåra användningen av Dynamic Media Viewer på din webbplats med Adobe Analytics. Samtidigt kan du använda händelser och data som visas av visningsprogrammen med andra Experience Platform-taggar-tillägg som kommer från Adobe eller en tredje part.

Mer information om Adobe-tillägg och tredjepartstillägg finns i [Adobe-tillägg](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/overview.html) i användarhandboken för Experience Platform Tags.

**Detta avsnitt är avsett för följande:** Webbplatsadministratörer, utvecklare av Adobe Experience Manager samt användare i Operations.

### Begränsningar i integreringen {#limitations-of-the-integration}

* Integrering med Experience Platform-taggar för Dynamic Media-visningsprogram fungerar inte i noden Experience Manager författare. Du kan inte se någon spårning från en WCM-sida förrän den har publicerats.
* Integrering med Experience Platform-taggar för Dynamic Media-visningsprogram stöds inte för åtgärdsläget&quot;popup&quot;, där visningsprogrammets URL hämtas med knappen&quot;URL&quot; på sidan Resursinformation.
* Integrering med Experience Platform-taggar kan inte användas samtidigt med integrering med äldre visningsprogram Analytics (via `config2=` parameter).
* Stödet för videospårning är begränsat till enbart huvudspårning av uppspelning, vilket beskrivs i [Spårningsöversikt](https://experienceleague.adobe.com/docs/media-analytics/using/tracking/track-av-playback/track-core-overview.html?lang=en#player-events). Speciellt stöds inte QoS, Ads, Chapter/Segments eller Errors tracking.
* Konfiguration av lagringstid för dataelement stöds inte för dataelement som använder *Dynamic Media Viewers* tillägg. Lagringsvaraktighet måste anges till **[!UICONTROL None]**.

### Användningsexempel för integreringen {#use-cases-for-the-integration}

Det viktigaste användningsområdet för integrering med Experience Platform Tags är kunder som använder både Experience Manager Assets och Experience Manager Sites. I så fall kan du konfigurera en standardintegrering mellan författarnoden i Experience Manager och Experience Platform-taggar och sedan associera platsinstansen med egenskapen Experience Platform-taggar. Efter det kommer alla Dynamic Media WCM-komponenter som läggs till på en Sites-sida att spåra data och händelser från tittarna.

Se [Spåra Dynamic Media-visningsprogram i Experience Manager Sites](#tracking-dynamic-media-viewers-in-aem-sites).

Ett sekundärt användningsfall som integreringen stöder är de kunder som bara använder Experience Manager Assets eller Dynamic Media Classic. I så fall får du inbäddningskoden för ditt visningsprogram och lägger till den på webbplatssidan. Hämta sedan URL:en för Experience Platform Tags-bibliotekets produktion från Experience Platform Tags och lägg till den manuellt i webbsideskoden.

Se [Spåra Dynamic Media-visningsprogram med hjälp av inbäddningskod](#tracking-dynamic-media-viewers-using-embed-code).

## Hur data- och händelsespårning fungerar i integreringen {#how-data-and-event-tracking-works-in-the-integration}

Integreringen utnyttjar två separata och oberoende typer av spårning av Dynamic Media Viewers: *Adobe Analytics* och *Adobe Analytics för ljud och video*.

### Om spårning med Adobe Analytics  {#about-tracking-using-adobe-analytics}

Med Adobe Analytics kan du spåra åtgärder som slutanvändaren utför när de interagerar med Dynamic Media-visningsprogram på webbplatsen. Med Adobe Analytics kan du också spåra visningsprogramspecifika data. Du kan till exempel spåra och spela in inläsningshändelser tillsammans med resursnamnet, eventuella zoomåtgärder som har utförts och videouppspelningsåtgärder.

I Experience Platform-taggar är det *Dataelement* och *Regler* samarbeta för att möjliggöra Adobe Analytics-spårning.

#### Om dataelement i Experience Platform-taggar {#about-data-elements-in-adobe-launch}

Ett dataelement i Experience Platform-taggar är en namngiven egenskap vars värde antingen är statiskt definierat eller dynamiskt beräknat baserat på webbsidans eller Dynamic Media Viewer-datas tillstånd.

Vilka alternativ som är tillgängliga för en dataelementsdefinition beror på listan med tillägg som är installerade i Experience Platform-taggegenskapen. Tillägget &quot;Core&quot; är förinstallerat och finns tillgängligt direkt i alla konfigurationer. Med det här tillägget Core kan du definiera ett dataelement som kommer från cookie, JavaScript-kod, frågesträng och många andra källor.

För Adobe Analytics tracking måste flera andra tillägg installeras, vilket beskrivs i [Installation och installation av tillägg](#installing-and-setup-of-extensions). Tillägget Dynamic Media Viewer ger möjlighet att definiera ett dataelement som är ett argument i Dynamic Viewer-händelsen. Det är till exempel möjligt att referera till visningsprogramtypen, eller resursnamnet som rapporteras av visningsprogrammet vid inläsning, den zoomnivå som rapporteras när slutanvändaren zoomar och mycket annat.

Dynamic Media Viewer-tillägget håller automatiskt värdena för dataelementen uppdaterade.

När du har definierat det kan ett dataelement användas på andra platser i användargränssnittet för Experience Platform-taggar med hjälp av widgeten för dataelementväljaren. Dataelement som definieras för spårning av Dynamic Media-visningsprogram refereras särskilt av tillägget Ange variabelåtgärd för Adobe Analytics (se nedan).

Se [Dataelement](https://experienceleague.adobe.com/docs/experience-platform/tags/ui/data-elements.html) i användarhandboken för Experience Platform Tags.

#### Om regler i Experience Platform-taggar {#about-rules-in-adobe-launch}

En regel i Experience Platform-taggar är en agnostisk konfiguration som definierar tre områden som utgör en regel: *Händelser*, *Villkor* och *Åtgärder*:

* *Händelser* (if) ange för Experience Platform taggar när en regel ska utlösas.
* *Villkor* (if) ange för Experience Platform Taggar vilka andra begränsningar som ska tillåtas eller inte när en regel aktiveras.
* *Åtgärder* (sedan) ange för Experience Platform-taggar vad som ska göras när en regel aktiveras.

Vilka alternativ som är tillgängliga i avsnittet Händelser, Villkor och Åtgärder beror på vilka tillägg som är installerade i Experience Platform Tags Property. The *Core* tillägget är förinstallerat och är tillgängligt direkt i valfri konfiguration. Tillägget innehåller flera alternativ för Händelser, t.ex. grundläggande åtgärder på webbläsarnivå som inkluderar fokusändringar, tangenttryckningar och formulärskickningar. Den innehåller även alternativ för Villkor, som cookie-värde, webbläsartyp och mycket annat. För Åtgärder är endast alternativet Anpassad kod tillgängligt.

För Adobe Analytics tracking måste flera andra tillägg installeras, vilket beskrivs i [Installation och installation av tillägg](#installing-and-setup-of-extensions). Särskilt:

* Tillägget Dynamic Media Viewer utökar listan med händelser som stöds till händelser som är specifika för Dynamic Media-visningsprogram, t.ex. visning, byte av resurser, inzoomning och videouppspelning.
* Adobe Analytics-tillägget utökar listan över åtgärder som stöds med två åtgärder som krävs för att skicka data till spårningsservrar: *Ange variabler* och *Skicka Beacon*.

Om du vill spåra Dynamic Media-visningsprogram kan du använda någon av följande typer:

* Händelser från Dynamic Media Viewer-tillägget, Core-tillägget eller andra tillägg.
* Villkor i regeldefinitionen. Du kan också lämna villkorsområdet tomt.

I avsnittet Åtgärder måste du ha en *Ange variabler* åtgärd. Den här åtgärden anger för Adobe Analytics hur spårningsvariabler ska fyllas i med data. Samtidigt är *Ange variabler* skickar ingenting till spårningsservern.

The *Ange variabler* måste följas av en *Skicka Beacon* åtgärd. The *Skicka Beacon* skickar data till analysspårningsservern. Båda åtgärderna, *Ange variabler* och *Skicka Beacon*, kommer från Adobe Analytics-tillägget.

Se [Regler](https://experienceleague.adobe.com/docs/experience-platform/tags/ui/rules.html) i användarhandboken för Experience Platform Tags.

#### Exempelkonfiguration {#sample-configuration}

I följande exempelkonfiguration i Experience Platform Tags visas hur du spårar ett resursnamn när visningsprogrammet läses in.

1. Från **[!UICONTROL Data Elements]** -flik, definiera ett dataelement `AssetName` som refererar `asset` parametern för `LOAD` -händelse från Dynamic Media Viewer-tillägget.

   ![image2019-11](assets/image2019-11.png)

1. Från **[!UICONTROL Rules]** -flik, definiera en regel *TrackAssetOnLoad*.

   I den här regeln **[!UICONTROL Event]** fältet använder **[!UICONTROL LOAD]** -händelse från Dynamic Media Viewer-tillägget.

   ![image2019-22](assets/image2019-22.png)

1. Åtgärdskonfigurationen har två åtgärdstyper från Adobe Analytics-tillägget:

   *Ange variabler* som mappar en analysvariabel till värdet av `AssetName` Dataelement.

   *Skicka Beacon*, som skickar spårningsinformation till Adobe Analytics.

   ![image2019-3](assets/image2019-3.png)

1. Den resulterande regelkonfigurationen ser ut så här:

   ![image2019-4](assets/image2019-4.png)

### Om Adobe Analytics för ljud och video {#about-adobe-analytics-for-audio-and-video}

När ett Experience Cloud-konto prenumererar på Adobe Analytics för ljud och video räcker det för att aktivera videospårning i *Dynamic Media Viewers* tilläggsinställningar. Videomått blir tillgängligt i Adobe Analytics. Videospårning beror på om det finns Adobe Media Analytics för ljud- och videotillägg.

Se [Installation och installation av tillägg](#installing-and-setup-of-extensions).

Stödet för videospårning är för närvarande begränsat till&quot;core playback&quot;-spårning, vilket beskrivs i [Spårningsöversikt](https://experienceleague.adobe.com/docs/media-analytics/using/tracking/track-av-playback/track-core-overview.html?lang=en#player-events). Speciellt stöds inte QoS, Ads, Chapter/Segments eller Errors tracking.

## Använda tillägget Dynamic Media Viewer {#using-the-dynamic-media-viewers-extension}

Som anges i [Användningsexempel för integreringen](#use-cases-for-the-integration)går det att spåra Dynamic Media-visningsprogram med den nya Experience Platform-taggintegreringen i Experience Manager Sites och med hjälp av inbäddningskod.

### Spåra Dynamic Media-visningsprogram i Experience Manager Sites {#tracking-dynamic-media-viewers-in-aem-sites}

Om du vill spåra Dynamic Media-visningsprogram i Experience Manager Sites följer du alla steg som anges under [Konfigurera alla integreringsdelar](#configuring-all-the-integration-pieces) -avsnittet måste utföras. Du måste skapa IMS-konfigurationen och molnkonfigurationen för Experience Platform Tags.

När konfigurationen är korrekt spåras data automatiskt i Adobe Analytics, Adobe Analytics for Video eller båda när du lägger till ett visningsprogram från Dynamic Media på en webbplats med en WCM-komponent som stöds av Dynamic Media.

Se [Lägga till Dynamic Media-resurser på sidor med Adobe Sites](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

### Spåra Dynamic Media-visningsprogram med hjälp av inbäddningskod {#tracking-dynamic-media-viewers-using-embed-code}

Kunder som inte använder Experience Manager Sites, eller bäddar in Dynamic Media-visningsprogram på webbsidor utanför Experience Manager Sites, eller båda, kan fortfarande använda integreringen med Experience Platform-taggar.

Slutför konfigurationsstegen från [Konfigurera Adobe Analytics](#configuring-adobe-analytics-for-the-integration) och [Konfigurera Experience Platform-taggar](#configuring-adobe-launch-for-the-integration) -avsnitt. Konfigurationssteg som rör Experience Manager behövs dock inte.

Om konfigurationen är korrekt kan du lägga till stöd för Experience Platform-taggar på en webbsida med ett Dynamic Media-visningsprogram.

Se [Lägg till inbäddad kod för Experience Platform-taggar](https://experienceleague.adobe.com/docs/platform-learn/implement-in-websites/configure-tags/add-embed-code.html) om du vill veta mer om hur du använder inbäddningskod för Experience Platform Tags-bibliotek.

Mer information om hur du använder funktionen för inbäddning i Experience Manager Dynamic Media finns i [Bädda in video- eller bildvisningsprogrammet på en webbsida](/help/assets/dynamic-media/embed-code.md).

**Spåra Dynamic Media-visningsprogram med hjälp av inbäddningskod:**

1. Ha en webbsida redo för inbäddning av ett Dynamic Media-visningsprogram.
1. Hämta inbäddningskoden för Experience Platform Tags-biblioteket genom att först logga in på Experience Platform Taggar (se [Konfigurera Experience Platform-taggar](#configuring-adobe-launch-for-the-integration)).
1. Välj **[!UICONTROL Property]** väljer du **[!UICONTROL Environments]** -fliken.
1. Plocka upp den miljönivå som är relevant för webbsidans miljö. Sedan i **[!UICONTROL Install]** markerar du ruteikonen.
1. **[!UICONTROL In the Web Install Instructions]** kopierar den fullständiga inbäddningskoden för Experience Platform-taggbiblioteket tillsammans med den omgivande `<script/>` -taggar.

## Referenshandbok för tillägget Dynamic Media Viewers {#reference-guide-for-the-dynamic-media-viewers-extension}

### Om konfigurationen för Dynamic Media Viewer {#about-the-dynamic-media-viewers-configuration}

Tillägget Dynamic Media Viewer integreras automatiskt med Experience Platform-taggbiblioteket om följande villkor är uppfyllda:

* globalt objekt för Experience Platform Taggar-biblioteket ( `_satellite`) finns på sidan.
* Tilläggsfunktionen Dynamic Media Viewer `_dmviewers_v001()` är definierad på `_satellite`.

* `config2=` Ingen visningsprogramparameter har angetts, vilket innebär att visningsprogrammet inte använder äldre Analytics-integrering.

Det finns också ett alternativ för att uttryckligen inaktivera integreringen av Experience Platform-taggar i visningsprogrammet genom att ange `launch=0` i visningsprogrammets konfiguration. Standardvärdet för den här parametern är `1`.

### Konfigurera tillägget Dynamic Media Viewer {#configuring-the-dynamic-media-viewers-extension}

Det enda konfigurationsalternativet för tillägget Dynamic Media Viewer är **[!UICONTROL Enable Adobe Media Analytics for Audio and Video]**.

När du markerar (aktiverar) det här alternativet och Adobe Media Analytics för ljud och video har installerats och konfigurerats skickas videouppspelningsstatistik till Adobe Analytics för ljud och video. Om du inaktiverar det här alternativet inaktiveras videospårning.

Om du aktiverar det här alternativet *utan* om du har installerat Adobe Media Analytics for Audio och Video har alternativet ingen effekt.

![image2019-7-22_12-4-23](assets/image2019-7-22_12-4-23.png)

### Om dataelement i Dynamic Media Viewer-tillägget {#about-data-elements-in-the-dynamic-media-viewers-extension}

Den enda dataelementtypen som tillägget Dynamic Media-visningsprogram tillhandahåller är **[!UICONTROL Viewer Event]** i listrutan **[!UICONTROL Data Element Type]**.

När du väljer det här alternativet återges ett formulär med två fält i dataelementsredigeraren:

* **[!UICONTROL DM viewers event data type]** – en listruta som identifierar alla visningsprogramhändelser som stöds av tillägget Dynamic Media-visningsprogrammet och som har argument, plus ett särskilt **[!UICONTROL COMMON]**-objekt. Objektet **[!UICONTROL COMMON]** representerar en lista med händelseparametrar som är gemensamma för alla typer av händelser som skickas av visningsprogrammen.
* **[!UICONTROL Tracking parameter]** - ett argument för den valda Dynamic Media Viewer-händelsen.

![image2019-7-22_12-5-46](assets/image2019-7-22_12-5-46.png)

Se [Referenshandbok för Dynamic Media Viewer](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/c-html5-s7-aem-asset-viewers.html) En förteckning över händelser som stöds av varje visningsprogramtyp. Gå till ett specifikt visningsprogramavsnitt och välj sedan Support för underavsnittet Adobe Analytics tracking. Referenshandboken för Dynamic Media Viewer dokumenterar för närvarande inte händelseargument.

Nu ska vi titta på Dynamic Media Viewer *Dataelement*. Värdet för det dataelementet fylls i efter att motsvarande Dynamic Media-visningsprogramhändelse inträffar på sidan. Anta att dataelementet pekar på **[!UICONTROL LOAD]** -händelsen och dess &quot;asset&quot;-argument. Värdet för det dataelementet tar emot giltiga data när visningsprogrammet kör LOAD-händelsen för första gången. Om dataelementet pekar på **[!UICONTROL ZOOM]** -händelsen och dess &quot;scale&quot;-argument, förblir värdet för dataelementet tomt tills användaren skickar en **[!UICONTROL ZOOM]** -händelse för första gången.

På samma sätt uppdateras värdena för dataelement automatiskt när visningsprogrammet skickar en motsvarande händelse på sidan. Värdeuppdateringen sker även om den särskilda händelsen inte har angetts i regelkonfigurationen. Anta t.ex. dataelement **[!UICONTROL ZoomScale]** definieras för parametern &quot;scale&quot; i ZOOM-händelsen. Den enda regel som finns i regelkonfigurationen aktiveras emellertid av **[!UICONTROL LOAD]** -händelse. Värdet för **[!UICONTROL ZoomScale]** uppdateras fortfarande varje gång en användare zoomar in i visningsprogrammet.

Alla Dynamic Media-visningsprogram har en unik identifierare på webbsidan. Dataelementet spårar själva värdet och det visningsprogram som har fyllt i värdet. Anta till exempel att det finns flera visningsprogram på samma sida, och en **[!UICONTROL AssetName]** Dataelement som pekar på **[!UICONTROL LOAD]** -händelsen och dess &quot;asset&quot;-argument. The **[!UICONTROL AssetName]** Data Element underhåller en samling resursnamn som är associerade med varje visningsprogram som läses in på sidan.

Det exakta värdet som returneras av dataelementet beror på sammanhanget. Om dataelementet begärs i en regel som utlöstes av en Dynamic Media-visningshändelse, returneras dataelementvärdet för det visningsprogram som initierade regeln. Dataelementet begärs dessutom i en regel som utlöstes av en händelse från ett annat tillägg för Experience Platform-taggar. I det skedet kommer dataelementets värde från det visningsprogram som senast uppdaterade det här dataelementet.

**Tänk på följande exempelinställningar:**

* En webbsida med två zoomningsvisningsprogram från Dynamic Media: *viewer1* och *visningsprogram2*.

* **[!UICONTROL ZoomScale]** Dataelementet pekar på **[!UICONTROL ZOOM]** -händelsen och dess &quot;scale&quot;-argument.
* **[!UICONTROL TrackPan]** Regel med följande:

   * Använder Dynamic Media Viewer **[!UICONTROL PAN]** -händelse som utlösare.
   * Skickar värdet för **[!UICONTROL ZoomScale]** Dataelement till Adobe Analytics.

* **[!UICONTROL TrackKey]** Regel med följande:

   * Använder tangenttryckningshändelsen från Core Experience Platform Tags-tillägget som utlösare.
   * Skickar värdet för **[!UICONTROL ZoomScale]** Dataelement till Adobe Analytics.

Anta nu att slutanvändaren läser in webbsidan med de två visningsprogrammen. I *viewer1* zoomar de in till 50 %. sedan *visningsprogram2* zoomar de in till 25 %. I *viewer1* panorerar de runt bilden och trycker slutligen på en tangent på tangentbordet.

Slutanvändarens aktivitet resulterar i följande två spårningsanrop till Adobe Analytics:

* Det första anropet sker eftersom **[!UICONTROL TrackPan]** Regeln aktiveras när användaren panorerar *viewer1*. Det anropet skickar 50 % som ett värde av **[!UICONTROL ZoomScale]** Dataelement eftersom dataelementet vet att regeln aktiveras av *viewer1* och hämtar motsvarande skalvärde,
* Det andra anropet sker eftersom **[!UICONTROL TrackKey]** Regeln aktiveras när användaren trycker på en tangent på tangentbordet. Det anropet skickar 25 % som ett värde av **[!UICONTROL ZoomScale]** Dataelement eftersom regeln inte utlöstes av användaren. Därför returnerar dataelementet det senaste värdet.

Samplingsuppsättningen ovan påverkar också dataelementvärdets livslängd. Värdet på dataelementet som hanteras av Dynamic Media Viewer lagras i bibliotekskoden för Experience Platform-taggar även efter att visningsprogrammet har tagits bort från webbsidan. Den här funktionen innebär att om det finns en regel som aktiveras av ett icke-Dynamic Media Viewer-tillägg och refererar till ett sådant dataelement, returnerar dataelementet det senast kända värdet. Även om visningsprogrammet inte längre finns på webbsidan.

Värdena för dataelement som drivs av Dynamic Media-visningsprogram lagras inte i den lokala lagringen eller på servern. i stället lagras de bara i Experience Platform-taggbiblioteket på klientsidan. Värdena för sådana dataelement försvinner när webbsidan läses in igen.

I allmänhet har dataelementsredigeraren stöd för [val av lagringstid](https://experienceleague.adobe.com/docs/experience-platform/tags/ui/data-elements.html#create-a-data-element). Dataelement som använder tillägget Dynamic Media Viewer har dock bara stöd för alternativet för lagringstid på **[!UICONTROL None]**. Det går att ange andra värden i användargränssnittet, men i det här fallet är dataelementets beteende inte definierat. Tillägget hanterar värdet för dataelementet separat: Data-elementet som behåller värdet för visningsprogrammets händelseargument under hela visningsprogrammets livscykel.

### Om regler i tillägget Dynamic Media Viewer {#about-rules-in-the-dynamic-media-viewers-extension}

I regelredigeraren lägger tillägget till nya konfigurationsalternativ för händelseredigeraren. Redigeraren har också ett alternativ för att manuellt referera till händelseparametrar i redigeraren som ett kortvarigt alternativ i stället för att använda förkonfigurerade dataelement.

#### Om händelseredigeraren {#about-the-events-editor}

I händelseredigeraren lägger tillägget Dynamic Media Viewer till ett **[!UICONTROL Event Type]** anropad **[!UICONTROL Viewer Event]**.

När det här alternativet är markerat återges listrutan av händelseredigeraren **[!UICONTROL Dynamic Media Viewer events]**, med en lista över alla tillgängliga händelser som stöds av visningsprogram i Dynamic Media.

![image2019-8-2_15-13-1](assets/image2019-8-2_15-13-1.png)

#### Om funktionsmakroredigeraren {#about-the-actions-editor}

Med Dynamic Media Viewer-tillägget kan du använda händelseparametrar för Dynamic Media-visningsprogram för att mappa till analysvariabler i Adobe Analytics-tilläggets Set Variables-redigerare.

Det enklaste sättet att göra detta är att slutföra följande tvåstegsprocess:

* Börja med att definiera ett eller flera dataelement, där varje dataelement representerar en parameter för en Dynamic Media Viewer-händelse.
* I redigeraren Ange variabler för Adobe Analytics-tillägget markerar du väljarikonen för dataelement (tre skiktade skivor) för att öppna dialogrutan Markera dataelement och väljer sedan ett dataelement.

![image2019-7-10_20-41-52](assets/image2019-7-10_20-41-52.png)

Det är dock möjligt att använda en alternativ metod och åsidosätta skapande av dataelement. Du kan referera direkt till ett argument från en Dynamic Media Viewer-händelse. Ange det fullständiga namnet på händelseargumentet i **[!UICONTROL value]** indatafält för variabeltilldelningen i Analytics. Försäkra dig om att du omger med procenttecken (%). Till exempel,

`%event.detail.dm.LOAD.asset%`

![image2019-7-12_19-2-35](assets/image2019-7-12_19-2-35.png)

Det finns en viktig skillnad mellan att använda dataelement och argumentreferens för direkt händelse. För dataelement spelar det ingen roll vilken händelse som utlöser åtgärden Ange variabler. Händelsen som utlöser regeln kan vara orelaterad till Dynamic Viewer (som att välja webbsidan från Core-tillägget). Men när du använder en referens för ett direkt argument är det viktigt att se till att händelsen som utlöser regeln motsvarar händelseargumentet som den refererar till.

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

Adobe rekommenderar att du granskar all dokumentation innan det här avsnittet så att du förstår den fullständiga integreringen.

I det här avsnittet beskrivs de konfigurationssteg som krävs för att integrera Dynamic Media-visningsprogram med Adobe Analytics och Adobe Analytics för ljud och video. Även om det går att använda Dynamic Media Viewer-tillägget för andra syften i Experience Platform-taggar, omfattas sådana scenarier inte av den här dokumentationen.

Du kommer att använda följande Adobe-produkter för att konfigurera din integrering:

* Adobe Analytics - används för att konfigurera spårningsvariabler och rapporter.
* Experience Platform-taggar - används för att definiera en egenskap, en eller flera regler och ett eller flera dataelement för att aktivera spårning av visningsprogram.

Om integrationslösningen används med Experience Manager Sites måste dessutom följande konfiguration göras:

* [Adobe Developer Console](https://developer.adobe.com/console/home) - integrering skapas för Experience Platform-taggar.
* Nod för författare i Experience Manager - IMS-konfiguration och molnkonfiguration för Experience Platform Tags.

Som en del av konfigurationen bör du kontrollera att du har tillgång till ett företag i Adobe Experience Cloud som redan har Adobe Analytics- och Experience Platform-taggar aktiverade.

## Konfigurera Adobe Analytics för integreringen {#configuring-adobe-analytics-for-the-integration}

När du har konfigurerat Adobe Analytics kommer följande att konfigureras för integreringen:

* En rapportsvit finns på plats och har valts.
* Analysvariabler är tillgängliga för att ta emot spårningsdata.
* Det finns rapporter för att visa insamlade data i Adobe Analytics.

Se även [Implementeringshandbok för analyser](https://experienceleague.adobe.com/docs/analytics/implementation/home.html).

**Så här konfigurerar du Adobe Analytics för integreringen:**

1. Börja med att gå till Adobe Analytics från Experience Cloud [hemsida](https://experience.adobe.com/#/home). På menyraden väljer du ikonen Lösningar (en tabell med tre punkter) i det övre högra hörnet av sidan och sedan väljer du **[!UICONTROL Analytics]**.

   ![2019-07-22_18-08-47](assets/2019-07-22_18-08-47.png)

   Välj en rapportsvit.

### Välj en rapportsvit {#selecting-a-report-suite}

1. I det övre högra hörnet av Adobe Analytics-sidan, till höger om fältet **[!UICONTROL Search Reports]**, väljer du rätt rapportsvit i listrutan. Om det finns flera rapportsviter och du är osäker på vilken du ska använda kontaktar du Adobe Analytics-administratören, som kan hjälpa dig att välja rätt rapportsvit.

   I exemplet nedan har en användare skapat en rapportserie med namnet *DynamicMediaViewersExtensionDoc* och markerade det i listrutan. Rapportsvitens namn är endast ett exempel. Namnet på den rapportsvit du väljer är upp till dig.

   Om ingen rapportsvit är tillgänglig måste du eller Adobe Analytics-administratören skapa en innan du kan fortsätta med konfigurationen.

   Se [Rapporter och rapportsviter](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/report-suites-admin.html) och [Skapa en rapportsvit](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/c-new-report-suite/t-create-a-report-suite.html).

   I Adobe Analytics hanteras rapportsviter under **[!UICONTROL Admin]** > **[!UICONTROL Report Suites]**.

   ![2019-07-22_18-09-49](assets/2019-07-22_18-09-49.png)

   Konfigurera Adobe Analytics-variabler.

### Ställa in Adobe Analytics-variabler {#setting-up-adobe-analytics-variables}

1. Ange en eller flera Adobe Analytics-variabler som du vill använda för att spåra Dynamic Media Viewer-beteendet på webbsidan.

   Det går att använda alla typer av variabler som stöds av Adobe Analytics. Beslutet om variabeltypen (som anpassad trafik) [proppar], konvertering [eVar]) styrs av specifika behov i er Analytics-implementering.

   Se [Översikt över utkast och eVars](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar.html#vars).

   I den här dokumentationen kommer endast en anpassad trafikvariabel (props) att användas eftersom de blir tillgängliga i en analysrapport inom några minuter efter att en åtgärd har utförts på en webbsida.

   Om du vill aktivera en ny anpassad trafikvariabel går du till Adobe Analytics i verktygsfältet på **[!UICONTROL Admin]** > **[!UICONTROL Report Suites]**.

1. På **[!UICONTROL Report Suite Manager]** väljer du rätt rapport och går till verktygsfältet **[!UICONTROL Edit Settings]** > **[!UICONTROL Traffic]** > **[!UICONTROL Traffic Variables]**.
1. Välj en oanvänd variabel, ge den ett beskrivande namn ( **[!UICONTROL Viewer asset (prop 30)]**) och ändra sedan kombinationsrutan till &quot;Aktiverad&quot; i kolumnen Aktiverad.

   Följande skärmbild är ett exempel på en anpassad trafikvariabel ( **[!UICONTROL prop30]**) för att spåra ett resursnamn som används av visningsprogrammet:

   ![image2019-6-26_23-6-59](/help/assets/dynamic-media/assets/image2019-6-26_23-6-59.png)

1. Längst ned i variabellistan väljer du **[!UICONTROL Save]**.

### Konfigurera en rapport {#setting-up-a-report}

1. Vanligtvis styrs skapandet av en rapport i Adobe Analytics av specifika projektbehov. Därför ligger detaljerad rapportkonfiguration utanför den här integreringens räckvidd.

   Det räcker dock att veta att rapporterna om anpassad trafik automatiskt blir tillgängliga i Adobe Analytics när du har konfigurerat anpassade trafikvariabler i **[Konfigurera Adobe Analytics-variabler](#setting-up-adobe-analytics-variables)**.

   Till exempel finns rapporten för variabeln **[!UICONTROL Viewer asset (prop 30)]** på menyn Rapporter under **[!UICONTROL Custom Traffic]** > **[!UICONTROL Custom Traffic 21-30]** > **[!UICONTROL Viewer asset (prop 30)]**.

   Inga data visas när du besöker den här rapporten direkt efter att **[!UICONTROL Viewer asset (prop 30)]** har skapats, vilket är som väntat vid den här tidpunkten i integreringen.

   ![image2019-6-26_23-12-49](/help/assets/dynamic-media/assets/image2019-6-26_23-12-49.png)

## Konfigurera Experience Platform-taggar för integreringen {#configuring-adobe-launch-for-the-integration}

När du har konfigurerat Experience Platform-taggar kommer följande att konfigureras för integreringen:

* Skapandet av en ny egenskap som håller ihop alla dina konfigurationer.
* Installation och installation av tillägg. Klientkoden för alla tillägg som är installerade i egenskapen kompileras tillsammans till ett bibliotek. Det här biblioteket används av webbsidan senare.
* Konfiguration av dataelement och regler. Den här konfigurationen definierar vilka data som ska hämtas från Dynamic Media-visningsprogram, när spårningslogiken ska utlösas och var visningsprogrammets data ska skickas i Adobe Analytics.
* Publicering av biblioteket.

**Så här konfigurerar du Experience Platform-taggar för integreringen:**

1. Börja med att gå till taggar från Experience Platform från Experience Cloud [hemsida](https://experience.adobe.com/#/home). På menyraden väljer du ikonen Lösningar (3 x 3 punkter) i det övre högra hörnet av sidan och väljer sedan **[!UICONTROL Tags]**.

   Du kan också [öppna Experience Platform-taggar direkt](https://launch.adobe.com/).

   ![image2019-7-8_15-38-44](assets/image2019-7-8_15-38-44.png)

### Skapa en egenskap i Experience Platform-taggar {#creating-a-property-in-adobe-launch}

En egenskap i Experience Platform Tags är en namngiven konfiguration som håller ihop alla inställningar. Ett bibliotek med konfigurationsinställningarna genereras och publiceras på olika miljönivåer (utveckling, mellanlagring och produktion).

Se även [Konfigurera en tryckningsegenskap](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/initial-configuration/configure-tags.html).

**Så här skapar du en egenskap i Experience Platform-taggar:**

1. I Experience Platform-taggar väljer du **[!UICONTROL New Property]**.
1. I dialogrutan **[!UICONTROL Create Property]** anger du ett beskrivande namn, till exempel webbplatsens titel, i fältet **[!UICONTROL Name]**. Till exempel, `DynamicMediaViewersProp.`
1. I **[!UICONTROL Domains]** anger du webbplatsens domän.
1. Aktivera **[!UICONTROL Configure for extension development (cannot be modified later)]** i listrutan **[!UICONTROL Advanced Options]** om det tillägg som du vill använda – i det här fallet *Dynamic Media-visningsprogram* – inte släppts än.

   ![image2019-7-8_16-3-47](assets/image2019-7-8_16-3-47.png)

1. Välj **[!UICONTROL Save]**.

   Välj den nyligen skapade egenskapen och fortsätt sedan till *Installation och installation av tillägg*.

### Installera och konfigurera tillägg {#installing-and-setup-of-extensions}

Alla tillgängliga tillägg i Experience Platform-taggar visas under **[!UICONTROL Extensions]** > **[!UICONTROL Catalog]**.

Om du vill installera ett tillägg väljer du **[!UICONTROL Install]**. Utför vid behov en engångskonfiguration och välj sedan **[!UICONTROL Save]**.

Om det behövs måste följande tillägg installeras och konfigureras:

* (Obligatoriskt) *Experience Cloud ID-tjänst* extension

Ingen ytterligare konfiguration behövs. Godkänn för föreslagna värden. Se till att du väljer **[!UICONTROL Save]**.

Se [Experience Cloud Identity Service-tillägg](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/id-service/overview.html).

* (Obligatoriskt) *Adobe Analytics* extension

Om du vill konfigurera det här tillägget måste du ha det Report Suite-ID som finns i Adobe Analytics, under **[!UICONTROL Admin]** > **[!UICONTROL Report Suite]**, under **[!UICONTROL Report Suite ID]** kolumnrubrik.

(Endast i demonstrationssyfte, rapportsvitens-ID för **[!UICONTROL DynamicMediaViewersExtensionDoc]** Report Suite används i följande skärmbilder. Detta ID skapades och användes tidigare när du [valde en rapportsvit](#selecting-a-report-suite).)

![image2019-7-8_16-45-34](assets/image2019-7-8_16-45-34.png)

På sidan Installera tillägg anger du rapportsvits-ID:t i fälten **[!UICONTROL Development Report Suites]**, **[!UICONTROL Staging Report Suites]** och **[!UICONTROL Production Report Suites]**.

![image2019-7-8_16-47-40](assets/image2019-7-8_16-47-40.png)

*Konfigurera endast följande objekt om du tänker använda videospårning:*

På **[!UICONTROL Install Extension]** sida, expandera **[!UICONTROL General]** anger sedan spårningsservern. Spårningsservern följer mallen `<trackingNamespace>.sc.omtrdc.net`, där `<trackingNamespace>` är den information som hämtas i e-postmeddelandet om etablering.

Välj **[!UICONTROL Save]**.

Se [Adobe Analytics Extension](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/analytics/overview.html).

* (Valfritt. Krävs endast om videospårning behövs) *Adobe Media Analytics för ljud och video* extension

Fyll i spårningsserverfältet. Spårningsservern för *Adobe Media Analytics för ljud och video* tillägget skiljer sig från spårningsservern som används för Adobe Analytics. Den följer mallen `<trackingNamespace>.hb.omtrdc.net`, där `<trackingNamespace>` är informationen från e-postmeddelandet om etablering.

Alla andra fält är valfria.

Se [Adobe Media Analytics för ljud- och videotillägg](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/media-analytics/overview.html).

* (Obligatoriskt) *Dynamic Media Viewers* extension

Välj **[!UICONTROL enable Adobe Analytics for Video]** om du vill aktivera (starta) spårning av pulsslag för video.

I skrivande stund är *Dynamic Media Viewers* tillägget är bara tillgängligt om taggegenskapen Experience Platform har skapats för utveckling.

Se [Skapa en egenskap i Experience Platform-taggar](#creating-a-property-in-adobe-launch).

När tilläggen har installerats och konfigurerats visas minst följande fem tillägg (fyra om du inte spårar video) under Tillägg > Installerat.

![image2019-7-22_12-7-36](assets/image2019-7-22_12-7-36.png)

### Ställ in dataelement och regler {#setting-up-data-elements-and-rules}

Skapa dataelement och regler som behövs för att spåra visningsprogram i Dynamic Media i Taggar för Experience Platform.

Se [Hur data- och händelsespårning fungerar i integreringen](#how-data-and-event-tracking-works-in-the-integration) för en översikt över spårning med Experience Platform-taggar.

Se [Exempelkonfiguration](#sample-configuration) om du vill ha en exempelkonfiguration i Experience Platform Taggar som visar hur du spårar ett resursnamn när visningsprogrammet läses in.

Se [Konfigurera tillägget Dynamic Media Viewer](#configuring-the-dynamic-media-viewers-extension) för detaljerad information om tilläggets funktioner.

### Publicera ett bibliotek {#publishing-a-library}

Om du vill ändra konfigurationen för taggar i Experience Platform (inklusive egenskapsinställningar, tillägg, regler och dataelement) måste du *publicera* sådana ändringar. Publicering i Experience Platform-taggar utförs från fliken Publicering under egenskapskonfigurationen.

Experience Platform-taggar kan ha flera utvecklingsmiljöer, en mellanlagringsmiljö och en produktionsmiljö. Som standard pekar Experience Platform Tags Cloud Configuration i Experience Manager på Experience Manager författarnoden mot scenmiljön för plattformstaggar. Noden Experience Manager Publish pekar på produktionsmiljön för Experience Platform-taggar. Detta innebär att med standardinställningarna för Experience Manager måste du publicera Experience Platform-taggbiblioteket till mellanlagringsmiljön. Om du gör det kan du använda det i författaren till Experience Manager. Du kan sedan publicera den i produktionsmiljön så att den kan användas i Experience Manager.

Se [Miljö](https://experienceleague.adobe.com/docs/experience-platform/tags/publish/environments/environments.html) om du vill ha mer information om Experience Platform Tags-miljöer.

Publicering av ett bibliotek omfattar följande två steg:

* Lägga till och skapa ett nytt bibliotek genom att inkludera alla nödvändiga ändringar (nya och uppdateringar) i biblioteket.
* Flytta upp biblioteket genom de olika miljönivåerna (från utveckling till mellanlagring och produktion).

#### Lägga till och skapa ett nytt bibliotek {#adding-and-building-a-new-library}

1. Första gången du öppnar fliken Publicera i Experience Platform-taggar är bibliotekslistan tom.

   I den vänstra kolumnen väljer du **[!UICONTROL Add New Library]**.

   ![image2019-7-15_14-43-17](assets/image2019-7-15_14-43-17.png)

1. På sidan Skapa nytt bibliotek, i **[!UICONTROL Name]** anger du ett beskrivande namn för det nya biblioteket. Till exempel,

   *DynamicMediaViewersLib*

   Välj miljönivå i listrutan Miljö. Till att börja med är bara utvecklingsnivån tillgänglig för val. I närheten av den nedre vänstra sidan av sidan väljer du **[!UICONTROL Add All Changed Resources]**.

   ![image2019-7-15_14-49-41](assets/image2019-7-15_14-49-41.png)

1. I sidans övre högra hörn väljer du **[!UICONTROL Save & Build for Development]**.

   Om några minuter är biblioteket klart att användas.

   ![image2019-7-15_15-3-34](assets/image2019-7-15_15-3-34.png)

   >[!NOTE]
   >
   >Nästa gång du ändrar konfigurationen för Experience Platform-taggar går du till **[!UICONTROL Publishing]** under **[!UICONTROL Property]** väljer du sedan det bibliotek du skapat tidigare.
   >
   >
   >På bibliotekets publiceringsskärm väljer du **[!UICONTROL Add All Changed Resources]** väljer **[!UICONTROL Save & Build for Development]**.

#### Flytta upp ett bibliotek via miljönivåer {#moving-a-library-up-through-environment-levels}

1. När ett nytt bibliotek har lagts till finns det i utvecklingsmiljön. Om du vill flytta den till nivån Mellanlagringsmiljö (som motsvarar kolumnen Skickat) går du till listrutan i biblioteket och väljer **[!UICONTROL Submit for Approval]**.

   ![image2019-7-15_15-52-37](assets/image2019-7-15_15-52-37.png)

1. I bekräftelsedialogrutan väljer du **[!UICONTROL Submit]**.

   När biblioteket har flyttats till kolumnen Skickat väljer du **[!UICONTROL Build for Staging]**.

   ![image2019-7-15_15-54-37](assets/image2019-7-15_15-54-37.png)

1. Om du vill flytta biblioteket från mellanlagringsmiljön till produktionsmiljön (kolumnen Publicerad) följer du en liknande process.

   Först väljer du **[!UICONTROL Approve for Publishing]**.

   ![image2019-7-15_16-7-39](assets/image2019-7-15_16-7-39.png)

1. Välj **[!UICONTROL Build & Publish to Production]**.

   ![image2019-7-15_16-8-9](assets/image2019-7-15_16-8-9.png)

   Se [Publicering](https://experienceleague.adobe.com/docs/experience-platform/tags/publish/overview.html) om du vill ha mer information om publiceringsprocessen i Experience Platform Tags.

## Konfigurera Adobe Experience Manager för integreringen {#configuring-adobe-experience-manager-for-the-integration}

<!-- Prerequisites list below should be verified by Sasha -->

Förutsättningar:

* Experience Manager kör både författarinstansen och publiceringsinstansen.
* Skribentnoden för Experience Manager har konfigurerats i Dynamic Media. <!-- Scene7 run mode (dynamicmedia_s7) -->
* Dynamic Media WCM-komponenter är aktiverade i Experience Manager Sites.

Konfigurationen av Experience Manager består av följande två stora steg:

* Konfiguration av Experience Manager IMS.
* Konfiguration av Experience Platform Tags Cloud.

### Konfigurera Experience Manager IMS {#configuring-aem-ims}

1. I Experience Manager väljer du verktygsikonen (hammer) och går till **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**.

   ![2019-07-25_11-52-58](assets/2019-07-25_11-52-58.png)

1. På konfigurationssidan för Adobe IMC, i det övre vänstra hörnet, väljer du **[!UICONTROL Create]**.
1. På **[!UICONTROL Adobe IMS Technical Account Configuration]** sida, på **[!UICONTROL Cloud Solution]** nedrullningsbar lista, välja **[!UICONTROL Experience Platform Data Collection]**.
1. Aktivera **[!UICONTROL Create new certificate]** anger du sedan ett meningsfullt värde för certifikatet i textfältet. Till exempel: *AdobeLaunchIMSCert*. Välj **[!UICONTROL Create certificate]**.

   Följande informationsmeddelande visas:

   *Om du vill hämta en giltig åtkomsttoken måste det nya certifikatets offentliga nyckel läggas till i det tekniska kontot på Adobe Developer!*

   Om du vill stänga dialogrutan Info väljer du **[!UICONTROL OK]**.

   ![2019-07-25_12-09-24](assets/2019-07-25_12-09-24.png)

1. Välj **[!UICONTROL Download Public Key]** för att ladda ned en fil med en offentlig nyckel (`*.crt`) till ditt lokala system.

   >[!NOTE]
   >
   >I det här skedet ***lämna öppen*** den **[!UICONTROL Adobe IMS Technical Account Configuration]** sida; ***inte*** stäng sidan och ***inte*** välj **[!UICONTROL Next]**. Du kommer att gå tillbaka till den här sidan senare i stegen.

   ![2019-07-25_12-52-24](assets/2019-07-25_12-52-24.png)

1. Navigera till [Adobe Developer Console](https://developer.adobe.com/console/integrations).

1. Från **[!UICONTROL Adobe I/O Console Integrations]** sida, nära det övre högra hörnet, markera **[!UICONTROL New integration]**.
1. I **[!UICONTROL Create a new integration]** se till att **[!UICONTROL Access an API]** alternativknappen är markerad och välj **[!UICONTROL Continue]**.

![2019-07-25_13-04-20](assets/2019-07-25_13-04-20.png)

1. På den andra **[!UICONTROL Create a new integration]**-sidan aktiverar du (sätter på) alternativknappen **[!UICONTROL Experience Platform Tags API]**. Välj **[!UICONTROL Continue]**.

   ![2019-07-25_13-13-54](assets/2019-07-25_13-13-54.png)

1. Den tredje **[!UICONTROL Create a new integration]** gör du följande på sidan:

   * I **[!UICONTROL Name]** anger du ett beskrivande namn. Till exempel: *DynamicMediaViewersIO*.

   * I **[!UICONTROL Description]** anger du en beskrivning av integreringen.

   * I **[!UICONTROL Public key certificates]** område, ladda upp filen med den offentliga nyckeln (`*.crt`) som du laddade ned tidigare i dessa steg.

   * Under **[!UICONTROL Select a role for Experience Platform Tags API]** rubrik, markera **[!UICONTROL Admin]**.

   * Under **[!UICONTROL Select one or more product profiles for Experience Platform Tags API]** väljer du produktprofilen med namnet **[!UICONTROL Tags - <your_company_name>]**.

   ![2019-07-25_13-49-18](assets/2019-07-25_13-49-18.png)

1. Välj **[!UICONTROL Create integration]**.
1. På **[!UICONTROL Integration created]** sida, markera **[!UICONTROL Continue to integration details]**.

   ![2019-07-25_14-16-33](assets/2019-07-25_14-16-33.png)

1. En integreringsinformationssida visas, som i följande exempel:

   >[!NOTE]
   >
   >***Låt den här sidan med integreringsinformation vara öppen.*** Du behöver olika typer av information från **[!UICONTROL Overview]** och **[!UICONTROL JWT]** tabbar på bara ett ögonblick.

   ![2019-07-25_14-35-30](assets/2019-07-25_14-35-30.png)
   *Sidan med integreringsinformation*

1. Gå tillbaka till sidan **[!UICONTROL Adobe IMS Technical Account Configuration]** som du öppnade tidigare. I det övre högra hörnet på sidan väljer du **[!UICONTROL Next]** för att öppna **[!UICONTROL Account]** sidan i **[!UICONTROL Adobe IMS Technical Account Configuration]** -fönstret.

   (Om du stängde sidan tidigare går du tillbaka till författaren av Experience Manager och går till **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**. Välj **[!UICONTROL Create]**. I listrutan **[!UICONTROL Cloud Solution]** väljer du **[!UICONTROL Experience Platform Tags]**. I listrutan **[!UICONTROL Certificate]** markerar du namnet på det tidigare skapade certifikatet.

   ![2019-07-25_20-57-50](assets/2019-07-25_20-57-50.png)
   *Adobe IMS Technical Account Configuration - certifikatsida*

1. The **[!UICONTROL Account]** sidan innehåller fem fält som kräver att du fyller i med information från sidan Integreringsinformation från föregående steg.

   ![2019-07-25_20-42-45](assets/2019-07-25_20-42-45.png)
   *Adobe IMS Technical Account Configuration - kontosida*

1. På **[!UICONTROL Account]** sidan, fyll i följande fält:

   * **[!UICONTROL Title]** - Ange en beskrivande kontotitel.
   * **[!UICONTROL Authorization Server]** - Gå tillbaka till sidan Integreringsinformation som du öppnade tidigare. Välj **[!UICONTROL JWT]** -fliken. Kopiera servernamnet - utan sökvägen - enligt markeringen nedan.

(exempelservernamnet är endast avsett för förklaringar)   Gå tillbaka till sidan **[!UICONTROL Account]** och klistra sedan in namnet i respektive fält.
Till exempel: `https://ims-na1.adobelogin.com/`
(exempelservernamnet är endast avsett för förklaringar)

   ![2019-07-25_15-01-53](assets/2019-07-25_15-01-53.png)
   *Detaljsida för integrering - fliken JWT*

1. **[!UICONTROL API Key]** – Gå tillbaka till sidan med integreringsinformation. Välj **[!UICONTROL Overview]** och sedan till höger om **[!UICONTROL API Key (Client ID)]** fält, markera **[!UICONTROL Copy]**.

   Gå tillbaka till sidan **[!UICONTROL Account]** och klistra sedan in nyckeln i respektive fält.

   ![2019-07-25_14-35-333](assets/2019-07-25_14-35-333.png)
   *Sidan med integreringsinformation*

1. **[!UICONTROL Client Secret]**– Gå tillbaka till sidan med integreringsinformation. Från **[!UICONTROL Overview]** flik, välja **[!UICONTROL Retrieve Client Secret]**. Till höger om **[!UICONTROL Client secret]** fält, markera **[!UICONTROL Copy]**.

   Gå tillbaka till sidan **[!UICONTROL Account]** och klistra sedan in nyckeln i respektive fält.

1. **[!UICONTROL Payload]** – Gå tillbaka till sidan med integreringsinformation. Från **[!UICONTROL JWT]** i JWT-nyttolastfältet kopierar hela JSON-objektkoden.

   Gå tillbaka till sidan **[!UICONTROL Account]** och klistra sedan in koden i respektive fält.

   ![2019-07-25_21-59-12](assets/2019-07-25_21-59-12.png)
   *Integrationsinformationssida - JWT-flik*

   Kontosidan, med alla fält ifyllda, ser ut ungefär så här:

   ![2019-07-25_22-08-30](assets/2019-07-25_22-08-30.png)

1. Nära det övre högra hörnet av **[!UICONTROL Account]** sida, markera **[!UICONTROL Create]**.

   När Experience Manager IMS är konfigurerat har du nu ett nytt IMSA-konto som listas under **[!UICONTROL Adobe IMS Configurations]**.

   ![image2019-7-15_14-17-54](assets/image2019-7-15_14-17-54.png)

## Konfigurera Experience Platform Tags Cloud för integrering {#configuring-adobe-launch-cloud-for-the-integration}

1. I Experience Manager, nära det övre vänstra hörnet, väljer du verktygsikonen (hammare) och går sedan till **[!UICONTROL Cloud Services]** > **[!UICONTROL Experience Platform Tags Configurations]**.

   ![2019-07-26_12-10-38](assets/2019-07-26_12-10-38.png)

1. På **[!UICONTROL Experience Platform Tags Configurations]** i den vänstra panelen väljer du en Experience Manager-plats som du vill använda Experience Platform-taggar för.

   Endast i exempelsyfte **`We.Retail`** Webbplatsen markeras i skärmbilden nedan.

   ![2019-07-26_12-20-06](assets/2019-07-26_12-20-06.png)

1. I närheten av sidans övre vänstra hörn väljer du **[!UICONTROL Create]**.
1. På sidan **[!UICONTROL General]** (sida 1/3) i fönstret **[!UICONTROL Create Experience Platform Tags Configuration]** fyller du i följande fält:

   * **[!UICONTROL Title]** - Ange en beskrivande konfigurationstitel. Till exempel, `We.Retail Tags cloud configuration`.

   * **[!UICONTROL Associated Adobe IMS Configuration]** - Välj den IMS-konfiguration som du skapade tidigare i [Konfigurera Experience Manager IMS](#configuring-aem-ims).

   * **[!UICONTROL Company]** - Från **[!UICONTROL Company]** väljer du företag i Experience Cloud. Listan fylls i automatiskt.

   * **[!UICONTROL Property]** - I listrutan Egenskaper väljer du Experience Platform-taggegenskapen som du skapade tidigare. Listan fylls i automatiskt.

När du fyllt i samtliga fält kan du **[!UICONTROL General]** ser sidan ut ungefär så här:

![image2019-7-15_14-34-23](assets/image2019-7-15_14-34-23.png)

1. I det övre vänstra hörnet väljer du **[!UICONTROL Next]**.
1. På sidan **[!UICONTROL Staging]** (sida 2/3) i fönstret **[!UICONTROL Create Experience Platform Tags Configuration]** fyller du i följande fält:

   I **[!UICONTROL Library URI]** (Uniform Resource Identifier) kontrollerar du platsen för mellanlagringsversionen av Experience Platform Tags Library. Experience Manager fyller i det här fältet automatiskt.

   I det här steget används endast bibliotek för Experience Platform-taggar som distribueras till Adobe CDN.

   >[!NOTE]
   >
   >Kontrollera att den automatiskt ifyllda biblioteks-URI:n (Uniform Resource Identifier) inte har fel format. Om det behövs kan du åtgärda det så att URI:n representerar en protokollrelativ URI. Det vill säga, det börjar med ett dubbelt snedstreck.
   >
   >
   >Till exempel: `//assets.adobetm.com/launch-xxxx`.

   Dina **[!UICONTROL Staging]** sidan ser förmodligen ut ungefär så här. The **[!UICONTROL Archive]** och **[!UICONTROL Load Library Asynchronously]** alternativ är ***not*** set:

   ![image2019-7-15_15-21-8](assets/image2019-7-15_15-21-8.png)

1. I det övre högra hörnet väljer du **[!UICONTROL Next]**.
1. På sidan **[!UICONTROL Production]** (sida 3/3) i fönstret **[!UICONTROL Create Experience Platform Tags Configuration]** korrigerar du (vid behov) den automatiskt ifyllda produktions-URI:n på samma sätt som på föregående **[!UICONTROL Staging]**-sida.
1. I det övre högra hörnet väljer du **[!UICONTROL Create]**.

   Din nya konfiguration av Experience Platform Tags Cloud skapas nu och visas bredvid din webbplats.

1. Markera din nya konfiguration för Experience Platform Tags Cloud (en bock visas till vänster om konfigurationstiteln när den är markerad). I verktygsfältet väljer du **[!UICONTROL Publish]**.

   ![image2019-7-15_15-47-6](assets/image2019-7-15_15-47-6.png)

Experience Manager-författaren stöder för närvarande inte integrering av Dynamic Media-visningsprogram med Experience Platform-taggar.

Det stöds dock i Experience Manager-publiceringsnoden. Med standardinställningarna i Experience Platform Tags Cloud Configuration används produktionsmiljön för Experience Platform Tags i Experience Manager-publiceringen. Det är därför nödvändigt att varje gång under testet överföra Experience Platform Tags-biblioteksuppdateringar från Development till produktionsmiljön.

Det är möjligt att kringgå denna begränsning. Ange utvecklings- eller mellanlagrings-URL för Experience Platform Tags-biblioteket i Experience Platform Tags Cloud-konfigurationen för Experience Manager-publicering ovan. Om du gör det använder Experience Manager-publiceringsnoden utvecklings- eller mellanlagringsversionen av Experience Platform-taggbiblioteket.

Se [Integrera Experience Platform-taggar och Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/overview.html#integrations) om du vill ha mer information om hur du konfigurerar Experience Platform Tags Cloud Configuration.
