---
title: Färgtaggar för bilder
description: Med Adobe Experience Manager Assets kan du skilja mellan färger i en bild och använda dem som taggar automatiskt. Du kan sedan använda dessa taggar för att söka efter och filtrera bilder.
exl-id: 3afa949b-ea1b-4b8e-ac94-06566e2c7147
feature: Smart Imaging, Interactive Images, Asset Management
role: User, Admin
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '1143'
ht-degree: 0%

---

# Färgtaggar för bilder {#color-tag-images}

![Banderoll för färgtaggning](assets/banner-image.png)

Adobe Experience Manager (AEM) Assets använder Adobe Sensei AI-funktioner för att skilja mellan färgerna i en bild och använda dem som taggar automatiskt vid intag. Dessa taggar möjliggör en förbättrad sökfunktion baserat på bildens färgkomposition.

Du kan konfigurera antalet färger, inom intervallet 1 till 40, som taggas i en bild så att du kan söka efter bilder baserade på dessa färger senare. Experience Manager Assets använder märkorden baserat på färgmängden i en bild. Du kan också konfigurera visningsformatet för en färgtagg.

I följande bild visas de åtgärder du utför för att konfigurera och hantera färgtaggning för bilder i Experience Manager Assets:

![Färgtaggning](assets/color-tagging-dfd.gif)

## Filformat som stöds {#supported-file-formats-color-tags}

| Filformat | Tillägg | MIME-typ | Indatafärgrymd | Största tillåtna källfilsstorlek | Maximal filstorlek som stöds |
|---|---|---|---|---|---|
| JPEG | .jpg och .jpeg | image/jpeg | sRGB | 15 GB | 2 000 × 2 000 pixlar |
| PNG | .png | bild/png | sRGB | 15 GB | 2 000 × 2 000 pixlar |
| TIFF | .tif och .tiff | bild/tiff | sRGB | 4 GB (begränsat av formatspecifikationer) | 2 000 × 2 000 pixlar |
| PSD | .psd | image/vnd.adobe.photoshop | sRGB | 2 GB (begränsat av formatspecifikationer) | 2 000 × 2 000 pixlar |
| GIF | .gif | image/gif | sRGB | 15 GB | 2 000 × 2 000 pixlar |
| BMP | .bmp | image/bmp | sRGB | 4 GB (begränsat av formatspecifikationer) | 2 000 × 2 000 pixlar |

## Hantera egenskaper för färgtaggning {#manage-color-tagging-properties}

Så här hanterar du färgtaggningsegenskaperna för bilder:

1. Navigera till **[!UICONTROL Tools > Assets > Color Tagging]**.

   ![Egenskaper för färgtaggning](assets/color-tag-settings.png)

1. Ange ett visningsformat för färgtaggen i fältet **[!UICONTROL Display Format]**. Möjliga alternativ är färgnamn, RGB eller HEX.

1. Ange antalet färger som du vill tagga för bilderna i fältet **[!UICONTROL Limit]**. Dessa färger visas när du visar en bilds egenskaper. I det här fältet kan du definiera ett tal mellan 1 och 40. Standardvärdet för det här fältet är tio färger.

1. Ange den lägsta färgtäckningsprocenten för att inkludera en färgtagg i sökresultaten i fältet **[!UICONTROL Coverage/Dominance Threshold %]**. Om den röda färgmängden i en bild till exempel är tio procent och du anger nio procent i det här fältet, inkluderas bilden när du söker efter bilder med röd färg. Om täckningen för den röda färgen i en bild är tio procent och du anger 11 procent i det här fältet tas bilden inte med när du söker efter bilder med röd färg.

   I det här fältet kan du ange valfritt tal mellan 5 och 100. Standardvärdet är 1.

   >[!NOTE]
   >
   >Adobe rekommenderar att du använder ett värde som ligger nära standardvärdet i det här fältet. Om du anger ett högt siffervärde för det här fältet (till exempel större än 25) kan det returnera få sökresultat. På samma sätt kan ett lågt siffervärde (till exempel mindre än 6) returnera för många sökresultat, vilket kanske inte är användbart.

