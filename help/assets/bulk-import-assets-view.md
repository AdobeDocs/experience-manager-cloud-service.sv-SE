---
title: Importera resurser gruppvis i Assets-vyn
description: Lär dig hur du importerar resurser satsvis med det nya användargränssnittet i Assets (Assets-vyn). Det ger administratörer möjlighet att importera ett stort antal resurser från en datakälla till AEM Assets.
exl-id: 10f9d679-7579-4650-9379-bc8287cb2ff1
feature: Asset Management, Publishing, Collaboration, Asset Processing
role: User
source-git-commit: 655f84593adb1199bcfc21cb54071feb3c8523c5
workflow-type: tm+mt
source-wordcount: '1694'
ht-degree: 0%

---

# Importera resurser gruppvis i Assets-vyn  {#bulk-import-assets-view}

Vyn Importera satsvis i AEM Assets ger administratörer möjlighet att importera ett stort antal resurser från en datakälla till AEM Assets. Administratörerna behöver inte längre överföra enskilda resurser eller mappar till AEM Assets.

>[!NOTE]
>
>Massimporteraren i Assets-vyn använder samma serverdel som bulkimporteraren i administratörsvyn. Det erbjuder dock fler datakällor att importera från och en smidigare användarupplevelse.

Du kan importera resurser från följande datakällor:

* Azure
* AWS
* Google Cloud
* Dropbox
* OneDrive

