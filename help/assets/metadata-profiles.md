---
title: Metadataprofiler
description: Lär dig mer om metadataprofiler för resurser. Lär dig hur du skapar en metadataprofil och använder den på mappresurser.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# Metadataprofiler {#metadata-profiles}

Med en metadataprofil kan du använda standardmetadata för resurser i en mapp. Skapa en metadataprofil och tillämpa den på en mapp. Alla resurser som du sedan överför till mappen ärver de standardmetadata som du konfigurerade i metadataprofilen.

<!-- See [Profiles for Processing Metadata, Images, and Videos](processing-profiles.md).

See also [Best Practices for Organizing your Digital Assets for using Processing Profiles](/help/assets/best-practices-for-file-management.md).

-->

## Lägg till en metadataprofil {#adding-a-metadata-profile}

1. Tryck på AEM-logotypen och navigera till **[!UICONTROL Verktyg > Resurser > Metadataprofiler]** och tryck sedan på **[!UICONTROL Skapa]**.
1. Ange en rubrik för metadataprofilen, till exempel Exempelmetadata, och tryck på **[!UICONTROL Skicka]**. Redigera formulär för metadataprofilen visas.
1. Klicka på en komponent och konfigurera dess egenskaper på fliken **[!UICONTROL Inställningar]** . Klicka till exempel på komponenten **[!UICONTROL Beskrivning]** och redigera dess egenskaper.
Redigera följande egenskaper för komponenten **[!UICONTROL Description]** :

   * **[!UICONTROL Fältetikett]** - metadataegenskapens visningsnamn. Det är bara till för användarreferensen.
   * **[!UICONTROL Mappa till egenskap]** - Värdet för den här egenskapen anger den relativa sökvägen/namnet till objektnoden där den sparas i databasen. Värdet ska alltid börja med `./` eftersom det anger att sökvägen finns under objektets nod.

      Värdet som du anger för **[!UICONTROL Mappa till egenskap]** lagras som en egenskap under objektets metadatanod. Om du till exempel anger . `/jcr:content/metadata/dc:desc` som namnet på **[!UICONTROL Mappa till egenskap]** lagrar AEM Resurser värdet `dc:desc` i objektets metadatanod.

   * **[!UICONTROL Standardvärde]** - Använd den här egenskapen om du vill lägga till ett standardvärde för metadatakomponenten. Om du till exempel anger &quot;Min beskrivning&quot; tilldelas det här värdet till egenskapen `dc:desc` vid objektets metadatanod.

      >[!NOTE]
      >
      >Lägga till ett standardvärde i en ny metadataegenskap (som inte finns redan i . `/jcr:content/metadata` nod) visar inte egenskapen och dess värde på objektets egenskapssida som standard. Om du vill visa den nya egenskapen på egenskapssidan för resursen ändrar du motsvarande schemaformulär.

1. (Valfritt) Lägg till fler komponenter i Redigera formulär på fliken **[!UICONTROL Skapa formulär]** och konfigurera deras egenskaper på fliken **[!UICONTROL Inställningar]** . Följande egenskaper är tillgängliga på fliken **[!UICONTROL Skapa formulär]** :

| Komponent | Egenskaper |
|------------------|----------------------------------------------------|
| Avsnittshuvud | Fältetikett, beskrivning |
| Enkelradstext | Fältetikett, Mappa till egenskap, Standardvärde |
| Flervärdestext | Fältetikett, Mappa till egenskap, Standardvärde |
|  Nummer | Fältetikett, Mappa till egenskap, Standardvärde |
| Date | Fältetikett, Mappa till egenskap, Standardvärde |
| Standardtaggar | Fältetikett, Mappa till egenskap, Standardvärde, Beskrivning |

1. Tryck på **[!UICONTROL Klar]**. Metadataprofilen läggs till i listan med profiler på sidan **[!UICONTROL Metadataprofiler]** .

## Kopiera en metadataprofil {#copying-a-metadata-profile}

1. Välj en metadataprofil på sidan **[!UICONTROL Metadataprofiler]** om du vill skapa en kopia av den.
1. Tryck på **[!UICONTROL Kopiera]** i verktygsfältet.
1. I dialogrutan **[!UICONTROL Kopiera metadataprofil]** anger du en rubrik för den nya kopian av metadataprofilen.
1. Tryck på **[!UICONTROL Kopiera]**. Kopian av metadataprofilen visas i listan över profiler på sidan **[!UICONTROL Metadataprofiler]** .

## Ta bort en metadataprofil {#deleting-a-metadata-profile}

1. På sidan **[!UICONTROL Metadataprofiler]** väljer du en profil som ska tas bort.
1. Tryck på **[!UICONTROL Ta bort metadataprofiler]** i verktygsfältet.
1. Klicka på **[!UICONTROL Ta bort]** i dialogrutan för att bekräfta borttagningen. Metadataprofilen tas bort från listan.

## Använda en metadataprofil för mappar {#applying-a-metadata-profile-to-folders}

När du tilldelar en metadataprofil till en mapp ärver alla undermappar automatiskt profilen från den överordnade mappen. Det innebär att du bara kan tilldela en metadataprofil till en mapp. Fundera därför noga över mappstrukturen för var du överför, lagrar, använder och arkiverar resurser.

