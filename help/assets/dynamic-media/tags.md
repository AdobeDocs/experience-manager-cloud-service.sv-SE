---
title: Integrera dynamiska mediavisare med taggar från Adobe Analytics och Experience Platform
description: Läs om tillägget Dynamic Media Viewer för Experience Platform Tags och Dynamic Media Viewer 5.13. Det gör att kunder som använder Adobe Analytics- och plattformstaggar kan använda händelser och data som är specifika för de dynamiska medievyerna i sin Experience Platform Tags-konfiguration.
contentOwner: Rick Brough
feature: Asset Reports
role: Admin,User
exl-id: a71fef45-c9a4-4091-8af1-c3c173324b7a
source-git-commit: 05c6c8bcd8140bed9a30179c5a12d3a3fa8cb37d
workflow-type: tm+mt
source-wordcount: '6272'
ht-degree: 6%

---

# Integrera dynamiska mediavisare med taggar från Adobe Analytics och Experience Platform {#integrating-dynamic-media-viewers-with-adobe-analytics-and-adobe-launch}

## Vad är Dynamic Media Viewer-integrering med Adobe Analytics- och Experience Platform-taggar? {#what-is-dynamic-media-viewers-integration-with-adobe-analytics-and-adobe-launch}

<!-- Leave this hidden path here; it points to the topic source from Sasha https://wiki.corp.adobe.com/pages/viewpage.action?spaceKey=~oufimtse&title=Dynamic+Media+Viewers+integration+with+Adobe+Launch 

name used to be Experience Platform Launch. Changed to Experience Platform Data Collection-->

Tillägget *Dynamiska medievyer* för Experience Platform-taggar fungerar med Dynamic Media Viewer 5.13. Med den kan Adobe Analytics- och Experience Platform Tags-kunder använda Dynamic Media Viewer-händelser och data i sina taggkonfigurationer.

Integrationen innebär att du kan spåra användningen av dynamiska medievyer på din webbplats med Adobe Analytics. Samtidigt kan du använda händelser och data som visas av visningsprogrammen med andra Experience Platform Tags-tillägg som kommer från Adobe eller en tredje part.

Mer information om Adobe-tillägg och tredjepartstillägg finns i [Adobe-tillägg](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/overview) i användarhandboken för Experience Platform-taggar.

**Det här avsnittet är avsett för följande:** Webbplatsadministratörer, utvecklare av Adobe Experience Manager-programmet och personer i Operations.

### Begränsningar i integreringen {#limitations-of-the-integration}

