---
title: Konfigurera metadatamappning mellan Workfront och Experience Manager Assets
description: Mappa metadatafälten för resurser mellan as a Cloud Service Adobe Workfront- och Experience Manager-program. När du skickar en resurs från Workfront till Experience Manager Assets kan du mappa metadata för resursen i Experience Manager Assets genom att mappa metadatafält.
exl-id: 71400769-b2bc-4f5d-8b6b-a73598e837b4
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 2%

---

# Konfigurera metadatamappning mellan Adobe Workfront och Experience Manager Assets {#asset-metadata-mapping-workfront-aem-assets}

Du kan mappa metadatafälten för resurser mellan as a Cloud Service Adobe Workfront- och Experience Manager-program. När du skickar en resurs från Workfront till Experience Manager Assets kan du mappa metadata för resursen i Experience Manager Assets genom att mappa metadatafält.

Om du till exempel behöver behålla metadatafälten för en bild som namn, beskrivning och det projekt som den tillhör i Workfront när du skickar bilden till Experience Manager Assets, ska du konfigurera och mappa dessa fält till Experience Manager Assets-egenskaper.

**Användningsfall**

En bild `add-users-workfront.png` finns i `Metadata Syncs` i Adobe Workfront. Du måste skicka bilden till Experience Manager Assets as a Cloud Service med följande metadata:

* Projektnamn

* Dokumentnamn

* Dokumentbeskrivning

## Förutsättningar {#prerequisites}

* Administratörsåtkomst till as a Cloud Service Workfront- och Experience Manager Assets-program.

