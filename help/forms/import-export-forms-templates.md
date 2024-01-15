---
title: Hur importerar, exporterar och organiserar man Adaptive Forms eller PDF forms i en AEM Forms-instans?
description: Lär dig att migrera adaptiva Forms, PDF forms, teman och andra stödresurser till och från en AEM.
topic-tags: forms-manager
role: Admin, User
feature: Adaptive Forms
source-git-commit: 527c9944929c28a0ef7f3e617ef6185bfed0d536
workflow-type: tm+mt
source-wordcount: '1127'
ht-degree: 0%

---

# Importera eller exportera anpassningsbara Forms- och AEM Forms-resurser {#importing-and-exporting-assets-to-aem-forms}

Du kan flytta adaptiva Forms och relaterade resurser som adaptiva formulärteman, formulärdatamodeller, adaptiva formulärmallar, dokumentfragment och PDF forms mellan [!DNL AEM Forms] -instanser. Du kan importera och exportera resurser i CRX-paket eller binära filformat.

När du exporterar ett anpassat formulär exporteras inte innehållsprinciperna och mallarna. Använd [Pakethanteraren](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#how-rolling-deployments-work) för att exportera sådana resurser.

## Ladda ned anpassningsbara Forms-, PDF forms- och samhörande resurser {#download-forms-amp-documents-assets}

Så här hämtar du formulär eller relaterade resurser:

1. Logga in på [!DNL AEM Forms] -instans.
1. Välj **[!UICONTROL Adobe Experience Manager]** ![adobeexperienceManager](assets/adobeexperiencemanager.png) ikon > **[!UICONTROL Navigation]** ![kompass](assets/Smock_Compass_18_N.svg) ikon > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**.
1. Markera resurserna och välj **[!UICONTROL Download]** -ikon.
1. Välj något av följande alternativ i Hämta resurser och välj sedan **[!UICONTROL Download]**.

   * **Hämta som CRX-paket:** Använd alternativet för att hämta och flytta alla markerade resurser och relaterade beroenden från en [!DNL AEM Forms] till en annan instans. Den hämtar alla resurser och mappar som ett CRX-paket, inklusive formulär som skapats i AEM (adaptiva Forms och adaptiva formulärfragment), formuläruppsättningar, formulärdatamodell, formulärmallar, PDF-dokument och refererade resurser (XSD-filer och bilder).
Fördelen med att hämta resurser som ett paket är att det även hämtar refererade resurser. Om du till exempel har ett adaptivt formulär som använder en formulärmall, XSD och en bild. När du väljer det här adaptiva formuläret och hämtar det som ett paket innehåller det hämtade paketet även formulärmallen, XSD och bilden. Alla metadataegenskaper (inklusive anpassade egenskaper) som är kopplade till resursen hämtas också.

   * **Hämta resurser som binära filer:** Använd alternativet om du bara vill hämta formulärmallar (XDP), PDF forms (PDF), dokument (PDF) och resurser (bilder, scheman, formatmallar). Du kan redigera dessa resurser med externa program. Det hämtar resurser som har binära filer, t.ex. bilder, PDF och andra format som stöds som en ZIP-fil.
Du kan inte hämta adaptiva Forms, adaptiva formulärfragment, teman och formuläruppsättningar med **[!UICONTROL Download assets as binary files]** alternativ. Om du vill hämta resurserna bör du använda **[!UICONTROL Download as CRX Package]** alternativ.

   De valda resurserna hämtas som ett arkiv (.zip-fil).

   >[!NOTE]
   >
   >Både AEM och binära filer hämtas som arkiv (.zip-fil). Mallarna för resurserna hämtas inte tillsammans med resurserna. Du måste exportera resursmallarna separat.

## Överför adaptiva Forms-, PDF forms- eller samhörande resurser {#upload-forms-amp-documents-assets}

Du kan överföra de resurstyper som stöds individuellt eller som ett ZIP-arkiv. För en ZIP-fil visas de relativa sökvägarna för alla resurser som stöds. Resurser som inte stöds i ZIP ignoreras och visas inte. Om ZIP-arkivet bara innehåller resurser som inte stöds visas ett felmeddelande i stället för popup-dialogrutan.
Så här överför du ett formulär eller en relaterad resurs:

1. Logga in på [!DNL AEM Forms] -instans.
1. Välj **[!UICONTROL Adobe Experience Manager]** ![adobeexperienceManager](assets/adobeexperiencemanager.png) ikon > **[!UICONTROL Navigation]** ![kompass](assets/Smock_Compass_18_N.svg) ikon > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**.
1. Välj **[!UICONTROL Create]** > **[!UICONTROL File Upload]**. En dialogruta visas.
1. I dialogrutan bläddrar du till och väljer paketet eller arkivet som ska importeras. Du kan också välja andra filtyper som stöds. Välj **[!UICONTROL Open]**. Mappen eller filnamnet som du väljer får inte innehålla några specialtecken.

   Verifiera i dialogrutan informationen om de resurser som överförs och välj **[!UICONTROL Upload]**.

   Om du överför en befintlig formulärresurs uppdateras resursen.

   >[!NOTE]
   >
   > * När ett namn hamnar i konflikt med olika resurstyper ersätter inte överföring av ett paket den befintliga mapphierarkin. Om du t.ex. har ett adaptivt formulär som heter &#39;Utbildning&#39; på platsen /content/dam/formSanddocuments på en server. Du hämtar det adaptiva formuläret och överför det till en annan server. Den andra servern har också en mapp med namnet &quot;Training&quot; på samma plats /content/dam/formSanddocuments. Överföringen misslyckas.
   > * Endast en medlem i `form-power-user` kan överföra XDP-filer.


## Hämta ett tema {#downloading-a-theme}

Du kan exportera teman i [!DNL AEM Forms] som du kan använda i andra projekt eller instanser. Med AEM kan du hämta teman som en zip-fil som du kan överföra till instansen.

Så här hämtar du ett tema:

1. Logga in på [!DNL AEM Forms] -instans.
1. Välj **[!UICONTROL Adobe Experience Manager]** ![adobeexperienceManager](assets/adobeexperiencemanager.png) ikon > **[!UICONTROL Navigation]** ![kompass](assets/Smock_Compass_18_N.svg) ikon > **[!UICONTROL Forms]** > **[!UICONTROL Themes]**.
1. Välj temat och välj **[!UICONTROL Download]**. Temat laddas ned som ett arkiv (.zip-fil).

## Överför ett tema {#uploading-a-theme}

Du kan överföra och använda teman som andra skapar i dina formulär. Så här överför du ett tema:

1. I Experience Manager går du till **[!UICONTROL Forms]** > **[!UICONTROL Themes]**.
1. På sidan Teman klickar du på **[!UICONTROL Create]** > **[!UICONTROL File Upload]**.
1. Bläddra och välj ett temapaket på datorn i filöverföringsprompten och klicka på **[!UICONTROL Upload]**. Det överförda temat är tillgängligt på temasidan.

<!-- ## Import and export assets in Correspondence Management {#import-and-export-assets-in-correspondence-management}

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

## Exportera ett arbetsflödesprogram {#export-a-workflow-application}

Du kan använda pakethanteraren för att exportera arbetsflödesprogram. Proceduren är som anges nedan:

1. Öppna [!DNL AEM Forms] pakethanteraren. URL för pakethanteraren är `https://[server]:[port]/crx/packmgr`.
1. Klicka på **[!UICONTROL Create Package]**. The **[!UICONTROL New Package]** visas.
1. Ange paketets namn, version och grupp. Klicka på **[!UICONTROL OK]**.
1. Klicka **[!UICONTROL Edit]** och öppna **[!UICONTROL Filters]** -fliken. Klicka på **[!UICONTROL Add Filter]**. Ange sökvägen till arbetsflödesprogrammet. Exempel: /etc/fd/dashboard/startpoints/homemortgage. Klicka på **[!UICONTROL Add rule]**.

1. Öppna **[!UICONTROL Advanced]** -fliken. Välj **[!UICONTROL Merge]** eller **[!UICONTROL Overwrite]** i fältet ACL-hantering. Klicka på **[!UICONTROL Save]**.
1. Klicka **[!UICONTROL Build]** för att skapa paketet.

   När paketet har skapats kan du hämta det och importera det till den andra servern. Arbetsflödesprogrammet visas på servern där paketet överförs.

   >[!NOTE]
   >
   >För att arbetsflödesprogrammet ska fungera på rätt sätt exporterar du även motsvarande adaptiva formulär- och arbetsflödesmodell med arbetsprogrammet.

## Använd mappar för att ordna adaptiva Forms-, PDF forms- och samhörande resurser  {#folders-and-organizing-assets}

Du kan använda mappar för att ordna och ordna resurser. Genom att ordna dokument och resurser i en mapp kan du gruppera filerna för enkel hantering. Du kan markera en mapp och välja att hämta eller ta bort den. Så här skapar du en mapp:

### Skapa en mapp {#create-a-folder}

1. Logga in på [!DNL AEM Forms] -instans.
1. Markera Experience Manager ![adobeexperienceManager](assets/adobeexperiencemanager.png) icon > navigation ![kompass](assets/Smock_Compass_18_N.svg) ikon> **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**.
1. Välj **[!UICONTROL Create]** > **[!UICONTROL Folder]**.
1. Ange följande information:

   * **[!UICONTROL Title]**: Visningsnamn för mappen
   * **[!UICONTROL Name]**: *(Obligatoriskt)* Det nodnamn under vilket du vill lagra mappen i databasen

   >[!NOTE]
   >
   >Som standard fylls namnfältets värde automatiskt i från titeln. Namnet får bara innehålla alfanumeriska tecken eller bindestreck (-) och understreck (_). Alla andra specialtecken som anges i titeln ersätts automatiskt med ett bindestreck och du uppmanas att bekräfta det nya namnet. Du kan välja att fortsätta med det föreslagna namnet eller redigera det ytterligare.

1. En ny mapp med den titel du har definierat visas på den aktuella platsen i resurslistan.

   Om det finns en mapp med det angivna namnet misslyckas överföringen. Du kan visa felmeddelandet genom att hovra över felet ![aem6forms_error_alert](assets/Smock_Alert_18_N.svg) -ikonen som visas bredvid namnfältet.

   Du kan markera den skapade mappen så att den hamnar i mappen och skapa resurser eller mappar i mappen. Du kan också markera en mapp och välja att placera den i kö för hämtning, ta bort den eller redigera namnet på den.


<!-- ### Create copies of one or more assets or letters {#create-copies-of-one-or-more-assets-or-letters}

You can use an existing assets to quickly create an asset with similar properties, content, and inherited assets.

Complete the following steps to create copies of assets and letters:

1. On the relevant assets page, select one or more assets. The UI displays the Copy icon.
1. Select **[!UICONTROL Copy]**. The UI displays the **[!UICONTROL Paste]** icon. You can also choose to go/navigate inside a folder before you paste. Different folders can contain assets with same names. For more information on folders, see [Folders and organizing assets](#folders-and-organizing-assets).
1. Select **[!UICONTROL Paste]**. The **[!UICONTROL Paste]** dialog appears. The system auto generates names and titles to the new copies of assets/letters, but you can edit the titles and names of the assets/letters.

   If you are copying and pasting the assets/letters at the same place, a suffix "-CopyXX" gets added to the existing name of the asset/letter. If no title existed for the copied asset/letter, the auto generated title field remains blank.

1. If necessary, edit the Title and Name with which you want to save the copy of the asset/letter.
1. Select **[!UICONTROL Paste]**. New copies of the copied assets are created.

## Search {#search-forms}

You ca use the top bar **[A]** to search your content. When you search for assets, a side panel is displayed. You can also select ![assets-browser-content-only](assets/assets-browser-content-only.png) &gt; Filter **[B]** to invoke the side panel. Using the various filters in the side panel, you can narrow down your search. The side panel also lets you save your searches.

![search_topbar](assets/search_topbar.png)

**A.** Search **B.** Filter

![Side panel - Filters](assets/search_sidepanel.png)

Side panel - Filters

On the side panel, you can use the following to narrow down your search results:

* Search Directory
* Tags
* Search Criteria; for example, Modified Dates, Publish Status, LiveCopy Status.

The side panel also lets you save your search settings with names of your choice.

For more information and instructions on using search, filters, saved search, and side panel, see [Search](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html). -->

>[!MORELIKETHIS]
>
>* [Använd teman i komponenter med adaptiv form](/help/forms/using-themes-in-core-components.md)