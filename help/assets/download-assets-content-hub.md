---
title: Hämta resurser från Content Hub
description: Lär dig hur du hämtar resurser från Content Hub-portalen
role: User
exl-id: 96d4ffba-4e3e-4496-9da2-6eb36be8331f
source-git-commit: 28424cb184d0378669498c78e571961227f6539a
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Hämta resurser från Content Hub {#download-assets}

| [Sök efter bästa praxis](/help/assets/search-best-practices.md) | [Metadata - bästa praxis](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [Dynamic Media med OpenAPI-funktioner](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets-dokumentation för utvecklare](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

<!-- ![Download assets](assets/download-asset.jpg) -->
![Hämta resurser](assets/download-asset-genstudio.jpeg)

>[!AVAILABILITY]
>
>Content Hub Guide finns nu i PDF-format. Ladda ned hela guiden och använd Adobe Acrobat AI Assistant för att besvara dina frågor.
>
>[!BADGE Content Hub Guide PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

Med Content Hub kan du hämta och dela dina resurser. Content Hub användargränssnitt visar endast godkända resurser. Dessa resurser kan vara bilder, videor eller annat digitalt innehåll. Content Hub förbättrar tillgängligheten och anpassbarheten för effektiv materialdistribution.

Du kan hämta en eller flera resurser och deras tillgängliga återgivningar med Content Hub.

## Hämta en resurs och dess återgivningar {#download-asset-renditions}

Så här hämtar du en resurs och dess återgivningar:

1. Klicka på resursen för att visa dess egenskaper.

1. Klicka på ![download](/help/assets/assets/download-icon.svg) för att starta hämtningsprocessen. På hämtningspanelen visas alla tillgängliga resursåtergivningar (original och andra återgivningar).

   >[!NOTE]
   >
   Återgivningarna visas bara om deras synlighet har aktiverats med användargränssnittet [Konfiguration](/help/assets/configure-content-hub-ui-options.md#renditions-content-hub) .

1. Markera återgivningarna och klicka på **[!UICONTROL Download]**.

   ![Hämta renderingar för en enskild resurs](/help/assets/assets/download-single-asset-renditions.png)


Om du hämtar en licensierad resurs väljer du **[!UICONTROL I have read and accepted the terms & conditions mentioned above]** och klickar sedan på **[!UICONTROL Download]**. Du kan också klicka på **[!UICONTROL terms & conditions]** för att visa resurslicensen. Förhandsgranskningen av licensen visas bara om resursen har godkänts i Assets as a Cloud Service redigeringsmiljö. Mer information finns i [Hantera licensierade mediefiler på Content Hub](/help/assets/manage-licensed-assets-on-content-hub.md).

## Hämta flera resurser och deras återgivningar {#download-multiple-assets-renditions}

Så här hämtar du flera resurser och deras återgivningar:

1. Markera resurserna och klicka på ![Hämta](/help/assets/assets/download-icon.svg) **[!UICONTROL Download]**. Skärmen [!UICONTROL Download assets] visar en lista med alla markerade resurser.
1. Klicka på **[!UICONTROL Download]** för att välja bland de olika hämtningsalternativen för att påbörja hämtningen:

   * **Hämta[!UICONTROL Originals]**: Välj det här alternativet om du vill hämta de valda resurserna i det ursprungliga formuläret.
   * **Hämta[!UICONTROL Renditions only]**: Välj det här alternativet om du vill hämta alla tillgängliga återgivningar av resurserna förutom de ursprungliga resurserna.
   * **Hämta[!UICONTROL Originals & All renditions]**: Välj det här alternativet om du vill hämta både original och återgivningar av de markerade resurserna.

     ![Hämta flera återgivningar](/help/assets/assets/download-multiple-renditions.png)

     >[!NOTE]
     >
     Återgivningarna visas bara om deras synlighet har aktiverats med användargränssnittet [Konfiguration](/help/assets/configure-content-hub-ui-options.md#renditions-content-hub) .

   Om någon av de markerade resurserna är en licensierad resurs klickar du på licensen för resursen i den vänstra rutan för att se förhandsvisningen, vilket gör att du kan välja **[!UICONTROL I have read and accepted the terms & conditions mentioned above]** och sedan klicka på **[!UICONTROL Download]**. Förhandsgranskningen av licensen visas bara om resursen har godkänts i Assets as a Cloud Service redigeringsmiljö. Mer information finns i [Hantera licensierade mediefiler på Content Hub](/help/assets/manage-licensed-assets-on-content-hub.md).

   ![download-multiple-license](/help/assets/assets/download-multiple-license.png)

<!--1. On the Content Hub homepage, select the asset and click **Download**. The **Download assets** dialog box displays a license or list of licenses associated with the selected assets in the left pane. 
1. Click a license in the left pane to see its PDF in the middle pane and the associated assets with it in the right pane. The license PDF preview is displayed only if the license is approved in your Assets as a Cloud Service environment. [Approve the license PDFs](/help/assets/approve-assets-content-hub.md) of the selected assets to see their previews.
1. Optional: Click ![remove-icon](/help/assets/assets/remove-icon.svg) to remove a license from the dialog box.
1. Select **I have read and accept all the terms and conditions mentioned above.** 
1. Click **Download** to download the selected assets.-->

<!---This dialog box displays the list of licenses associated with the selected assets in the left pane. Select a license to preview its terms and conditions (in pdf format) in the middle pane and the preview of the associated assets to the license in the right. Reviewed licenses are highlighted in light blue.


The dialog box that displays depends on whether the download list includes expired assets or only non-expired assets. <br/>
**Download expired assets dialog box:** This dialog box displays the expired assets' preview along with their expiry date in the left pane. The expired assets' count out of total selected displays in the right pane. Click **Proceed with all assets** to download expired assets with other assets (if present). The Download assets dialog box displays. See the [Download assets dialog box](#Download-asset-dialog-box) to proceed further.
    
    >[!NOTE]
    >
    >[Enable the download option for expired assets](/help/assets/configure-content-hub-ui-options.md#expired-assets-content-hub) to download them. Only expired assets that have enabled downloading are available for download.

   <a id="Download-asset-dialog-box"></a> **Download assets dialog box:** This dialog box displays the list of licenses associated with the selected assets in the left pane. Select a license to preview its terms and conditions (in pdf format) in the middle pane and the associated assets' preview and their count in the right pane. Reviewed licenses are highlighted in light blue.

    >[!NOTE]
    >
    > The **Download Asset dialog box** previews licensing terms and conditions only for approved licenses. [Approve the assets' licenses](/help/assets/approve-assets-content-hub.md) before downloading them to preview their licensing terms in the **Download Asset dialog box**.

1. Click  ![remove-icon](/help/assets/assets/remove-icon.svg) to remove a license from the download dialog box. 

1. Accept the terms and conditions and then click **Download** to download assets associated with the available licenses in the left pane.-->
<!--![download-multiple-license](/help/assets/assets/download-multiple-license.png)-->

<!---
### Download non-licensed Assets {#download-non-licensed-assets}

 To download non-licensed assets, select the assets and click ![download](/help/assets/assets/download-icon.svg) from the top rail.-->