Om du har tilldelat en annan metadataprofil till en mapp åsidosätter den nya profilen den tidigare profilen. De tidigare befintliga mappresurserna ändras inte. Den nya profilen används för resurser som läggs till i mappen senare.

Mappar som har tilldelats en profil visas i användargränssnittet med namnet på profilen som visas i kortnamnet.

Du kan tillämpa metadataprofiler på specifika mappar eller globalt på alla resurser.

Du kan bearbeta resurser i en mapp som redan har en befintlig metadataprofil som du senare ändrade. <!-- See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

### Använda metadataprofiler på specifika mappar {#applying-metadata-profiles-to-specific-folders}

Du kan tillämpa en metadataprofil på en mapp från **[!UICONTROL Verktyg]** -menyn eller, om du är i mappen, från **[!UICONTROL Egenskaper]**. I det här avsnittet beskrivs hur du använder metadataprofiler på mappar på båda sätten.

Mappar som redan har tilldelats en profil visas genom att profilens namn visas direkt under mappnamnet.

Du kan bearbeta resurser i en mapp som redan har en befintlig videoprofil som du senare ändrade. <!--See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

#### Använda metadataprofiler på mappar från användargränssnittet för profiler {#applying-metadata-profiles-to-folders-from-profiles-user-interface}

1. Tryck på AEM-logotypen och navigera till **[!UICONTROL Verktyg > Resurser > Metadataprofiler]**.
1. Välj den metadataprofil som du vill använda för en eller flera mappar.
1. Tryck på **[!UICONTROL Använd metadataprofil för mappar]** och markera den eller de mappar som du vill använda för att ta emot de nyligen överförda resurserna. Tryck sedan på **[!UICONTROL Klar]**. Mappar som redan har tilldelats en profil visas genom att profilens namn visas direkt under mappnamnet.

#### Använd metadataprofiler på mappar från Egenskaper {#applying-metadata-profiles-to-folders-from-properties}

1. I den vänstra listen trycker du på **[!UICONTROL Resurser]** och navigerar sedan till mappen som du vill använda en metadataprofil på.
1. På mappen: tryck eller klicka på bockmarkeringen för att markera den och tryck eller klicka sedan på **Egenskaper**.
1. Välj fliken **[!UICONTROL Metadataprofiler]** och välj profilen i listrutan och tryck på **Spara]**. Mappar som redan har tilldelats en profil visas genom att profilens namn visas direkt under mappnamnet.

### Använd en metadataprofil globalt {#applying-a-metadata-profile-globally}

Förutom att tillämpa en profil på en mapp kan du även tillämpa en profil globalt så att allt innehåll som överförs till AEM-resurser i en mapp har den valda profilen.

Du kan bearbeta resurser i en mapp som redan har en befintlig metadataprofil som du senare ändrade. <!--See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

**Om du vill använda en metadataprofil globalt gör du något av följande**

* Navigera till `https://<AEM server>/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam` och använd rätt profil och tryck på **Spara**.

* Navigera till CRXDE Lite till följande nod: `/content/dam/jcr:content`. Lägg till egenskapen `metadataProfile:/etc/dam/metadata/dynamicmedia/<name of metadata profile>` och tryck på **Spara alla**.

## Ta bort en metadataprofil från mappar {#removing-a-metadata-profile-from-folders}

När du tar bort en metadataprofil från en mapp ärver alla undermappar automatiskt borttagningen av profilen från den överordnade mappen. All bearbetning av filer som har inträffat i mapparna förblir dock oförändrad.

Du kan ta bort en metadataprofil från en mapp från **Verktyg** -menyn eller, om du är i mappen, från **Egenskaper**. I det här avsnittet beskrivs hur du tar bort metadataprofiler från mappar på båda sätten.

### Ta bort metadataprofiler från mappar via användargränssnittet Profiles {#removing-metadata-profiles-from-folders-via-profiles-user-interface}

1. Tryck eller klicka på AEM-logotypen och navigera till **[!UICONTROL Verktyg > Resurser > Metadataprofiler]**.
1. Markera den metadataprofil som du vill ta bort från en eller flera mappar.
1. Tryck på **[!UICONTROL Ta bort metadataprofil från]** mapp(ar) och markera den eller de mappar du vill ta bort en profil från och tryck sedan på **[!UICONTROL Klar]**.

   Du kan bekräfta att metadataprofilen inte längre används för en mapp eftersom namnet inte längre visas under mappnamnet.

### Ta bort metadataprofiler från mappar via Egenskaper {#removing-metadata-profiles-from-folders-via-properties}

1. Tryck på AEM-logotypen, navigera till **[!UICONTROL Resurser]** och sedan till den mapp som du vill ta bort en metadataprofil från.
1. Markera mappen genom att trycka på bockmarkeringen och sedan på **[!UICONTROL Egenskaper]**.
1. Välj fliken **[!UICONTROL Metadataprofiler]** och välj **[!UICONTROL Ingen]** i listrutan och klicka på **[!UICONTROL Spara]**. Mappar som redan har tilldelats en profil visas genom att profilens namn visas direkt under mappnamnet.