* Integrering med Experience Platform Tags för dynamiska medievyer fungerar inte i Experience Manager författarnod. Du kan inte se någon spårning från en WCM-sida förrän den har publicerats.
* Integrering med Experience Platform Tags för Dynamic Media-visningsprogram stöds inte för&quot;popup&quot;-åtgärdsläge, där visningsprogrammets URL hämtas med knappen &quot;URL&quot; på sidan Resursinformation.
* Integrering med Experience Platform Tags kan inte användas samtidigt med integrering med äldre visningsprogram med Analytics (med parametern `config2=`).
* Stödet för videospårning är begränsat till enbart huvuduppspelningsspårning, vilket beskrivs i [Spårningsöversikt](https://experienceleague.adobe.com/en/docs/media-analytics/using/tracking/track-core-overview#player-events). I synnerhet stöds inte QoS, Ads, Chapter/Segments eller Errors tracking.
* Lagringsvaraktighetskonfigurationen för dataelement stöds inte för dataelement med tillägget *Dynamiska medievyer*. Lagringstid måste anges till **[!UICONTROL None]**.

### Användningsexempel för integreringen {#use-cases-for-the-integration}

Det viktigaste användningsområdet för integreringen med Experience Platform Tags är kunder som använder både Experience Manager Assets och Experience Manager Sites. I sådana fall kan du skapa en standardintegrering mellan Experience Manager-författarnoden och Experience Platform Tags och sedan associera platsinstansen med Experience Platform Tags-egenskapen. Efter det kommer alla WCM-komponenter för Dynamic Media som läggs till på en Sites-sida att spåra data och händelser från tittarna.

Se [Spåra visningar för dynamiska media i Experience Manager Sites](#tracking-dynamic-media-viewers-in-aem-sites).

Ett sekundärt användningsfall som integreringen stöder är de kunder som bara använder Experience Manager Assets eller Dynamic Media Classic. I så fall får du inbäddningskoden för ditt visningsprogram och lägger till den på webbplatssidan. Hämta sedan Experience Platform Tags-bibliotekets produktions-URL från Experience Platform Tags och lägg till den manuellt i webbsideskoden.

Se [Spåra visningar för dynamiska media med inbäddad kod](#tracking-dynamic-media-viewers-using-embed-code).

## Hur data- och händelsespårning fungerar i integreringen {#how-data-and-event-tracking-works-in-the-integration}

Integreringen utnyttjar två separata och oberoende typer av spårning av dynamiska medievyer: *Adobe Analytics* och *Adobe Analytics för ljud och video*.

### Om spårning med Adobe Analytics {#about-tracking-using-adobe-analytics}

Med Adobe Analytics kan du spåra åtgärder som en användare utför när de interagerar med dynamiska medievyer på webbplatsen. Med Adobe Analytics kan du också spåra visningsprogramspecifika data. Du kan till exempel spåra och spela in inläsningshändelser tillsammans med resursnamnet, eventuella zoomåtgärder som har utförts och videouppspelningsåtgärder.

I Experience Platform-taggar fungerar koncepten för *dataelement* och *regler* tillsammans för att aktivera Adobe Analytics-spårning.

#### Om dataelement i Experience Platform-taggar {#about-data-elements-in-adobe-launch}

Ett dataelement i Experience Platform-taggar är en namngiven egenskap vars värde antingen är statiskt definierat eller dynamiskt beräknat baserat på en webbsidas eller dynamiska medievydata.

Vilka alternativ som är tillgängliga för en dataelementsdefinition beror på listan med tillägg som är installerade i egenskapen Experience Platform Tags. Tillägget &quot;Core&quot; är förinstallerat och finns tillgängligt direkt i alla konfigurationer. Med det här tillägget Core kan du definiera ett dataelement som kommer från cookie, JavaScript-kod, frågesträng och många andra källor.

För Adobe Analytics tracking måste flera andra tillägg vara installerade, vilket beskrivs i [Installation och konfiguration av tillägg](#installing-and-setup-of-extensions). Tillägget Dynamic Media Viewer ger möjlighet att definiera ett dataelement som är ett argument i Dynamic Viewer-händelsen. Det är till exempel möjligt att referera till visningsprogramtypen, eller resursnamnet som rapporteras av visningsprogrammet vid inläsning, den zoomnivå som rapporteras när slutanvändaren zoomar och mycket annat.

Tillägget Dynamic Media Viewer håller automatiskt värdena för dataelementen uppdaterade.

När du har definierat det kan ett dataelement användas på andra platser i användargränssnittet för Experience Platform-taggar med hjälp av widgeten för dataelementväljaren. **Ange variabelåtgärd** för Adobe Analytics-tillägget i en regel refererar till dataelement som definierats för spårning av dynamiska medievyer (se nedan).

Se [Dataelement](https://experienceleague.adobe.com/en/docs/experience-platform/tags/ui/data-elements) i användarhandboken för Experience Platform-taggar.

#### Om regler i Experience Platform-taggar {#about-rules-in-adobe-launch}

En regel i Experience Platform-taggar är en agnostisk konfiguration som definierar tre områden som utgör en regel: *Händelser*, *Villkor* och *Åtgärder*:

* *Händelser* (if) anger för Experience Platform-taggar när en regel ska utlösas.
* *Villkor* (if) anger för Experience Platform-taggar vilka andra begränsningar som ska tillåtas eller inte när en regel aktiveras.
* *Åtgärder* (sedan) anger för Experience Platform-taggar vad som ska göras när en regel aktiveras.

Vilka alternativ som är tillgängliga i avsnittet Händelser, Villkor och Åtgärder beror på vilka tillägg som är installerade i egenskapen Experience Platform Tags. Tillägget *Core* är förinstallerat och är tillgängligt direkt i alla konfigurationer. Tillägget innehåller flera alternativ för Händelser, t.ex. grundläggande åtgärder på webbläsarnivå som inkluderar fokusändringar, tangenttryckningar och formulärskickningar. Den innehåller även alternativ för Villkor, som cookie-värde, webbläsartyp och mycket annat. För Åtgärder är endast alternativet Anpassad kod tillgängligt.

För Adobe Analytics-spårning måste flera andra tillägg installeras, vilket beskrivs i [Installation och konfiguration av tillägg](#installing-and-setup-of-extensions). Mer specifikt:

* Tillägget Dynamic Media Viewer utökar listan med händelser som stöds till händelser som är specifika för Dynamic Media-visningsprogram, t.ex. inläsning av visningsprogram, resursväxling, inzoomning och videouppspelning.
* Adobe Analytics-tillägget utökar listan med åtgärder som stöds med två åtgärder som krävs för att skicka data till spårningsservrar: *Ange variabler* och *Skicka signal*.

Om du vill spåra Dynamic Media-visningsprogram kan du använda någon av följande typer:

* Händelser från tillägget Dynamic Media Viewer, Core-tillägget eller något annat tillägg.
* Villkor i regeldefinitionen. Du kan också lämna villkorsområdet tomt.

I avsnittet Åtgärder måste du ha en *Ange variabler*-åtgärd. Den här åtgärden anger för Adobe Analytics hur spårningsvariabler ska fyllas i med data. Samtidigt skickar inte åtgärden *Ange variabler* något till spårningsservern.

Åtgärden **Skicka Beacon** måste följa åtgärden **Ange variabler**. Åtgärden *Skicka Beacon* skickar data till analysspårningsservern. Båda åtgärderna, *Ange variabler* och *Skicka fyr*, kommer från Adobe Analytics-tillägget.

Se [Regler](https://experienceleague.adobe.com/en/docs/experience-platform/tags/ui/rules) i användarhandboken för Experience Platform-taggar.

#### Exempelkonfiguration {#sample-configuration}

I följande exempelkonfiguration i Experience Platform Tags visas hur du spårar ett resursnamn när visningsprogrammet läses in.

1. På fliken **[!UICONTROL Data Elements]** definierar du ett dataelement `AssetName` som refererar till parametern `asset` för händelsen `LOAD` från tillägget Dynamiska medievyer.

   ![image2019-11](assets/image2019-11.png)

1. Definiera en regel *TrackAssetOnLoad* från fliken **[!UICONTROL Rules]**.

   I den här regeln använder fältet **[!UICONTROL Event]** händelsen **[!UICONTROL LOAD]** från tillägget för dynamiska medievyer.

   ![image2019-22](assets/image2019-22.png)

1. Åtgärdskonfigurationen har två åtgärdstyper från Adobe Analytics-tillägget:

   *Ange variabler* som mappar en analysvariabel som du väljer till värdet för dataelementet `AssetName`.

   *Skicka Beacon* som skickar spårningsinformation till Adobe Analytics.

   ![image2019-3](assets/image2019-3.png)

1. Den resulterande regelkonfigurationen ser ut så här:

   ![image2019-4](assets/image2019-4.png)

### Om Adobe Analytics för ljud och video {#about-adobe-analytics-for-audio-and-video}

När ett Experience Cloud-konto prenumererar på Adobe Analytics för ljud och video räcker det att aktivera videospårning i tilläggsinställningarna för *Dynamiska medievyer*. Videomått blir tillgängligt i Adobe Analytics. Videospårning beror på att det finns Adobe Media Analytics för ljud- och videotillägg.

Se [Installation och konfiguration av tillägg](#installing-and-setup-of-extensions).

Stödet för videospårning är för närvarande begränsat till enbart huvuduppspelningsspårning, vilket beskrivs i [Spårningsöversikt](https://experienceleague.adobe.com/en/docs/media-analytics/using/tracking/track-core-overview#player-events). I synnerhet stöds inte QoS, Ads, Chapter/Segments eller Errors tracking.

## Använda tillägget Dynamic Media Viewer {#using-the-dynamic-media-viewers-extension}

Som nämndes i [Användningsexempel för integreringen](#use-cases-for-the-integration) är det möjligt att spåra visningar för dynamiska media med den nya integreringen av Experience Platform-taggar i Experience Manager Sites och genom att använda inbäddningskod.

### Spåra Dynamic Media-visningsprogram i Experience Manager Sites {#tracking-dynamic-media-viewers-in-aem-sites}

Om du vill spåra Dynamic Media-visningsprogram i Experience Manager Sites måste alla steg som listas under avsnittet [Konfigurera alla integrationsdelar](#configuring-all-the-integration-pieces) utföras. Du måste skapa IMS-konfigurationen och Experience Platform Tags Cloud Configuration.

Om du använder en WCM-komponent som stöds av Dynamic Media, spåras data automatiskt till Adobe Analytics, Adobe Analytics for Video eller båda, efter rätt konfiguration.

Se [Lägg till Assets för dynamiska media på sidor med Adobe Sites](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

### Spåra Dynamic Media-visningsprogram med hjälp av inbäddningskod {#tracking-dynamic-media-viewers-using-embed-code}

Kunder som inte använder Experience Manager Sites, eller bäddar in Dynamic Media-visningsprogram på webbsidor utanför Experience Manager Sites, eller båda, kan fortfarande använda Experience Platform Tags-integreringen.

Slutför konfigurationsstegen i avsnitten [Konfigurera Adobe Analytics](#configuring-adobe-analytics-for-the-integration) och [Konfigurera Experience Platform-taggar](#configuring-adobe-launch-for-the-integration). Experience Manager-relaterade konfigurationssteg behövs dock inte.

Om konfigurationen är korrekt kan du lägga till stöd för Experience Platform-taggar på en webbsida med ett dynamiskt medievisningsprogram.

Mer information om hur du använder inbäddningskoden för Experience Platform-taggbiblioteket finns i [Lägga till Experience Platform-taggar ](https://experienceleague.adobe.com/en/docs/platform-learn/implement-in-websites/configure-tags/add-embed-code) .

Mer information om hur du använder den inbäddade kodfunktionen i Experience Manager Dynamic Media finns i [Bädda in video- eller bildvisningsprogrammet på en webbsida](/help/assets/dynamic-media/embed-code.md).

**Spåra dynamiska medievyer med inbäddad kod:**

1. Ha en webbsida redo för inbäddning av ett dynamiskt medievisningsprogram.
1. Hämta inbäddningskoden för Experience Platform Tags-biblioteket genom att först logga in på Experience Platform Tags (se [Konfigurera Experience Platform Tags](#configuring-adobe-launch-for-the-integration)).
1. Välj **[!UICONTROL Property]** och klicka sedan på fliken **[!UICONTROL Environments]**.
1. Plocka upp den miljönivå som är relevant för webbsidans miljö. Klicka sedan på ruteikonen i kolumnen **[!UICONTROL Install]**.
1. **[!UICONTROL In the Web Install Instructions]**-dialogrutan kopierar den fullständiga inbäddningskoden för Experience Platform-taggbiblioteket tillsammans med de omgivande `<script/>` -taggarna.

## Referenshandbok för tillägget Dynamic Media Viewers {#reference-guide-for-the-dynamic-media-viewers-extension}

### Om konfigurationen för Dynamic Media Viewer {#about-the-dynamic-media-viewers-configuration}

Tillägget Dynamic Media Viewer integreras automatiskt med Experience Platform Tags Library om följande villkor är uppfyllda:

* Experience Platform Tags-bibliotekets globala objekt ( `_satellite`) finns på sidan.
* Tilläggsfunktionen `_dmviewers_v001()` för Dynamic Media Viewer har definierats för `_satellite`.

* `config2=`-visningsprogramparametern har inte angetts, vilket innebär att visningsprogrammet inte använder äldre Analytics-integrering.

Det finns också ett alternativ för att inaktivera integreringen av Experience Platform-taggar explicit i visningsprogrammet genom att ange parametern `launch=0` i visningsprogrammets konfiguration. Standardvärdet för parametern är `1`.

### Konfigurera tillägget Dynamiska medievyer {#configuring-the-dynamic-media-viewers-extension}

Det enda konfigurationsalternativet för tillägget för dynamiska medievyer är **[!UICONTROL Enable Adobe Media Analytics for Audio and Video]**.

När du markerar (aktiverar) det här alternativet och Adobe Media Analytics för ljud och video-tillägget har installerats och konfigurerats skickas videouppspelningsstatistik till Adobe Analytics för ljud och video. Om du inaktiverar det här alternativet inaktiveras videospårning.

Om du aktiverar det här alternativet *utan att* ha Adobe Media Analytics för ljud och video installerat, har alternativet ingen effekt.

![image2019-7-22_12-4-23](assets/image2019-7-22_12-4-23.png)

### Om dataelement i tillägget Dynamiska medievisningsprogram {#about-data-elements-in-the-dynamic-media-viewers-extension}

Den enda dataelementtypen som tillägget Dynamic Media-visningsprogram tillhandahåller är **[!UICONTROL Viewer Event]** i listrutan **[!UICONTROL Data Element Type]**.

När du väljer det här alternativet återges ett formulär med två fält i dataelementsredigeraren:

* **[!UICONTROL DM viewers event data type]** - en nedrullningsbar lista visar alla visningsprogramhändelser med argument som stöds av tillägget Dynamic Media Viewer, tillsammans med ett särskilt **[!UICONTROL COMMON]**-objekt. Objektet **[!UICONTROL COMMON]** representerar en lista med händelseparametrar som är gemensamma för alla typer av händelser som skickas av visningsprogrammen.
* **[!UICONTROL Tracking parameter]** - ett argument för den valda Dynamic Media Viewer-händelsen.

![image2019-7-22_12-5-46](assets/image2019-7-22_12-5-46.png)

I referenshandboken för [Dynamiska medievisningsprogram](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/c-html5-s7-aem-asset-viewers) finns en lista över händelser som stöds av varje visningsprogramtyp. Gå till den specifika visningsprogramsektionen och välj sedan underavsnittet Stöd för Adobe Analytics-spårning. För närvarande dokumenterar inte referenshandboken för Dynamic Media Viewer händelseargument.

Nu ska vi titta på livscykeln för de dynamiska medievyerna *Dataelement*. Värdet för ett sådant dataelement fylls i efter att motsvarande Dynamic Media Viewer-händelse inträffar på sidan. Anta till exempel att dataelementet pekar på händelsen **[!UICONTROL LOAD]** och dess &quot;asset&quot;-argument. Värdet för ett sådant dataelement tar emot giltiga data när visningsprogrammet kör LOAD-händelsen för första gången. Om dataelementet pekar på händelsen **[!UICONTROL ZOOM]** och dess &quot;scale&quot;-argument, förblir värdet för dataelementet tomt tills användaren skickar en **[!UICONTROL ZOOM]** -händelse för första gången.

På samma sätt uppdateras värdena för dataelement automatiskt när visningsprogrammet skickar en motsvarande händelse på sidan. Värdeuppdateringen sker även om den särskilda händelsen inte har angetts i regelkonfigurationen. Anta till exempel att dataelementet **[!UICONTROL ZoomScale]** har definierats för parametern &quot;scale&quot; i ZOOM-händelsen. Händelsen **[!UICONTROL LOAD]** är dock den enda utlösaren i regelkonfigurationen. Värdet för **[!UICONTROL ZoomScale]** uppdateras fortfarande varje gång en användare zoomar in i visningsprogrammet.

Alla Dynamic Media-visningsprogram har en unik identifierare på webbsidan. Dataelementet spårar själva värdet och det visningsprogram som har fyllt i värdet. Anta till exempel att det finns flera visningsprogram på samma sida och ett **[!UICONTROL AssetName]**-dataelement som pekar på händelsen **[!UICONTROL LOAD]** och dess &quot;asset&quot;-argument. Dataelementet **[!UICONTROL AssetName]** underhåller en samling resursnamn som är associerade med varje visningsprogram som har lästs in på sidan.

Det exakta värdet som returneras av dataelementet beror på sammanhanget. Om en regel som utlöses av en händelse i Dynamic Media Viewer begär dataelementet, returneras värdet för det visningsprogram som initierade regeln. Om en regel som utlöses av en händelse från ett annat Experience Platform Tags-tillägg begär dataelementet, följer den den motsvarande händelsens kontext. I det skedet kommer dataelementets värde från det visningsprogram som senast uppdaterade det här dataelementet.

**Överväg följande exempelinställningar:**

* En webbsida med två zoomningsvisningsprogram för Dynamic Media: *viewer1* och *viewer2*.

* **[!UICONTROL ZoomScale]** Dataelement pekar på händelsen **[!UICONTROL ZOOM]** och dess &quot;scale&quot;-argument.
* **[!UICONTROL TrackPan]** Regel med följande:

   * Använder Dynamic Media Viewer **[!UICONTROL PAN]**-händelsen som utlösare.
   * Skickar värdet för dataelementet **[!UICONTROL ZoomScale]** till Adobe Analytics.

* **[!UICONTROL TrackKey]** Regel med följande:

   * Använder tangenttryckningshändelsen från Core Experience Platform Tags-tillägget som utlösare.
   * Skickar värdet för dataelementet **[!UICONTROL ZoomScale]** till Adobe Analytics.

Anta nu att användaren läser in webbsidan med de två visningsprogrammen. I *viewer1* zoomar de in till 50 % skala och i *viewer2* zoomar de sedan in till 25 % skala. I *visningsprogrammet1* panorerar de bilden och trycker slutligen på en tangent på tangentbordet.

Användarens aktivitet resulterar i följande två spårningsanrop till Adobe Analytics:

* Det första anropet sker eftersom regeln **[!UICONTROL TrackPan]** aktiveras när användaren panorerar i *viewer1*. Det anropet skickar **50%** som värde för dataelementet **[!UICONTROL ZoomScale]** eftersom det känner igen att *viewer1* utlöste regeln och hämtar motsvarande skalvärde.
* Det andra anropet sker eftersom regeln **[!UICONTROL TrackKey]** aktiveras när användaren trycker på en tangent på tangentbordet. Det anropet skickar 25 % som värde för dataelementet **[!UICONTROL ZoomScale]** eftersom visningsprogrammet inte utlöste regeln. Därför returnerar dataelementet det senaste värdet.

Samplingsuppsättningen ovan påverkar också dataelementvärdets livslängd. Värdet för dataelementet som hanteras av Dynamic Media Viewer lagras i Experience Platform Tags-bibliotekskoden även efter att visningsprogrammet har tagits bort från webbsidan. Den här funktionen innebär att om en regel som aktiveras av ett icke-dynamiskt visningsprogramtillägg refererar till dataelementet, returneras det senast kända värdet. Även om visningsprogrammet inte längre finns på webbsidan.

Värden för dataelement som hanteras av dynamiska medievisningsprogram lagras inte i den lokala lagringen eller på servern. De lagras bara i klientsidans Experience Platform-taggbibliotek. Värdena för sådana dataelement försvinner när webbsidan läses in igen.

I allmänhet har dataelementsredigeraren stöd för [val av lagringstid](https://experienceleague.adobe.com/en/docs/experience-platform/tags/ui/data-elements#create-a-data-element). Dataelement som använder tillägget för dynamiska medievyer stöder dock bara alternativet för lagringstid på **[!UICONTROL None]**. Det går att ange andra värden i användargränssnittet, men i det här fallet är dataelementets beteende inte definierat. Tillägget hanterar värdet på dataelementet separat: det dataelement som behåller värdet på visningsprogrammets händelseargument under hela visningsprogrammets livscykel.

### Regler i tillägget Dynamiska medievyer {#about-rules-in-the-dynamic-media-viewers-extension}

I regelredigeraren lägger tillägget till nya konfigurationsalternativ för händelseredigeraren. Redigeraren har också ett alternativ för att manuellt referera till händelseparametrar i Action Editor som ett kortvarigt alternativ i stället för att använda förkonfigurerade dataelement.

#### Om händelseredigeraren {#about-the-events-editor}

I händelseredigeraren lägger tillägget för dynamiska medievyer till **[!UICONTROL Event Type]** med namnet **[!UICONTROL Viewer Event]**.

När du väljer det här alternativet visas listrutan **[!UICONTROL Dynamic Media Viewer events]** i händelseredigeraren. Den innehåller alla händelser som stöds av visningsprogram för dynamiska media.

![image2019-8-2_15-13-1](assets/image2019-8-2_15-13-1.png)

#### Om funktionsmakroredigeraren {#about-the-actions-editor}

Med tillägget Dynamic Media Viewer kan du använda händelseparametrar för Dynamic Media-visningsprogram för att mappa till analysvariabler i Adobe Analytics-tilläggets Set Variables-redigerare.

Det enklaste sättet att göra detta är att slutföra följande tvåstegsprocess:

* Börja med att definiera ett eller flera dataelement, där varje dataelement representerar en parameter för en Dynamic Media Viewer-händelse.
* I redigeraren Ange variabler i Adobe Analytics-tillägget klickar du på ![Dataikonen, dataelementväljaren](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) **Dataelementväljaren** för att öppna dialogrutan Markera dataelement och klickar sedan på ett dataelement från den.

![image2019-7-10_20-41-52](assets/image2019-7-10_20-41-52.png)

Det är dock möjligt att använda en alternativ metod och åsidosätta skapande av dataelement. Du kan referera direkt till ett argument från en Dynamic Media Viewer-händelse. Ange det fullständiga, kvalificerade namnet på händelseargumentet i indatafältet **[!UICONTROL value]** i variabeltilldelningen för Analytics. Se till att procenttecken (%) omges. Exempel:

`%event.detail.dm.LOAD.asset%`

![image2019-7-12_19-2-35](assets/image2019-7-12_19-2-35.png)

Det finns en viktig skillnad mellan att använda dataelement och argumentreferens för direkt händelse. För dataelement spelar det ingen roll vilken händelse som utlöser åtgärden Ange variabler. Händelsen som utlöser regeln kan vara orelaterad till Dynamic Viewer (som att välja webbsidan från Core-tillägget). Men när du använder en referens för ett direkt argument är det viktigt att se till att händelsen som utlöser regeln motsvarar händelseargumentet som den refererar till.

Om till exempel händelsen **[!UICONTROL LOAD]** från tillägget Dynamic Media Viewer utlöser regeln returnerar referensen till `%event.detail.dm.LOAD.asset%` rätt resursnamn.

Det returnerar dock ett tomt värde för alla andra händelser.

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
   <td><code>BANNER</code><br /> </td>
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

Adobe rekommenderar att du granskar all dokumentation innan detta avsnitt så att du förstår den fullständiga integreringen.

I det här avsnittet beskrivs de konfigurationssteg som krävs för att integrera dynamiska medievyer med Adobe Analytics och Adobe Analytics för ljud och video. Även om det är möjligt att använda tillägget Dynamic Media Viewer för andra syften i Experience Platform Tags, beskrivs inte sådana scenarier i den här dokumentationen.

Du kommer att använda följande Adobe-produkter för att konfigurera din integrering:

* Adobe Analytics - används för att konfigurera spårningsvariabler och rapporter.
* Experience Platform-taggar - används för att definiera en egenskap, en eller flera regler och ett eller flera dataelement för att aktivera spårning av visningsprogram.

Om integrationslösningen används med Experience Manager Sites måste dessutom följande konfiguration göras:

* [Adobe Developer Console](https://developer.adobe.com/console/home) - integrering skapas för Experience Platform-taggar.
* Nod för Experience Manager-författare - IMS-konfiguration och Experience Platform Tags Cloud Configuration.

Som en del av konfigurationen bör du kontrollera att du har tillgång till ett företag i Adobe Experience Cloud som redan har Adobe Analytics- och Experience Platform-taggar aktiverade.

## Konfigurera Adobe Analytics för integreringen {#configuring-adobe-analytics-for-the-integration}

När du har konfigurerat Adobe Analytics konfigureras integreringen för följande:

* En rapportsvit finns på plats och har valts.
* Analysvariabler är tillgängliga för att ta emot spårningsdata.
* Det finns rapporter för att visa data som samlats in inifrån Adobe Analytics.

Se även [Implementeringshandbok för analyser](https://experienceleague.adobe.com/en/docs/analytics/implementation/home).

**Så här konfigurerar du Adobe Analytics för integreringen:**

1. Börja med att gå till Adobe Analytics från Experience Cloud [hemsida](https://experience.adobe.com/#/home). På menyraden klickar du på ikonen ![Appar, lösningar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Apps_18_N.svg) **Lösningar** i det övre högra hörnet av sidan och väljer sedan **[!UICONTROL Analytics]**.

   ![2019-07-22_18-08-47](assets/2019-07-22_18-08-47.png)

   Välj en rapportsvit.

### Välj en rapportsvit {#selecting-a-report-suite}

1. I det övre högra hörnet av Adobe Analytics-sidan, till höger om fältet **[!UICONTROL Search Reports]**, väljer du rätt rapportsvit i listrutan. Om det finns flera rapportsviter tillgängliga och du är osäker på vilken du ska använda ber du om hjälp. Din Adobe Analytics-administratör kan vägleda dig när du väljer lämplig rapportserie.

   I exemplet nedan skapade en användare en rapportserie med namnet *DynamicMediaViewersExtensionDoc* och markerade den i listrutan. Rapportsvitens namn är endast ett exempel. Namnet på den rapportsvit du väljer är upp till dig.

   Om ingen rapportsvit är tillgänglig måste du eller Adobe Analytics-administratören skapa en innan du kan fortsätta med konfigurationen.

   Se [Rapporter och rapportsviter](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/report-suites-admin) och [Skapa en rapportsvit](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/c-new-report-suite/t-create-a-report-suite).

   I Adobe Analytics hanteras rapportsviter under **[!UICONTROL Admin]** > **[!UICONTROL Report Suites]**.

   ![2019-07-22_18-09-49](assets/2019-07-22_18-09-49.png)

   Konfigurera Adobe Analytics-variabler.

### Ställa in Adobe Analytics-variabler {#setting-up-adobe-analytics-variables}

1. Ange en eller flera Adobe Analytics-variabler som du vill använda för att spåra beteendet hos dynamiska medievisningsprogram på webbsidan.

   Du kan använda alla variabeltyper som stöds av Adobe Analytics. Din Analytics-implementering måste avgöra lämplig variabeltyp, till exempel Anpassad trafik (`props`) eller Konvertering (`eVar`).

   Se [Översikt över utkast och eVars](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/page-vars/evar#vars).

   I den här dokumentationen används endast en anpassad trafikvariabel (props) eftersom de blir tillgängliga i en analysrapport inom några minuter efter att en åtgärd har utförts på en webbsida.

   Om du vill aktivera en ny anpassad trafikvariabel går du till **[!UICONTROL Admin]** > **[!UICONTROL Report Suites]** i verktygsfältet i Adobe Analytics.

1. Välj rätt rapport på sidan **[!UICONTROL Report Suite Manager]**.
1. Klicka på **[!UICONTROL Edit Settings]** > **[!UICONTROL Traffic]** > **[!UICONTROL Traffic Variables]** i verktygsfältet.
1. Välj en variabel som inte används, ge den ett beskrivande namn (**[!UICONTROL Viewer asset (prop 30)]**) och ändra sedan kombinationsrutan till Aktiverad i kolumnen Aktiverad.

   Följande skärmbild är ett exempel på en anpassad trafikvariabel (**[!UICONTROL prop30]**) för att spåra ett resursnamn som används av visningsprogrammet:

   ![image2019-6-26_23-6-59](/help/assets/dynamic-media/assets/image2019-6-26_23-6-59.png)

1. Klicka på **[!UICONTROL Save]** längst ned i variabellistan.

### Konfigurera en rapport {#setting-up-a-report}

Vanligtvis styr specifika projektbehov hur du skapar en rapport i Adobe Analytics. Därför ligger en detaljerad rapportkonfiguration utanför omfånget för den här integreringen.

Det räcker dock att känna till att rapporter om anpassad trafik automatiskt blir tillgängliga i Adobe Analytics när du har konfigurerat anpassade trafikvariabler i **[Konfigurera Adobe Analytics-variabler](#setting-up-adobe-analytics-variables)**.

Rapporten för variabeln **[!UICONTROL Viewer asset (prop 30)]** är till exempel tillgänglig på menyn Rapporter under **[!UICONTROL Custom Traffic]** > **[!UICONTROL Custom Traffic 21-30]** > **[!UICONTROL Viewer asset (prop 30)]**.

Inga data visas när du besöker den här rapporten direkt efter att **[!UICONTROL Viewer asset (prop 30)]** har skapats, vilket är som väntat vid den här tidpunkten i integreringen.

![image2019-6-26_23-12-49](/help/assets/dynamic-media/assets/image2019-6-26_23-12-49.png)

## Konfigurera Experience Platform-taggar för integreringen {#configuring-adobe-launch-for-the-integration}

När du har konfigurerat Experience Platform Tags ställs följande objekt in för integreringen:

* Skapandet av en ny egenskap som håller ihop alla dina konfigurationer.
* Installation och installation av tillägg. Klientkoden för alla tillägg som är installerade i egenskapen kompileras tillsammans till ett bibliotek. Det här biblioteket används av webbsidan senare.
* Konfiguration av dataelement och regler. Den här konfigurationen definierar vilka data som ska hämtas från de dynamiska medievyn, när spårningslogiken ska utlösas och var data ska skickas i Adobe Analytics.
* Publicering av biblioteket.

**Så här konfigurerar du Experience Platform-taggar för integreringen:**

1. Börja med att gå till Experience Platform-taggar från Experience Cloud [hemsida](https://experience.adobe.com/#/home). Klicka på ikonen ![Appar, lösningar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Apps_18_N.svg) **Lösningar** i det övre högra hörnet av sidan på menyraden och klicka sedan på **[!UICONTROL Tags]**.

   ![image2019-7-8_15-38-44](assets/image2019-7-8_15-38-44.png)

### Skapa en egenskap i Experience Platform Tags {#creating-a-property-in-adobe-launch}

En egenskap i Experience Platform Tags är en namngiven konfiguration som håller ihop alla inställningar. Ett bibliotek med konfigurationsinställningarna genereras och publiceras på olika miljönivåer (utveckling, mellanlagring och produktion).

Se även [Konfigurera en markeringsegenskap](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/initial-configuration/configure-tags).

**Så här skapar du en egenskap i Experience Platform-taggar:**

1. Klicka på **[!UICONTROL New Property]** i Experience Platform Tags.
1. I dialogrutan **[!UICONTROL Create Property]** anger du ett beskrivande namn, till exempel webbplatsens titel, i fältet **[!UICONTROL Name]**. Exempel: `DynamicMediaViewersProp.`
1. Ange webbplatsens domän i fältet **[!UICONTROL Domains]**.
1. Aktivera **[!UICONTROL Configure for extension development (cannot be modified later)]** i listrutan **[!UICONTROL Advanced Options]** om det tillägg som du vill använda - i det här fallet *Dynamiska mediavisare* - inte har släppts än.

   ![image2019-7-8_16-3-47](assets/image2019-7-8_16-3-47.png)

1. Välj **[!UICONTROL Save]**.

   Välj den skapade egenskapen och gå sedan vidare till *Installation och konfiguration av tillägg*.

### Installera och konfigurera tillägg {#installing-and-setup-of-extensions}

Alla tillgängliga tillägg i Experience Platform-taggar visas under **[!UICONTROL Extensions]** > **[!UICONTROL Catalog]**.

Klicka på **[!UICONTROL Install]** om du vill installera ett tillägg. Utför vid behov en engångskonfiguration och klicka sedan på **[!UICONTROL Save]**.

Om det behövs måste följande tillägg installeras och konfigureras:

* (Obligatoriskt) *Tillägget Experience Cloud ID Service*

Ingen ytterligare konfiguration behövs, förutom föreslagna värden. Klicka på **[!UICONTROL Save]** när du är klar.

Se [Experience Cloud Identity Service-tillägg](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/client/id-service/overview).

* (Obligatoriskt) *Adobe Analytics*-tillägg

Om du vill konfigurera det här tillägget måste du ha det Report Suite-ID som finns i Adobe Analytics, under **[!UICONTROL Admin]** > **[!UICONTROL Report Suite]**, under kolumnrubriken **[!UICONTROL Report Suite ID]**.

(Endast i demonstrationssyfte används rapportsvitens-ID **[!UICONTROL DynamicMediaViewersExtensionDoc]** i följande skärmbilder. Detta ID skapades och användes tidigare när du [valde en rapportsvit](#selecting-a-report-suite).)

![image2019-7-8_16-45-34](assets/image2019-7-8_16-45-34.png)

På sidan Installera tillägg anger du rapportsvits-ID:t i fälten **[!UICONTROL Development Report Suites]**, **[!UICONTROL Staging Report Suites]** och **[!UICONTROL Production Report Suites]**.

![image2019-7-8_16-47-40](assets/image2019-7-8_16-47-40.png)

*Konfigurera endast följande objekt om du tänker använda videospårning:*

Expandera **[!UICONTROL General]** på sidan **[!UICONTROL Install Extension]** och ange sedan spårningsservern. Spårningsservern följer mallen `<trackingNamespace>.sc.omtrdc.net`, där `<trackingNamespace>` är den information som hämtas i e-postmeddelandet om etablering.

Välj **[!UICONTROL Save]**.

Se [Adobe Analytics-tillägg](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/client/analytics/overview).

* (Valfritt. Krävs endast om videospårning behövs) *Adobe Media Analytics för ljud och video*-tillägg

Fyll i spårningsserverfältet. Spårningsservern för tillägget *Adobe Media Analytics för ljud och video* skiljer sig från spårningsservern som används för Adobe Analytics. Det följer mallen `<trackingNamespace>.hb.omtrdc.net`, där `<trackingNamespace>` är informationen från e-postmeddelandet om etablering.

Alla andra fält är valfria.

Se [Adobe Media Analytics för ljud- och videotillägg](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/client/media-analytics/overview).

* (Obligatoriskt) Tillägget *Dynamiska medievisningsprogram*

Välj **[!UICONTROL enable Adobe Analytics for Video]** om du vill aktivera (starta) spårning av pulsslag för video.

Från och med den här skrivningen är tillägget *Dynamiska medievisningsprogram* bara tillgängligt om Experience Platform Tags Property har skapats för utveckling.

Se [Skapa en egenskap i Experience Platform-taggar](#creating-a-property-in-adobe-launch).

När tilläggen har installerats och konfigurerats visas minst följande fem tillägg (fyra om du inte spårar video) under Tillägg > Installerat.

![image2019-7-22_12-7-36](assets/image2019-7-22_12-7-36.png)

### Ställ in dataelement och regler {#setting-up-data-elements-and-rules}

I Experience Platform Tags skapar du dataelement och regler som behövs för att spåra visare för dynamiska media.

Se [Hur data- och händelsespårning fungerar i integreringen](#how-data-and-event-tracking-works-in-the-integration) för en översikt över spårning med Experience Platform-taggar.

Se [Exempelkonfiguration](#sample-configuration) för en exempelkonfiguration i Experience Platform Tags som visar hur du spårar ett resursnamn när visningsprogrammet läses in.

Se [Konfigurera tillägget för dynamiska mediavisare](#configuring-the-dynamic-media-viewers-extension) för detaljerad information om tilläggets funktioner.

### Publicera ett bibliotek {#publishing-a-library}

Om du vill ändra konfigurationen för Experience Platform-taggar (inklusive inställningar för egenskaper, tillägg, regler och dataelement) måste du *publicera* sådana ändringar. Publicering i Experience Platform-taggar utförs från fliken Publicering under egenskapskonfigurationen.

Experience Platform Tags kan ha flera utvecklingsmiljöer, en mellanlagringsmiljö och en produktionsmiljö. Som standard pekar Experience Platform Tags Cloud Configuration i Experience Manager på Experience Manager författarnoden mot Stage-miljön för plattformstaggar. Experience Manager publiceringsnod pekar på produktionsmiljön i Experience Platform Tags. Detta innebär att med standardinställningarna för Experience Manager måste du publicera Experience Platform Tags-biblioteket till mellanlagringsmiljön. Om du gör det kan du använda det i redigeringsläge i Experience Manager. Du kan sedan publicera den i produktionsmiljön så att den kan användas i Experience Manager-publicering.

Mer information om Experience Platform Tags-miljöer finns i [Miljö](https://experienceleague.adobe.com/en/docs/experience-platform/tags/publish/environments/environments).

Publicering av ett bibliotek omfattar följande två steg:

* Lägga till och skapa ett nytt bibliotek genom att inkludera alla nödvändiga ändringar (nya och uppdateringar) i biblioteket.
* Flytta upp biblioteket genom de olika miljönivåerna (från utveckling till mellanlagring och produktion).

#### Lägga till och skapa ett nytt bibliotek {#adding-and-building-a-new-library}

1. Första gången du öppnar fliken Publicera i Experience Platform Tags är bibliotekslistan tom.

   Klicka på **[!UICONTROL Add New Library]** i den vänstra kolumnen.

   ![image2019-7-15_14-43-17](assets/image2019-7-15_14-43-17.png)

1. På sidan Skapa nytt bibliotek anger du det beskrivande namnet för det nya biblioteket i fältet **[!UICONTROL Name]**. Exempel:

   *DynamicMediaViewersLib*

   Välj miljönivå i listrutan Miljö. Till att börja med är bara utvecklingsnivån tillgänglig för val. Klicka på **[!UICONTROL Add All Changed Resources]** i sidans nedre vänstra hörn.

   ![image2019-7-15_14-49-41](assets/image2019-7-15_14-49-41.png)

1. Klicka på **[!UICONTROL Save & Build for Development]** i det övre högra hörnet på sidan.

   Om några minuter är biblioteket klart att användas.

   ![image2019-7-15_15-3-34](assets/image2019-7-15_15-3-34.png)

   >[!NOTE]
   >
   >Nästa gång du ändrar konfigurationen för Experience Platform-taggar går du till fliken **[!UICONTROL Publishing]** under konfigurationen för **[!UICONTROL Property]** och väljer sedan det bibliotek du skapat tidigare.
   >
   >
   >Klicka på **[!UICONTROL Add All Changed Resources]** på bibliotekets publiceringsskärm och sedan på **[!UICONTROL Save & Build for Development]**.

#### Flytta upp ett bibliotek via miljönivåer {#moving-a-library-up-through-environment-levels}

1. När ett nytt bibliotek har lagts till finns det i utvecklingsmiljön. Om du vill flytta den till nivån Mellanlagringsmiljö (som motsvarar kolumnen Skickat) går du till bibliotekets nedrullningsbara meny och klickar på **[!UICONTROL Submit for Approval]**.

   ![image2019-7-15_15-52-37](assets/image2019-7-15_15-52-37.png)

1. Klicka på **[!UICONTROL Submit]** i bekräftelsedialogrutan.

   När biblioteket har flyttats till kolumnen Skickat klickar du på **[!UICONTROL Build for Staging]** på bibliotekets nedrullningsbara meny.

   ![image2019-7-15_15-54-37](assets/image2019-7-15_15-54-37.png)

1. Om du vill flytta biblioteket från mellanlagringsmiljön till produktionsmiljön (kolumnen Publicerad) följer du en liknande process.

   Klicka först på **[!UICONTROL Approve for Publishing]** i listrutan.

   ![image2019-7-15_16-7-39](assets/image2019-7-15_16-7-39.png)

1. Klicka på **[!UICONTROL Build & Publish to Production]** i listrutan.

   ![image2019-7-15_16-8-9](assets/image2019-7-15_16-8-9.png)

   Mer information om publiceringsprocessen i Experience Platform Tags finns i [Publicera](https://experienceleague.adobe.com/en/docs/experience-platform/tags/publish/overview).

## Konfigurera Adobe Experience Manager för integreringen {#configuring-adobe-experience-manager-for-the-integration}

<!-- Prerequisites list below should be verified by Sasha -->

Förutsättningar:

* Experience Manager kör både redigeringsläget och publiceringsläget.
* Experience Manager-författarnod är konfigurerad i Dynamic Media. <!-- Scene7 run mode (dynamicmedia_s7) -->
* Dynamic Media WCM-komponenter är aktiverade i Experience Manager Sites.

Experience Manager-konfigurationen består av följande två huvudsteg:

* Konfiguration av Experience Manager IMS.
* Konfiguration av Experience Platform Tags Cloud.

### Konfigurera Experience Manager IMS {#configuring-aem-ims}

1. I Experience Manager-författaren klickar du på ikonen ![Hammer, verktyg](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Hammer_18_N.svg) **Verktyg** och sedan på **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**.

   ![2019-07-25_11-52-58](assets/2019-07-25_11-52-58.png)

1. Klicka på **[!UICONTROL Create]** i det övre vänstra hörnet på konfigurationssidan för Adobe IMC.
1. På sidan **[!UICONTROL Adobe IMS Technical Account Configuration]** går du till listrutan **[!UICONTROL Cloud Solution]** och klickar på **[!UICONTROL Experience Platform Data Collection]**.
1. Aktivera **[!UICONTROL Create new certificate]** och ange sedan ett meningsfullt värde för certifikatet i textfältet. Exempel: *AdobeLaunchIMSCert*. Klicka på **[!UICONTROL Create certificate]**.

   Följande informationsmeddelande visas:

   *Om du vill hämta en giltig åtkomsttoken måste det nya certifikatets offentliga nyckel läggas till i det tekniska kontot på Adobe Developer!*

   Klicka på **[!UICONTROL OK]** om du vill stänga dialogrutan Info.

   ![2019-07-25_12-09-24](assets/2019-07-25_12-09-24.png)

1. Välj **[!UICONTROL Download Public Key]** om du vill hämta en offentlig nyckelfil (`*.crt`) till ditt lokala system.

   >[!NOTE]
   >
   >***lämna sidan*** öppen **[!UICONTROL Adobe IMS Technical Account Configuration]** i det här läget. ***stäng inte*** sidan och ***klicka inte*** **[!UICONTROL Next]** i det här läget. Du kommer att gå tillbaka till den här sidan senare i stegen.

   ![2019-07-25_12-52-24](assets/2019-07-25_12-52-24.png)

1. Gå till [Adobe Developer Console](https://developer.adobe.com/console/integrations) på en ny flik i webbläsaren.

1. Klicka på **[!UICONTROL New integration]** på sidan **[!UICONTROL Adobe Developer Console Integrations]** i det övre högra hörnet.
1. I dialogrutan **[!UICONTROL Create a new integration]** kontrollerar du att alternativknappen **[!UICONTROL Access an API]** är markerad och sedan klickar du på **[!UICONTROL Continue]**.

   ![2019-07-25_13-04-20](assets/2019-07-25_13-04-20.png)

1. På den andra **[!UICONTROL Create a new integration]**-sidan aktiverar du (sätter på) alternativknappen **[!UICONTROL Experience Platform Tags API]**. I sidans nedre högra hörn klickar du på **[!UICONTROL Continue]**.

   ![2019-07-25_13-13-54](assets/2019-07-25_13-13-54.png)

1. Gör följande på den tredje **[!UICONTROL Create a new integration]**-sidan:

   * Ange ett beskrivande namn i fältet **[!UICONTROL Name]**. Exempel: *DynamicMediaViewersIO*.

   * I fältet **[!UICONTROL Description]** anger du en beskrivning för integreringen.

   * I området **[!UICONTROL Public key certificates]** överför du filen med den offentliga nyckeln (`*.crt`) som du laddade ned tidigare i dessa steg.

   * Klicka på **[!UICONTROL Admin]** under rubriken **[!UICONTROL Select a role for Experience Platform Tags API]**.

   * Välj produktprofilen **[!UICONTROL Tags - <your_company_name>]** under rubriken **[!UICONTROL Select one or more product profiles for Experience Platform Tags API]**.

   ![2019-07-25_13-49-18](assets/2019-07-25_13-49-18.png)

1. Välj **[!UICONTROL Create integration]**.
1. Klicka på **[!UICONTROL Continue to integration details]** på sidan **[!UICONTROL Integration created]**.

   ![2019-07-25_14-16-33](assets/2019-07-25_14-16-33.png)

1. En integreringsinformationssida visas, som i följande exempel:

   >[!NOTE]
   >
   >***Låt den här sidan med integreringsinformation vara öppen.*** Du kommer att behöva olika uppgifter från flikarna **[!UICONTROL Overview]** och **[!UICONTROL JWT]** om bara ett ögonblick.

   ![2019-07-25_14-35-30](assets/2019-07-25_14-35-30.png)
   *Sidan med integreringsinformation*

1. Gå tillbaka till sidan **[!UICONTROL Adobe IMS Technical Account Configuration]** som du öppnade tidigare. Klicka på **[!UICONTROL Next]** i det övre högra hörnet av sidan för att öppna sidan **[!UICONTROL Account]** i fönstret **[!UICONTROL Adobe IMS Technical Account Configuration]**.

   (Om du stängde sidan tidigare går du tillbaka till Experience Manager-författaren och går till **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**. Välj **[!UICONTROL Create]**. Klicka på **[!UICONTROL Experience Platform Tags]** i listrutan **[!UICONTROL Cloud Solution]**. Klicka på namnet på det certifikat som skapades tidigare i listrutan **[!UICONTROL Certificate]**.

   ![2019-07-25_20-57-50](assets/2019-07-25_20-57-50.png)
   *Adobe IMS Technical Account Configuration - certifikatsida*

1. Sidan **[!UICONTROL Account]** innehåller fem fält som kräver att du fyller i med information från sidan Integreringsinformation från föregående steg.

   ![2019-07-25_20-42-45](assets/2019-07-25_20-42-45.png)
   *Adobe IMS Technical Account Configuration - kontosida*

1. På sidan **[!UICONTROL Account]** fyller du i följande fält:

   * **[!UICONTROL Title]** - Ange en beskrivande kontotitel.
   * **[!UICONTROL Authorization Server]** - Återgå till sidan Integreringsinformation som du öppnade tidigare. Välj fliken **[!UICONTROL JWT]**. Kopiera servernamnet - utan sökvägen - enligt markeringen nedan.

   Gå tillbaka till sidan **[!UICONTROL Account]** och klistra sedan in namnet i respektive fält.
Exempel: `https://ims-na1.adobelogin.com/`
(exempelservernamnet är endast avsett för förklaringar)

   ![2019-07-25_15-01-53](assets/2019-07-25_15-01-53.png)
   *Detaljsida för integrering - JWT-flik*

1. **[!UICONTROL API Key]** – Gå tillbaka till sidan med integreringsinformation. Välj fliken **[!UICONTROL Overview]** och klicka sedan på **[!UICONTROL Copy]** till höger om fältet **[!UICONTROL API Key (Client ID)]**.

   Gå tillbaka till sidan **[!UICONTROL Account]** och klistra sedan in nyckeln i respektive fält.

   ![2019-07-25_14-35-333](assets/2019-07-25_14-35-333.png)
   *Sidan med integreringsinformation*

1. **[!UICONTROL Client Secret]**– Gå tillbaka till sidan med integreringsinformation. Klicka på **[!UICONTROL Retrieve Client Secret]** på fliken **[!UICONTROL Overview]**. Till höger om fältet **[!UICONTROL Client secret]** klickar du på **[!UICONTROL Copy]**.

   Gå tillbaka till sidan **[!UICONTROL Account]** och klistra sedan in nyckeln i respektive fält.

1. **[!UICONTROL Payload]** – Gå tillbaka till sidan med integreringsinformation. Kopiera hela JSON-objektkoden från fliken **[!UICONTROL JWT]** i fältet JWT-nyttolast.

   Gå tillbaka till sidan **[!UICONTROL Account]** och klistra sedan in koden i respektive fält.

   ![2019-07-25_21-59-12](assets/2019-07-25_21-59-12.png)
   *Sidan Integrationsinformation - JWT-flik*

   Kontosidan, med alla fält ifyllda, ser ut ungefär så här:

   ![2019-07-25_22-08-30](assets/2019-07-25_22-08-30.png)

1. Klicka på **[!UICONTROL Create]** i det övre högra hörnet på sidan **[!UICONTROL Account]**.

   När Experience Manager IMS är konfigurerat har du nu ett nytt IMSAccount som visas under **[!UICONTROL Adobe IMS Configurations]**.

   ![image2019-7-15_14-17-54](assets/image2019-7-15_14-17-54.png)

## Konfigurera Experience Platform Tags Cloud för integrering {#configuring-adobe-launch-cloud-for-the-integration}

1. Klicka på ikonen ![Hammer, verktygen](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Hammer_18_N.svg) **Verktyg** i det övre vänstra hörnet i Experience Manager-redigeringsläget och gå sedan till **[!UICONTROL Cloud Services]** > **[!UICONTROL Experience Platform Tags Configurations]**.

   ![2019-07-26_12-10-38](assets/2019-07-26_12-10-38.png)

1. På sidan **[!UICONTROL Experience Platform Tags Configurations]** i den vänstra panelen väljer du en Experience Manager-webbplats som du vill använda Experience Platform Tags Configuration för.

   **`We.Retail`**-platsen är endast vald som exempel i skärmbilden nedan.

   ![2019-07-26_12-20-06](assets/2019-07-26_12-20-06.png)

1. Klicka på **[!UICONTROL Create]** i det övre vänstra hörnet av sidan.
1. På sidan **[!UICONTROL General]** (sida 1/3) i fönstret **[!UICONTROL Create Experience Platform Tags Configuration]** fyller du i följande fält:

   * **[!UICONTROL Title]** - Ange en beskrivande konfigurationstitel. Exempel: `We.Retail Tags cloud configuration`.

   * **[!UICONTROL Associated Adobe IMS Configuration]** - Välj den IMS-konfiguration som du skapade tidigare i [Konfigurera Experience Manager IMS](#configuring-aem-ims).

   * **[!UICONTROL Company]** - I listrutan **[!UICONTROL Company]** väljer du ditt Experience Cloud-företag. Listan fylls i automatiskt.

   * **[!UICONTROL Property]** - I listrutan Egenskaper väljer du egenskapen Experience Platform Tags som du skapade tidigare. Listan fylls i automatiskt.

   När du har fyllt i alla fält ser sidan **[!UICONTROL General]** ut ungefär så här:

   ![image2019-7-15_14-34-23](assets/image2019-7-15_14-34-23.png)

1. Klicka på **[!UICONTROL Next]** i det övre vänstra hörnet.
1. På sidan **[!UICONTROL Staging]** (sida 2/3) i fönstret **[!UICONTROL Create Experience Platform Tags Configuration]** fyller du i följande fält:

   Kontrollera platsen för mellanlagringsversionen av ditt Experience Platform Tags-bibliotek i fältet **[!UICONTROL Library URI]** (Uniform Resource Identifier). Experience Manager fyller i detta fält automatiskt.

   I det här steget används endast bibliotek för Experience Platform-taggar som distribueras till Adobe CDN.

   >[!NOTE]
   >
   >Kontrollera att den automatiskt ifyllda biblioteks-URI:n (Uniform Resource Identifier) är korrekt formaterad. Om det behövs kan du åtgärda det så att URI:n representerar en protokollrelativ URI. Det vill säga, det börjar med ett dubbelt snedstreck.
   >
   >
   >Till exempel: `//assets.adobetm.com/launch-xxxx`.

   Sidan **[!UICONTROL Staging]** ser förmodligen ut ungefär så här. Alternativen **[!UICONTROL Archive]** och **[!UICONTROL Load Library Asynchronously]** är ***inte*** angivna:

   ![image2019-7-15_15-21-8](assets/image2019-7-15_15-21-8.png)

1. Klicka på **[!UICONTROL Next]** i det övre högra hörnet.
1. På sidan **[!UICONTROL Production]** (sida 3/3) i fönstret **[!UICONTROL Create Experience Platform Tags Configuration]** korrigerar du (vid behov) den automatiskt ifyllda produktions-URI:n på samma sätt som på föregående **[!UICONTROL Staging]**-sida.
1. Klicka på **[!UICONTROL Create]** i det övre högra hörnet.

   Din nya Experience Platform Tags Cloud-konfiguration skapas och visas bredvid din webbplats.

1. Markera din nya Experience Platform Tags Cloud-konfiguration (en bockmarkering visas till vänster om konfigurationstiteln när den har valts). Klicka på **[!UICONTROL Publish]** i verktygsfältet.

   ![image2019-7-15_15-47-6](assets/image2019-7-15_15-47-6.png)

För närvarande stöder inte Experience Manager-författare integrering av dynamiska medievyer med Experience Platform-taggar.

Det stöds dock i Experience Manager publiceringsnod. Med standardinställningarna för Experience Platform Tags Cloud Configuration används produktionsmiljön för Experience Platform Tags i Experience Manager-publiceringen. Därför måste Experience Platform Tags Library-uppdateringarna från Development till Production Environment varje gång under testet skickas.

Det är möjligt att kringgå denna begränsning. Ange utvecklings- eller mellanlagrings-URL:en för Experience Platform Tags-biblioteket i Experience Platform Tags Cloud Configuration för Experience Manager ovan. När du gör det använder Experience Manager publiceringsnod utvecklings- eller mellanlagringsversionen av Experience Platform Tags-biblioteket.

Mer information om hur du konfigurerar Experience Platform Tags Cloud finns i [Integrera Experience Platform-taggar och Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-learn/sites/integrations/experience-platform-data-collection-tags/overview#integrations) .
