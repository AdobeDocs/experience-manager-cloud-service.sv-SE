---
title: Metadataschema för mapp
description: Lär dig hur du skapar metadatamatchning för resursmappar i AEM Resurser
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# Metadataschema för mapp {#folder-metadata-schema}

Med Adobe Experience Manager Assets (AEM) kan du skapa metadatamappar för resursmappar, som definierar layouten och metadata som visas på mappegenskapssidor.

## Lägga till ett schemaformulär för mappmetadata {#add-a-folder-metadata-schema-form}

Använd redigeraren för schemaformulär för mappmetadata när du vill skapa och redigera metadatascheman för mappar.

1. Tryck/klicka på AEM-logotypen och gå till **[!UICONTROL Verktyg]** > **[!UICONTROL Resurser]** > **[!UICONTROL Mappmetadatascheman]**.
1. Tryck/klicka på **[!UICONTROL Skapa]** på sidan för schemaformulär för mappmetadata.
1. Ange ett namn för formuläret och tryck/klicka på **[!UICONTROL Skapa]**. Det nya schemaformuläret visas på sidan Schemaformulär.

## Redigera schemaformulär för mappmetadata {#edit-folder-metadata-schema-forms}

Du kan redigera ett nyligen tillagt eller befintligt metadatchemaformulär, som innehåller följande:

* Tabbar
* Formulärobjekt på flikar.

Du kan mappa/konfigurera dessa formulärobjekt till ett fält i en metadatanod i CRX-databasen. Du kan lägga till nya flikar eller formulärobjekt i metadatchemaformuläret.

1. På sidan Schemaformulär väljer du det formulär du skapade och trycker/klickar sedan på ikonen **[!UICONTROL Redigera]** i verktygsfältet.
1. Tryck/klicka på ikonen **[!UICONTROL +]** för att lägga till en flik i formuläret på sidan Schemaredigerare för mappmetadata. Om du vill byta namn på fliken trycker/klickar du på standardnamnet och anger det nya namnet under **[!UICONTROL Inställningar]**.

   ![custom_tab](assets/custom_tab.png)

   Om du vill lägga till fler flikar trycker du på/klickar på **[!UICONTROL +]** -ikonen. Tryck/klicka på **[!UICONTROL X]** för att ta bort en flik.

1. Lägg till en eller flera komponenter från fliken **[!UICONTROL Skapa formulär]** på den aktiva fliken.

   ![adding_components](assets/adding_components.png)

   Om du skapar flera flikar trycker/klickar du på en viss flik för att lägga till komponenter.

1. Om du vill konfigurera en komponent markerar du den och ändrar dess egenskaper på fliken **[!UICONTROL Inställningar]** .

   Om det behövs tar du bort en komponent från fliken **[!UICONTROL Inställningar]** .

   ![configure_properties](assets/configure_properties.png)

1. Tryck/klicka på **[!UICONTROL Spara]** i verktygsfältet för att spara ändringarna.

### Komponenter för att skapa formulär {#components-to-build-forms}

På fliken **[!UICONTROL Skapa formulär]** visas formulärobjekt som du använder i schemaformuläret för mappmetadata. På fliken **[!UICONTROL Inställningar]** visas attributen för varje objekt som du väljer på fliken **[!UICONTROL Skapa formulär]** . Här är en lista över de formulärobjekt som är tillgängliga på fliken **[!UICONTROL Skapa formulär]** :

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
   <td><p> Nummer</p> </td>
   <td><p> Lägg till en sifferkomponent.</p> </td>
  </tr>
  <tr>
   <td><p>Date</p> </td>
   <td><p> Lägg till en datumkomponent.</p> </td>
  </tr>
  <tr>
   <td><p>Listruta</p> </td>
   <td><p> Lägg till en nedrullningsbar lista.</p> </td>
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

Om du vill redigera egenskaperna för formulärobjekt trycker/klickar du på komponenten och redigerar alla eller en delmängd av följande egenskaper på fliken **[!UICONTROL Inställningar]** .

**[!UICONTROL Fältetikett]**: Namnet på metadataegenskapen som visas på egenskapssidan för mappen.