1. Klicka på **[!UICONTROL Save]**.


   >[!VIDEO](https://video.tv.adobe.com/v/340108)


### Inaktivera färgtaggning {#disable-color-tagging}

Färgtaggning för bilder är aktiverat som standard. Du kan inaktivera färgtaggning på mappnivå. Alla underordnade mappar ärver egenskaperna för färgtaggning från den överordnade mappen.

Så här inaktiverar du färgtaggning på mappnivå:

1. Navigera till **[!UICONTROL Adobe Experience Manager > Assets > Files]**.

1. Markera mappen och klicka på **[!UICONTROL Properties]**.

1. Gå till mappen **[!UICONTROL Color Tags for images]** på fliken **[!UICONTROL Asset Processing]**. Välj något av följande värden i listrutan:

   * Ärvd - Mappen ärver aktiverings- eller inaktiveringsalternativen från den överordnade mappen.

   * Aktivera - Aktiverar färgtaggning för den valda mappen.

   * Inaktivera - Inaktiverar färgtaggning för den valda mappen.

   ![Inställningar för färgtaggning](assets/color-tags-folder.png)

## Konfigurera metadatamatchemat för att lägga till en komponent för smarta färgtaggar {#configure-metadata-schema}

Metadata-scheman innehåller specifika fält för specifik information som ska fyllas i. Den innehåller även layoutinformation för att visa metadatafält på ett användarvänligt sätt. Metadataegenskaperna innehåller titel, beskrivning, MIME-typer, taggar med mera. Du kan använda redigeraren [!UICONTROL Metadata Schema Forms] för att ändra befintliga scheman eller lägga till anpassade metadatamatcheman.

>[!NOTE]
>
>Fältet Smart Color Tag är tillgängligt i standardmetadataschemat. Om du använder ett anpassat metadatamatchema konfigurerar du schemat så att ett smart färgtaggfält läggs till.

Så här lägger du till komponenten Smarta färgtaggar i Formulärredigeraren för metadataschning:

1. Navigera till **[!UICONTROL Tools > Assets > Metadata Schemas]**.

1. Markera schemanamnet och klicka på **[!UICONTROL Edit]**.

1. Dra **[!UICONTROL Smart Color Tags]** från fliken **[!UICONTROL Build Form]** till **[!UICONTROL Metadata Schema Form Editor]**.

1. Klicka på **[!UICONTROL Smart Color Tag Field]** i **[!UICONTROL Metadata Schema Form Editor]**.

1. Ange ett lämpligt värde i fältet **[!UICONTROL Field Label]** på fliken **[!UICONTROL Settings]**.

1. Klicka på **[!UICONTROL Save]**.

   >[!VIDEO](https://video.tv.adobe.com/v/340124)

## Färgtaggar för befintliga bilder i DAM {#color-tags-existing-images}

De befintliga bilderna i DAM färgläggs inte automatiskt. [!UICONTROL Reprocess Assets] manuellt om du vill generera färgtaggar för dem.

Så här färgar du bilder eller mappar (inklusive undermappar) med resurser som finns i resurskatalogen:

1. Välj logotypen [!DNL Adobe Experience Manager] och välj sedan resurser på sidan [!UICONTROL Navigation].

1. Välj [!UICONTROL Files].

1. I Assets-gränssnittet navigerar du till den mapp som du vill använda färgtaggar på.

1. Markera hela mappen eller specifika bilder.

1. Välj ikonen ![Bearbeta om resurser](assets/do-not-localize/reprocess-assets-icon.png) [!UICONTROL Reprocess Assets] och välj alternativet [!UICONTROL Full Process] .

När processen har slutförts går du till sidan [!UICONTROL Properties] för en bild i mappen. De automatiskt tillagda taggarna visas i avsnittet [!UICONTROL Smart Color Tags] på fliken [!UICONTROL Basic].


## Visa smarta färgtaggar för bilder {#view-color-tags}

Så här visar du smarta färgtaggar för bilder:

1. Navigera till **[!UICONTROL Adobe Experience Manager > Assets > Files]**.

1. Klicka på lämplig mapp och markera bilden.

1. Markera **[!UICONTROL Properties]** och visa taggarna i fältet **[!UICONTROL Smart Color Tags]**.

   ![Visa färgtaggar](assets/view-color-tags.png)

   Håll muspekaren över en färgtagg så att du kan visa **[!UICONTROL Coverage/Dominance Threshold %]** för en färg i en bild.

## Konfigurera AEM Assets-färgpredikat {#configure-search-predicate}

Du kan konfigurera ett sökfilter för bilder. Du kan sedan basera sökvillkoren på en viss färg för att filtrera resultaten.

>[!NOTE]
>
>Konfigurera AEM Assets färgpredikat endast om du inte använder standardsökformuläret.

Om du vill konfigurera sökfiltret skapar du ett predikat för resursfärg med Assets Admin Search Rail.

Så här konfigurerar du sökfilter:

1. Navigera till **[!UICONTROL Tools > General > Search Forms]**.

1. Markera **[!UICONTROL Assets Admin Search Rail]** och klicka på **[!UICONTROL Edit]**.

1. Dra **[!UICONTROL Asset Color Predicate]** från fliken **[!UICONTROL Select Predicate]** till **[!UICONTROL Search Form Editor]**.

1. Ange ett lämpligt värde i fältet **[!UICONTROL Field Label]** på fliken **[!UICONTROL Settings]**.

1. Klicka på **[!UICONTROL Done]** om du vill spara inställningarna.

   >[!VIDEO](https://video.tv.adobe.com/v/340110)

## Söka efter bilder baserat på färger {#search-images-based-on-colors}

>[!VIDEO](https://video.tv.adobe.com/v/340761)

När du har konfigurerat alla egenskaper för färgtaggning och [konfigurerat Assets-färgpredikatet](#search-images-based-on-colors) kan du söka efter bilder baserat på en färg som ett filter.

Så här söker du efter bilder baserat på färger:

1. Navigera till **[!UICONTROL Assets > Files]**.

1. Välj **[!UICONTROL Filter]** i listrutan.
   ![Filtrera Assets](assets/filter-assets.png)

1. Välj [AEM Assets-färgpredikatet](#configure-search-predicate).

1. Välj lämplig färg genom att dra färgväljaren. Den valda färgen visas i det skrivskyddade fältet under färgväljaren. Du kan välja RGB eller HEX som visningsformat för färgen.

   ![Färgväljaren](assets/color-picker-color-tags.png)

   Du kan filtrera bilder baserat på valet av en färg. De bilder som har den valda färgen som en av de smarta färgtaggarna och ovanför [täcknings-/översiktströskeln %](#manage-color-tagging-settings) visas i den högra rutan.

1. Rensa filtret genom att klicka på X i sökfältet.

**Se även**

* [Översätt Assets](translate-assets.md)
* [ASSETS HTTP API](mac-api-assets.md)
* [Filformat som stöds av Assets](file-format-support.md)
* [Sök resurser](search-assets.md)
* [Anslutna resurser](use-assets-across-connected-assets-instances.md)
* [Resursrapporter](asset-reports.md)
* [Metadata-scheman](metadata-schemas.md)
* [Hämta resurser](download-assets-from-aem.md)
* [Hantera metadata](manage-metadata.md)
* [Sök efter ansikten](search-facets.md)
* [Hantera samlingar](manage-collections.md)
* [Import av massmetadata](metadata-import-export.md)
* [Publicera Assets till AEM och Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
