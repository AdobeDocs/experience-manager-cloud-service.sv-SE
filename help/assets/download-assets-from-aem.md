---
title: Hämta resurser från AEM
description: Lär dig hur du hämtar resurser från AEM och aktiverar eller inaktiverar hämtningsfunktionen.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 6998ee5f3c1c1563427e8739998effe0eba867fc

---


# Hämta resurser från AEM {#download-assets-from-aem}

Du kan hämta resurser, inklusive statiska och dynamiska återgivningar. Hämtade resurser paketeras i en ZIP-fil. Den komprimerade ZIP-filen har en maximal filstorlek på 1 GB för exportjobbet. Du tillåts maximalt 500 totala resurser per exportjobb.

>[!NOTE]
>
>För att kunna hämta resurserna måste medlemmarna ha behörighet att starta arbetsflöden som utlöser hämtning av resurser.

Om du vill hämta resurser går du till en resurs, markerar resursen och trycker/klickar på **[!UICONTROL hämtningsikonen]** i verktygsfältet. I den dialogruta som visas anger du dina hämtningsalternativ.

Det går inte att hämta resurstyperna Bilduppsättningar, Snurra uppsättningar, Blandade medieuppsättningar och Carousel-uppsättningar.

![Tillgängliga alternativ när du hämtar resurser från AEM Assets](assets/asset_download_dialog.png)*Bild: Tillgängliga alternativ vid hämtning av resurser från AEM Assets*

Följande är alternativen för export/hämtning. Dynamiska renderingar är unika för Dynamic Media och gör att du kan generera renderingar direkt utöver den resurs du valt - det alternativet är bara tillgängligt om du har Dynamic Media aktiverat.

| Export- eller nedladdningsalternativ | Beskrivningar |
|---|---|
| [!UICONTROL Assets] | Välj det här om du vill hämta resursen i dess ursprungliga form utan några återgivningar. |
| [!UICONTROL Återgivningar] | En återgivning är den binära representationen av en resurs. Resurser har en primär representation - den som utgörs av den överförda filen. De kan ha valfritt antal representationer. <br> Med det här alternativet kan du välja de återgivningar du vill hämta. Vilka renderingar som är tillgängliga beror på vilken resurs du väljer. |
| [!UICONTROL Dynamiska renderingar] | En dynamisk återgivning genererar andra återgivningar direkt. När du väljer det här alternativet väljer du också de återgivningar som du vill skapa dynamiskt genom att välja i listan med bildförinställningar. Du kan dessutom välja storlek och måttenhet, format, färgrymd, upplösning och alla bildmodifierare (t.ex. för att invertera bilden) |
| [!UICONTROL Skapa separata mappar för varje resurs] | Välj det här om du vill bevara mapphierarkin när du hämtar resurser. Som standard ignoreras mapphierarkin och alla resurser hämtas i en mapp på det lokala systemet. |

Alternativet för återgivningar är tillgängligt om resursen har några återgivningar. Alternativet Delresurser är tillgängligt om tillgången innehåller delresurser.

När du väljer en mapp att hämta hämtas hela resurshierarkin under mappen. Om du vill inkludera varje resurs som du hämtar (inklusive resurser i underordnade mappar som är kapslade under den överordnade mappen) i en enskild mapp väljer du **[!UICONTROL Skapa en separat mapp för varje resurs]**.

## Aktivera resurshämtningsserver {#enable-asset-download-servlet}

Med standardservleten i AEM kan autentiserade användare skicka godtyckligt stora, samtidiga hämtningsbegäranden för att skapa ZIP-filer med resurser som är synliga för dem och som kan överbelasta servern och nätverket. För att minska de potentiella DoS-riskerna som orsakas av den här funktionen är `AssetDownloadServlet` OSGi-komponenten inaktiverad som standard för publiceringsinstanser.

Om du vill tillåta hämtning av resurser från DAM, till exempel när du använder Assets Share Commons eller någon annan portalliknande implementering, aktiverar du servleten manuellt via en OSGi-konfiguration. Adobe rekommenderar att du anger en så låg hämtningsstorlek som möjligt utan att det påverkar kraven för den dagliga hämtningen. Ett högt värde kan påverka prestandan.

1. Skapa en mapp med en namnkonvention som anger publiceringsmiljön som mål, det vill säga `config.publish`:

   `/apps/<your-app-name>/config.publish`

1. Skapa en ny fil av typen `nt:file` med namnet i config-mappen `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`.
1. Fyll `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` med följande: Anger en maximal storlek (i byte) för hämtningen som värdet för `asset.download.prezip.maxcontentsize`. Nedanstående exempel konfigurerar den maximala storleken för ZIP-nedladdningen till högst 100 kB.

   ```
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

## Inaktivera resurshämtningsserver {#disable-asset-download-servlet}

Du `Asset Download Servlet` kan inaktivera funktionen på en AEM Publish-instans genom att uppdatera dispatcherns konfiguration för att blockera eventuella hämtningsbegäranden. Servern kan även inaktiveras manuellt via OSGi-konsolen direkt.

1. Om du vill blockera resurshämtningsbegäranden via en dispatcherkonfiguration redigerar du `dispatcher.any` konfigurationen och lägger till en ny regel i [filteravsnittet](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#defining-a-filter).

   `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

