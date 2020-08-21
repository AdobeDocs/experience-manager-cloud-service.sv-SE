---
title: Metadataprofiler
description: Lär dig mer om metadataprofiler för resurser. Lär dig hur du skapar en metadataprofil och använder den på mappresurser.
contentOwner: AG
translation-type: tm+mt
source-git-commit: c240f9aa465b019fa77cc471f865db1f4ab45532
workflow-type: tm+mt
source-wordcount: '1168'
ht-degree: 24%

---


# Metadataprofiler {#metadata-profiles}

Med en metadataprofil kan du använda standardmetadata för resurser i en mapp. Skapa en metadataprofil och tillämpa den på en mapp. Alla resurser som du sedan överför till mappen ärver de standardmetadata som du konfigurerade i metadataprofilen.

## Lägg till en metadataprofil {#adding-a-metadata-profile}

1. Tryck på AEM logotyp, navigera till **[!UICONTROL Tools > Assets > Metadata Profiles]** och tryck sedan på **[!UICONTROL Create]**.
1. Ange en rubrik för metadataprofilen, till exempel Exempelmetadata, och tryck på **[!UICONTROL Submit]**. Redigera formulär för metadataprofilen visas.
1. Klicka på en komponent och konfigurera dess egenskaper på **[!UICONTROL Settings]** fliken. Klicka till exempel på **[!UICONTROL Description]** komponenten och redigera dess egenskaper.
Redigera följande egenskaper för **[!UICONTROL Description]** komponenten:

   * **[!UICONTROL Field Label]** - Visningsnamnet för metadataegenskapen. Det är bara till för användarreferensen.
   * **[!UICONTROL Map to Property]** - Värdet för den här egenskapen anger den relativa sökvägen/namnet till resursnoden där den sparas i databasen. Värdet ska alltid börja med `./` eftersom det anger att sökvägen finns under objektets nod.

      The value you specify for **[!UICONTROL Map to property]** is stored as a property under the asset&#39;s metadata node. Om du till exempel anger . `/jcr:content/metadata/dc:desc` som namn på **[!UICONTROL Map to property]** lagrar AEM Assets värdet `dc:desc` på objektets metadatanod.

   * **[!UICONTROL Default Value]** - Använd den här egenskapen om du vill lägga till ett standardvärde för metadatakomponenten. Om du till exempel anger &quot;Min beskrivning&quot; tilldelas det här värdet till egenskapen `dc:desc` vid objektets metadatanod.

      >[!NOTE]
      >
      >Lägga till ett standardvärde i en ny metadataegenskap (som inte finns redan i . `/jcr:content/metadata` nod) visar inte egenskapen och dess värde på objektets egenskapssida som standard. Om du vill visa den nya egenskapen på egenskapssidan för resursen ändrar du motsvarande schemaformulär.

1. (Valfritt) Lägg till fler komponenter i Redigera formulär på fliken **[!UICONTROL Build Form]** och konfigurera deras egenskaper på fliken **[!UICONTROL Settings]**. Följande egenskaper är tillgängliga på fliken **[!UICONTROL Build Form]**:

| Komponent | Egenskaper |
|------------------|----------------------------------------------------|
| Avsnittshuvud | Fältetikett, beskrivning |
| Enkelradstext | Fältetikett, Mappa till egenskap, Standardvärde |
| Flervärdestext | Fältetikett, Mappa till egenskap, Standardvärde |
| Siffra | Fältetikett, Mappa till egenskap, Standardvärde |
| Date | Fältetikett, Mappa till egenskap, Standardvärde |
| Standardtaggar | Fältetikett, Mappa till egenskap, Standardvärde, Beskrivning |

1. Tryck på **[!UICONTROL Done]**. Metadataprofilen läggs till i listan med profiler på **[!UICONTROL Metadata Profiles]** sidan.

## Kopiera en metadataprofil {#copying-a-metadata-profile}

1. Välj en metadataprofil på **[!UICONTROL Metadata Profiles]** sidan om du vill skapa en kopia av den.
1. Tap **[!UICONTROL Copy]** from the toolbar.
1. I **[!UICONTROL Copy Metadata Profile]** dialogrutan anger du en rubrik för den nya kopian av metadataprofilen.
1. Tryck på **[!UICONTROL Copy]**. Kopian av metadataprofilen visas i listan med profiler på sidan **[!UICONTROL Metadata Profiles]**.

## Ta bort en metadataprofil {#deleting-a-metadata-profile}

1. På **[!UICONTROL Metadata Profiles]** sidan väljer du en profil att ta bort.
1. Tap **[!UICONTROL Delete Metadata Profiles]** in the toolbar.
1. Klicka på **[!UICONTROL Delete]** för att bekräfta borttagningen i dialogrutan. Metadataprofilen tas bort från listan.

## Använda en metadataprofil för mappar {#applying-a-metadata-profile-to-folders}

När du tilldelar en metadataprofil till en mapp ärver alla undermappar automatiskt profilen från den överordnade mappen. Det innebär att du bara kan tilldela en metadataprofil till en mapp. Fundera därför noga över mappstrukturen för var du överför, lagrar, använder och arkiverar resurser.

