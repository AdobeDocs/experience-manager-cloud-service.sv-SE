---
title: Distribuera och dela resurser, mappar och samlingar
description: Distribuera dina digitala resurser med metoder som att dela som en länk, hämta och via  [!DNL Brand Portal], [!DNL desktop app] och [!DNL Asset Link].
feature: Asset Management, Collaboration, Asset Distribution
role: Admin, User
exl-id: 14e897cc-75c2-42bd-8563-1f5dd23642a0
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '1771'
ht-degree: 0%

---

# Dela och distribuera resurser som hanteras i [!DNL Experience Manager] {#share-assets-from-aem}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/link-sharing.html?lang=sv-SE) |
| AEM as a Cloud Service | Den här artikeln |

Med [!DNL Adobe Experience Manager Assets] kan du dela resurser, mappar och samlingar med medlemmar i din organisation och externa entiteter, inklusive partners och leverantörer. Använd följande metoder för att dela resurser från [!DNL Experience Manager Assets] som en [!DNL Cloud Service]:

* [Dela som länk](#sharelink).
* [Hämta resurser](/help/assets/download-assets-from-aem.md) och dela separat.
* Dela med [[!DNL Experience Manager] skrivbordsappen](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html?lang=sv-SE).
* Dela med [[!DNL Adobe Asset Link]](https://www.adobe.com/creativecloud/business/enterprise/adobe-asset-link.html).
* Dela med [[!DNL Brand Portal]](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html?lang=sv-SE).

## Förutsättningar {#prerequisites}

Du behöver administratörsbehörighet för att [konfigurera inställningar för delning av resurser som en länk](#config-link-share-settings).

## Konfigurera inställningar för länkdelning {#config-link-share-settings}

I [!DNL Experience Manager Assets] kan du konfigurera standardinställningarna för länkdelning.

1. Klicka på logotypen [!DNL Experience Manager] och navigera sedan till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Assets Configuration]** > **[!UICONTROL Link Share]**.
1. Inledande inställningar:

   * **Inkludera original:**

      * Välj `Select Include Originals` om du vill välja alternativet `Include Originals` som standard i dialogrutan för länkdelning.
      * Välj hur alternativet `Include Originals` visas i dialogrutan Länkdelning. [!UICONTROL Editable] tillåter användaren att ändra de inställningar som definieras här i Inledande inställningar. Med `Read-only` visas inställningen, men den kan inte ändras. `Hidden` döljer inställningen och använder det värde som konfigurerats här i de ursprungliga inställningarna.
   * **Inkludera återgivningar:**
      * Välj alternativet `Select Include Renditions` om du vill välja alternativet `Include Renditions` som standard i dialogrutan för länkdelning.
      * Välj hur alternativet `Include Renditions` visas i dialogrutan Länkdelning. [!UICONTROL Editable] tillåter användaren att ändra de inställningar som definieras här i Inledande inställningar. Med `Read-only` visas inställningen, men den kan inte ändras. `Hidden` döljer inställningen och använder det värde som konfigurerats här i de ursprungliga inställningarna.

1. Ange standardgiltighetsperioden för länken i fältet `Validity Period` i avsnittet `Expiration date`.

1. **[!UICONTROL Link share]**-knapp i åtgärdsfältet:
   * Alla användare med `jcr:modifyAccessControl` behörigheter kan visa alternativet [!UICONTROL Link share]. Den är synlig som standard för alla administratörer. Knappen [!UICONTROL Link share] är som standard synlig för alla. Du kan konfigurera så att det här alternativet endast visas för de definierade grupperna eller så kan du även neka det här alternativet från specifika grupper. Välj `Allow only for groups` om du vill tillåta att specifika grupper kan visa alternativet `Share Link`. Välj `Deny from groups` om du vill neka alternativet `Share Link` från specifika grupper. När du har valt något av dessa alternativ anger du gruppnamnen med fältet `Select Groups` för att lägga till gruppnamnen som du måste tillåta eller neka.

Information om inställningar för e-postkonfiguration finns på [Dokumentation för e-posttjänst](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/examples/email-service.html?lang=sv-SE)

![Konfigurera e-posttjänst](/help/assets/assets/config-email-service.png)

## Dela resurser som en länk {#sharelink}

Att dela resurser via en länk är ett bekvämt sätt att göra resurserna tillgängliga för externa parter, marknadsförare och andra [!DNL Experience Manager]-användare. Med den här funktionen kan anonyma användare få åtkomst till och hämta de resurser som delas med dem. När du hämtar resurser från en delad länk använder [!DNL Experience Manager Assets] en asynkron tjänst som ger snabbare och oavbruten hämtning. De resurser som ska laddas ned står i kö i bakgrunden i ZIP-arkiv med hanterbar filstorlek. Vid stora nedladdningar paketeras nedladdningen i flera filer på 100 GB per filstorlek.

<!--
Users with administrator privileges or with read permissions at `/var/dam/share` location are able to view the links shared with them. 
-->

>[!NOTE]
>
>* Du behöver behörigheten Redigera åtkomstkontrollista för mappen eller resursen som du vill dela som en länk.
>* [Aktivera utgående e-post](/help/implementing/developing/introduction/development-guidelines.md#sending-email) innan du delar en länk med användarna.

Det finns två sätt att dela resurserna med hjälp av länkdelningsfunktionen:

1. Generera en delad länk, [kopiera och dela resurslänken](#copy-and-share-assets-link) med andra användare.
1. Generera en delad länk och [dela resurslänken via e-post](#share-assets-link-through-email). Du kan ändra standardvärdena, till exempel förfallodatum och förfallotid, och tillåta hämtning av originalresurserna och dess återgivningar. Du kan skicka e-post till flera användare genom att lägga till deras e-postadresser.

   ![Dialogrutan Länkdelning](assets/share-link.png)

I båda fallen kan du ändra standardvärdena, t.ex. utgångsdatum och -tid, och tillåta hämtning av de ursprungliga resurserna och dess återgivningar.

### Kopiera och dela resurslänken{#copy-and-share-asset-link}

Så här delar du resurser som en offentlig URL:

1. Logga in på [!DNL Experience Manager Assets] och navigera till **[!UICONTROL Files]**.
1. Markera de resurser eller den mapp som innehåller resurser. Klicka på **[!UICONTROL Share Link]** i verktygsfältet.
1. Dialogrutan **[!UICONTROL Link Sharing]** som innehåller en autogenererad resurslänk i fältet **[!UICONTROL Share Link]** visas.
1. Ange förfallodatumet för den delade länken efter behov.
1. Markera eller avmarkera `Include Originals` eller `Include Renditions` under **[!UICONTROL Link Settings]** om du vill inkludera eller exkludera någon av de två. Du måste välja minst ett alternativ.
1. Namnen på den markerade Assets-filen visas i den högra kolumnen i dialogrutan [!DNL Share Link].
1. Kopiera resurslänken och dela den med användarna.

### Dela resurslänk via e-postmeddelande {#share-assets-link-through-email}

Så här delar du resurser via e-post:

1. Markera de resurser eller den mapp som innehåller resurser. Klicka på **[!UICONTROL Share Link]** i verktygsfältet.
1. Dialogrutan **[!UICONTROL Link Sharing]** som innehåller en autogenererad resurslänk i fältet **[!UICONTROL Share Link]** visas.

   * Skriv e-postadressen till den användare som du vill dela länken med i rutan E-postadress. Du kan dela länken med flera användare. Om användaren är medlem i din organisation väljer du dennes e-postadress bland de förslag som visas i listrutan. Skriv e-postadressen till den användare som du vill dela länken med i textfältet för e-postadress och klicka på [!UICONTROL Enter]. Du kan dela länken med flera användare.

   * I rutan **[!UICONTROL Subject]** anger du ett ämne för att ange syftet med resurserna som delas.
   * Skriv ett meddelande i rutan **[!UICONTROL Message]** om det behövs.
   * I fältet **[!UICONTROL Expiration]** använder du datumväljaren för att ange ett förfallodatum och en förfallotid för länken.
   * Aktivera kryssrutan **[!UICONTROL Allow download of the original file]** om du vill tillåta mottagarna att hämta den ursprungliga återgivningen.

1. Klicka på **[!UICONTROL Share]**. Ett meddelande bekräftar att länken delas med användarna. Användarna får ett e-postmeddelande med den delade länken.

   ![E-post för länkdelning](assets/link-sharing-email-notification.png)

### Anpassa e-postmall {#customize-email-template}

En väldesignad mall förmedlar professionalism och kompetens och ökar trovärdigheten för ert budskap och er organisation. Med [!DNL Adobe Experience Manager] kan du anpassa e-postmallen, som skickas till mottagarna som tar emot e-postmeddelandet som innehåller den delade länken. Anpassade e-postmallar gör det dessutom möjligt att personalisera ditt e-postinnehåll genom att adressera mottagarna med namn och referensspecifik information som är relevant för dem. Denna personliga beröring kan få mottagaren att känna sig värderad och öka engagemanget. Inte bara det, en anpassad mall säkerställer att e-postmeddelandena är i linje med varumärkesidentiteten, inklusive logotyper, färger och teckensnitt. Enhetlighet stärker varumärkesigenkänningen och förtroendet bland mottagarna.

#### Format för en anpassad e-postmall {#format-of-custom-email-template}

E-postmallen kan anpassas med oformaterad text eller HTML. Den redigerbara malllänken som är standard finns på `/libs/settings/dam/adhocassetshare/en.txt`. Du kan åsidosätta mallen genom att skapa filen `/apps/settings/dam/adhocassetshare/en.txt`. Du kan ändra e-postmallen så många gånger som behövs.

| Platshållare | Beskrivning |
|---|-----|
| `${emailSubject}` | Ämne för ett e-postmeddelande |
| `${emailInitiator}` | E-post-ID för den användare som skapade e-postmeddelandet |
| `${emailMessage}` | E-postbrödtext |
| `${pagePath}` | URL för den delade länken |
| `${linkExpiry}` | Utgångsdatum för delad länk |

<!--| `${host.prefix}` | Origin of the [!DNL Experience Manager] instance, for example `http://www.adobe.com"` |-->

#### Exempel på anpassad e-postmall {#custom-email-template-example}

```
subject: ${emailSubject}

<!DOCTYPE html>
<html><body>
<p><strong>${emailInitiator}</strong> invited you to review assets.</p>
<p>${emailMessage}</p>
<p>The shared link will be available until ${linkExpiry}.
<p>
    <a href="${pagePath}" target="_blank"><strong>Open</strong></a>
</p>

</body></html>
```

<!--Sent from instance: ${host.prefix}-->

### Hämta resurser via resurslänken {#download-assets-using-asset-link}

Alla användare som har tillgång till länken för delade resurser kan hämta de resurser som paketerats i en zip-mapp. Hämtningsprocessen är densamma oavsett om en användare använder länken för det kopierade objektet eller resurslänken som delas via e-postmeddelandet.

* Klicka på resurslänken eller klistra in URL-adressen i webbläsaren. Gränssnittet [!UICONTROL Link Share] öppnas där du kan växla till [!UICONTROL Card View] eller [!UICONTROL List View].

* I [!UICONTROL Card View] kan du hålla muspekaren över den delade resursen eller den delade resursmappen för att antingen välja resurserna eller placera dem i kö för hämtning.

* Som standard visas alternativet **[!UICONTROL Download Inbox]** i användargränssnittet. Den visar en lista över alla delade resurser eller mappar som är köade för hämtning tillsammans med deras status.

* När du väljer resurser eller mapp visas ett **[!UICONTROL Queue Download]**-alternativ på skärmen. Klicka på alternativet **[!UICONTROL Queue Download]** för att starta hämtningsprocessen.

  ![Köhämtning](assets/queue-download.png)

* Klicka på alternativet **[!UICONTROL Download Inbox]** när hämtningsfilen förbereds för att visa status för hämtningen. För stora hämtningar klickar du på knappen **[!UICONTROL Refresh]** för att uppdatera statusen.

  ![Hämta inkorgen](assets/link-sharing-download-inbox.png)

* När bearbetningen är klar klickar du på knappen **[!UICONTROL Download]** för att hämta zip-filen.

<!--
You can also copy the auto-generated link and share it with the users. The default expiration time for the link is one day.
-->

>[!NOTE]
>
>Om en delad resurs flyttas till en annan plats slutar länken att fungera. Återskapa länken och dela den på nytt med användarna.


<!--
## Share assets as a link {#sharelink}

To generate the URL for assets you want to share with users, use the Link Sharing dialog. Users with administrator privileges or with read permissions at `/var/dam/share` location are able to view the links shared with them. Sharing assets through a link is a convenient way of making resources available to external parties without them having to first log in to Experience Manager Assets.

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

   For the local and author properties, provide the URL for the local and author instance respectively. Both local and author properties have the same value if you run a single Experience Manager author instance. For publish, provide the URL for the publish instance.

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
   >Experience Manager supports generating the preview of assets of these MIME types: JPG, PNG, GIF, BMP, INDD, PDF, and PPT. You can only download the assets of the other MIME types.

1. To download the shared asset, click/tap **[!UICONTROL Select]** from the toolbar, click/tap the asset, and then click/tap **[!UICONTROL Download]** from the toolbar.
1. To view the assets you shared as links, go to the Assets user interface and click/tap the GlobalNav icon. Choose **[!UICONTROL Navigation]** from the list to display the Navigation pane.
1. From the Navigation pane, choose **[!UICONTROL Shared Links]** to display a list of shared assets.
1. To un-share an asset, select it and tap/click **[!UICONTROL Unshare]** from the toolbar.

A message confirms that you unshared the asset. In addition, the entry for the asset is removed from the list.
-->

## Ladda ned resurser och dela separat {#download-and-share-assets}

Användare kan hämta de nödvändiga resurserna och dela dem utanför [!DNL Experience Manager]. Mer information finns i [söka efter resurser](/help/assets/search-assets.md), [hämta resurser](/help/assets/download-assets-from-aem.md) och [hämta samlingar](manage-collections.md#download-a-collection)

## Dela material med kreatörer {#share-with-creatives}

Marknadsförare och andra användare kan enkelt dela godkänt material med sina kreatörer genom att

* **Experience Manager-datorprogrammet**: Programmet fungerar i Windows och Mac. Se [Översikt över datorprogrammet](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html?lang=sv-SE). Om du vill veta hur en auktoriserad skrivbordsanvändare enkelt kan komma åt de delade resurserna läser du [bläddra bland, söka efter och förhandsgranska resurser](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=sv-SE#browse-search-preview-assets). Skrivbordsanvändare kan skapa resurser och dela dem med sina motsvarigheter som är Experience Manager-användare, till exempel genom att överföra nya bilder. Se [Överför resurser med ett skrivbordsprogram](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=sv-SE#upload-and-add-new-assets-to-aem).

* **Adobe Asset Link**: Kreatörer kan söka efter och använda resurser direkt inifrån [!DNL Adobe InDesign], [!DNL Adobe Illustrator] och [!DNL Adobe Photoshop].

## Konfigurera resursdelning {#configure-sharing}

De olika alternativen för att dela resurserna kräver specifik konfiguration och har särskilda krav.

### Konfigurera delning av resurslänkar {#asset-link-sharing}

<!-- TBD: Web Console is not there so how to configure Day CQ email service? Or is it not required now? -->

Använd dialogrutan Länkdelning för att generera URL:en för resurser som du vill dela med användare. Användare med administratörsbehörighet eller läsbehörighet på platsen `/var/dam/share` kan visa de länkar som delas med dem. Att dela resurser via en länk är ett bekvämt sätt att göra resurser tillgängliga för externa parter utan att de först behöver logga in på [!DNL Assets].

>[!NOTE]
>
>Om du vill dela länkar från författarinstansen till externa entiteter måste du se till att du bara visar följande URL:er för `GET`-begäranden. Blockera andra URL:er för att säkerställa att din författarinstans är säker.
>
>* `[aem_server]:[port]/linkshare.html`
>* `[aem_server]:[port]/linksharepreview.html`
>* `[aem_server]:[port]/linkexpired.html`

<!--
1. From the list of services, locate **[!UICONTROL Day CQ Mail Service]**.
1. Click the **[!UICONTROL Edit]** icon beside the service, and configure the following parameters for **Day CQ Mail Service** with the details mentioned against their names:

    * SMTP server host name: email server host name
    * SMTP server port: email server port
    * SMTP user: email server user name
    * SMTP password: email server password
-->

<!-- TBD: Commenting as Web Console is not available. Document the appropriate OSGi config method if available in CS.
### Configure maximum data size {#maxdatasize}

When you download assets from the link shared using the Link Sharing feature, Experience Manager compresses the asset hierarchy from the repository and then returns the asset in a ZIP file. However, in the absence of limits to the amount of data that can be compressed in a ZIP file, huge amounts of data is subjected to compression, which causes out of memory errors in JVM. To secure the system from a potential denial of service attack due to this situation, you can configure the maximum size of the downloaded files. If uncompressed size of the asset exceeds the configured value, asset download requests are rejected. The default value is 100 MB.

1. Click/Tap the Experience Manager logo and then go to **[!UICONTROL Tools]** &gt; **[!UICONTROL Operations]** &gt; **[!UICONTROL Web Console]**.
1. From the web console, locate the **[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]** configuration.
1. Open the configuration in edit mode, and modify the value of the **[!UICONTROL Max Content Size (uncompressed)]** parameter.
1. Save the changes.
-->

<!--
Add content or link about how to configure sharing via BP, DA, AAL, etc.
-->

### Aktivera skrivbordsåtgärder som ska användas med skrivbordsappen {#desktop-actions}

I [!DNL Assets]-användargränssnittet i en webbläsare kan du utforska resursplatserna eller checka ut och öppna resursen för redigering i skrivbordsprogrammet. Dessa alternativ kallas skrivbordsåtgärder och för att aktivera dem, se [aktivera skrivbordsåtgärder i [!DNL Assets] webbgränssnittet](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=sv-SE#desktopactions-v2).

![Aktivera skrivbordsåtgärder som ska användas som genväg när du arbetar med skrivbordsappen](assets/enable_desktop_actions.png)

### Konfigurationer som ska använda [!DNL Adobe Asset Link] {#configure-asset-link}

Adobe Asset Link effektiviserar samarbetet mellan kreatörer och marknadsförare vid framtagningen av innehåll. Den ansluter [!DNL Adobe Experience Manager Assets] till [!DNL Creative Cloud] skrivbordsappar, [!DNL Adobe InDesign], [!DNL Adobe Photoshop] och [!DNL Adobe Illustrator]. På panelen [!DNL Adobe Asset Link] kan användare få tillgång till och ändra innehåll som lagras i [!DNL Assets] utan att lämna de kreativa program de är mest bekanta med.

Se [hur du konfigurerar [!DNL Assets] att använda det med [!DNL Adobe Asset Link]](https://helpx.adobe.com/se/enterprise/using/configure-aem-assets-for-asset-link.html).

## Bästa praxis och felsökning {#bestpractices}

* Resursmappar eller samlingar som innehåller ett tomt utrymme i namnet kanske inte delas.
* Om användarna inte kan hämta de delade resurserna bör du fråga Experience Manager-administratören om vilka hämtningsgränser som finns. Standardvärdet är 100 MB.
* För att en användare ska kunna förhandsgranska en video som delas via länkdelning måste videon ha en statisk videoåtergivning tillgänglig på `/jcr:content/renditions`-platsen i videons nod i databasen. Förhandsgranskningen är inte beroende av tillgängligheten för en [!DNL Dynamic Media]-återgivning.
* När du hämtar en videoresurs via länkresurs inkluderas inte återgivningarna [!DNL Dynamic Media] i det hämtade arkivet.

<!--
* If you cannot send email with links to shared assets or if the other users cannot receive your email, check with your Experience Manager administrator if the [email service](/help/assets/configure-asset-sharing.md#configmailservice) is configured or not. 
* If you cannot share assets using link sharing functionality, ensure that you have the appropriate permissions. See [share assets](#sharelink).
-->

<!-- TBD: Add content or link about how to share using Brand Portal when it is available on [!DNL Cloud Service].
-->

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