>[!VIDEO](https://video.tv.adobe.com/v/3426857/?learn=on){transcript=true}

## Förutsättningar {#prerequisites}

| Data Source | Förutsättningar |
|-----|------|
| Azure | <ul> <li>Azure Storage-konto </li> <li> Azure Blob Container <li> Azure Access Key eller SAS-token baserat på autentiseringsläge </li></ul> |
| AWS | <ul> <li>AWS </li> <li> AWS Bucket <li> AWS Access Key </li><li> AWS Access Secret </li></ul> |
| Google Cloud | <ul> <li>GCP Bucket </li> <li> E-postadress för GCP-tjänstkonto <li> Privat nyckel för GCP-tjänstkonto</li></ul> |
| Dropbox | <ul> <li>Dropbox klient-ID (programnyckel) </li> <li> Dropbox Client Secret (apphemlighet)</li></ul> |
| OneDrive | <ul> <li>Klient-ID för OneDrive  </li> <li> OneDrive-klient-ID</li><li> OneDrive-klienthemlighet</li></ul> |

Förutom dessa krav som baseras på datakällan måste du vara medveten om källmappsnamnet som finns i datakällan och som innehåller alla resurser som behöver importeras till AEM Assets.

## Konfigurera Dropbox utvecklarprogram {#dropbox-developer-application}

Skapa och konfigurera Dropbox-utvecklarprogrammet innan du importerar resurser från ditt Dropbox-konto till AEM Assets.

Utför följande steg:

1. Logga in på ditt [Dropbox-konto](https://www.dropbox.com/developers) och klicka på **[!UICONTROL Create apps]**. <br>Om du använder ett Enterprise Dropbox-konto måste du ha tillgång till rollen Innehållsadministratör.

1. Markera den enda tillgängliga alternativknappen i avsnittet **[!UICONTROL Choose an API]**.

1. Välj något av följande alternativ i avsnittet **[!UICONTROL Choose the type of access you need]**:

   * Välj **[!UICONTROL App folder]** om du behöver åtkomst till en enda mapp som skapats i ditt program i ditt Dropbox-konto.

   * Välj **[!UICONTROL Full Dropbox]** om du behöver åtkomst till alla filer och mappar på ditt Dropbox-konto.

1. Ange ett namn för programmet och klicka på **[!UICONTROL Create app]**.

1. Lägg till https://experience.adobe.com i avsnittet **[!UICONTROL Settings]** på fliken **[!UICONTROL Redirect URIs]** i ditt program.

1. Kopiera värdena för fälten **[!UICONTROL App key]** och **[!UICONTROL App secret]**. Värdena krävs när verktyget för bulkimport konfigureras i AEM Assets.

1. Lägg till följande behörigheter i avsnittet **[!UICONTROL Permissions]** på fliken **[!UICONTROL Individual scopes]**.

   * account_info.read

   * files.metadata.read

   * files.content.read

   * files.content.write

1. Klicka på **[!UICONTROL Submit]** om du vill spara ändringarna.

## Konfigurera OneDrive-utvecklarprogrammet {#onedrive-developer-application}

Skapa och konfigurera OneDrive-utvecklarprogrammet innan du importerar resurser från ditt OneDrive-konto till AEM Assets.

### Skapa ett program

1. Logga in på ditt [OneDrive-konto](https://portal.azure.com/#view/Microsoft_AAD_RegisteredApps/ApplicationsListBlade) och klicka på **[!UICONTROL New registration]**.

1. Ange ett namn för programmet och välj **[!UICONTROL Accounts in this organizational directory only (Adobe only - Single tenant)]** från **[!UICONTROL Supported account types]**.

1. Utför följande steg för att lägga till omdirigerings-URI:er:

   1. Välj **[!UICONTROL Select a platform]** i listrutan **[!UICONTROL Web]**.

   1. Lägg till https://experience.adobe.com i avsnittet **[!UICONTROL Redirect URIs]**.
   <!-- Add the first URI and click **[!UICONTROL Configure]** to add it. You can add more by clicking **[!UICONTROL Add URI]** option available in the **[!UICONTROL Web]** section on the **[!UICONTROL Authentication]** page. -->

1. Klicka på **[!UICONTROL Register]**. Programmet har skapats.

1. Kopiera värdena för fälten **[!UICONTROL Application (client) ID]** och **[!UICONTROL Directory (tenant) ID]**. Värdena krävs när verktyget för bulkimport konfigureras i AEM Assets.

1. Klicka på **[!UICONTROL Add a certificate or secret]** som motsvarar alternativet **[!UICONTROL Client credentials]**.

1. Klicka på **[!UICONTROL New client secret]**, ange beskrivning av klienthemlighet, förfallodatum och klicka på **[!UICONTROL Add]**.

1. När du har skapat klienthemligheten kopierar du fältet **[!UICONTROL Value]** (kopiera inte fältet för hemligt ID). Det krävs när bulkimport konfigureras i AEM Assets.

### Lägg till API-behörigheter

Utför följande steg för att lägga till API-behörigheter för programmet:

1. Klicka på **[!UICONTROL API permissions]** i den vänstra rutan och klicka på **[!UICONTROL Add a permission]**.
1. Klicka på **[!UICONTROL Microsoft Graph]** > **[!UICONTROL Delegated permissions]**. Avsnittet **[!UICONTROL Select Permission]** visar tillgängliga behörigheter.
1. Välj `offline_access` behörighet från `OpenId permissions` och `Files.ReadWrite.All` behörighet från `Files`.
1. Klicka på **[!UICONTROL Add permissions]** för att spara uppdateringarna.

## Skapa bulkimportkonfiguration {#create-bulk-import-configuration}

Utför följande steg för att skapa en bulkimportkonfiguration i [!DNL Experience Manager Assets]:

1. Klicka på **[!UICONTROL Bulk Import]** i den vänstra rutan och klicka på **[!UICONTROL Create Import]**.
1. Välj datakälla. De tillgängliga alternativen är **[!UICONTROL Azure]**, **[!UICONTROL AWS]**, **[!UICONTROL Google Cloud]**, **[!UICONTROL Dropbox]** och **[!UICONTROL OneDrive]**.
1. Ange ett namn för bulkimportkonfigurationen i fältet **[!UICONTROL Name]**.
1. Ange de autentiseringsuppgifter som är specifika för datakällan och som anges i [Förutsättningar](#prerequisites).
1. Ange namnet på rotmappen som innehåller resurser i datakällan i fältet **[!UICONTROL Source Folder]**.

   >[!NOTE]
   >
   >Om du använder Dropbox som datakälla anger du källmappens sökväg baserat på följande regler:
   >* Om du väljer **Fullständig Dropbox** när du skapar Dropbox-programmet och den mapp som innehåller resurserna finns på `https://www.dropbox.com/home/bulkimport-assets` anger du `bulkimport-assets` i fältet **[!UICONTROL Source Folder]**.
   >* Om du väljer **App-mapp** när du skapar Dropbox-programmet och den mapp som innehåller resurserna finns på `https://www.dropbox.com/home/Apps/BulkImportAppFolderScope/bulkimport-assets` anger du `bulkimport-assets` i fältet **[!UICONTROL Source Folder]** där `BulkImportAppFolderScope` refererar till programmets namn. `Apps` läggs automatiskt till efter `home` i det här fallet.

   >[!NOTE]
   >
   >Om du använder OneDrive som datakälla anger du sökvägen till källmappen baserat på följande regler:
   >* Ange endast namnet på rotmappen, utan domänen. Om den fullständiga URL-sökvägen för mappen är `https://my.sharepoint.com/my?id=/personal/user/Documents/Importfolder/` anger du `/Importfolder/` i fältet **[!UICONTROL Source Folder]**.
   >* Om mappnamnet innehåller flera ord avgränsade med mellanslag anger du namnet med mellanslag i konfigurationen för massimport.
   >* Källmappen måste finnas i katalogens rot. Mappsökvägar stöds inte.

1. (Valfritt) Välj alternativet **[!UICONTROL Delete source file after import]** om du vill ta bort originalfilerna från källdatalagret när filerna har importerats till Experience Manager Assets.
1. Välj **[!UICONTROL Import Mode]**. Välj **[!UICONTROL Skip]**, **[!UICONTROL Replace]** eller **[!UICONTROL Create Version]**. Hoppa över är standardläget och i det här läget hoppar användaren över att importera en resurs om den redan finns.
   ![Importera källinformation](/help/assets/assets/bulk-import-source-details.png)

1. (Valfritt) Ange den metadatafil som ska importeras i CSV-format i fältet **[!UICONTROL Metadata File]**. Källfilen för metadata måste finnas i källmappen. Klicka på **[!UICONTROL Next]** för att navigera till **[!UICONTROL Location & Filters]**.

   >[!NOTE]
   >
   >Beroende på din organisations säkerhetsregler kan du behöva administratörsgodkännande för att det här programmet ska kunna ansluta till verktyget för massimport. Om detta krävs måste administratören ge sitt samtycke innan bulkimportkonfigurationen kan sparas.

1. Om du vill definiera en plats i DAM där resurser ska importeras med fältet **[!UICONTROL Assets Target Folder]** anger du en sökväg. Exempel: `/content/dam/imported_assets`.
1. (Valfritt) I avsnittet **[!UICONTROL Choose Filters]** anger du den minsta filstorleken för resurser i MB som ska inkluderas i inmatningsprocessen i fältet **[!UICONTROL Filter by Min Size]**.
1. (Valfritt) Ange den maximala filstorleken för resurser i MB som ska inkluderas i inmatningsprocessen i fältet **[!UICONTROL Filter by Max Size]**.
1. (Valfritt) Välj de MIME-typer som ska inkluderas i inmatningsprocessen med hjälp av fältet **[!UICONTROL Include MIME Type]**. Du kan välja flera MIME-typer i det här fältet. Om du inte definierar något värde inkluderas alla MIME-typer i inmatningsprocessen.

1. (Valfritt) Välj de MIME-typer som ska uteslutas i inmatningsprocessen med hjälp av fältet **[!UICONTROL Exclude MIME Type]**. Du kan välja flera MIME-typer i det här fältet. Om du inte definierar något värde inkluderas alla MIME-typer i inmatningsprocessen.

   ![Massimportfilter](assets/bulk-import-location.png)

1. Klicka på **[!UICONTROL Next]**. Välj något av följande alternativ efter dina önskemål:

   * **[!UICONTROL Save import]** om du vill spara konfigurationen för tillfället så att du kan köra den senare.
   * **[!UICONTROL Save & run import]** om du vill spara konfigurationen och köra bulkimporten.
   * **[!UICONTROL Save & schedule import]** om du vill spara konfigurationen och schemalägga bulkimporten en senare gång. Du kan välja frekvens för bulkimporten och ange datum och tid för importen. Massimporten körs på det angivna datumet och den angivna tiden i den valda frekvensen.

   ![Kör bulkimport](assets/save-run.png)

1. Klicka på **[!UICONTROL Save]** för att köra det valda alternativet.

### Hantera filnamn vid bulkimport {#filename-handling-bulkimport-assets-view}

När du importerar resurser eller mappar i grupp importerar [!DNL Experience Manager Assets] hela strukturen för det som finns i importkällan. [!DNL Experience Manager] följer de inbyggda reglerna för specialtecken i resurs- och mappnamnen, och därför måste dessa filnamn saneras. För både mappnamn och resursnamn ändras inte den rubrik som definieras av användaren och lagras i `jcr:title`.

Under bulkimporten letar [!DNL Experience Manager] efter de befintliga mapparna för att undvika att importera resurserna och mapparna igen, och verifierar även rensningsreglerna som tillämpas i den överordnade mappen där importen sker. Om saneringsreglerna tillämpas i den överordnade mappen, tillämpas samma regler på importkällan. För ny import används följande saneringsregler för att hantera filnamnen på resurser och mappar.

Mer information om otillåtna namn, hantering av resursnamn och hantering av mappnamn vid bulkimport finns i [Hantera filnamn vid bulkimport i administrationsvyn](add-assets.md##filename-handling-bulkimport).

## Visa befintliga bulkimportkonfigurationer {#view-import-configuration}

Om du vill visa den befintliga massimporten väljer du alternativet **[!UICONTROL Bulk Imports]** i den vänstra rutan. Sidan för bulkimport visas med listan **[!UICONTROL Executed Imports]**. <br>
Du kan även visa **[!UICONTROL Saved Imports]** och **[!UICONTROL Scheduled Imports]** från listrutan.

![Spara bulkimportkonfiguration](assets/bulk-import-options.png)

## Redigera bulkimportkonfiguration {#edit-import-configuration}

Om du vill redigera konfigurationsinformationen klickar du på ![Mer ikon](assets/do-not-localize/more-icon.svg) som motsvarar konfigurationsnamnet och sedan på **[!UICONTROL Edit]**. Du kan inte redigera titeln för konfigurationen och importdatakällan när du utför redigeringsåtgärden. Du kan redigera konfigurationen med hjälp av flikarna Körd, Schemalagd eller Sparad import.

![Redigera bulkimportkonfiguration](assets/edit-bulk-import.png)

## Schemalägg engångs- eller återkommande importer {#schedule-imports}

Så här schemalägger du en enstaka eller återkommande bulkimport:

1. Klicka på ![Mer ikon](assets/do-not-localize/more-icon.svg) som motsvarar konfigurationsnamnet som finns på fliken **[!UICONTROL Executed Imports]** eller **[!UICONTROL Saved Imports]** och klicka på **[!UICONTROL Schedule]**. Du kan också schemalägga om en befintlig schemalagd import genom att gå till fliken **[!UICONTROL Scheduled Imports]** och klicka på **[!UICONTROL Schedule]**.

1. Ställ in ett engångsintag eller schemalägg ett timschema, ett dagligt eller ett veckoschema. Klicka på **[!UICONTROL Submit]**.

   ![Schemalägg bulkimportkonfiguration](assets/bulk-import-schedule.png)

## Utför en hälsokontroll vid import {#import-health-check}

Om du vill validera anslutningen till datakällan klickar du på ![Mer ikon](assets/do-not-localize/more-icon.svg) som motsvarar konfigurationsnamnet och sedan på **[!UICONTROL Check]**. Om anslutningen lyckas visas följande meddelande i Experience Manager Assets:

![Hälsokontroll för massimport](assets/bulk-import-health-check.png)

## Utför en torr körning innan du utför en import {#dry-run-bulk-import}

Klicka på ![Mer ikon](assets/do-not-localize/more-icon.svg) som motsvarar konfigurationsnamnet och klicka på **[!UICONTROL Dry Run]** för att starta en testkörning för massimportjobbet. Experience Manager Assets visar följande information om massimportjobbet:

![Hälsokontroll för massimport](assets/bulk-import-dry-run.png)

## Köra en bulkimport {#run-bulk-import}

Om du har sparat importen när du skapade konfigurationen kan du navigera till fliken Sparad import, klicka på ikonen ![Mer](assets/do-not-localize/more-icon.svg) som motsvarar konfigurationen och klicka på **[!UICONTROL Run]**.

Om du behöver köra en import som redan har slutförts går du till fliken Executed Imports, klickar på ![More icon](assets/do-not-localize/more-icon.svg) som motsvarar konfigurationsnamnet och klickar på **[!UICONTROL Run]**.

## Stoppa eller schemalägg en pågående import {#schedule-stop-ongoing-report}

Du kan schemalägga eller stoppa en pågående bulkimport med dialogrutan för status vid bulkimport som visas på startsidan för massimport under en import.

![Pågående import](assets/bulk-import-progress.png)

Du kan också visa de resurser som har importerats till målmappen genom att klicka på **[!UICONTROL View Assets]**.

## Ta bort en bulkimportkonfiguration {#delete-bulk-import-configuration}

Klicka på ikonen ![Mer](assets/do-not-localize/more-icon.svg) som motsvarar konfigurationsnamnet på flikarna **[!UICONTROL Executed Imports]**, **[!UICONTROL Scheduled Imports]** eller **[!UICONTROL Saved Imports]** och klicka på **[!UICONTROL Delete]** för att ta bort konfigurationen för massimport.

## Navigera till resurser när du har utfört bulkimport {#view-assets-after-bulk-import}

Om du vill visa Assets-målplatsen där resurserna importeras efter att du har kört massimportjobbet klickar du på ![Mer ikon](assets/do-not-localize/more-icon.svg) som motsvarar konfigurationsnamnet och sedan på **[!UICONTROL View Assets]**.
