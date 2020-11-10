---
title: Dela resurser, mappar och samlingar som en länk
description: I den här artikeln beskrivs hur du delar resurser, mappar och samlingar i Experience Manager Assets som en hyperlänk.
contentOwner: AG
translation-type: tm+mt
source-git-commit: b1586cd9d6b3e9da115bff802d840a72d1207e4a
workflow-type: tm+mt
source-wordcount: '878'
ht-degree: 0%

---


# Dela och distribuera resurser som hanteras i Experience Manager {#share-assets-from-aem}

Med Adobe Experience Manager (AEM) Assets kan du dela resurser, mappar och samlingar med medlemmar i organisationen och externa enheter, inklusive partners och leverantörer. Använd följande metoder om du vill dela resurser från Experience Manager Assets som en Cloud Service:

* Dela som en länk.
* Ladda ned resurser och dela dem separat.
* Dela via AEM program.
* Dela via Adobe Asset Link.
* (Kommande funktioner) Dela via varumärkesportalen.

## Dela resurser som en länk {#sharelink}

Använd dialogrutan Länkdelning för att generera URL:en för resurser som du vill dela med användare. Användare med administratörsbehörighet eller läsbehörighet på `/var/dam/share` platsen kan visa de länkar som delas med dem. Att dela resurser via en länk är ett bekvämt sätt att göra resurser tillgängliga för externa parter utan att de först behöver logga in på AEM Assets.

>[!NOTE]
>
>* Du behöver behörigheten Redigera åtkomstkontrollista för mappen eller resursen som du vill dela som en länk.
>* Innan du delar en länk med användarna måste du kontrollera att Dag CQ Mail Service har konfigurerats. Annars inträffar ett fel.


1. I Assets-användargränssnittet väljer du den resurs som ska delas som en länk.
1. From the toolbar, click/tap the **[!UICONTROL Share Link]**. En resurslänk skapas automatiskt i **[!UICONTROL Share Link]** fältet. Kopiera den här länken och dela den med användarna. Länkens standardförfallotid är en dag.

   >[!NOTE]
   >
   >Om en delad resurs flyttas till en annan plats slutar länken att fungera. Återskapa länken och dela den på nytt med användarna.

<!--
## Share assets as a link {#sharelink}

To generate the URL for assets you want to share with users, use the Link Sharing dialog. Users with administrator privileges or with read permissions at `/var/dam/share` location are able to view the links shared with them. Sharing assets through a link is a convenient way of making resources available to external parties without them having to first log in to AEM Assets.

>[!NOTE]
>
>* You need Edit ACL permission on the folder or the asset that you want to share as a link.
>* Before you share a link with users, ensure that Day CQ Mail Service is configured. Otherwise, an error occurs.

1. In the Assets user interface, select the asset to share as a link.
1. From the toolbar, click/tap the **[!UICONTROL Share Link]**.

   An asset link is auto-created in the **[!UICONTROL Share Link]** field. Copy this link and share it with the users. The default expiration time for the link is one day.

   Alternatively, proceed to perform steps 3-7 of this procedure to add email recipients, configure the expiration time for the link, and send it from the dialog.

   >[!NOTE]
   >
   >If a shared asset is moved to a different location, its link stops working. Re-create the link and re-share with the users.

1. From the web console, open the **[!UICONTROL Day CQ Link Externalizer]** configuration and modify the following properties in the **[!UICONTROL Domains]** field with the values mentioned against each:

    * local
    * author
    * publish

   For the local and author properties, provide the URL for the local and author instance respectively. Both local and author properties have the same value if you run a single AEM author instance. For publish, provide the URL for the publish instance.