* Integrering mellan [as a Cloud Service Workfront- och Experience Manager Assets-program](https://one.workfront.com/s/document-item?bundleId=the-new-workfront-experience&amp;topicId=Content%2FDocuments%2FAdobe_Workfront_for_Experience_Manager_Assets_Essentials%2Fsetup-asset-essentials.htm&amp;_LANG=enus).

## Ställ in metadatamappning i Workfront {#set-up-metadata-mapping}

Så här anger du metadatamappning för fälten Projektnamn, Dokumentnamn och Dokumentbeskrivning i Workfront:

1. Klicka på ikonen Huvudmeny ![Visa meny](assets/show-menu.svg) i det övre högra hörnet av Adobe Workfront-programmet och klicka sedan på **[!UICONTROL Setup]**.

1. Välj **[!UICONTROL Documents]** i den vänstra panelen väljer **[!UICONTROL Experience Manager Assets]**.

1. Välj Experience Manager Assets-integrering och klicka på **[!UICONTROL Edit]**.

1. Klicka på **[!UICONTROL Metadata]**. I **[!UICONTROL Assets]** mappa [!UICONTROL Project] > [!UICONTROL Name] Workfront-fält till `wm:projectName` Fält i Experience Manager Assets. Om du inte hittar den exakta matchningen rekommenderar Adobe att du söker efter den bästa matchningen för att mappa fältet Workfront och Experience Manager Assets. Du kan undvika att mappa fält med olika datatyper. Du kan till exempel mappa ett Workfront-datumfält till ett Assets-beskrivningsfält.
1. Mappa [!UICONTROL Document] > [!UICONTROL Name] Workfront-fält till `wm:documentName` Fält i Experience Manager Assets.

   ![Mappning i Workfront](assets/workfront-metadata-mapping.png)

1. Mappa [!UICONTROL Document] > [!UICONTROL Description] Workfront-fält till `dc:description` Fält i Experience Manager Assets.

   >[!VIDEO](https://video.tv.adobe.com/v/344255)

## Skicka bilden från Workfront till Experience Manager Assets {#send-image-workfront-assets}

Så här skickar du bilden från Workfront till Experience Manager Assets:

1. Klicka på ikonen Huvudmeny ![Visa meny](assets/show-menu.svg) i det övre högra hörnet av Adobe Workfront-programmet och klicka sedan på **[!UICONTROL Projects]**.

1. Klicka **[!UICONTROL New Project]** för att skapa ett nytt projekt.

1. Klicka **[!UICONTROL Documents]** som finns i den vänstra rutan drar och markerar sedan den bild som du vill skicka till Experience Manager Assets.

1. Klicka **[!UICONTROL Send to]** väljer du sedan integrationsnamnet för Experience Manager Assets Essentials.

   ![Skicka till AEM](assets/send-to-aem.png)

1. Välj målmapp för resursen och klicka sedan på **[!UICONTROL Select Folder]**.

1. Klicka på **[!UICONTROL Save]**.

## Konfigurera metadatamappning för resurser på Experience Manager as a Cloud Service {#metadata-mapping-aem}

Efter [konfigurera metadatamappning av resurser i Adobe Workfront](#set-up-metadata-mapping)måste du använda samma mappning i Experience Manager Assets as a Cloud Service program för att visa lämpliga metadateresultat för bilden.

Metadatamappning utförs med metadatamappningar i Experience Manager Assets. Du kan redigera ett nyligen tillagt eller befintligt metadatchemaformulär. Metadatchemaformuläret innehåller flikar och formulärobjekt på flikar. Du kan mappa/konfigurera dessa formulärobjekt till ett fält i en metadatanod i CRX-databasen. Du kan lägga till flikar eller formulärobjekt i metadatchemaformuläret. Mer information finns i [Metadata-scheman](metadata-schemas.md).

Så här konfigurerar du metadatamappning med ett nytt metadataformulär i Experience Manager Assets as a Cloud Service:

1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Metadata Schemas]**.

1. Klicka på **[!UICONTROL Create]** i verktygsfältet. Ange schemaformulärets rubrik i dialogrutan och klicka på **[!UICONTROL Create]** för att slutföra formulärskapandet.

1. Markera schemaformuläret och klicka på **[!UICONTROL Edit]**.

1. (Valfritt) Klicka på Formulärredigeraren för metadatamodell i `+` för att skapa en ny flik för Workfront-fälten.

1. Klicka på **[!UICONTROL Build Form]** och dra **[!UICONTROL Single Line Text]** till formuläret. Klicka på komponenten i formuläret. I **[!UICONTROL Build Form]** tab:

   1. Ange `Project Name` i **[!UICONTROL Field Label]** fält.

   1. Ange `./jcr:content/metadata/wm:projectName` i **[!UICONTROL Map to property]** fält. Som vägledning kan du använda följande mall för att definiera fältmappningar i Experience Manager Assets:
      `./jcr:content/metadata/<mapping defined for the field in workfront>`.

      När du konfigurerar mappningar i Workfront har du mappat `wm:projectName` Experience Manager Assets-fält till Projekt > Namn på Workfront-fält.

      `wm` refererar till namnutrymmets namn och `projectName` refererar till egenskapsrubriken. Använd `namespace:propertyTitle` format för att definiera mappningar av metadatafält.

      ![Skicka till AEM](assets/metadata-schema-mapping.png)

1. Klicka på **[!UICONTROL Build Form]** och dra **[!UICONTROL Single Line Text]** till formuläret. Klicka på komponenten i formuläret. I **[!UICONTROL Build Form]** tab:

   1. Ange `Document Name` i **[!UICONTROL Field Label]** fält.

   1. Ange `./jcr:content/metadata/wm:documentName` i **[!UICONTROL Map to property]** fält.
När du konfigurerar mappningar i Workfront har du mappat `wm:documentName` Experience Manager Assets-fält till Dokument > Namn på Workfront-fält.

1. Klicka på **[!UICONTROL Build Form]** och dra **[!UICONTROL Multi Line Text]** till formuläret. Klicka på komponenten i formuläret. I **[!UICONTROL Build Form]** tab:

   1. Ange `Document Description` i **[!UICONTROL Field Label]** fält.

   1. Ange `./jcr:content/metadata/dc:description` i **[!UICONTROL Map to property]** fält.
När du konfigurerar mappningar i Workfront har du mappat `dc:description` Experience Manager Assets-fält till Dokument > Workfront-beskrivningsfält.

1. Klicka **[!UICONTROL Save]** för att spara ändringarna.

   >[!VIDEO](https://video.tv.adobe.com/v/344314)

## Använd metadatainställningar för bildmappen {#apply-metadata-settings-image-folder}

När du har konfigurerat metadatainställningarna i det as a Cloud Service Experience Manager-programmet använder du de inställningarna i [mapp som innehåller den bild som skickas från Workfront-programmet](#send-image-workfront-assets).

Så här använder du metadatainställningar för bildmappen:

1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Metadata Schemas]**.

1. Välj metadatamatchemat i listan och klicka på **[!UICONTROL Apply to Folder(s)]**.

1. Välj målmappen som [bilden skickas från Adobe Workfront-programmet](#send-image-workfront-assets) och klicka **[!UICONTROL Apply]**.

Du kan navigera till bilden i Experience Manager Assets och visa de metadata som är associerade med bilden. Markera bilden och klicka på **[!UICONTROL Properties]** för att visa bildens metadata.

**Se även**

* [Översätt resurser](translate-assets.md)
* [HTTP API för Assets](mac-api-assets.md)
* [Resurser som stöds i filformat](file-format-support.md)
* [Söka efter resurser](search-assets.md)
* [Anslutna resurser](use-assets-across-connected-assets-instances.md)
* [Materialrapporter](asset-reports.md)
* [Metadata-scheman](metadata-schemas.md)
* [Hämta resurser](download-assets-from-aem.md)
* [Hantera metadata](manage-metadata.md)
* [Söka efter fasetter](search-facets.md)
* [Hantera samlingar](manage-collections.md)
* [Import av massmetadata](metadata-import-export.md)
