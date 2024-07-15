---
title: Hur importerar, exporterar och organiserar man Adaptive Forms eller PDF forms i en AEM Forms-instans?
description: Lär dig att migrera adaptiva Forms, PDF forms, teman och andra stödresurser till och från en AEM.
topic-tags: forms-manager
role: Admin, User
feature: Adaptive Forms
exl-id: f5105fb7-b8c0-4656-8095-b21d392746c0
source-git-commit: 6f547bd743932d45e45e0a3c47ff5eb2129cb664
workflow-type: tm+mt
source-wordcount: '1025'
ht-degree: 1%

---



| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/manage-administer-aem-forms/import-export-forms-templates) |
| AEM as a Cloud Service | Den här artikeln |

# Importera eller exportera anpassningsbara Forms- och AEM Forms-resurser {#importing-and-exporting-assets-to-aem-forms}

Du kan flytta adaptiva Forms och relaterade resurser som adaptiva formulärteman, formulärdatamodell (FDM), adaptiva formulärmallar, fragment och PDF forms mellan [!DNL AEM Forms]-instanser.

## Ladda ned anpassningsbara Forms-, PDF forms- och samhörande resurser {#download-forms-amp-documents-assets}

Så här hämtar du formulär eller relaterade resurser:

1. Logga in på din [!DNL Experience Manager Forms]-instans.
1. Välj **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**.

   ![Välj Forms](/help/forms/assets/select-forms.png)

1. Markera resurserna och klicka på ikonen **[!UICONTROL Download]** i den övre listen.

   ![Hämta Forms](/help/forms/assets/download-form.png)

   När du hämtar formuläret visas dialogrutan **[!UICONTROL Download Asset(s)]**.

   ![Hämta formulärresurser](/help/forms/assets/download-form-assets.png)

1. Klicka på **[!UICONTROL Download]**.

De valda resurserna hämtas som ett arkiv (.zip-fil).

## Överför adaptiva Forms-, PDF forms- eller samhörande resurser {#upload-forms-amp-documents-assets}

Du kan överföra de resurstyper som stöds individuellt eller som ett ZIP-arkiv. För en ZIP-fil visas de relativa sökvägarna för alla resurser som stöds. Resurser som inte stöds i ZIP ignoreras och visas inte. Om ZIP-arkivet bara innehåller resurser som inte stöds visas ett felmeddelande i stället för popup-dialogrutan.
Så här överför du ett formulär eller en relaterad resurs:

1. Logga in på din [!DNL Experience Manager Forms]-instans.
1. Välj **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**.

   ![Välj Forms](/help/forms/assets/select-forms.png)

1. Välj **[!UICONTROL Create]** > **[!UICONTROL File Upload]**. En dialogruta visas.

   ![Överför Forms](/help/forms/assets/form-upload.png)

1. I dialogrutan bläddrar du till och väljer paketet eller arkivet som ska importeras. Du kan också välja andra filtyper som stöds. Välj **[!UICONTROL Open]**. Mappen eller filnamnet som du väljer får inte innehålla några specialtecken.

   Verifiera informationen om resurser som överförs i dialogrutan och välj **[!UICONTROL Upload]**.

   Om du överför en befintlig formulärresurs uppdateras resursen.

   >[!NOTE]
   >
   > När ett namn hamnar i konflikt med olika resurstyper ersätter inte överföring av ett paket den befintliga mapphierarkin. Om du till exempel har ett adaptivt formulär med namnet &quot;Training&quot; på platsen `/content/dam/formsanddocuments` på en server. Du kan hämta det adaptiva formuläret och överföra det till en annan server. Den andra servern har också en mapp med namnet &quot;Training&quot; på samma plats `/content/dam/formsanddocuments`. Överföringen misslyckas.

## Hämta ett tema

Du kan exportera teman i [!DNL AEM Forms] som du kan använda i andra projekt eller instanser. Med AEM kan du hämta teman som en zip-fil som du kan överföra till instansen.
Så här hämtar du ett tema:

1. Logga in på din [!DNL Experience Manager Forms] Author-instans.
1. Välj **[!UICONTROL Forms]** > **[!UICONTROL Themes]**.

   ![Välj tema](/help/forms/assets/select-theme.png)

