---
title: Metadataprofiler
description: Lär dig mer om metadataprofiler för resurser. Lär dig hur du skapar en metadataprofil och använder den på mappresurser.
contentOwner: AG
feature: Metadata
role: User, Admin
exl-id: eef90c6a-b354-4342-8b97-21d067ae2979
source-git-commit: ab2cf8007546f538ce54ff3e0b92bb0ef399c758
workflow-type: tm+mt
source-wordcount: '1324'
ht-degree: 17%

---

# Metadataprofiler {#metadata-profiles}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/metadata-config.html?lang=en) |
| AEM as a Cloud Service | Den här artikeln |

Med en metadataprofil kan du använda standardmetadata för resurser i en mapp. Skapa en metadataprofil och tillämpa den på en mapp. Alla resurser som du sedan överför till mappen ärver de standardmetadata som du konfigurerade i metadataprofilen.

Ett viktigt koncept när det gäller användningen av profiler i Experience Manager Assets är att de tilldelas mappar. I en profil finns inställningar i form av metadataprofiler, tillsammans med videoprofiler eller bildprofiler. De här inställningarna bearbetar innehållet i en mapp tillsammans med någon av dess undermappar. Det innebär att hur du namnger filer och mappar, hur du ordnar undermappar och hur du hanterar filerna i dessa mappar har stor inverkan på hur resurserna bearbetas av en profil.
Genom att använda konsekventa och lämpliga namngivningsstrategier för filer och mappar samt god metadatapraxis får du ut det mesta av din digitala resurssamling och ser till att rätt filer bearbetas med rätt profil.

## Lägg till en metadataprofil {#adding-a-metadata-profile}

1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Metadata Profiles]** och klicka sedan på **[!UICONTROL Create]**.
1. Ange en rubrik för metadataprofilen, till exempel Exempelmetadata, och välj **[!UICONTROL Submit]**. Redigera formulär för metadataprofilen visas.
1. Klicka på en komponent och konfigurera dess egenskaper i **[!UICONTROL Settings]** -fliken. Klicka till exempel på **[!UICONTROL Description]** och redigera dess egenskaper.
Redigera följande egenskaper för **[!UICONTROL Description]** komponent:

   * **[!UICONTROL Field Label]** - Visningsnamnet för metadataegenskapen. Det är bara till för användarreferensen.
   * **[!UICONTROL Map to Property]** - Värdet för den här egenskapen anger den relativa sökvägen/namnet till resursnoden där den sparas i databasen. Värdet ska alltid börja med `./` eftersom det anger att sökvägen finns under objektets nod.

     Värdet som du anger för **[!UICONTROL Map to property]** lagras som en egenskap under objektets metadatanod. Om du till exempel anger . `/jcr:content/metadata/dc:desc` som namnet på **[!UICONTROL Map to property]**, [!DNL Adobe Experience Manager Assets] lagrar värdet `dc:desc` på resursens metadatanod.

   * **[!UICONTROL Default Value]** - Använd den här egenskapen om du vill lägga till ett standardvärde för metadatakomponenten. Om du till exempel anger &quot;Min beskrivning&quot; tilldelas det här värdet till egenskapen `dc:desc` på resursens metadatanod.

     >[!NOTE]
     >
     >Lägga till ett standardvärde i en ny metadataegenskap (som inte finns på `/jcr:content/metadata` nod) visar inte egenskapen och dess värde på objektets egenskapssida som standard. Visa den nya egenskapen på [!UICONTROL Properties] ändrar du motsvarande schemaformulär.

1. (Valfritt) Lägg till fler komponenter i Redigera formulär på fliken **[!UICONTROL Build Form]** och konfigurera deras egenskaper på fliken **[!UICONTROL Settings]**. Följande egenskaper är tillgängliga på fliken **[!UICONTROL Build Form]**:

| Komponent | Egenskaper |
|------------------|----------------------------------------------------|
| Avsnittshuvud | Fältetikett, beskrivning |
| Enkelradstext | Fältetikett, Mappa till egenskap, Standardvärde |
| Flervärdestext | Fältetikett, Mappa till egenskap, Standardvärde |
| Nummer | Fältetikett, Mappa till egenskap, Standardvärde |
| Datum | Fältetikett, Mappa till egenskap, Standardvärde |
| Standardtaggar | Fältetikett, Mappa till egenskap, Standardvärde, Beskrivning |

1. Klicka på **[!UICONTROL Done]**. Metadataprofilen läggs till i listan över profiler i **[!UICONTROL Metadata Profiles]** sida.

## Kopiera en metadataprofil {#copying-a-metadata-profile}

1. Från **[!UICONTROL Metadata Profiles]** väljer du en metadataprofil för att skapa en kopia av den.
1. Klicka på **[!UICONTROL Copy]** i verktygsfältet.
1. I **[!UICONTROL Copy Metadata Profile]** anger du en rubrik för den nya kopian av metadataprofilen.
1. Klicka på **[!UICONTROL Copy]**. Kopian av metadataprofilen visas i listan med profiler på sidan **[!UICONTROL Metadata Profiles]**.

## Ta bort en metadataprofil {#deleting-a-metadata-profile}

1. Från **[!UICONTROL Metadata Profiles]** väljer du en profil att ta bort.
1. Klicka **[!UICONTROL Delete Metadata Profiles]** i verktygsfältet.
1. Klicka på **[!UICONTROL Delete]** för att bekräfta borttagningsåtgärden. Metadataprofilen tas bort från listan.

## Använda en metadataprofil för mappar {#applying-a-metadata-profile-to-folders}

När du tilldelar en metadataprofil till en mapp ärver alla undermappar automatiskt profilen från den överordnade mappen. Arvet upphör när en annan profil tillämpas på en undermapp. Du kan bara tilldela en metadataprofil till en mapp. Därför bör du noga tänka på mappstrukturen där du överför, lagrar, använder och arkiverar resurser.

Om du tilldelade en annan metadataprofil till en mapp åsidosätter den nya profilen den tidigare profilen. De tidigare befintliga mappresurserna ändras inte. Den nya profilen tillämpas på de resurser som läggs till i mappen efter ändringen. Du kan tillämpa metadataprofiler på specifika mappar eller globalt på alla resurser.

Mappar som har tilldelats en profil visas i användargränssnittet med namnet på profilen som visas i kortnamnet.

Du kan bearbeta resurser i en mapp som redan har en befintlig metadataprofil som du senare ändrade. <!-- See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

### Använda metadataprofiler på specifika mappar {#applying-metadata-profiles-to-specific-folders}

Du kan använda en metadataprofil på en mapp från menyn **[!UICONTROL Tools]** eller, om du är i mappen, från **[!UICONTROL Properties]**. I det här avsnittet beskrivs hur du använder metadataprofiler på mappar på båda sätten.

För mappar som redan har tilldelats en profil visas profilens namn direkt under mappnamnet.

Du kan bearbeta resurser i en mapp som redan har en befintlig videoprofil som du senare ändrade. <!--See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

#### Använda metadataprofiler på mappar från användargränssnittet för profiler {#applying-metadata-profiles-to-folders-from-profiles-user-interface}

1. Navigera till **[!UICONTROL Tools > Assets > Metadata Profiles]**.
1. Välj den metadataprofil som du vill använda för en eller flera mappar.
1. Klicka **[!UICONTROL Apply Metadata Profile to Folders]** och markera den eller de mappar som du vill använda för att ta emot de nyligen överförda resurserna och klicka på **[!UICONTROL Done]**. För mappar som redan har tilldelats en profil visas profilens namn direkt under mappnamnet.

#### Använd metadataprofiler på mappar från Egenskaper {#applying-metadata-profiles-to-folders-from-properties}

