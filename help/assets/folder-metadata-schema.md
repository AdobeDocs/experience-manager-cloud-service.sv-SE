---
title: Metadataschema för mapp
description: Lär dig hur du skapar metadatamappar för resursmappar i [!DNL Experience Manager Assets]
contentOwner: AG
feature: Metadata
role: User,Admin
exl-id: c86760ed-169d-40f7-91a4-8aee449b286c
source-git-commit: abe5f8a4b19473c3dddfb79674fb5f5ab7e52fbf
workflow-type: tm+mt
source-wordcount: '1002'
ht-degree: 3%

---

# Metadataschema för mapp {#folder-metadata-schema}

[!DNL Adobe Experience Manager Assets] Med kan du skapa metadatascheman för resursmappar, som definierar layouten och metadata som visas på mappegenskapssidor.

## Lägga till ett schemaformulär för mappmetadata {#add-a-folder-metadata-schema-form}

Använd schemaredigeraren för mappmetadata i Forms för att skapa och redigera metadatascheman för mappar.

1. Välj [!DNL Experience Manager] logotyp och gå till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Folder Metadata Schemas]**.
1. På Forms-sidan för mappmetadataschema väljer du **[!UICONTROL Create]**.
1. Ange ett namn för formuläret och välj **[!UICONTROL Create]**. Det nya schemaformuläret visas på Forms-sidan Schema.

## Redigera schemaformulär för mappmetadata {#edit-folder-metadata-schema-forms}

Du kan redigera ett nyligen tillagt eller befintligt metadatchemaformulär, som innehåller följande:

* Tabbar
* Formulärobjekt på flikar.

Du kan mappa/konfigurera dessa formulärobjekt till ett fält i en metadatanod i CRX-databasen. Du kan lägga till nya flikar eller formulärobjekt i metadatchemaformuläret.

1. På Forms-sidan Schema väljer du det formulär du skapade och väljer sedan **[!UICONTROL Edit]** -ikonen i verktygsfältet.
1. På sidan Redigerare för schema för mappmetadata väljer du **[!UICONTROL +]** om du vill lägga till en flik i formuläret. Om du vill byta namn på fliken markerar du standardnamnet och anger det nya namnet under **[!UICONTROL Settings]**.

   ![custom_tab](assets/custom_tab.png)

   Välj knappen **[!UICONTROL +]** -ikon. Välj **[!UICONTROL X]** för att ta bort en flik.

1. Lägg till en eller flera komponenter från fliken Aktiv **[!UICONTROL Build Form]** -fliken.

   ![adding_components](assets/adding_components.png)

   Om du skapar flera flikar väljer du en viss flik för att lägga till komponenter.

1. Konfigurera en komponent genom att markera den och ändra dess egenskaper i **[!UICONTROL Settings]** -fliken.

   Ta bort en komponent från **[!UICONTROL Settings]** -fliken.

   ![configure_properties](assets/configure_properties.png)

1. Välj **[!UICONTROL Save]** i verktygsfältet för att spara ändringarna.

### Komponenter för att skapa formulär {#components-to-build-forms}

The **[!UICONTROL Build Form]** På fliken visas formulärobjekt som du använder i schemaformuläret för mappmetadata. The **[!UICONTROL Settings]** på -fliken visas attributen för varje objekt som du väljer i **[!UICONTROL Build Form]** -fliken. Här är en lista över de tillgängliga formulärobjekten i **[!UICONTROL Build Form]** tab:

<table>
 <tbody>
  <tr>
   <td><p><strong>Komponentnamn</strong></p> </td>
   <td><p><strong>Beskrivning</strong></p> </td>
  </tr>
  <tr>
   <td><p>Avsnittshuvud</p> </td>
   <td><p> Lägg till en avsnittsrubrik för en lista med gemensamma komponenter.</p> </td>
  </tr>
  <tr>
   <td><p>Enkelradstext</p> </td>
   <td><p> Lägg till en enkelradig textegenskap. Den lagras som en sträng.</p> </td>
  </tr>
  <tr>
   <td><p>Flervärdestext</p> </td>
   <td><p> Lägg till en textegenskap med flera värden. Den lagras som en strängarray.</p> </td>
  </tr>
  <tr>
   <td><p>Nummer</p> </td>
   <td><p> Lägg till en sifferkomponent.</p> </td>
  </tr>
  <tr>
   <td><p>Datum</p> </td>
   <td><p> Lägg till en datumkomponent.</p> </td>
  </tr>
  <tr>
   <td><p>Listruta</p> </td>
   <td><p> Lägg till en listruta.</p> </td>
  </tr>
  <tr>
   <td><p>Standardtaggar</p> </td>
   <td><p> Lägg till en tagg. </p> </td>
  </tr>
  <tr>
   <td><p>Dolt fält</p> </td>
   <td><p> Lägg till ett dolt fält. Den skickas som en POST-parameter när resursen sparas.</p> </td>
  </tr>
 </tbody>
</table>

### Redigera formulärobjekt {#editing-form-items}

