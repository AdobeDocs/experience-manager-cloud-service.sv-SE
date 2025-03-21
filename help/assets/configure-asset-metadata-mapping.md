---
title: Konfigurera metadatamappning mellan Workfront och Experience Manager Assets
description: Mappa metadatafält för resurser mellan Adobe Workfront- och Experience Manager as a Cloud Service-program. När du skickar en resurs från Workfront till Experience Manager Assets kan du mappa metadata för resursen i Experience Manager Assets genom att mappa metadatafält.
exl-id: 71400769-b2bc-4f5d-8b6b-a73598e837b4
feature: Metadata, Workfront Integrations and Apps
role: User, Admin
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '982'
ht-degree: 0%

---

# Konfigurera metadatamappning mellan Adobe Workfront och Experience Manager Assets {#asset-metadata-mapping-workfront-aem-assets}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime och Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets-integrering med Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI-utökningsbarhet</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Aktivera Dynamic Media Prime och Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Sök efter bästa praxis</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Metadata - bästa praxis</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamiska media med OpenAPI-funktioner</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets-dokumentation för utvecklare</b></a>
        </td>
    </tr>
</table>

Du kan mappa metadatafälten för resurser mellan Adobe Workfront- och Experience Manager as a Cloud Service-program. När du skickar en resurs från Workfront till Experience Manager Assets kan du mappa metadata för resursen i Experience Manager Assets genom att mappa metadatafält.

Om du till exempel behöver behålla metadatafälten för en bild som namn, beskrivning och det projekt som den tillhör i Workfront när du skickar bilden till Experience Manager Assets, ska du konfigurera och mappa dessa fält till Experience Manager Assets-egenskaper.

**Använd skiftläge**

Det finns en bild `add-users-workfront.png` i projektet `Metadata Syncs` i Adobe Workfront-programmet. Du måste skicka bilden till Experience Manager Assets as a Cloud Service med följande metadata:

* Projektnamn

* Dokumentnamn

* Dokumentbeskrivning

## Förutsättningar {#prerequisites}

* Administratörsåtkomst till Workfront- och Experience Manager Assets as a Cloud Service-program.