1. Välj temat på sidan Teman och klicka på ikonen **[!UICONTROL Download]** i den övre listen.

   ![Hämta tema](/help/forms/assets/download-theme.png)

   När du hämtar temat visas dialogrutan **[!UICONTROL Download Asset(s)]**.

   ![Hämta temaresurser](/help/forms/assets/download-theme-asset.png)

1. Klicka på **[!UICONTROL Download]**.

De valda resurserna hämtas som ett arkiv (.zip-fil).

## Överför ett tema {#uploading-a-theme}

Du kan överföra och använda teman som andra skapar i dina formulär.
Så här överför du ett tema:

1. Logga in på din [!DNL Experience Manager Forms]-instans.
1. Gå till **[!UICONTROL Forms]** > **[!UICONTROL Themes]** i Experience Manager.

   ![Välj tema](/help/forms/assets/select-theme.png)

1. På sidan Teman klickar du på **[!UICONTROL Create]** > **[!UICONTROL File Upload]**.

   ![Överför tema](/help/forms/assets/theme-upload.png)

1. Bläddra och välj ett temapaket på datorn och klicka på **[!UICONTROL Upload]**. Det överförda temat blir tillgängligt på sidan Teman.

## Använd mappar för att ordna adaptiva Forms-, PDF forms- och samhörande resurser  {#folders-and-organizing-assets}

Du kan använda mappar för att ordna och ordna resurser. Genom att ordna dokument och resurser i en mapp kan du gruppera filerna för enkel hantering. Du kan markera en mapp och välja att hämta eller ta bort den.

### Skapa en mapp {#create-a-folder}

Så här skapar du en mapp:

1. Logga in på din [!DNL Experience Manager Forms]-instans.
1. Välj **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**.

   ![Välj formulär](/help/forms/assets/select-forms.png)

1. Välj **[!UICONTROL Create]** > **[!UICONTROL Folder]**.

   ![Skapa mapp](/help/forms/assets/create-folder.png)

   Dialogrutan **[!UICONTROL Add Folder]** visas.
1. Ange **[!UICONTROL Title]**. **[!UICONTROL Name]** fylls i automatiskt när du skriver **[!UICONTROL Title]**.

   ![Lägg till mapp](/help/forms/assets/add-folder.png)

1. Klicka på **[!UICONTROL Create]**.

   >[!NOTE]
   >
   >Som standard fylls namnfältets värde automatiskt i från titeln. Namnet får bara innehålla alfanumeriska tecken eller bindestreck (-) och understreck (_). Alla andra specialtecken som anges i titeln ersätts automatiskt med ett bindestreck och du uppmanas att bekräfta det nya namnet. Du kan välja att fortsätta med det föreslagna namnet eller redigera det ytterligare.

En ny mapp med den titel du har definierat visas på den aktuella platsen i resurslistan.

Om det finns en mapp med det angivna namnet misslyckas överföringen. Du kan visa felmeddelandet genom att hovra över ikonen ![aem6forms_error_alert](assets/Smock_Alert_18_N.svg) som visas bredvid namnfältet.

Du kan markera den skapade mappen så att den hamnar i mappen och skapa resurser eller mappar i mappen. Du kan också markera en mapp och välja att placera den i kö för hämtning, ta bort den eller redigera namnet på den.

### Skapa kopior av en eller flera resurser {#create-copies-of-one-or-more-assets-or-letters}

Du kan använda en befintlig resurs för att snabbt skapa en resurs med liknande egenskaper, innehåll och ärvda resurser.

Så här skapar du kopior av resurser:

1. Logga in på din [!DNL Experience Manager Forms]-instans.
1. Välj en eller flera resurser på den relevanta tillgångssidan. Gränssnittet visar ikonen **[!UICONTROL Copy]**.
1. Välj **[!UICONTROL Copy]**. Gränssnittet visar ikonen ![Klistra in](/help/forms/assets/Smock_Paste_18_N.svg) .

   ![Kopiera resurs](/help/forms/assets/copy-asset.png)

   Du kan också välja att gå/navigera i en mapp innan du klistrar in. Olika mappar kan innehålla resurser med samma namn. Mer information om mappar finns i [Mappar och ordna resurser](#folders-and-organizing-assets).
1. Välj **[!UICONTROL Paste]**.

   ![Klistra in resurs](/help/forms/assets/paste-asset.png)

1. Dialogrutan **[!UICONTROL Paste]** visas. I systemet genereras namn och titlar automatiskt till de nya kopiorna av resurser, men du kan redigera namn och namn för resurserna.

   Om du kopierar och klistrar in resurserna på samma plats läggs suffixet&quot;-CopyXX&quot; till i det befintliga namnet på `asset`. Om det inte finns någon titel för den kopierade resursen förblir det automatiskt genererade titelfältet tomt.

   ![Klistra in resurs på ny plats](/help/forms/assets/paste-click-asset.png)

   Om det behövs redigerar du **[!UICONTROL Title]** som du vill spara kopian av resursen med. **[!UICONTROL Name]** fylls i automatiskt när du skriver **[!UICONTROL Title]**.
1. Välj **[!UICONTROL Paste]**. Nya kopior av de kopierade resurserna skapas.

## Sök {#search-forms}

När du har ett stort antal resurser är det tidskrävande att söka efter rätt resurs. Du kan utföra en textbaserad sökning efter en viss resurs på resurssidan.

Så här söker du efter resursen:

1. Logga in på din [!DNL Experience Manager Forms]-instans.
1. Klicka på sökikonen ![sök](assets/folder-search-icon.svg) .

   ![Sökformulär](/help/forms/assets/search-form.png)

1. Ange namnet på resursen som du vill söka efter i sökfältet.

1. En lista över relaterade resurser visas. Välj önskad resurs i den visade resurslistan.

   ![Söka efter resurser](/help/forms/assets/search-bar.png)

Mer information och instruktioner om hur du använder sökfunktionen finns i [Sök](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html).

<!--
## Export or create a package {#export-a-workflow-application}

You can use packages to install new content, install new functionality, transfer content between instances, and back up content.
To export or create a package:

1. Log in to your [!DNL Experience Manager Forms] instance.
1. Navigate to **[!UICONTROL Tools]** ![hammer](assets/hammer.png) &gt; **[!UICONTROL Deployment]** &gt; **[!UICONTROL Packages]**.

   ![Package Manager](/help/forms/assets/package-manager.png)

1. Click **[!UICONTROL Create Package]**.

   ![Create package](/help/forms/assets/create-package.png)   
   
   When **[!UICONTROL Create Package]** is clicked, the **[!UICONTROL New Package]** dialog box appears.
1. Specify the package name, version, and group for the package. 
   
   ![New package](/help/forms/assets/new-package.png)  

   * **Package Name** - Select a descriptive name to help you identify the contents of the package.

   * **Version** - It is a textual field to indicate a version. This is appended to the package name to form the name of the zip file.

   * **Group** - This is the target group (or folder) name. Groups help you organize your packages. A folder is created for the group if it does not already exist. If you leave the group name blank, it creates the package in the main package list.

1. Click **[!UICONTROL OK]**.

   Once the package is created, it appears at the top of the list of packages.

1. Click **[!UICONTROL Edit]**.
   
   ![Edit Package](/help/forms/assets/edit-package.png)
    
1. Open the **[!UICONTROL Filters]** tab.
   
   ![Open filter tab](/help/forms/assets/add-filter-package.png)
   
1.  Click **[!UICONTROL Add Filter]**. 
   
      ![Add filter](/help/forms/assets/add-filter.png)

      You can specify the path of the package. You can also add rules and other validations for the package.

      ![Add path](/help/forms/assets/add-path.png)

1. Click **[!UICONTROL Save]** after you are finished editing the settings.
1. Click **[!UICONTROL Build]** to create the package.
    
     ![Build path](/help/forms/assets/build-package.png)

   After the package is built, you can download the package and import it to the other server. The workflow application appears on the server where the package is uploaded.

   >[!NOTE]
   >
   >For the workflow application to work properly, also export the corresponding Adaptive Form and workflow model with the work application.

   Once a package is uploaded to AEM, you can modify its settings. You can also download or delete the package.

## Import and export assets in Correspondence Management {#import-and-export-assets-in-correspondence-management}

To share assets, such as data dictionaries, letters, and document fragments, between two different implementations of Correspondence Management, you can create and share .cmp files. A .cmp file can include one or more data dictionaries, letters, document fragments, and forms.

### Export Document Fragments, Letters, and/or Data Dictionaries {#export-document-fragments-letters-and-or-data-dictionaries}

1. In the letters, document fragments, or data dictionary pages, select and select the assets you want to export to a single package, and then select Queue For Download. The assets are lined-up for export.
1. As required, repeat the above step to add letters, document fragments, and data dictionaries.
1. Select **Download**.
1. Correspondence Management displays Download Asset(s) dialog with a list of assets in the export list.

   ![export](assets/export.png)

1. To view the dependencies that are exported, Select Resolve. Or skip to the next step. Even if you do not select resolve, the dependencies are still exported.
1. To download the .cmp file, select **OK**.
1. Correspondence Management downloads a .cmp file to your computer.

   The .cmp file includes the exported assets. You can share the .cmp file with others. Other users can import the .cmp file in a different server to get all the assets in the new server.

### Export all the Correspondence Management assets as a package {#export-all-the-correspondence-management-assets-as-a-package}

Use this option to download all the Correspondence Management assets and related dependencies as a package from an [!DNL AEM Forms] instance.

For example, if Correspondence Management has a letter that uses an image and text, the downloaded package also contains the image and the text related to the letter. All the metadata properties (including custom properties) associated with the asset are also downloaded. Once you have downloaded the package (.cmp), you can [import the package to a different [!DNL AEM Forms] instance](import-export-forms-templates.md#p-upload-forms-documents-assets-p).

To download all the Correspondence Management assets and related dependencies as a package, complete the following steps:

1. Log in to [!DNL AEM Forms] server as a forms user.
1. Select **Adobe Experience Manager** in the Global Navigation bar.
1. Select tools ( ![tools](assets/tools.png)) and then select **Forms**.
1. Select **Export Correspondence Management Assets**.

   ![publish-cmp-assets-1](assets/publish-cmp-assets-1.png)

   ( ``The Export All Correspondence Management Assets page appears and displays the information about the last time the Export process was attempted and a link to download the last successfully exported package.

   ![export-last-run-details](assets/export-last-run-details.png)

1. Select **Export** and, in the confirm message, select **OK**.

   After a batch process is complete, the last run details and the link to download the package are updated. This includes information such as the Administrator login and if the batch run successfully or failed. The assets are exported to a package and the Download Exported Package link appears.

   >[!NOTE]
   >
   >The Export All Assets process cannot be canceled once initiated. Also, while the export all operation is in process, do not create, delete, modify, or publish any assets or initiate Publish All Assets process.a

1. Select the **Download Exported Package** link to download the package file.

   To add the assets in the package to another instance of Correspondence Management, [import the package to an [!DNL AEM Forms] instance](import-export-forms-templates.md#p-upload-forms-documents-assets-p).

<!-- ### Import Document Fragments, Letters and/or Data Dictionaries into Correspondence Management {#import-document-fragments-letters-and-or-data-dictionaries-into-correspondence-management}

You can import assets that are exported into a .cmp file. A .cmp file can have one or more letters, data dictionaries, document fragments, and dependent assets.

>[!NOTE]
>
>While importing old Correspondence Management assets for migration, log in using an Admin account. For more information on Migrating old Correspondence Management assets, see [Migrate Correspondence Management assets to AEM 6.1 forms](migration-utility.md).

1. On the data dictionary, letters, or document fragments page, select **Create &gt; File Upload** and select the .cmp file.
1. Correspondence Management displays the Import Assets dialog with the list of assets that are imported. Select **Import**.

   After importing the assets, the following properties of the assets are updated while the other properties remain the same:

    * Author: Displays the ID of the user that imported the asset to the server
    * Modified: The time when the asset was imported to the server

   >[!NOTE]
   >
   >For you to be able to upload XDPs (as part of the cmp file or otherwise), you need to be a part of forms-power-users group. For access rights, contact the administrator. -->

## Se även {#see-also}

{{see-also}}