1. Klicka på **[!UICONTROL Assets]** navigera sedan till den mapp som du vill använda en metadataprofil på.
1. Markera kryssrutan i mappen och markera den sedan. **Egenskaper**.
1. Välj **[!UICONTROL Metadata Profiles]** och välj profilen i listrutan och klicka på **[!UICONTROL Save]**. För mappar som redan har tilldelats en profil visas profilens namn direkt under mappnamnet.

### Använd en metadataprofil globalt {#applying-a-metadata-profile-globally}

Förutom att tillämpa en profil på en mapp kan du även tillämpa en profil globalt så att allt innehåll som överförs till [!DNL Experience Manager Assets] i alla mappar där den valda profilen används.

Du kan bearbeta resurser i en mapp som redan har en befintlig metadataprofil som du senare ändrade. <!--See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

**Om du vill använda en metadataprofil globalt gör du något av följande**

* Navigera till `https://[aem_server]/mnt/overlay/dam/gui/content/assets/v2/foldersharewizard.html/content/dam` och använda rätt profil och klicka på **[!UICONTROL Save]**.

* Navigera till CRXDE Lite till följande nod: `/content/dam/jcr:content`. Lägg till egenskapen `metadataProfile:/etc/dam/metadata/dynamicmedia/<name of metadata profile>`. Klicka **Spara alla**.

## Ta bort en metadataprofil från mappar {#removing-a-metadata-profile-from-folders}

När du tar bort en metadataprofil från en mapp ärver alla undermappar automatiskt borttagningen av profilen från den överordnade mappen. All bearbetning av filer som har inträffat i mapparna förblir dock oförändrad.

Du kan ta bort en metadataprofil från en mapp från menyn **Verktyg** eller, om du är i mappen, från **Egenskaper**. I det här avsnittet beskrivs hur du tar bort metadataprofiler från mappar på båda sätten.

### Ta bort metadataprofiler från mappar via användargränssnittet Profiles {#removing-metadata-profiles-from-folders-via-profiles-user-interface}

1. Klicka på Experience Manager logotyp och navigera till **[!UICONTROL Tools > Assets > Metadata Profiles]**.
1. Markera den metadataprofil som du vill ta bort från en eller flera mappar.
1. Klicka **[!UICONTROL Remove Metadata Profile from Folders]** och markera den eller de mappar som du vill ta bort en profil från och klicka på **[!UICONTROL Done]**.

   Du kan bekräfta att metadataprofilen inte längre används för en mapp eftersom namnet inte längre visas under mappnamnet.

### Ta bort metadataprofiler från mappar via Egenskaper {#removing-metadata-profiles-from-folders-via-properties}

1. Klicka på Experience Manager logotyp och navigera **[!UICONTROL Assets]** och sedan till mappen som du vill ta bort en metadataprofil från.
1. Markera mappen genom att klicka på bockmarkeringen och klicka sedan på **[!UICONTROL Properties]**.
1. Välj fliken **[!UICONTROL Metadata Profiles]**, välj **[!UICONTROL None]** i listrutan och klicka på **[!UICONTROL Save]**. För mappar som redan har tilldelats en profil visas profilens namn direkt under mappnamnet.

**Se även**

* [Översätt resurser](translate-assets.md)
* [Resurser för HTTP API](mac-api-assets.md)
* [Resurser som stöds i filformat](file-format-support.md)
* [Sök resurser](search-assets.md)
* [Anslutna resurser](use-assets-across-connected-assets-instances.md)
* [Resursrapporter](asset-reports.md)
* [Metadata-scheman](metadata-schemas.md)
* [Hämta resurser](download-assets-from-aem.md)
* [Hantera metadata](manage-metadata.md)
* [Sök efter ansikten](search-facets.md)
* [Hantera samlingar](manage-collections.md)
* [Import av massmetadata](metadata-import-export.md)
* [Publicera resurser till AEM och Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