1. In the email address box of the **[!UICONTROL Link Sharing]** dialog, type the email ID of the user you want to share the link with. You can also share the link with multiple users.

   If the user is a member of your organization, select the user's email ID from the suggested email IDs that appear in the list below the typing area. For an external user, type the complete email ID and then select it from the list.

   To enable emails to be sent out to users, configure the SMTP server details in [Day CQ Mail Service](/help/assets/configure-asset-sharing.md#configmailservice).

   >[!NOTE]
   >
   >If you enter an email ID of a user that is not a member of your organization, the words "External User" are prefixed with the email ID of the user.

1. In the **[!UICONTROL Subject]** box, enter a subject for the asset you want to share.
1. In the **[!UICONTROL Message]** box, enter an optional message.
1. In the **[!UICONTROL Expiration]** field, specify an expiration date and time for the link using the date picker. By default, the expiration date is set for a week from the date you share the link.
1. To let users download the original image along with the renditions, select **[!UICONTROL Allow download of original file]**.

   >[!NOTE]
   >
   >By default, users can only download the renditions of the asset that you share as a link.

1. Click **[!UICONTROL Share]**. A message confirms that the link is shared with the users through an email.
1. To view the shared asset, click/tap the link in the email that is sent to the user. The shared asset is displayed in the **[!UICONTROL Adobe Marketing Cloud]** page.

   To toggle to the list view, click/tap the layout icon in the toolbar.

1. To generate a preview of the asset, click/tap the shared asset. To close the preview and return to the **[!UICONTROL Marketing Cloud]** page, click/tap **[!UICONTROL Back]** in the toolbar. If you have shared a folder, click/tap **[!UICONTROL Parent Folder]** to return to the parent folder.

   >[!NOTE]
   >
   >AEM supports generating the preview of assets of these MIME types: JPG, PNG, GIF, BMP, INDD, PDF, and PPT. You can only download the assets of the other MIME types.

1. To download the shared asset, click/tap **[!UICONTROL Select]** from the toolbar, click/tap the asset, and then click/tap **[!UICONTROL Download]** from the toolbar.
1. To view the assets you shared as links, go to the Assets user interface and click/tap the GlobalNav icon. Choose **[!UICONTROL Navigation]** from the list to display the Navigation pane.
1. From the Navigation pane, choose **[!UICONTROL Shared Links]** to display a list of shared assets.
1. To un-share an asset, select it and tap/click **[!UICONTROL Unshare]** from the toolbar.

A message confirms that you unshared the asset. In addition, the entry for the asset is removed from the list.
-->

## Hämta och dela resurser {#download-and-share-assets}

Users can download the required assets and share these outside of [!DNL Experience Manager]. Mer information finns i [Söka efter resurser](/help/assets/search-assets.md), [hur du hämtar resurser](/help/assets/download-assets-from-aem.md)och [hur du hämtar samlingar](manage-collections.md#download-a-collection)

## Dela material med kreatörer {#share-with-creatives}

Marknadsförare och andra användare kan enkelt dela godkänt material med sina kreatörer genom att

* **AEM datorprogram**: Appen fungerar i Windows och Mac. Se Översikt över [datorprogrammet](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html). Om du vill veta hur en auktoriserad skrivbordsanvändare enkelt kan komma åt de delade resurserna läser du [Bläddra, söka och förhandsgranska resurser](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#browse-search-preview-assets). Skrivbordsanvändare kan skapa resurser och dela dem med sina kollegor som AEM användare, till exempel genom att överföra nya bilder. Se [Överföra resurser med skrivbordsappen](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem).

* **Adobe Asset Link**: Kreatörer kan söka efter och använda material direkt från Adobe InDesign, Adobe Illustrator och Adobe Photoshop.

## Konfigurera materialdelning {#configure-sharing}

De olika alternativen för att dela resurserna kräver specifik konfiguration och har särskilda krav.

### Konfigurera delning av resurslänkar {#asset-link-sharing}

<!-- TBD: Web Console is not there so how to configure Day CQ email service? Or is it not required now? -->

Använd dialogrutan Länkdelning för att generera URL:en för resurser som du vill dela med användare. Användare med administratörsbehörighet eller läsbehörighet på `/var/dam/share` platsen kan visa de länkar som delas med dem. Att dela resurser via en länk är ett bekvämt sätt att göra resurser tillgängliga för externa parter utan att de först behöver logga in på AEM Assets.

>[!NOTE]
>
>Om du vill dela länkar från din AEM Author-instans till externa entiteter måste du se till att du bara visar följande URL:er för `GET` begäranden. Blockera andra URL:er för att säkerställa att din AEM Author-instans är säker.
>* `[aem_server]:[port]/linkshare.html`
>* `[aem_server]:[port]/linksharepreview.html`
>* `[aem_server]:[port]/linkexpired.html`


<!--
## Configure Day CQ mail service {#configmailservice}

Before you can share assets as links, configure the email service.

1. Click or tap the AEM logo, and then navigate to **[!UICONTROL Tools]** &gt; **[!UICONTROL Operations]** &gt; **[!UICONTROL Web Console]**.
1. From the list of services, locate **[!UICONTROL Day CQ Mail Service]**.
1. Click the **[!UICONTROL Edit]** icon beside the service, and configure the following parameters for **Day CQ Mail Service]** with the details mentioned against their names:

    * SMTP server host name: email server host name
    * SMTP server port: email server port
    * SMTP user: email server user name
    * SMTP password: email server password

1. Click/tap **[!UICONTROL Save]**.
-->

### Konfigurera maximal datastorlek {#maxdatasize}

När du hämtar resurser från den länk som delas med funktionen Länkdelning komprimerar AEM resurshierarkin från databasen och returnerar sedan resursen i en ZIP-fil. I avsaknad av begränsningar för den mängd data som kan komprimeras i en ZIP-fil utsätts stora mängder data för komprimering, vilket leder till minnesfel i JVM. För att skydda systemet från en potentiell denial of service-attack på grund av den här situationen kan du konfigurera den maximala storleken på de hämtade filerna. Om resursens okomprimerade storlek överskrider det konfigurerade värdet, avvisas begäranden om hämtning av resurser. Standardvärdet är 100 MB.

1. Click/Tap the AEM logo and then go to **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
1. Leta reda på konfigurationen från webbkonsolen **[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]** .
1. Öppna konfigurationen i redigeringsläge och ändra värdet på **[!UICONTROL Max Content Size (uncompressed)]** parametern.
1. Spara ändringarna.

<!--
Add content or link about how to configure sharing via BP, DA, AAL, etc.
-->

### Aktivera skrivbordsåtgärder som ska användas med skrivbordsappen {#desktop-actions}

I Assets-användargränssnittet i en webbläsare kan du utforska resursplatserna eller checka ut och öppna resursen för redigering i datorprogrammet. Dessa alternativ kallas skrivbordsåtgärder och för att aktivera dem, se [aktivera skrivbordsåtgärder i AEM webbgränssnitt](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2).

![Aktivera skrivbordsåtgärder som ska användas som genväg när du arbetar med skrivbordsappen](assets/enable_desktop_actions.png)

### Konfigurationer för användning av Adobe Asset Link {#configure-asset-link}

Adobe Asset Link effektiviserar samarbetet mellan kreatörer och marknadsförare när det gäller att skapa innehåll. Det kopplar samman Adobe Experience Manager (AEM) Assets med Creative Cloud-programmen Adobe InDesign, Adobe Photoshop och Adobe Illustrator. På Adobe Asset Link-panelen kan kreativa användare komma åt och ändra innehåll som lagras i AEM Assets utan att lämna de kreativa program de är mest bekanta med.

Se [hur du konfigurerar AEM för Adobe Asset Link](https://helpx.adobe.com/enterprise/using/configure-aem-assets-for-asset-link.html).

## Bästa praxis och felsökning {#bestpractices}

* Resursmappar eller samlingar som innehåller ett tomt utrymme i namnet kanske inte delas.
* Om användarna inte kan hämta de delade resurserna, bör du fråga AEM administratören vilka [hämtningsgränser](#maxdatasize) som finns.

<!--
* If you cannot send email with links to shared assets or if the other users cannot receive your email, check with your AEM administrator if the [email service](/help/assets/configure-asset-sharing.md#configmailservice) is configured or not. 
* If you cannot share assets using link sharing functionality, ensure that you have the appropriate permissions. See [share assets](#sharelink).
-->

<!--
Add content or link about how to share using Brand Portal when it is available on Cloud Service.
-->
