---
title: Arbeta med 3D-resurser i Dynamic Media
seo-title: Arbeta med 3D-resurser i Dynamic Media
description: Lär dig hur du arbetar med 3D-resurser i Dynamic Media
seo-description: Lär dig hur du arbetar med 3D-resurser i Dynamic Media
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS and AEM as a Cloud Service
topic-tags: introduction
content-type: reference
translation-type: tm+mt
source-git-commit: bc0852120580065a93923e7fe730485012afba6e
workflow-type: tm+mt
source-wordcount: '2061'
ht-degree: 1%

---


# Arbeta med 3D-resurser i Dynamic Media {#working-with-three-d-assets-dm}

Med Dynamic Media kan du överföra, hantera, visa och leverera 3D-resurser som engagerande upplevelser.

* Publicera 3D-bilder med ett klick (med **[!UICONTROL Quick Publish]** i verktygsfältet) för att generera webbadressen.
* Optimerat stöd för 3D-material med den högkvalitativa, interaktiva Dimensional-visningsförinställningen som bygger på Adobe Dimension. Visningsförinställningen innehåller bland annat en samling interaktiva kamerakontroller som du kan använda för att rotera, zooma och panorera.
* Med 3D Media WCM-komponenten kan du enkelt lägga till 3D-resurser på dina AEM Sites-sidor.

Det finns ingen installation eller konfiguration av något slag för att använda 3D-resurser i Dynamic Media.

![sko i 3d](/help/assets/dynamic-media/assets/3d-dimensional-viewer-quickpublish-url-embed2.png)

<!-- See also [Dynamic Media 3D Release Notes](/help/release-notes/aem3d-release-notes.md). -->

## 3D-filformat som stöds i Dynamic Media {#supported-three-d-file-formats-in-dm}

Dynamic Media har stöd för följande 3D-filformat:

| 3D-filtillägg | Filformat | MIME-typ | Anteckningar |
|---|---|---|---|
| GLB | Binär GL-överföring | model/gltf-binary | Inkluderar texturerna med resursen i stället för att referera till dem som externa bilder. |
| OBJ | WaveFront 3D-objektfil | application/x-tgif |  |
| STL | Stereolitografi | application/vnd.ms-pki.stl |  |
| USDZ | Zip-arkiv för universell scenbeskrivning | model/vnd.usdz+zip | *Stöd endast för förtäring. ingen visning eller interaktion är tillgänglig.* USDZ är Apples egna 3D-format som endast kan läsas av Safari eller iOS. |

## Snabbstart: 3D-resurser i Dynamic Media {#quick-start-three-d}

Följande steg-för-steg-beskrivning av arbetsflödet hjälper dig att komma igång snabbt med 3D-resurser i Dynamic Media.

Innan du arbetar med 3D-resurser i Dynamic Media måste du kontrollera att AEM-administratören redan har aktiverat och konfigurerat Dynamic Media Cloud Services.

Se [Konfigurera Dynamic Media Cloud-tjänster](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services).

