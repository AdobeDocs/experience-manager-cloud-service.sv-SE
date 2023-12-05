---
title: Hämta resurser
description: Hämta resurser från [!DNL Adobe Experience Manager Assets] och aktivera eller inaktivera nedladdningsfunktionen.
contentOwner: Vishabh Gupta
feature: Asset Management
role: User
exl-id: f68b03ba-4ca1-4092-b257-16727fb12e13
source-git-commit: abe5f8a4b19473c3dddfb79674fb5f5ab7e52fbf
workflow-type: tm+mt
source-wordcount: '1300'
ht-degree: 0%

---

# Hämta resurser från [!DNL Adobe Experience Manager] {#download-assets-from-aem}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/download-assets-from-aem.html?lang=en) |
| AEM as a Cloud Service | Den här artikeln |

Du kan hämta resurser, inklusive statiska och dynamiska återgivningar. Du kan även skicka e-postmeddelanden med länkar till resurser direkt från [!DNL Adobe Experience Manager Assets]. Hämtade resurser paketeras i en ZIP-fil. <!-- The compressed ZIP file has a maximum file size of 1 GB for the export job. A maximum of 500 total assets per export job are allowed. -->

<!--
>[!NOTE]
>
>Recipients of emails must be members of the `dam-users` group to access the ZIP download link in the email message. To be able to download the assets, the members must have permissions to launch workflows that trigger downloading of assets.
-->

Följande resurstyper kan inte laddas ned: Bilduppsättningar, snurpuppsättningar, blandade medieuppsättningar och Carousel-uppsättningar.

Du kan hämta resurser från Experience Manager på följande sätt:

<!-- * [Link Share](#link-share-download) -->

* [Experience Manager användargränssnitt](#download-assets)
* [Kommandon för resursdelning](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html)
* [Skrivbordsapp](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#download-assets)

## Hämta resurser med [!DNL Experience Manager] gränssnitt {#download-assets}

Experience Manager optimerar nedladdningen baserat på resurskvantitet och storlek. Mindre filer hämtas från användargränssnittet i realtid. [!DNL Experience Manager] hämtar direkt enskilda resursbegäranden för originalfilen i stället för att bifoga enskilda resurser i ett ZIP-arkiv för snabbare nedladdningar. Experience Manager stöder stora nedladdningar med asynkrona begäranden. Hämtningsbegäranden som är större än 100 GB delas upp i flera ZIP-arkiv med en maximal storlek på 100 MB vardera.

Som standard [!DNL Experience Manager] utlöser ett meddelande i [[!DNL Experience Manager] Inkorg](/help/sites-cloud/authoring/getting-started/inbox.md) när ett nedladdningsarkiv skapas.

![Inkorgsmeddelande](assets/inbox-notification-for-large-downloads.png)


### Aktivera e-postmeddelanden för stora nedladdningar {#enable-emails-for-large-downloads}

Asynkrona nedladdningar aktiveras i följande fall:

* Om det finns fler än tio resurser
* Om hämtningsstorleken är större än 100 MB
* Om nedladdningen tar mer än 30 sekunder att förbereda

Medan den asynkrona nedladdningen körs i bakgrunden kan användaren fortsätta utforska och arbeta vidare i Experience Manager. Utöver meddelanden i inkorgen för Experience Manager kan Experience Manager skicka e-post för att meddela användaren när hämtningen är klar. Om du vill aktivera den här funktionen kan administratören konfigurera e-posttjänsten genom att [konfigurera en SMTP-serveranslutning](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html#sending-email).

När e-posttjänsten har konfigurerats kan administratörer och användare aktivera e-postmeddelanden från Experience Manager-gränssnittet.

Så här aktiverar du e-postmeddelanden:

1. Logga in på [!DNL Experience Manager Assets].
1. Klicka på användarikonen i det övre högra hörnet och klicka sedan på **[!UICONTROL My Preferences]** för att öppna fönstret Användarinställningar.
1. Välj **[!UICONTROL Asset Download email notifications]** kryssruta och klicka **[!UICONTROL Accept]**.

   ![enable-email-notifications-for-large-downloads](/help/assets/assets/enable-email-for-large-downloads.png)


Så här hämtar du resurser:

1. I [!DNL Experience Manager] användargränssnitt, klicka **[!UICONTROL Assets]** > **[!UICONTROL Files]**.
1. Navigera till resurserna som du vill hämta. Markera mappen eller välj en eller flera resurser i mappen. I verktygsfältet klickar du på **[!UICONTROL Download]**.

   ![Tillgängliga alternativ vid hämtning av resurser från [!DNL Experience Manager Assets]](/help/assets/assets/asset-download1.png)

1. I hämtningsdialogrutan väljer du de hämtningsalternativ som du vill ha.

   | Hämtningsalternativ | Beskrivning |
   |---|---|
   | **[!UICONTROL Create separate folder for each asset]** | Välj det här alternativet om du vill skapa en mapp för varje resurs som innehåller alla hämtade återgivningar för resursen. Om du inte markerar det här alternativet finns varje resurs (och dess återgivningar om de har valts för hämtning) i den överordnade mappen för det genererade arkivet. |
   | **[!UICONTROL Email]** | Välj det här alternativet om du vill skicka ett e-postmeddelande (som innehåller en länk till din hämtning) till en annan användare. Mottagaranvändaren måste vara medlem i `dam-users` grupp. Standardmallar för e-post finns på följande platser:<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> Mallar som du anpassar under distributionen finns på följande platser: <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul>Du kan lagra klientspecifika anpassade mallar på följande platser:<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> |
   | **[!UICONTROL Asset(s)]** | Välj det här alternativet om du vill hämta resursen i dess ursprungliga form.<br>Alternativet Delresurser är tillgängligt om den ursprungliga tillgången har delresurser. |
   | **[!UICONTROL Rendition(s)]** | En återgivning är den binära representationen av en resurs. Resurser har en primär representation - den som utgörs av den överförda filen. De kan ha ett valfritt antal representationer. <br> Med det här alternativet kan du välja de återgivningar du vill hämta. Vilka återgivningar som är tillgängliga beror på vilken resurs du har valt. |
   | **[!UICONTROL Smart Crops]** | Välj det här alternativet om du vill hämta alla smarta beskärningsåtergivningar för den valda resursen inifrån [!DNL Experience Manager]. En ZIP-fil med renderingarna Smart Crop skapas och hämtas till din lokala dator. |
   | **[!UICONTROL Dynamic Rendition(s)]** | Välj det här alternativet om du vill generera en serie alternativa återgivningar i realtid. När du väljer det här alternativet väljer du också de återgivningar som du vill skapa dynamiskt genom att välja bland [Bildförinställning](/help/assets/dynamic-media/image-presets.md) lista. <br>Du kan dessutom välja storlek och måttenhet, format, färgrymd, upplösning och alla valfria bildmodifierare, t.ex. invertering av bilden. Alternativet är bara tillgängligt om du har [!DNL Dynamic Media] aktiverat. |

1. Klicka på **[!UICONTROL Download]**.

   Om e-postmeddelanden har aktiverats för stora nedladdningar visas ett e-postmeddelande med en nedladdnings-URL för den arkiverade zip-mappen i inkorgen. Klicka på nedladdningslänken i e-postmeddelandet för att ladda ned zip-arkivet.

   ![e-postmeddelanden-för-stora nedladdningar](/help/assets/assets/email-for-large-notification.png)

   Du kan även visa meddelandet i [!DNL Experience Manager] Inkorgen.

   ![inbox-notifications-for-large-downloads](/help/assets/assets/inbox-notification-for-large-downloads.png)

## Hämta resurser som delas via länkdelning {#link-share-download}

Att dela resurser via en länk är ett bekvämt sätt att göra det tillgängligt för intresserade utan att de behöver logga in på [!DNL Assets]. Se [Funktionen för delning av länkar](/help/assets/share-assets.md#sharelink).

När användare hämtar resurser från delade länkar, [!DNL Assets] använder en asynkron tjänst som ger snabbare och oavbruten nedladdning. De resurser som ska laddas ned köas i bakgrunden i en inkorg i ZIP-arkiv med hanterbar filstorlek. För större nedladdningar grupperas nedladdningen i filer på 100 GB.

The [!UICONTROL Download Inbox] visar status för varje arkiv. När bearbetningen är klar kan du hämta arkiven från inkorgen.

![Hämta inkorg](assets/link-sharing-download-inbox.png)

## Aktivera resurshämtningsserver {#enable-asset-download-servlet}

Standardservleten i [!DNL Experience Manager] tillåter autentiserade användare att utfärda godtyckligt stora, samtidiga hämtningsbegäranden för att skapa ZIP-filer med resurser. Förberedelsen kan påverka prestanda eller till och med överbelasta servern och nätverket. För att minska sådana potentiella DoS-liknande risker som den här funktionen medför, `AssetDownloadServlet` OSGi-komponenten är inaktiverad för publiceringsinstanser. Om du inte behöver nedladdningsfunktionen för författarinstanser inaktiverar du den som skapade den.

Om du vill tillåta hämtning av resurser från DAM, till exempel när du använder Assets Share Commons eller någon annan portalliknande implementering, aktiverar du servleten manuellt via en OSGi-konfiguration. Adobe rekommenderar att du anger en så låg hämtningsstorlek som möjligt utan att det påverkar den dagliga hämtningen. Ett högt värde kan påverka prestandan.

1. Skapa en mapp med en namnkonvention som anger publiceringskörningsläget, det vill säga `config.publish`:

   `/apps/<your-app-name>/config.publish`

1. Skapa en fil av typen i konfigurationsmappen `nt:file` namngiven `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`.
1. Fylla `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` med följande. Anger en maximal storlek (i byte) för hämtningen som värdet av `asset.download.prezip.maxcontentsize`. Nedanstående exempel konfigurerar den maximala storleken för ZIP-nedladdningen till högst 100 kB.

   ```java
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

## Inaktivera resurshämtningsserver {#disable-asset-download-servlet}

Om du inte behöver nedladdningsfunktionen kan du inaktivera servleten för att förhindra DoS-liknande risker. The `Asset Download Servlet` kan inaktiveras på en [!DNL Experience Manager] skapa och publicera instanser genom att uppdatera dispatcherns konfiguration för att blockera alla förfrågningar om hämtning av resurser. Servern kan även inaktiveras manuellt via OSGi-konsolen direkt.

1. Om du vill blockera hämtningsbegäranden via en dispatcherns konfiguration redigerar du `dispatcher.any` konfigurera och lägga till en ny regel i [filtersektion](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#configuring).

   `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

## OnTime- eller OffTime-återgivning {#on-off-time-rendition}

Aktivera `OnOffTimeAssetAccessFilter` måste du skapa en OSGi-konfiguration. Den här tjänsten tillåter blockering av åtkomst till återgivningar och metadata utöver själva resursen baserat på tidsinställningarna på/av. OSGi-konfigurationen ska vara för `com.day.cq.dam.core.impl.servlet.OnOffTimeAssetAccessFilter`. Följ stegen nedan:

1. Skapa en konfigurationsfil på `/apps/system/config/com.day.cq.dam.core.impl.servlet.OnOffTimeAssetAccessFilter.cfg.json`. Filen ska innehålla `{}` som innehåll, vilket innebär en tom OSGi-konfiguration för motsvarande OSGi-komponent. Den här åtgärden aktiverar tjänsten.
1. Distribuera koden, inklusive den nya konfigurationen, via [!DNL Cloud Manager].
1. När de distribuerats är återgivningarna och metadata tillgängliga enligt objektens tidsinställningar. Om det aktuella datumet eller den aktuella tiden infaller före eller efter tidpunkten för avaktiveringen visas ett felmeddelande.
Mer information om hur du lägger till en tom OSGi-konfiguration finns i det här [stödlinje](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/configuring-osgi.html?lang=en).

## Tips och begränsningar {#tips-limitations}

* Om du hämtar en tom mapp [!DNL Experience Manager] förmedlar ett meddelande om att ett ZIP-arkiv har skapats, men arkivet har inte skapats.

**Se även**

* [Översätt resurser](translate-assets.md)
* [Resurser för HTTP API](mac-api-assets.md)
* [Resurser som stöds i filformat](file-format-support.md)
* [Sök resurser](search-assets.md)
* [Anslutna resurser](use-assets-across-connected-assets-instances.md)
* [Resursrapporter](asset-reports.md)
* [Metadata-scheman](metadata-schemas.md)
* [Hantera metadata](manage-metadata.md)
* [Sök efter ansikten](search-facets.md)
* [Hantera samlingar](manage-collections.md)
* [Import av massmetadata](metadata-import-export.md)

>[!MORELIKETHIS]
>
>* [Hämta DRM-skyddade resurser](drm.md)
>* [Hämta resurser med datorprogrammet Experience Manager på Win eller Mac](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)
>* [Hämta resurser med Adobe Assets Link inifrån de Adobe Creative Cloud-appar som stöds](https://helpx.adobe.com/se/enterprise/using/manage-assets-using-adobe-asset-link.html)