Om du vill redigera egenskaperna för formulärobjekt markerar du komponenten och redigerar alla eller en delmängd av följande egenskaper i dialogrutan **[!UICONTROL Settings]** -fliken. Vi rekommenderar att du bara mappar ett fält till en viss egenskap i metadataschemat. I annat fall hämtas det senast tillagda fältet som är mappat till egenskapen av systemet.

**[!UICONTROL Field Label]**: Namnet på metadataegenskapen som visas på egenskapssidan för mappen.

**[!UICONTROL Map to Property]**: This property specifies the relative path of the folder node in the CRX database where it is saved. Det börjar med &quot;**./**&quot;, vilket anger att sökvägen finns under mappens nod.

Nedan följer exempel på giltiga värden för en egenskap:

* `./jcr:content/metadata/dc:title`: Lagrar värdet i mappens metadatanod som egenskapen `dc:title`.

* `./jcr:created`: Lagrar datum och tid för när en resurs skapades. Det är en skyddad egenskap. Om du konfigurerar de här egenskaperna bör du markera dem som [!UICONTROL Disable Edit].

För att komponenten ska visas på rätt sätt i schemaformuläret för metadata ska du inte ta med något utrymme i egenskapssökvägen.

**[!UICONTROL JSON Path]**: Använd den för att ange sökvägen till JSON-filen där du anger nyckelvärdepar för alternativ.

**[!UICONTROL Placeholder]**: Använd den här egenskapen för att ange relevant platshållartext för metadataegenskapen.

**[!UICONTROL Choices]**: Använd den här egenskapen för att ange alternativ i en lista.

**[!UICONTROL Description]**: Använd den här egenskapen om du vill lägga till en kort beskrivning för metadatakomponenten.

**[!UICONTROL Class]**: Objektklass som egenskapen är associerad med.

## Ta bort schemaformulär för mappmetadata {#delete-folder-metadata-schema-forms}

Du kan ta bort schemaformulär för mappmetadata från Forms-sidan för mappmetadataschema. Om du vill ta bort ett formulär markerar du det och väljer ikonen Ta bort i verktygsfältet.

![delete_form](assets/delete_form.png)

## Tilldela ett mappmetadatchema {#assign-a-folder-metadata-schema}

Du kan tilldela ett mappmetadatchema till en mapp från Forms-sidan för mappmetadataschema eller när du skapar en mapp.

Om du konfigurerar ett metadataschema för en mapp lagras sökvägen till schemaformuläret i `folderMetadataSchema` egenskapen för mappnoden under .*/jcr:innehåll*.

### Tilldela till ett schema från sidan Mappmetadatamatchema {#assign-to-a-schema-from-the-folder-metadata-schema-page}

1. Välj [!DNL Experience Manager] logotyp och gå till **[!UICONTROL Tools]** > **[!UICONTROL Assets]**> **[!UICONTROL Folder Metadata Schemas]**.
1. På Forms-sidan för mappmetadataschema väljer du det schemaformulär som du vill tillämpa på en mapp.
1. Välj **[!UICONTROL Apply to Folders]** i verktygsfältet.

1. Välj den mapp som schemat ska tillämpas på och välj sedan **[!UICONTROL Apply]**. Om ett metadatamatchema redan används för mappen visas ett varningsmeddelande om att du håller på att skriva över det befintliga metadatamodemet. Välj **[!UICONTROL Overwrite]**.
1. Öppna metadataegenskaperna för den mapp som du tillämpade metadataschemat på.

   ![folder_properties](assets/folder_properties.png)

   Om du vill visa metadatafälten för mappen väljer du **[!UICONTROL Folder Metadata]** -fliken.

   ![folder_metadata_properties](assets/folder_metadata_properties.png)

### Tilldela ett schema när du skapar en mapp {#assign-a-schema-when-creating-a-folder}

Du kan tilldela ett mappmetadatchema när du skapar en mapp. Om det finns minst ett mappmetadatchema i systemet visas en extra lista i **[!UICONTROL Create Folder]** -dialogrutan. Du kan välja önskat schema. Som standard är inget schema valt.

1. Från [!DNL Experience Manager Assets] användargränssnitt, välja **[!UICONTROL Create]** i verktygsfältet.
1. Ange en rubrik och ett namn för mappen.
1. Välj önskat schema i listan Mappmetadatamatchema. Välj sedan **[!UICONTROL Create]**.

   ![select_schema](assets/select_schema.png)

1. Öppna metadataegenskaperna för den mapp som du tillämpade metadataschemat på.
1. Om du vill visa metadatafälten för mappen väljer du **[!UICONTROL Folder Metadata]** -fliken.

## Använd mappens metadatamatchema {#use-the-folder-metadata-schema}

Öppna egenskaperna för en mapp som har konfigurerats med ett schema för mappmetadata. En flik för **[!UICONTROL Folder Metadata]** visas på sidan med mappegenskaper. Om du vill visa formuläret för schemat med mappmetadata väljer du den här fliken.

Ange metadatavärden i de olika fälten och välj **[!UICONTROL Save]** för att lagra värdena. De värden du anger lagras i mappnoden i CRX-databasen.

![folder_metadata_properties-1](assets/folder_metadata_properties-1.png)

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