>[!MORELIKETHIS]
>
>* [Hämta DRM-skyddade resurser](drm.md)
>* [Hämta resurser med hjälp av AEM-datorprogrammet på Win- eller Mac-datorer](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html)
>* [Hämta resurser med Adobe Assets Link inifrån de Adobe Creative Cloud-program som stöds](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html)


<!-- FULL ARTICLE ARCHIVE IS BELOW 

You can download assets including static and dynamic renditions. Alternatively, you can send emails with links to assets directly from AEM Assets. Downloaded assets are bundled in a ZIP file. The compressed ZIP file has a maximum file size of 1 GB for the export job. You are allowed a maximum of 500 total assets per export job.

>[!NOTE]
>
>Recipients of emails must be members of the `dam-users` group to access the ZIP download link in the email message. To be able to download the assets, the members must have permissions to launch workflows that trigger downloading of assets.

To download assets, navigate to an asset, select the asset, and tap/click the **[!UICONTROL Download]** icon from the toolbar. In the resulting dialog, specify your download options.

The asset types Image Sets, Spin Sets, Mixed Media Sets, and Carousel Sets cannot be downloaded.

![Available options when downloading assets from AEM Assets](assets/asset_download_dialog.png)
*Figure: Available options when downloading assets from AEM Assets*

The following are the Export/Download options. Dynamic renditions are unique to Dynamic Media and let you generate renditions on-the-fly in addition to the asset you selected - that option is only available if you have Dynamic Media enabled.

|Export or download options|Descriptions|
|---|---|
| [!UICONTROL Assets]| Select this to download the asset in its original form without any renditions.|
| [!UICONTROL Renditions] |A rendition is the binary representation of an asset. Assets have a primary representation - that of the uploaded file. They can have any number of representations. <br> With this option, you can select the renditions you want downloaded. The renditions available depend on the asset you select.|
| [!UICONTROL Dynamic Renditions] |A dynamic rendition generates other renditions on-the-fly. When you select this option, you also select the renditions you want to create dynamically by selecting from the image presets list. In addition, you can select the size and unit of measurement, format, color space, resolution, and any image modifiers (for example to invert the image)|
| [!UICONTROL Email] |An email notification is sent to the user. Standard emails templates are available at the following locations:<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`</li></ul> Templates that you customize during deployment should be present at these locations: <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`</li></ul>You can store tenant-specific custom templates at these locations:<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`</li></ul>|
| [!UICONTROL Create separate folder for each asset] |Select this to preserve the folder hierarchy while downloading assets. By default, the folder hierarchy is ignored and all assets are downloaded in one folder in your local system.|

The option renditions option is available if the asset has any renditions. The subassets option is available if the asset includes subassets.

When you select a folder to download, the complete asset hierarchy under the folder is downloaded. To include each asset you download (including assets in child folders nested under the parent folder) in an individual folder, select **[!UICONTROL Create separate folder for each asset]**.

## Enable asset download servlet {#enable-asset-download-servlet}

The default servlet in AEM allows authenticated users to issue arbitrarily-large, concurrent download requests for creating ZIP files of assets visible to them that can overload the server and the network. To mitigate potential DoS risks caused by this feature, `AssetDownloadServlet` OSGi component is disabled by default for publish instances.

To allow downloading assets from your DAM, say when using something like Asset Share Commons or other portal-like implementation, manually enable the servlet via an OSGi configuration. Adobe recommends setting the permissible download size as low as possible without affecting the day-to-day download requirements. A high value may impact performance.

1. Create a folder with a naming convention that targets the publish runmode, that is, `config.publish`:

   `/apps/<your-app-name>/config.publish`

1. In the config folder, create a new file of type `nt:file` named `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`.
1. Populate `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` with the following. Sets a maximum size (in bytes) for the download as value of `asset.download.prezip.maxcontentsize`. The below sample configures the maximum size of the ZIP download to not exceed 100 kB.

   ```
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

## Disable asset download servlet {#disable-asset-download-servlet}

The `Asset Download Servlet` can be disabled on an AEM Publish instances by updating the dispatcher configuration to block any asset download requests. The servlet can also be manually disabled via the OSGi console directly.

1. To block asset download requests via a dispatcher configuration edit the `dispatcher.any` configuration and add a new rule to the [filter section](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#defining-a-filter).

   `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

>[!MORELIKETHIS]
>
>* [Download DRM protected assets](drm.md)
>* [Download assets using AEM desktop app on Win or Mac desktop](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html)
>* [Download assets using Adobe Assets Link from within the supported Adobe Creative Cloud apps](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html)


-->