* En integrering mellan [Workfront- och Experience Manager Assets as a Cloud Service-program](https://one.workfront.com/s/document-item?bundleId=the-new-workfront-experience&amp;topicId=Content%2FDocuments%2FAdobe_Workfront_for_Experience_Manager_Assets_Essentials%2Fsetup-asset-essentials.htm&amp;_LANG=enus).

## Ställ in metadatamappning i Workfront {#set-up-metadata-mapping}

Så här anger du metadatamappning för fälten Projektnamn, Dokumentnamn och Dokumentbeskrivning i Workfront:

1. Klicka på ikonen Huvudmeny ![Visa meny](assets/show-menu.svg) i det övre högra hörnet av Adobe Workfront-programmet och klicka sedan på **[!UICONTROL Setup]**.

1. Välj **[!UICONTROL Documents]** i den vänstra panelen och välj sedan **[!UICONTROL Experience Manager Assets]**.

1. Välj Experience Manager Assets-integrering och klicka på **[!UICONTROL Edit]**.

1. Klicka på **[!UICONTROL Metadata]**. Mappa fältet [!UICONTROL Project] > [!UICONTROL Name] Workfront till fältet `wm:projectName` Experience Manager Assets på fliken **[!UICONTROL Assets]**. Om du inte hittar den exakta matchningen rekommenderar Adobe att du söker efter den bästa matchningen för att mappa fältet Workfront och Experience Manager Assets. Du kan undvika att mappa fält med olika datatyper. Du kan till exempel mappa ett Workfront-datumfält till ett Assets-beskrivningsfält.
1. Mappa fältet [!UICONTROL Document] > [!UICONTROL Name] Workfront till fältet `wm:documentName` Experience Manager Assets.

   ![Mappning i Workfront](assets/workfront-metadata-mapping.png)

1. Mappa fältet [!UICONTROL Document] > [!UICONTROL Description] Workfront till fältet `dc:description` Experience Manager Assets.

   >[!VIDEO](https://video.tv.adobe.com/v/344255)

## Skicka bilden från Workfront till Experience Manager Assets {#send-image-workfront-assets}

Skicka bilden från Workfront till Experience Manager Assets:

1. Klicka på ikonen Huvudmeny ![Visa meny](assets/show-menu.svg) i det övre högra hörnet av Adobe Workfront-programmet och klicka sedan på **[!UICONTROL Projects]**.

1. Klicka på **[!UICONTROL New Project]** om du vill skapa ett projekt.

1. Klicka på alternativet **[!UICONTROL Documents]** i den vänstra rutan, dra och markera sedan bilden som du vill skicka till Experience Manager Assets.

1. Klicka på **[!UICONTROL Send to]** och välj sedan integrationsnamnet för Experience Manager Assets Essentials.

   ![Skicka till AEM](assets/send-to-aem.png)

1. Välj målmapp för resursen och klicka sedan på **[!UICONTROL Select Folder]**.

1. Klicka på **[!UICONTROL Save]**.

## Konfigurera metadatamappning av resurser i Experience Manager as a Cloud Service {#metadata-mapping-aem}

När du har [konfigurerat mappningen av metadata för resursen i Adobe Workfront](#set-up-metadata-mapping) måste du använda samma mappning i Experience Manager Assets as a Cloud Service-programmet för att visa lämpliga metadataresultat för bilden.

Metadatamappning utförs med metadatamappningar i Experience Manager Assets. Du kan redigera ett nyligen tillagt eller befintligt metadatchemaformulär. Metadatchemaformuläret innehåller flikar och formulärobjekt på flikar. Du kan mappa/konfigurera dessa formulärobjekt till ett fält i en metadatanod i CRX-databasen. Du kan lägga till flikar eller formulärobjekt i metadatchemaformuläret. Mer information finns i [Metadata Schemas](metadata-schemas.md).

Så här konfigurerar du metadatamappning med ett nytt metadataformulär i Experience Manager Assets as a Cloud Service:

1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Metadata Schemas]**.

1. Klicka på **[!UICONTROL Create]** i verktygsfältet. Ange schemaformulärets rubrik i dialogrutan och klicka på **[!UICONTROL Create]** för att slutföra formulärskapandet.

1. Markera schemaformuläret och klicka på **[!UICONTROL Edit]**.

1. (Valfritt) Klicka på `+` i Formulärredigeraren för metadataschema för att skapa en flik för Workfront-fälten.

1. Klicka på fliken **[!UICONTROL Build Form]** och dra komponenten **[!UICONTROL Single Line Text]** till formuläret. Klicka på komponenten i formuläret. På fliken **[!UICONTROL Build Form]**:

   1. Ange `Project Name` i fältet **[!UICONTROL Field Label]**.

   1. Ange `./jcr:content/metadata/wm:projectName` i fältet **[!UICONTROL Map to property]**. Som vägledning kan du använda följande mall för att definiera fältmappningar i Experience Manager Assets:
      `./jcr:content/metadata/<mapping defined for the field in workfront>`.

      När du konfigurerade mappningar i Workfront mappades `wm:projectName` Experience Manager Assets-fält till Project > Name Workfront-fält.

      `wm` refererar till namnutrymmets namn och `projectName` refererar till egenskapens titel. Använd formatet `namespace:propertyTitle` för att definiera metadatafältsmappningar.

      ![Skicka till AEM](assets/metadata-schema-mapping.png)

1. Klicka på fliken **[!UICONTROL Build Form]** och dra komponenten **[!UICONTROL Single Line Text]** till formuläret. Klicka på komponenten i formuläret. På fliken **[!UICONTROL Build Form]**:

   1. Ange `Document Name` i fältet **[!UICONTROL Field Label]**.

   1. Ange `./jcr:content/metadata/wm:documentName` i fältet **[!UICONTROL Map to property]**.
När du konfigurerade mappningar i Workfront mappades `wm:documentName` Experience Manager Assets-fält till fältet Dokument > Namn på Workfront.

1. Klicka på fliken **[!UICONTROL Build Form]** och dra komponenten **[!UICONTROL Multi Line Text]** till formuläret. Klicka på komponenten i formuläret. På fliken **[!UICONTROL Build Form]**:

   1. Ange `Document Description` i fältet **[!UICONTROL Field Label]**.

   1. Ange `./jcr:content/metadata/dc:description` i fältet **[!UICONTROL Map to property]**.
När du konfigurerade mappningar i Workfront mappades `dc:description` Experience Manager Assets-fält till Workfront-fältet Dokument > Beskrivning.

1. Klicka på **[!UICONTROL Save]** om du vill spara ändringarna.

   >[!VIDEO](https://video.tv.adobe.com/v/344314)

## Använd metadatainställningar för bildmappen {#apply-metadata-settings-image-folder}

När du har konfigurerat metadatainställningarna i Experience Manager as a Cloud Service-programmet kan du använda de inställningarna i mappen [som innehåller den bild som skickas från Workfront-programmet](#send-image-workfront-assets).

Så här använder du metadatainställningar för bildmappen:

1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Metadata Schemas]**.

1. Välj metadatamatchemat i listan och klicka på **[!UICONTROL Apply to Folders]**.

1. Markera målmappen som [bilden skickas till från Adobe Workfront-programmet](#send-image-workfront-assets) och klicka på **[!UICONTROL Apply]**.

Du kan navigera till bilden i Experience Manager Assets och visa de metadata som är associerade med bilden. Markera bilden och klicka på **[!UICONTROL Properties]** för att visa bildens metadata.

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