1. **Överför 3D-resurser**

   * [Överföra dina 3D-resurser för användning i Dynamic Media](/help/assets/add-assets.md#upload-assets).
   * [3D-filformat som stöds för överföring i Dynamic Media](#supported-three-d-file-formats-in-dm).

1. **Hantera 3D-resurser**

   * Ordna och söka i 3D-resurser

      * [Organisera digitalt material](/help/assets/organize-assets.md).
      * [Söka efter 3D-resurser](/help/assets/search-assets.md).
   * Visa 3D-resurser

      * [Visa och interagera med 3D-resurser](#viewing-three-d-assets).
      * [Hantera visningsförinställningen](/help/assets/dynamic-media/managing-viewer-presets.md)för Dimensional.
   * Arbeta med metadata för 3D-resurser

      * [Hantera metadata för digitala resurser](/help/assets/manage-digital-assets.md#editing-properties).
      * [Metadata-scheman](/help/assets/metadata-schemas.md).



1. **Publicera 3D-resurser**

   * [Publicera 3D-resurser för dynamiska media](#publishing-three-d-assets)

## Visa och interagera med 3D-resurser {#viewing-three-d-assets}

I det här avsnittet beskrivs hur du visar och interagerar med 3D-resurser på två olika sätt: från sidan med resursinformation och från 3D-mediekomponenten i Sites.

Det interaktiva 3D-visningsprogrammet innehåller bland annat en samling interaktiva kamerakontroller där du kan omforma, zooma och panorera 3D-resursen.

Tänk på att den tid det tar att öppna en 3D-resurs i vyn Resursinformation beror på flera faktorer. Bland dessa faktorer finns följande:

* Bandbredd till servern.
* Latenser till servern
* Bildens komplexitet.

Dessutom är funktioner i klientdatorn, t.ex. en arbetsstation, bärbar dator eller en mobil pekenhet, också viktiga att tänka på när du manipulerar kameran interaktivt. Ett relativt kraftfullt system med bra grafikfunktioner kan göra den interaktiva 3D-visningen smidigare och mer gynnsam.

>[!TIP]
>
>Du kan öppna Dimensional Viewer-förinställningen i Viewer Preset Editor för att öva på att navigera i en 3D-resurs utan att först behöva överföra några 3D-filer. Förinställningen för Dimensional Viewer har en inbyggd 3D-resurs som du kan interagera med.
>
>Se [Hantera visningsförinställningar](/help/assets/dynamic-media/managing-viewer-presets.md).

## Visa och interagera med en 3D-resurs från sidan med resursinformation {#viewing-three-d-assets-from-asset-details-page}

Se även [Förhandsgranska resurser i programgränssnittet](/help/assets/dynamic-media/previewing-assets.md).

**Visa och interagera med en 3D-resurs från sidan med resursinformation**

1. Kontrollera att du har överfört 3D-resurser till AEM.

   Se [Överföra dina 3D-resurser för användning i Dynamic Media](/help/assets/add-assets.md#upload-assets).

1. Tryck på AEM på **[!UICONTROL Navigation]** sidan **[!UICONTROL Assets > Files]**.
1. Near the upper-right corner of the page, from the **[!UICONTROL View]** drop-down list, tap **[!UICONTROL Card View]**.
1. Navigera till en 3D-resurs som du vill visa.
1. Tryck på 3D-resursens kort för att öppna den på sidan med resursinformation.
1. Gör något av följande på informationssidan för 3D-resursen:

   * **Vrid kameran** - Du kan rotera vyn runt 3D-scenen och objekten.
      * _Mus_: Vänsterklicka och dra.
      * _Pekskärm_: Tryck med ett finger och dra.
   * **Panorera kameran** - Panorera vyn åt vänster, åt höger, uppåt eller nedåt.
      * _Mus_: Högerklicka och dra.
      * _Pekskärm_: Tryck med två fingrar och dra.
   * **Zooma kameran** - Zooma kameran för att flytta in och ut i områden i 3D-scenen.
      * _Mus_: Rullningshjul.
      * _Pekskärm_: Nyp med två fingrar.
   * **Centrera kameran** igen - Centrera kameran igen till en punkt på ett objekt i 3D-scenen.
      * _Mus_: Dubbelklicka.
      * _Pekskärm_: Dubbeltryck.
   * **Återställ** - I närheten av det nedre högra hörnet av sidan trycker du på ikonen Återställ för att återställa vymålpunkten till mitten av 3D-resursen. Återställ flyttar också kameran närmare eller längre bort för att visa resursen i dess helhet och med en rimlig visningsstorlek.
   * **Helskärmsläge** - Tryck på ikonen Helskärm i det nedre högra hörnet av sidan för att öppna helskärmsläget.

1. I det övre högra hörnet av sidan trycker du på **[!UICONTROL Close]** för att gå tillbaka till sidan Resurser.

## Visa och interagera med en 3D-resurs inuti en 3D-mediekomponent {#interacting-with-asset-inside-three-d-media-component}

När en webbsida är i **[!UICONTROL Edit]** läge går det inte att interagera med en 3D-resurs. Om du vill göra resursen interaktiv kan du använda funktionen för att visa webbsidan i sidredigeraren med fullständig åtkomst till 3D Media-komponentens funktioner. **[!UICONTROL Preview]**

>[!IMPORTANT]
>
>Du kan bara utföra den här åtgärden när du har lagt till en 3D-mediekomponent på en webbsida och tilldelat en 3D-resurs till komponenten. Se [Lägga till 3D-mediekomponenten på en webbsida](#adding-the-three-d-media-component-to-a-web-page) och [Tilldela en 3D-resurs till en 3D-mediekomponent](#assigning-a-three-d-asset-to-the-component).

Se även [Förhandsgranska resurser i programgränssnittet](/help/assets/dynamic-media/previewing-assets.md).

**Visa och interagera med en 3D-resurs inuti en 3D-mediekomponent**

1. Gör något av följande när en webbsida är i **[!UICONTROL Edit]** läge:

   * Klicka i det övre högra hörnet på sidan för **[!UICONTROL Preview]** att gå in i **[!UICONTROL Preview]** läget.
   * Ta bort `/editor.html` från sidans URL i webbläsaren.
   ![3D-resurs som visas inuti 3D Media-komponenten](/help/assets/dynamic-media/assets/3d-asset-in-3d-media.png)En helt interaktiv 3D-resurs som visas i **[!UICONTROL Preview]** läget.

1. Gör något av följande när du är i **[!UICONTROL Preview]** läget:

   * **Vrid kameran** - Du kan rotera vyn runt 3D-scenen och objekten.
      * _Mus_: Vänsterklicka och dra.
      * _Pekskärm_: Tryck med ett finger och dra.
   * **Panorera kameran** - Panorera vyn åt vänster, åt höger, uppåt eller nedåt.
      * _Mus_: Högerklicka och dra.
      * _Pekskärm_: Tryck med två fingrar och dra.
   * **Zooma kameran** - Zooma kameran för att flytta in och ut i områden i 3D-scenen.
      * _Mus_: Rullningshjul.
      * _Pekskärm_: Nyp med två fingrar.
   * **Centrera kameran** igen - Centrera kameran igen till en punkt på ett objekt i 3D-scenen.
      * _Mus_: Dubbelklicka.
      * _Pekskärm_: Dubbeltryck.
   * **Återställ** - I närheten av det nedre högra hörnet av sidan trycker du på ikonen Återställ för att återställa vymålpunkten till mitten av 3D-resursen. Återställ flyttar också kameran närmare eller längre bort för att visa resursen i dess helhet och med en rimlig visningsstorlek.
   * **Helskärmsläge** - Tryck på ikonen Helskärm i det nedre högra hörnet av sidan för att öppna helskärmsläget.

## Arbeta med 3D Media-komponenten {#working-with-three-d-media-component}

Dynamic Media innehåller en 3D-mediakomponent för dynamiska media som du kan använda i AEM Sites för att aktivera interaktiv visning av 3D-modeller på dina webbsidor.

* [Lägga till komponenten 3D Media i sidmallen](#adding-three-d-media-component-to-page-template)
* [Lägga till komponenten 3D Media på en webbsida](#adding-the-three-d-media-component-to-a-web-page)
   * [Valfritt - Konfigurera komponenten 3D Media](#configuring-the-three-d-component)
* [Tilldela en 3D-resurs till 3D-mediekomponenten](#assigning-a-three-d-asset-to-the-component)


## Lägga till komponenten 3D Media i sidmallen {#adding-three-d-media-component-to-page-template}

1. Navigera till **[!UICONTROL Tools > General > Templates]**.
1. Navigera till den sidmall som du vill aktivera 3D-komponenten i och markera mallen.
1. Tryck **[!UICONTROL Edit]** för att öppna mallen.
1. I den nedrullningsbara menyn uppe till höger på sidan väljer du **[!UICONTROL Structure]** läge, om det inte redan är aktivt.

   ![3d-media-component-structure](/help/assets/dynamic-media/assets/3d-media-component-structure.png)

1. Tryck på ett tomt område i **[!UICONTROL Layout Container]** regionen för att markera det och öppna det tillhörande verktygsfältet.
1. Tryck på **[!UICONTROL Policy]** ikonen i verktygsfältet för att öppna **[!UICONTROL Policy Editor]**.
1. Bläddra till i **[!UICONTROL Properties]** avsnittet under **[!UICONTROL Allowed Components]** fliken **[!UICONTROL Dynamic Media]** och expandera sedan listan och markera **[!UICONTROL 3D Media]**.
1. Tryck **[!UICONTROL Done]** för att spara ändringarna och stänga **[!UICONTROL Policy Editor]**.

   Nu kan du placera komponenten Dynamic Media 3D Media på alla sidor som använder den här mallen.

## Lägga till komponenten 3D Media på en webbsida {#adding-the-three-d-media-component-to-a-web-page}

Om du använder Adobe Experience Manager som webbinnehållshanteringssystem kan du lägga till 3D-resurser på dina webbsidor med hjälp av 3D Media-komponenten.

See also [Adding Dynamic Media assets to pages](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

1. Öppna AEM Sites och välj den webbsida där du vill lägga till komponenten Dynamic Media 3D Media.
1. Tryck på **[!UICONTROL Edit]** pennikonen för att öppna sidan i sidredigeraren. Kontrollera att **[!UICONTROL Edit]** läget är markerat i sidans övre högra hörn.

   ![3d-media-component-add](/help/assets/dynamic-media/assets/3d-media-component-edit.png)

1. Tryck på ikonen för panelen Sida i verktygsfältet för att växla eller aktivera visningen av panelen.

1. I sidopanelen: tryck på plustecknet för att öppna **[!UICONTROL Components]** listan.

   ![3d-media-component-drag-drop](/help/assets/dynamic-media/assets/3d-assets-filter.png)

1. Dra **[!UICONTROL 3D Media]** komponenten från **[!UICONTROL Components]** listan till den plats på sidan där du vill att 3D-visningsprogrammet ska visas.

Nu kan du tilldela en 3D-resurs till komponenten.

Se [Tilldela en 3D-resurs till en 3D-mediekomponent](#assigning-a-three-d-asset-to-the-component).

### Valfritt - Konfigurera komponenten 3D Media {#configuring-the-three-d-component}

1. I sidredigeraren AEM Sites väljer du den **[!UICONTROL 3D Media Viewer]** komponent som du tidigare lade till på sidan.
1. Tryck på **[!UICONTROL Configuration]** ikonen (skiftnyckel) för att öppna dialogrutan för komponentkonfiguration.

   ![3d-media-component-config](/help/assets/dynamic-media/assets/3d-media-component-config.png)

1. I dialogrutan 3D-media i listrutan Visningsförinställning väljer du **[!UICONTROL Dimensional]** att tilldela visningsförinställningen Dimensional till komponenten.

   ![3d-media-component-edit-config](/help/assets/dynamic-media/assets/3d-media-component-edit-config.png)

1. Tryck på bockmarkeringen i det övre högra hörnet för att spara ändringarna.

## Tilldela en 3D-resurs till 3D-mediekomponenten {#assigning-a-three-d-asset-to-the-component}

När du har lagt till en 3D-mediekomponent på en webbsida kan du tilldela den en 3D-resurs.

Se [Lägga till komponenten 3D Media på en webbsida](#adding-the-three-d-media-component-to-a-web-page).

1. I sidredigeraren AEM Sites klickar du på **[!UICONTROL Assets]** ikonen för att öppna den **[!UICONTROL Assets]** i sidpanelen.
1. I listrutan väljer du **[!UICONTROL 3D]** att bara visa 3D-resursens filtyper.
1. På sidopanelen söker du efter eller bläddrar till den 3D-resurs som du vill visa på sidan som redigeras.
1. Dra 3D-resursen från resurspanelen och släpp den på den **[!UICONTROL 3D Media]** komponent som du tidigare lagt till på sidan.

   ![Tilldela 3d-resurs till 3d Media-komponent](/help/assets/dynamic-media/assets/3d-asset-add.png)

>[!NOTE]
>
>När en webbsida är i AEM Sites- **[!UICONTROL Edit]** läge visar 3D-mediekomponenten 3D-resursen, men det går inte att interagera med resursen. Om du vill göra resursen interaktiv kan du använda funktionen för att visa webbsidan i sidredigeraren med fullständig åtkomst till 3D Media-komponentens funktioner. **[!UICONTROL Preview]**

## Publishing Dynamic Media 3D assets {#publishing-three-d-assets}

Dynamic Media kan hantera en mängd olika 3D-filformat som stöds som *statiskt innehåll* i Dynamic Media. Statiskt innehåll innebär att du kan överföra och publicera 3D-resurser, men det finns inget stöd för *dynamisk* bildåtergivning eller bildåtergivning som är associerat med 3D-resursen. Orsaken är att Dynamic Media Imaging Server inte känner igen 3D-format. När du har publicerat en 3D-resurs i Dynamic Media får du en direkt URL som du kan kopiera. URL:en för 3D-resursen följer den vanliga URL-strukturen för dynamiska media. Du kan dock inte redigera några parametrar i resursens URL, till skillnad från traditionella bildresurser i Dynamic Media.

I **[!UICONTROL Card View]** visas en liten globikon direkt under namnet på en resurs och till vänster om dess datum och tid för att ange att den publiceras. I **[!UICONTROL List View]** anger kolumnen **[!UICONTROL Published]** vilka resurser som har publicerats och inte.

Se även [Publicera mediematerial](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)för dynamiska media.

Se även [Publicera sidor](/help/sites-cloud/authoring/fundamentals/publishing-pages.md).

>[!MORELIKETHIS]
>
>Om du använder ett webbinnehållshanteringssystem från tredje part kan du länka eller bädda in 3D-resurser på dina webbsidor.
>
>See [Linking URLs to your web application](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md).

**Publicera 3D-resurser för dynamiska media**

1. Öppna en 3D-resurs (GLB-, OBJ- eller STL-filformat) för att visa den på sidan med tillgångsinformation.
1. Tryck på i verktygsfältet **[!UICONTROL Quick Publish]**.

   ![3d-asset-quick-publish](/help/assets/dynamic-media/assets/3d-asset-quick-publish.png)

1. Tryck för **[!UICONTROL Close]** att stänga dialogrutan och återgå till sidan med resursinformation.
1. Tryck på i listrutan till vänster om 3D-resursens filnamn **[!UICONTROL Renditions]**.

   ![3d-asset-renditions](/help/assets/dynamic-media/assets/3d-asset-renditions.png)

1. Tryck på **[!UICONTROL original]**. När en 3D-resurs publiceras (eller&quot;aktiveras&quot;) visas URL-knappen i det nedre vänstra hörnet av sidan om alla följande 3D-resursvillkor uppfylls:
   * 3D-resursen har ett format som stöds (GLB, OBJ, STL och USDZ).
   * 3D-resursen har importerats till Dynamic Media Image Production System (IPS).
   * 3D-resursen publiceras.
   ![3d-asset-url](/help/assets/dynamic-media/assets/3d-asset-url.png)

1. Tryck **[!UICONTROL URL]** för att visa 3D-resursens produktions-URL.
