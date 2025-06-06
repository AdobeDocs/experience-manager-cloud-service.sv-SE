---
title: Arbeta med 3D-resurser i Dynamic Media
description: Lär dig arbeta med 3D-resurser i Dynamic Media.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS and Experience Manager as a Cloud Service
topic-tags: introduction
content-type: reference
feature: 3D Assets
role: User
exl-id: 82084ba7-1302-4cbd-8626-d77b3aaa4ed1
source-git-commit: 36ab36ba7e14962eba3947865545b8a3f29f6bbc
workflow-type: tm+mt
source-wordcount: '2181'
ht-degree: 2%

---

# Arbeta med 3D-resurser i Dynamic Media {#working-with-three-d-assets-dm}

Med Dynamic Media kan du överföra, hantera, visa och leverera 3D-resurser som engagerande upplevelser.

* Publicering med ett klick (med **[!UICONTROL Quick Publish]** i verktygsfältet) av 3D-resurser för att generera en URL.
* Optimerat stöd för 3D-material med den högkvalitativa, interaktiva Dimensional-visningsförinställningen som drivs av Adobe Dimension.
* Med 3D Media WCM-komponenten kan du enkelt lägga till 3D-resurser på dina [!DNL Adobe Experience Manager Sites]-sidor.

Det krävs ingen ytterligare installation för att använda 3D-resurser i Dynamic Media.

![Visa i 3d](/help/assets/dynamic-media/assets/3d-dimensional-viewer-quickpublish-url-embed2a.png)

<!-- See also [Dynamic Media 3D Release Notes](/help/release-notes/aem3d-release-notes.md). -->

## 3D-format som stöds i Dynamic Media {#supported-three-d-file-formats-in-dm}

Dynamic Media har stöd för följande 3D-filformat.

