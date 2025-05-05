---
title: Hämta resurser från Content Hub
description: Lär dig hur du hämtar resurser från Content Hub-portalen
role: User
exl-id: 96d4ffba-4e3e-4496-9da2-6eb36be8331f
source-git-commit: e108d25f3cdc025e0fbe8010854f245f62786baf
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 0%

---

# Hämta resurser från Content Hub {#download-assets}

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
   >* Återgivningarna visas bara om deras synlighet har aktiverats med användargränssnittet [Konfiguration](/help/assets/configure-content-hub-ui-options.md#renditions-content-hub) .
   >* Du kan hämta alla [statiska, dynamiska och smarta beskärningsåtergivningar](#types-of-renditions) när du hämtar en resurs.

1. Markera en eller flera återgivningar och klicka på **[!UICONTROL Download]**.

   ![Hämta renderingar för en enskild resurs](/help/assets/assets/download-single-asset-renditions.png)


Om du hämtar en licensierad resurs väljer du **[!UICONTROL I have read and accepted the terms & conditions mentioned above]** och klickar sedan på **[!UICONTROL Download]**. Du kan också klicka på **[!UICONTROL terms & conditions]** för att visa resurslicensen. Förhandsgranskningen av licensen visas bara om resursen har godkänts i Assets as a Cloud Service-redigeringsmiljön. Mer information finns i [Hantera licensierade mediefiler på Content Hub](/help/assets/manage-licensed-assets-on-content-hub.md).

>[!NOTE]
>
> De användare som har tillgång till [Dynamiska medier med Open API-funktioner](/help/assets/dynamic-media-open-apis-overview.md) kan visa och hämta dynamiska och smarta beskärningsrenderingar.

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
     >* Återgivningarna visas bara om deras synlighet har aktiverats med användargränssnittet [Konfiguration](/help/assets/configure-content-hub-ui-options.md#renditions-content-hub) .
     >* Du kan bara hämta [statiska återgivningar](#types-of-renditions) när du hämtar flera resurser.

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

* [Dynamiska återgivningar](/help/assets/renditions.md#dynamic-renditions): Dynamiska återgivningar är anpassade versioner av resurser i realtid som utför olika åtgärder, till exempel att ändra storlek på bilder för olika enhetsupplösningar eller beskära för att passa olika proportioner. Med dessa renderingar kan ni erbjuda personaliserade och optimerade upplevelser för större behov. Dynamiska återgivningar av resurser skapas i [!DNL Adobe Experience Manager Assets]-redigeringsmiljön. Mer information om steg som krävs för att aktivera dynamiska renderingar finns i [Aktivera dynamiska renderingar](#enable-dynamic-media-renditions).

* [Smart beskärning](/help/assets/dynamic-media/image-profiles.md#creating-image-profiles): Den smarta beskärningen fokuserar enbart på den viktigaste delen av en resurs under beskärningsprocessen. Dynamic media smart crop for utnyttjar artificiell intelligens som drivs av Adobe Sensei för att spåra intressepunkten och säkerställa att våra resurser ser ut som de bästa på alla skärmstorlekar. [!DNL Adobe Experience Manager] smart beskärning visar bredden och höjden på en resursåtergivning tillsammans med titeln. Mer information finns på [med SmartCrop med AEM Assets Dynamic Media](https://experienceleague.adobe.com/sv/docs/experience-manager-learn/assets/dynamic-media/images/smart-crop-feature-video-use).

  Smart Crop-renderingar visas och är bara tillgängliga för hämtning om du har tillgång till [Dynamic Media med OpenAPI-funktioner](/help/assets/dynamic-media-open-apis-overview.md). Återgivningar för smart beskärning är bara tillgängliga för bildresurser.

  ![Återgivningstyper](/help/assets/assets/renditions-types.png)

### Aktivera dynamiska återgivningar {#enable-dynamic-media-renditions}

Så här aktiverar du dynamiska återgivningar:

1. Kontrollera att du har tillgång till [Dynamiska media med OpenAPI-funktioner](/help/assets/dynamic-media-open-apis-overview.md).

   När du har tillgång till Dynamic Media med OpenAPI-funktioner är alla resurser som markerats som `Approved` tillgängliga för offentlig leverans med Dynamic Media.

1. Ange [godkännandemålet för resursen](/help/assets/approve-assets-content-hub.md#set-approval-target) till Content Hub för att godkänna resurser enbart för Content Hub.

1. Aktivera växeln **[!UICONTROL Enable availability of renditions]** som finns på fliken **[!UICONTROL Renditions]** i användargränssnittet [Configuration](/help/assets/configure-content-hub-ui-options.md#access-configuration-options-content-hub).

1. Spara om de befintliga bildförinställningarna så att de blir tillgängliga i Content Hub. Det gäller endast om du nyligen har anslutit till Dynamic Media med OpenAPI.

   Om du vill spara om de befintliga bildförinställningarna går du till administratörsvyn och väljer **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Image Presets]**. Välj en förinställning, klicka på **[!UICONTROL Edit]** och sedan på **[!UICONTROL Save]**.



   >[!NOTE]
   > 
   > Dynamiska återgivningar är bara tillgängliga för bildresurser.



