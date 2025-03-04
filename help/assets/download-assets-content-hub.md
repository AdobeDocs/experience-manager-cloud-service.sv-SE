---
title: Hämta resurser från Content Hub
description: Lär dig hur du hämtar resurser från Content Hub-portalen
role: User
exl-id: 96d4ffba-4e3e-4496-9da2-6eb36be8331f
source-git-commit: 523ba2ae59bfc0d35cca350a8daf3e20ac9e5332
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 0%

---

# Hämta resurser från Content Hub {#download-assets}

| [Sök efter bästa praxis](/help/assets/search-best-practices.md) | [Metadata - bästa praxis](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [Dynamiska media med OpenAPI-funktioner](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets-dokumentation för utvecklare](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
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

Se [typer av renderingar i Content Hub](#types-of-renditions).

## Hämta en resurs och dess återgivningar {#download-asset-renditions}

Så här hämtar du en resurs och dess återgivningar:

1. Klicka på resursen för att visa dess egenskaper.

1. Klicka på ![download](/help/assets/assets/download-icon.svg) för att starta hämtningsprocessen. På hämtningspanelen visas alla tillgängliga resursåtergivningar.

   >[!NOTE]
   >
   * Återgivningarna visas bara om deras synlighet har aktiverats med användargränssnittet [Konfiguration](/help/assets/configure-content-hub-ui-options.md#renditions-content-hub) .
   * Du kan hämta alla [statiska, dynamiska och smarta beskärningsåtergivningar](#types-of-renditions) när du hämtar en resurs.

1. Markera en eller flera återgivningar och klicka på **[!UICONTROL Download]**.

   ![Hämta renderingar för en enskild resurs](/help/assets/assets/download-single-asset-renditions.png)


Om du hämtar en licensierad resurs väljer du **[!UICONTROL I have read and accepted the terms & conditions mentioned above]** och klickar sedan på **[!UICONTROL Download]**. Du kan också klicka på **[!UICONTROL terms & conditions]** för att visa resurslicensen. Förhandsgranskningen av licensen visas bara om resursen har godkänts i Assets as a Cloud Service-redigeringsmiljön. Mer information finns i [Hantera licensierade mediefiler på Content Hub](/help/assets/manage-licensed-assets-on-content-hub.md).

>[!NOTE]
>
De användare som har tillgång till [Dynamiska medier med Open API-funktioner](/help/assets/dynamic-media-open-apis-overview.md) kan visa och hämta dynamiska och smarta beskärningsrenderingar.

## Hämta flera resurser och deras återgivningar {#download-multiple-assets-renditions}

Så här hämtar du flera resurser och deras återgivningar:

1. Markera resurserna och klicka på ![Hämta](/help/assets/assets/download-icon.svg) **[!UICONTROL Download]**. Skärmen [!UICONTROL Download assets] visar en lista med alla markerade resurser.
1. Klicka på **[!UICONTROL Download]** för att välja bland de olika hämtningsalternativen för att påbörja hämtningen:

   * **Hämta[!UICONTROL Originals]**: Välj det här alternativet om du vill hämta de valda resurserna i det ursprungliga formuläret.
   * **Hämta[!UICONTROL Static Renditions only]**: Välj det här alternativet om du vill hämta alla tillgängliga statiska återgivningar av resurser förutom de ursprungliga resurserna.
   * **Hämta[!UICONTROL Originals & Static Renditions]**: Välj det här alternativet om du vill hämta både ursprungliga och statiska återgivningar av de valda resurserna.

     ![Hämta flera återgivningar](/help/assets/assets/download-multiple-renditions.png)

     >[!NOTE]
     >
     * Återgivningarna visas bara om deras synlighet har aktiverats med användargränssnittet [Konfiguration](/help/assets/configure-content-hub-ui-options.md#renditions-content-hub) .
     * Du kan bara hämta [statiska återgivningar](#types-of-renditions) när du hämtar flera resurser.

   Om någon av de markerade resurserna är en licensierad resurs klickar du på licensen för resursen i den vänstra rutan för att se förhandsvisningen, vilket gör att du kan välja **[!UICONTROL I have read and accepted the terms & conditions mentioned above]** och sedan klicka på **[!UICONTROL Download]**. Förhandsgranskningen av licensen visas bara om resursen har godkänts i Assets as a Cloud Service-redigeringsmiljön. Mer information finns i [Hantera licensierade mediefiler på Content Hub](/help/assets/manage-licensed-assets-on-content-hub.md).

   <!--![download-multiple-license](/help/assets/assets/download-multiple-license.png)-->

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


## Typ av återgivning {#types-of-renditions}

Resursåtergivningar är olika representationer av en tillgångs originalfil. Det kan vara miniatyrbilder, optimerade versioner för webb eller mobiler, vattenstämplade eller DRM-skyddade filer eller till och med dynamiska element som smarta beskärningar. De behöver inte matcha den ursprungliga filtypen, utan de representerar resursen i olika fall.

Läs mer om att [visa och hantera återgivningar i Experience Manager Assets](/help/assets/renditions.md).

[!DNL Experience Manager Assets] stöder följande typer av återgivningar:

* [Statiska återgivningar](/help/assets/renditions.md#static-renditions): Statiska återgivningar är förskapade versioner av digitala resurser, som vanligtvis genereras vid tillgångsintag eller ändring. De är optimerade för specifika användningsområden och plattformar, som webbminiatyrer, mobilvänliga format för responsiv design eller högupplösta filer för utskrift, vilket ger en smidig och enhetlig upplevelse.

* [Dynamiska återgivningar](/help/assets/renditions.md#dynamic-renditions): Dynamiska återgivningar är anpassade versioner av resurser i realtid som utför olika åtgärder, till exempel att ändra storlek på bilder för olika enhetsupplösningar eller beskära för att passa olika proportioner. Med dessa renderingar kan ni erbjuda personaliserade och optimerade upplevelser för större behov. Dynamiska återgivningar av resurser skapas i [!DNL Adobe Experience Manager Assets]-redigeringsmiljön.

* [Smart beskärning](/help/assets/dynamic-media/image-profiles.md#creating-image-profiles): Den smarta beskärningen fokuserar enbart på den viktigaste delen av en resurs under beskärningsprocessen. Dynamic media smart crop for utnyttjar artificiell intelligens som drivs av Adobe Sensei för att spåra intressepunkten och säkerställa att våra resurser ser ut som de bästa på alla skärmstorlekar. [!DNL Adobe Experience Manager] smart beskärning visar bredden och höjden på en resursåtergivning tillsammans med titeln. Mer information finns på [med SmartCrop med AEM Assets Dynamic Media](https://experienceleague.adobe.com/en/docs/experience-manager-learn/assets/dynamic-media/images/smart-crop-feature-video-use).

  ![Återgivningstyper](/help/assets/assets/renditions-types.png)


>[!NOTE]
> 
* Funktionen för dynamiska och smarta beskärningsåtergivningar är i tidiga Adobe-faser. [Skapa och skicka ett Adobe kundsupportärende](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html) om du vill få tillgång till funktionen.
* Nya kunder som har anslutit till [Dynamic Media Open API-tjänster](/help/assets/dynamic-media-open-apis-overview.md) måste ändra sina befintliga bildförinställningar för godkännande.



