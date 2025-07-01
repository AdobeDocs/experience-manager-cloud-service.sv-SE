---
title: Hämta resurser från Content Hub
description: Lär dig hur du hämtar en eller flera resurser och deras återgivningar från Content Hub-portalen.
role: User
exl-id: 96d4ffba-4e3e-4496-9da2-6eb36be8331f
source-git-commit: 31c9e742d8bdf69c12788794670817864c9c027a
workflow-type: tm+mt
source-wordcount: '777'
ht-degree: 0%

---

# Hämta resurser från Content Hub {#download-assets}

Med [!DNL Content Hub] kan du hämta och dela dina resurser. Användargränssnittet [!DNL Content Hub] visar bara godkända resurser. Dessa resurser kan vara bilder, videor eller annat digitalt innehåll. [!DNL Content Hub] förbättrar tillgängligheten och anpassbarheten för effektiv resursdistribution.

Du kan hämta en eller flera resurser och deras tillgängliga återgivningar med [!DNL Content Hub].

Se de [typer av återgivningar som är tillgängliga i Content Hub](#types-of-renditions).

## Hämta en eller flera resurser och deras återgivningar {#download-asset-renditions}

Så här hämtar du en eller flera resurser och deras återgivningar:

1. Om du vill hämta en resurs väljer du ![hämta](/help/assets/assets/download-icon.svg) som finns på resurskortet för att förhandsgranska resursen, markerar de tillgängliga återgivningarna och klickar på alternativet **[!UICONTROL Download]** i dialogrutan för att hämta de valda återgivningarna som en ZIP-fil. Om dialogrutan visar en resurslicens (för en licensierad mediefil) godkänner du licensvillkoren och klickar på **[!UICONTROL Download]**.
   ![](/help/assets/assets/download-an-asset-CH-from-asset-card.png)

   Du kan också klicka på resursens miniatyrbild och välja ![download](/help/assets/assets/download-icon.svg) för att markera och visa de tillgängliga återgivningarna i dialogrutan innan du hämtar dem.

1. Om du vill hämta flera resurser markerar du resurserna, klickar på ![hämta](/help/assets/assets/download-icon.svg) **[!UICONTROL Download]** och granskar listan över valda resurser i dialogrutan **[!UICONTROL Download assets]**. Klicka på ![avmarkera](/help/assets/assets/Close.svg) bredvid en resurs för att avmarkera den i listan. Markera en eller flera återgivningar och klicka på **[!UICONTROL Download]** för att hämta dem som en ZIP-fil. Om du väljer **[!UICONTROL Smart Crop]** och **[!UICONTROL Static Renditions]** hämtas alla tillgängliga statiska och smarta beskärningsåtergivningar för varje markerad resurs.
   ![hämta flera resurser](/help/assets/assets/download-multiple-assets-CH.png)
Du kan fortsätta använda [!DNL Content Hub] medan hämtningen pågår. Content Hub avbryter inte arbetsflödet under hämtningen.
   ![hämta flera resurser](/help/assets/assets/download-assets-notification-ch.png)
Om dialogrutan **[!UICONTROL Download assets]** visar resurslicenser väljer du varje licens i den vänstra rutan ([!UICONTROL T&C Documents] avsnitt) för att förhandsgranska licensen och visa de valda resurserna som är kopplade till licensen i den mittersta rutan i dialogrutan. När du har granskat varje licens väljer du renderingarna, klickar på **[!UICONTROL I have read and accepted the terms & conditions mentioned above]** och väljer **[!UICONTROL Download]** för att hämta dem.
   ![hämta flera resurser](/help/assets/assets/download-multiple-licensed-assets-CH.png)

   >[!NOTE]
   >
   >* Återgivningarna visas bara om deras synlighet har aktiverats med användargränssnittet [[!UICONTROL Configuration]](/help/assets/configure-content-hub-ui-options.md#renditions-content-hub).
   >* De användare som har åtkomst till [[!DNL Dynamic Media with Open API capabilities]](/help/assets/dynamic-media-open-apis-overview.md) kan visa och hämta dynamiska och smarta beskärningsåtergivningar.
   >* Förhandsgranskningen av licensen visas bara om resursen har godkänts med [!DNL Assets as a Cloud Service]-redigeringsmiljön. Mer information finns i [Hantera licensierade mediefiler på Content Hub](/help/assets/manage-licensed-assets-on-content-hub.md).

<!--

## Download an asset and its renditions {#download-asset-renditions} 

To download an asset and its renditions, execute the following steps: 

1. Click the asset to view its properties.

1. Click ![download](/help/assets/assets/download-icon.svg) to see the list of available asset renditions in the **[!UICONTROL Download]** panel.

   >[!NOTE]
   >
   >* The renditions display only if their visibility is enabled using the [Configuration](/help/assets/configure-content-hub-ui-options.md#renditions-content-hub) User Interface.
   >* You can download all [static, dynamic, and smart crop renditions](#types-of-renditions) while downloading an asset.

1. Select one or more renditions and click **[!UICONTROL Download]** to download the selected renditions as a zip file. 
While downloading a licensed asset, select **[!UICONTROL I have read and accepted the terms & conditions mentioned above]** before clicking **[!UICONTROL Download]**. You can also click **[!UICONTROL terms & conditions]** to view the asset license. The preview of the license displays only if the asset is approved using Assets as a Cloud Service authoring environment. For more information, see [Manage licensed assets on Content Hub](/help/assets/manage-licensed-assets-on-content-hub.md).

   ![Download single asset renditions](/help/assets/assets/download-single-asset-renditions.png)


If you are downloading a licensed asset, select **[!UICONTROL I have read and accepted the terms & conditions mentioned above]** and then click **[!UICONTROL Download]**. You can also click **[!UICONTROL terms & conditions]** to view the asset license. The preview of the license displays only if the asset is approved using Assets as a Cloud Service authoring environment. For more information, see [Manage licensed assets on Content Hub](/help/assets/manage-licensed-assets-on-content-hub.md).

>[!NOTE]
>
> The users with access to [Dynamic Media with Open API capabilities](/help/assets/dynamic-media-open-apis-overview.md) can view and download dynamic and smart crop renditions.

## Download multiple assets and their renditions {#download-multiple-assets-renditions} 

To download multiple assets and their renditions, execute the following steps: 

1. Select the assets and click ![download](/help/assets/assets/download-icon.svg) **[!UICONTROL Download]**. The [!UICONTROL Download assets] screen displays listing all the selected assets. 
1. Click **[!UICONTROL Download]** to select from the various download options to begin download:

    * **Download [!UICONTROL Originals]**: Select this option to download the selected assets in the original form.
    * **Download [!UICONTROL Static Renditions only]**: Select this option to download all available static renditions of assets except the original assets.
    * **Download [!UICONTROL Originals & Static Renditions]**: Select this option to download both original and static renditions of the selected assets. 

      ![Download multiple renditions](/help/assets/assets/download-multiple-renditions.png)

      >[!NOTE]
      >
      >* The renditions display only if their visibility is enabled using the [Configuration](/help/assets/configure-content-hub-ui-options.md#renditions-content-hub) User Interface.
      >* You can only download [static renditions](#types-of-renditions) while downloading multiple assets.

    If any of the selected asset is a licensed asset, click the license of the asset in left pane to see its preview, which enables you to select **[!UICONTROL I have read and accepted the terms & conditions mentioned above]** and then click **[!UICONTROL Download]**. The preview of the license displays only if the asset is approved using Assets as a Cloud Service authoring environment. For more information, see [Manage licensed assets on Content Hub](/help/assets/manage-licensed-assets-on-content-hub.md).

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

Läs mer om att [visa och hantera återgivningar i [!DNL Experience Manager Assets]](/help/assets/renditions.md).

[!DNL Experience Manager Assets] stöder följande typer av återgivningar:

* [Statiska återgivningar](/help/assets/renditions.md#static-renditions): Statiska återgivningar är förskapade versioner av digitala resurser, som vanligtvis genereras vid tillgångsintag eller ändring. De är optimerade för specifika användningsområden och plattformar, som webbminiatyrer, mobilvänliga format för responsiv design eller högupplösta filer för utskrift, vilket ger en smidig och enhetlig upplevelse.

* [Dynamiska återgivningar](/help/assets/renditions.md#dynamic-renditions): Dynamiska återgivningar är anpassade versioner av resurser i realtid som utför olika åtgärder, till exempel att ändra storlek på bilder för olika enhetsupplösningar eller beskära för att passa olika proportioner. Med dessa renderingar kan ni erbjuda personaliserade och optimerade upplevelser för större behov. Dynamiska återgivningar av resurser skapas i [!DNL Adobe Experience Manager Assets]-redigeringsmiljön. Mer information om steg som krävs för att aktivera dynamiska renderingar finns i [Aktivera dynamiska renderingar](#enable-dynamic-media-renditions).

* [Smart beskärning](/help/assets/dynamic-media/image-profiles.md#creating-image-profiles): Den smarta beskärningen fokuserar enbart på den viktigaste delen av en resurs under beskärningsprocessen. Dynamic Media Smart crop utnyttjar artificiell intelligens från Adobe Sensei för att spåra intressepunkten och säkerställa att våra resurser ser så bra ut som möjligt på alla skärmstorlekar. [!DNL Adobe Experience Manager] smart beskärning visar bredden och höjden på en resursåtergivning tillsammans med titeln. Mer information finns på [med SmartCrop med AEM Assets Dynamic Media](https://experienceleague.adobe.com/en/docs/experience-manager-learn/assets/dynamic-media/images/smart-crop-feature-video-use).

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