**[!UICONTROL Mappa till egenskap]**: This property specifies the relative path of the folder node in the CRX database where it is saved. Det börjar med &quot;**./**&quot;, vilket anger att sökvägen finns under mappens nod.

Följande är giltiga värden för den här egenskapen:

* `./jcr:content/metadata/dc:title`: Lagrar värdet i mappens metadatanod som egenskap `dc:title`.

* `./jcr:created`: Visar JCR-egenskapen vid mappens nod. Om du konfigurerar dessa egenskaper i CRXDE bör du markera dem som Inaktivera redigering eftersom de är skyddade. Annars inträffar felet `Asset(s) failed to modify`&quot; när du sparar resursens egenskaper.

För att komponenten ska visas på rätt sätt i schemaformuläret för metadata ska du inte ta med något utrymme i egenskapssökvägen.

**[!UICONTROL JSON-sökväg]**: Använd den för att ange sökvägen till JSON-filen där du anger nyckelvärdepar för alternativ.

**[!UICONTROL Platshållare]**: Använd den här egenskapen för att ange relevant platshållartext för metadataegenskapen.

**[!UICONTROL Alternativ]**: Använd den här egenskapen för att ange alternativ i en lista.

**[!UICONTROL Beskrivning]**: Använd den här egenskapen om du vill lägga till en kort beskrivning för metadatakomponenten.

**[!UICONTROL Klass]**: Den objektklass som egenskapen är associerad med.

## Ta bort schemaformulär för mappmetadata {#delete-folder-metadata-schema-forms}

Du kan ta bort schemaformulär för mappmetadata från sidan för schemaformulär för mappmetadata. Om du vill ta bort ett formulär markerar du det och trycker/klickar på ikonen Ta bort i verktygsfältet.

![delete_form](assets/delete_form.png)

## Tilldela ett mappmetadatchema {#assign-a-folder-metadata-schema}

Du kan tilldela ett mappmetadatamatchema till en mapp antingen från sidan för schemaformulär för mappmetadata eller när du skapar en mapp.

Om du konfigurerar ett metadataschema för en mapp lagras sökvägen till schemaformuläret i mappnodens egenskap under `folderMetadataSchema` .*/jcr:content*.

### Tilldela till ett schema från sidan Mappmetadatamatchema {#assign-to-a-schema-from-the-folder-metadata-schema-page}

1. Tryck/klicka på AEM-logotypen och gå till **[!UICONTROL Verktyg]** > **[!UICONTROL Resurser]**> **[!UICONTROL Mappmetadatascheman]**.
1. På sidan Schemaformulär för mappmetadata väljer du det schemaformulär som du vill tillämpa på en mapp.
1. Tryck/klicka på **[!UICONTROL Tillämpa på mapp(ar)]** i verktygsfältet.

1. Välj den mapp som du vill använda schemat på och klicka/tryck sedan på **[!UICONTROL Använd]**. Om ett metadatamatchema redan används för mappen visas ett varningsmeddelande om att du håller på att skriva över det befintliga metadatamodemet. Tryck/klicka på **[!UICONTROL Skriv över]**.
1. Öppna metadataegenskaperna för den mapp som du tillämpade metadataschemat på.

   ![folder_properties](assets/folder_properties.png)

   Om du vill visa metadatafälten för mappen trycker du på/klickar på fliken **[!UICONTROL Mappmetadata]** .

   ![folder_metadata_properties](assets/folder_metadata_properties.png)

### Tilldela ett schema när du skapar en mapp {#assign-a-schema-when-creating-a-folder}

Du kan tilldela ett mappmetadatchema när du skapar en mapp. Om det finns minst ett mappmetadatchema i systemet visas en extra lista i dialogrutan **[!UICONTROL Skapa mapp]** . Du kan välja önskat schema. Som standard är inget schema valt.

1. I användargränssnittet för AEM Resurser trycker/klickar du på **[!UICONTROL Skapa]** i verktygsfältet.
1. Ange en rubrik och ett namn för mappen.
1. Välj önskat schema i listan Mappmetadatamatchema. Tryck/klicka sedan på **[!UICONTROL Skapa]**.

   ![select_schema](assets/select_schema.png)

1. Öppna metadataegenskaperna för den mapp som du tillämpade metadataschemat på.
1. Om du vill visa metadatafälten för mappen trycker du på/klickar på fliken **[!UICONTROL Mappmetadata]** .

## Använd mappens metadatamatchema {#use-the-folder-metadata-schema}

Öppna egenskaperna för en mapp som har konfigurerats med ett mappmetadatchema. Fliken **[!UICONTROL Mappmetadata]** visas på mappegenskapssidan. Om du vill visa schemaformuläret för mappmetadata väljer du den här fliken.

Ange metadatavärden i de olika fälten och lagra värdena genom att trycka/klicka på **[!UICONTROL Spara]** . De värden du anger lagras i mappnoden i CRX-databasen.

![folder_metadata_properties-1](assets/folder_metadata_properties-1.png)