Se även [3D-format som stöds i Experience Manager Assets](/help/assets/file-format-support.md#support-3d-formats)

| 3D-filtillägg | Filformat | MIME-typ | Anteckningar |
|---|---|---|---|
| GLB | Binär GL-överföring | model/gltf-binary | Materialen och texturerna inkluderas som en enda resurs. |
| OBJ | WaveFront 3D-objektfil | application/x-tgif |  |
| STL | Stereolithografi | application/vnd.ms-pki.stl |  |
| USDZ | Zip-arkiv för universell scenbeskrivning | model/vnd.usdz+zip | *Stöd endast för inmatning; ingen visning eller interaktion är tillgänglig.* USDZ är ett tillverkarspecifikt 3D-format som kan visas direkt av Safari eller iOS. |

3D Media WCM-komponenten och 3D-förhandsvisningen på en tillgångs informationssida är inte kompatibla med den senaste versionen av Chrome (97.x). Om du i stället vill arbeta med 3D-resurser använder du Firefox eller Safari, eller en tidigare version av Chrome (96.x).

## Snabbstart: 3D-resurser i Dynamic Media {#quick-start-three-d}

Följande steg-för-steg-beskrivning av arbetsflödet hjälper dig att komma igång snabbt med 3D-resurser i Dynamic Media.

Innan du arbetar med 3D-resurser i Dynamic Media måste du kontrollera att administratören för [!DNL Experience Manager] redan har aktiverat och konfigurerat Dynamic Media Cloud Services.

Se [Konfigurera tjänster i Dynamic Media Cloud](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services).

1. **Överför 3D-resurser**

   * [Överför dina 3D-resurser för användning i Dynamic Media](/help/assets/add-assets.md#upload-assets)
   * [3D-filformat som stöds för överföring i Dynamic Media](#supported-three-d-file-formats-in-dm)

1. **Hantera 3D-resurser**

   * Ordna och söka i 3D-resurser

      * [Organisera digitala resurser](/help/assets/organize-assets.md)
      * [Söka efter 3D-resurser](/help/assets/search-assets.md)

   * Visa 3D-resurser

      * [Visa och interagera med 3D-resurser](#viewing-three-d-assets)
      * [Hantera förinställningen för Dimensional Viewer](/help/assets/dynamic-media/managing-viewer-presets.md)

   * Arbeta med metadata för 3D-resurser

      * [Hantera metadata för digitala resurser](/help/assets/manage-digital-assets.md#editing-properties)
      * [Metadata-scheman](/help/assets/metadata-schemas.md)

1. **Publicera 3D-resurser**

   * [Publicera statiska 3D-resurser för dynamiska media](#publishing-three-d-assets)
   * [Alternativa metoder för publicering av 3D-resurser i Dynamic Media med Dimensional Viewer](#alternate-publish-methods)

## Visa och interagera med 3D-resurser {#viewing-three-d-assets}

I det här avsnittet beskrivs hur du visar och interagerar med 3D-resurser på två olika sätt: från sidan med resursinformation och från 3D-mediekomponenten i Sites.

Det interaktiva 3D-visningsprogrammet innehåller bland annat en samling interaktiva kamerakontroller där du kan omforma, zooma och panorera 3D-resursen.

Hur lång tid det tar att öppna en 3D-resurs i vyn Resursinformation beror på flera faktorer. Bland dessa faktorer finns följande:

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

Se även [Förhandsgranska resurser med programgränssnittet](/help/assets/dynamic-media/previewing-assets.md).

**Så här visar och interagerar du med en 3D-resurs från sidan med resursinformation:**

1. Kontrollera att du har överfört 3D-resurser till [!DNL Experience Manager].

   Se [Överför dina 3D-resurser för användning i dynamiska media](/help/assets/add-assets.md#upload-assets).

1. Välj **[!UICONTROL Assets > Files]** på sidan [!DNL Experience Manager].**[!UICONTROL Navigation]**
1. I den nedrullningsbara listan **[!UICONTROL View]** i det övre högra hörnet på sidan väljer du **[!UICONTROL Card View]**.
1. Navigera till en 3D-resurs som du vill visa.
1. Om du vill öppna resursen på detaljsidan väljer du kortet för 3D-resursen.
1. Gör något av följande på sidan Detaljer för 3D-resursen:

   | Visa | Beskrivning | Musåtgärd | Åtgärd på pekskärmen |
   | --- | --- | --- | --- |
   | **Vrid kameran** | Ordna vyn runt 3D-scenen och objekt. | Vänsterklicka och dra. | Tryck med ett finger och dra. |
   | **Panorera kameran** | Panorera vyn åt vänster, åt höger, uppåt eller nedåt. | Högerklicka och dra. | Tryck med två fingrar och dra. |
   | **Zooma kameran** | Flytta in och ut från områden i 3D-scenen. | Rullningshjul. | Nyp med två fingrar. |
   | **Ange kameran igen** | Centrera kameran igen till en punkt på ett objekt i 3D-scenen. | Dubbelklicka. | Dubbelmarkera. |
   | **Återställ** | I närheten av det nedre högra hörnet av sidan väljer du ikonen Återställ om du vill återställa målpunkten till mitten av 3D-resursen. Återställ flyttar också kameran närmare eller längre bort för att visa resursen i dess helhet och med en rimlig visningsstorlek. |   |   |
   | **Helskärmsläge** | Om du vill aktivera helskärmsläget väljer du Helskärmsikonen längst ned till höger på sidan. |   |   |

1. I det övre högra hörnet av sidan väljer du **[!UICONTROL Close]** för att gå tillbaka till Assets-sidan.

## Visa och interagera med en 3D-resurs inuti en 3D-mediekomponent {#interacting-with-asset-inside-three-d-media-component}

När en webbsida är i läget **[!UICONTROL Edit]** går det inte att interagera med en 3D-resurs. Om du vill göra resursen interaktiv kan du använda funktionen **[!UICONTROL Preview]** för att visa webbsidan i sidredigeraren med fullständig åtkomst till funktionerna i 3D Media-komponenten.

>[!IMPORTANT]
>
>Du kan bara utföra den här åtgärden när du har lagt till en 3D-mediekomponent på en webbsida och tilldelat en 3D-resurs till komponenten. Se [Lägga till 3D-mediekomponenten på en webbsida](#adding-the-three-d-media-component-to-a-web-page) och [Tilldela en 3D-resurs till en 3D-mediekomponent](#assigning-a-three-d-asset-to-the-component).

Se även [Förhandsgranska resurser med programgränssnittet](/help/assets/dynamic-media/previewing-assets.md).

**Så här visar och interagerar du med en 3D-resurs i en 3D-mediekomponent:**

1. Gör något av följande när en webbsida är i läget **[!UICONTROL Edit]**:

   * Klicka på **[!UICONTROL Preview]** uppe till höger på sidan för att öppna läget **[!UICONTROL Preview]**.
   * Ta bort `/editor.html` från sidans URL i webbläsaren.

   ![3D-resurs som visas inuti 3D-mediekomponenten](/help/assets/dynamic-media/assets/3d-asset-in-3d-mediaa.png)
En helt interaktiv 3D-resurs som visas i **[!UICONTROL Preview]** -läge.

1. Gör något av följande i **[!UICONTROL Preview]**-läget:

   | Visa | Beskrivning | Musåtgärd | Åtgärd på pekskärmen |
   | --- | --- | --- | --- |
   | **Vrid kameran** | Ordna vyn runt 3D-scenen och objekt. | Vänsterklicka och dra. | Tryck med ett finger och dra. |
   | **Panorera kameran** | Panorera vyn åt vänster, åt höger, uppåt eller nedåt. | Högerklicka och dra. | Tryck med två fingrar och dra. |
   | **Zooma kameran** | Flytta in och ut från områden i 3D-scenen. | Rullningshjul. | Nyp med två fingrar. |
   | **Ange kameran igen** | Centrera kameran igen till en punkt på ett objekt i 3D-scenen. | Dubbelklicka. | Dubbelmarkera. |
   | **Återställ** | I närheten av det nedre högra hörnet av sidan väljer du ikonen Återställ om du vill återställa målpunkten till mitten av 3D-resursen. Återställ flyttar också kameran närmare eller längre bort för att visa resursen i dess helhet och med en rimlig visningsstorlek. |   |   |
   | **Helskärmsläge** | Om du vill aktivera helskärmsläget väljer du Helskärmsikonen längst ned till höger på sidan. |   |   |

## Arbeta med 3D Media-komponenten {#working-with-three-d-media-component}

Dynamic Media innehåller en 3D Media-komponent för dynamiska media som du kan använda i [!DNL Experience Manager Sites] för att aktivera interaktiv visning av 3D-modeller på dina webbsidor.

* [Lägga till komponenten 3D Media i sidmallen](#adding-three-d-media-component-to-page-template)
* [Lägga till komponenten 3D Media på en webbsida](#adding-the-three-d-media-component-to-a-web-page)
   * [Valfritt - Konfigurera komponenten 3D Media](#configuring-the-three-d-component)
* [Tilldela en 3D-resurs till 3D-mediekomponenten](#assigning-a-three-d-asset-to-the-component)

## Lägga till komponenten 3D Media i sidmallen {#adding-three-d-media-component-to-page-template}

1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL General]** > **[!UICONTROL Templates]**.
1. Navigera till den sidmall som du vill aktivera 3D-komponenten i och markera mallen.
1. Om du vill öppna mallen väljer du **[!UICONTROL Edit]**.
1. I den nedrullningsbara menyn uppe till höger på sidan väljer du läget **[!UICONTROL Structure]**, om det inte redan är aktivt.

   ![3d-media-component-structure](/help/assets/dynamic-media/assets/3d-media-component-structurea.png)

1. Om du vill markera ett tomt område och öppna det tillhörande verktygsfältet markerar du det tomma området i **[!UICONTROL Layout Container]**-regionen.
1. I verktygsfältet väljer du ikonen **[!UICONTROL Policy]** för att öppna **[!UICONTROL Policy Editor]**.
1. I avsnittet **[!UICONTROL Properties]**, under fliken **[!UICONTROL Allowed Components]**, bläddrar du till **[!UICONTROL Dynamic Media]**, expanderar sedan listan och kontrollerar **[!UICONTROL 3D Media]**.
1. Välj **[!UICONTROL Done]** om du vill spara ändringarna och stänga **[!UICONTROL Policy Editor]**.

   Nu kan du placera komponenten Dynamic Media 3D Media på alla sidor som använder den här mallen.

## Lägga till komponenten 3D Media på en webbsida {#adding-the-three-d-media-component-to-a-web-page}

Om du använder [!DNL Experience Manager] som webbinnehållshanteringssystem kan du lägga till 3D-resurser på dina webbsidor med hjälp av komponenten 3D Media.

Se även [Lägg till dynamiska medieresurser på sidor](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

1. Öppna [!DNL Experience Manager Sites] och markera den webbsida där du vill lägga till 3D-mediakomponenten för dynamiska media.
1. Om du vill öppna sidan i sidredigeraren väljer du ikonen **[!UICONTROL Edit]** (penna). Kontrollera att läget **[!UICONTROL Edit]** är markerat i sidans övre högra hörn.

   ![3d-media-component-add](/help/assets/dynamic-media/assets/3d-media-component-edita.png)

1. I verktygsfältet väljer du ikonen för panelen Sida för att växla eller aktivera visningen av panelen.

1. I sidopanelen väljer du plustecknet för att öppna listan **[!UICONTROL Components]**.

   ![3d-media-component-drag-drop](/help/assets/dynamic-media/assets/3d-assets-filtera.png)

1. Dra **[!UICONTROL 3D Media]**-komponenten från listan **[!UICONTROL Components]** till den plats på sidan där du vill att 3D-visningsprogrammet ska visas.

Nu kan du tilldela en 3D-resurs till komponenten.

Se [Tilldela en 3D-resurs till 3D-mediekomponenten](#assigning-a-three-d-asset-to-the-component)

### Valfritt - Konfigurera komponenten 3D Media {#configuring-the-three-d-component}

1. I sidredigeraren [!DNL Experience Manager Sites] väljer du komponenten **[!UICONTROL 3D Media Viewer]** som du tidigare har lagt till på sidan.
1. Om du vill öppna dialogrutan för komponentkonfiguration väljer du ikonen **[!UICONTROL Configuration]** (skiftnyckel).

   ![3d-media-component-config](/help/assets/dynamic-media/assets/3d-media-component-configa.png)

1. I dialogrutan 3D-media väljer du **[!UICONTROL Dimensional]** i listrutan Visningsförinställning för att tilldela komponenten förinställningen för Dimensional Viewer.

   ![3d-media-component-edit-config](/help/assets/dynamic-media/assets/3d-media-component-edit-configa.png)

1. Markera bockmarkeringen i det övre högra hörnet för att spara ändringarna.

## Tilldela en 3D-resurs till 3D-mediekomponenten {#assigning-a-three-d-asset-to-the-component}

När du har lagt till en 3D-mediekomponent på en webbsida kan du tilldela den en 3D-resurs.

Se [Lägga till komponenten 3D Media på en webbsida](#adding-the-three-d-media-component-to-a-web-page).

1. Klicka på ikonen **[!UICONTROL Assets]** i sidredigeraren [!DNL Experience Manager Sites] för att öppna **[!UICONTROL Assets]** på sidpanelen.
1. I listrutan väljer du **[!UICONTROL 3D]** om du bara vill visa filtyper för 3D-resurser.
1. På sidopanelen söker du efter eller bläddrar till den 3D-resurs som du vill visa på sidan som redigeras.
1. Dra 3D-resursen från sidopanelen i Assets och släpp den på komponenten **[!UICONTROL 3D Media]** som du tidigare lade till på sidan.

   ![Tilldela 3d-resurs till 3d Media-komponent](/help/assets/dynamic-media/assets/3d-asset-adda.png)

>[!NOTE]
>
>När en webbsida är i läget [!DNL Experience Manager Sites] **[!UICONTROL Edit]** visar 3D-mediekomponenten 3D-resursen, men ingen interaktion med resursen är möjlig. Om du vill göra resursen interaktiv kan du använda funktionen **[!UICONTROL Preview]** för att visa webbsidan i sidredigeraren med fullständig åtkomst till funktionerna i 3D Media-komponenten.

## Publicera statiska 3D-resurser för dynamiska media {#publishing-three-d-assets}

Dynamic Media accepterar olika 3D-filformat som stöds som *statiskt innehåll* i Dynamic Media. Statiskt innehåll innebär att du kan överföra och publicera 3D-resurser, men det finns inget stöd för *dynamisk* bildåtergivning eller bildåtergivning som är associerat med 3D-resursen. Orsaken är att Dynamic Media Imaging Server inte känner igen 3D-format. När du har publicerat en 3D-resurs i Dynamic Media får du en direkt URL som du kan kopiera. URL:en för 3D-resursen följer den vanliga URL-strukturen för dynamiska media. Du kan dock inte redigera några parametrar i resursens URL, till skillnad från traditionella bildresurser i Dynamic Media.

Se även [Hämta en URL för en statisk resurs](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-a-static-asset).

I **[!UICONTROL Card View]** visas en liten global ikon direkt under namnet på en resurs och till vänster om dess datum och tid för att ange att den är publicerad. I **[!UICONTROL List View]** anger kolumnen **[!UICONTROL Published]** vilka resurser som har publicerats och inte.

Om du använder [!DNL Experience Manager] som WCM-fil använder du den här publiceringsmetoden för att lägga till 3D-resurser för dynamiska media direkt på webbsidan.

Se även [Publicera dynamiska medieresurser](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

Se även [Publicera sidor](/help/sites-cloud/authoring/sites-console/publishing-pages.md).

**Så här publicerar du statiska 3D-resurser för dynamiska media:**

1. Öppna en 3D-resurs (filformatet GLB, OBJ eller STL).
1. Välj **[!UICONTROL Quick Publish]** på detaljsidan i verktygsfältet.

   ![3d-asset-quick-publish](/help/assets/dynamic-media/assets/3d-asset-quick-publisha.png)

1. Välj **[!UICONTROL Close]** om du vill stänga dialogrutan och gå tillbaka till sidan med resursinformation.
1. Välj **[!UICONTROL Renditions]** i listrutan till vänster om 3D-resursens filnamn.

   ![3d-asset-renditions](/help/assets/dynamic-media/assets/3d-asset-renditionsa.png)

1. Välj **[!UICONTROL original]**. När en 3D-resurs publiceras (eller&quot;aktiveras&quot;) visas knappen **[!UICONTROL URL]** i det nedre vänstra hörnet på sidan om alla följande 3D-resursvillkor uppfylls:
   * 3D-resursen har ett format som stöds (GLB, OBJ, STL och USDZ).
   * 3D-resursen har importerats till Dynamic Media Image Production System (IPS).
   * 3D-resursen publiceras.

   ![3d-asset-url](/help/assets/dynamic-media/assets/3d-asset-urla.png)

1. Välj **[!UICONTROL URL]** om du vill visa 3D-resursens URL för direktproduktion som du kan kopiera och använda på webbsidor.

### Alternativa metoder för publicering av 3D-resurser i Dynamic Media med Dimensional Viewer {#alternate-publish-methods}

Använd följande två metoder för att publicera 3D-resurser för dynamiska media om du *inte* använder [!DNL Experience Manager] som WCM-fil.

* **[!UICONTROL URL]** - Använd **[!UICONTROL URL]** om du använder ett tredjepartssystem för hantering av webbinnehåll och vill länka 3D-resurser för dynamiska media till dina webbsidor med Dimensional Viewer.

  Se [Länka URL:er till ditt webbprogram](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset).

* **[!UICONTROL Embed]** - Använd **[!UICONTROL Embed]** när du vill visa en 3D-resurs för dynamiska media som är inbäddad på en webbsida med Dimensional Viewer. Du kopierar inbäddningskoden till Urklipp så att du kan klistra in den på webbsidorna. Det är inte tillåtet att redigera koden i dialogrutan **[!UICONTROL Embed]**.

  Se [Bädda in Dynamic Media Video, Image Viewer eller Dimensional Viewer på en webbsida](/help/assets/dynamic-media/embed-code.md#embedding-the-video-or-image-viewer-on-a-web-page).