Om du har tilldelat en annan metadataprofil till en mapp åsidosätter den nya profilen den tidigare profilen. De tidigare befintliga mappresurserna ändras inte. Den nya profilen används för resurser som läggs till i mappen senare.

Mappar som har tilldelats en profil visas i användargränssnittet med namnet på profilen som visas i kortnamnet.

Du kan tillämpa metadataprofiler på specifika mappar eller globalt på alla resurser.

Du kan bearbeta resurser i en mapp som redan har en befintlig metadataprofil som du senare ändrade. <!-- See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

### Använda metadataprofiler på specifika mappar {#applying-metadata-profiles-to-specific-folders}

Du kan använda en metadataprofil på en mapp från menyn **[!UICONTROL Tools]** eller, om du är i mappen, från **[!UICONTROL Properties]**. I det här avsnittet beskrivs hur du använder metadataprofiler på mappar på båda sätten.

För mappar som redan har tilldelats en profil visas profilens namn direkt under mappnamnet.

Du kan bearbeta resurser i en mapp som redan har en befintlig videoprofil som du senare ändrade. <!--See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

#### Använda metadataprofiler på mappar från användargränssnittet för profiler {#applying-metadata-profiles-to-folders-from-profiles-user-interface}

1. Tryck på AEM-logotypen och navigera till **[!UICONTROL Tools > Assets > Metadata Profiles]**.
1. Välj den metadataprofil som du vill använda för en eller flera mappar.
1. Tryck på **[!UICONTROL Apply Metadata Profile to Folder(s)]** och markera den eller de mappar som du vill ska ta emot de nyligen överförda resurserna och tryck sedan på **[!UICONTROL Done]**. För mappar som redan har tilldelats en profil visas profilens namn direkt under mappnamnet.

#### Använd metadataprofiler på mappar från Egenskaper {#applying-metadata-profiles-to-folders-from-properties}

1. Gå **[!UICONTROL Assets]** sedan till den mapp som du vill använda en metadataprofil på i den vänstra listen.
1. På mappen: tryck eller klicka på bockmarkeringen för att markera den och tryck eller klicka sedan på **Egenskaper**.
1. Markera fliken **[!UICONTROL Metadata Profiles]**, välj profilen i listrutan och tryck på **[[Spara]**. För mappar som redan har tilldelats en profil visas profilens namn direkt under mappnamnet.

### Använd en metadataprofil globalt {#applying-a-metadata-profile-globally}

Förutom att tillämpa en profil på en mapp kan du även tillämpa en profil globalt så att allt innehåll som överförs till AEM resurser i en mapp har den valda profilen.

Du kan bearbeta resurser i en mapp som redan har en befintlig metadataprofil som du senare ändrade. <!--See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

**Om du vill använda en metadataprofil globalt gör du något av följande**

* Navigera till `https://<AEM server>/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam` och använd rätt profil och tryck på **Spara**.

* Navigera till CRXDE Lite till följande nod: `/content/dam/jcr:content`. Lägg till egenskapen `metadataProfile:/etc/dam/metadata/dynamicmedia/<name of metadata profile>` och tryck på **Spara alla**.

## Ta bort en metadataprofil från mappar {#removing-a-metadata-profile-from-folders}

När du tar bort en metadataprofil från en mapp ärver alla undermappar automatiskt borttagningen av profilen från den överordnade mappen. All bearbetning av filer som har inträffat i mapparna förblir dock oförändrad.

Du kan ta bort en metadataprofil från en mapp från menyn **Verktyg** eller, om du är i mappen, från **Egenskaper**. I det här avsnittet beskrivs hur du tar bort metadataprofiler från mappar på båda sätten.

### Ta bort metadataprofiler från mappar via användargränssnittet Profiles {#removing-metadata-profiles-from-folders-via-profiles-user-interface}

1. Tap or click the AEM logo and navigate to **[!UICONTROL Tools > Assets > Metadata Profiles]**.
1. Markera den metadataprofil som du vill ta bort från en eller flera mappar.
1. Tryck på **[!UICONTROL Remove Metadata Profile from Folder(s)]** och markera den eller de mappar som du vill ta bort en profil från och tryck sedan på **[!UICONTROL Done]**.

   Du kan bekräfta att metadataprofilen inte längre används för en mapp eftersom namnet inte längre visas under mappnamnet.

### Ta bort metadataprofiler från mappar via Egenskaper {#removing-metadata-profiles-from-folders-via-properties}

1. Tryck på AEM logotyp och navigera **[!UICONTROL Assets]** sedan till mappen som du vill ta bort en metadataprofil från.
1. Markera mappen genom att trycka på bockmarkeringen och sedan på **[!UICONTROL Properties]**.
1. Välj fliken **[!UICONTROL Metadata Profiles]**, välj **[!UICONTROL None]** i listrutan och klicka på **[!UICONTROL Save]**. För mappar som redan har tilldelats en profil visas profilens namn direkt under mappnamnet.
