---
title: Hämta resurser från AEM
description: Lär dig hur du hämtar resurser från AEM och aktiverar eller inaktiverar hämtningsfunktionen.
contentOwner: AG
translation-type: tm+mt
source-git-commit: c978be66702b7f032f78a1509f2a11315d1ed89f
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 1%

---


# Hämta resurser från AEM {#download-assets-from-aem}

Du kan hämta resurser, inklusive statiska och dynamiska återgivningar. Hämtade resurser paketeras i en ZIP-fil. Den komprimerade ZIP-filen har en maximal filstorlek på 1 GB för exportjobbet. Du tillåts maximalt 500 totala resurser per exportjobb.

>[!NOTE]
>
>För att kunna hämta resurserna måste medlemmarna ha behörighet att starta arbetsflöden som utlöser hämtning av resurser.

Om du vill hämta resurser går du till en resurs, markerar resursen och trycker/klickar på **[!UICONTROL Download]** ikonen i verktygsfältet. I den dialogruta som visas anger du dina hämtningsalternativ.

Det går inte att hämta resurstyperna Bilduppsättningar, Snurra uppsättningar, Blandade medieuppsättningar och Carousel-uppsättningar.

![Tillgängliga alternativ vid hämtning av resurser från AEM Assets](assets/asset_download_dialog.png)

*Bild: Tillgängliga alternativ när du hämtar resurser från AEM Resurser.*

Följande är alternativen för export/hämtning. Dynamiska renderingar är unika för Dynamic Media och gör att du kan generera renderingar direkt utöver den resurs du valt - det alternativet är bara tillgängligt om du har Dynamic Media aktiverat.

| Export- eller nedladdningsalternativ | Beskrivningar |
|---|---|
| [!UICONTROL Assets] | Välj det här om du vill hämta resursen i dess ursprungliga form utan några återgivningar. |
| [!UICONTROL Renditions] | En återgivning är den binära representationen av en resurs. Resurser har en primär representation - den som utgörs av den överförda filen. De kan ha valfritt antal representationer. <br> Med det här alternativet kan du välja de återgivningar du vill hämta. Vilka renderingar som är tillgängliga beror på vilken resurs du väljer. |
| [!UICONTROL Dynamic Renditions] | En dynamisk återgivning genererar andra återgivningar direkt. När du väljer det här alternativet väljer du också de återgivningar som du vill skapa dynamiskt genom att välja i listan med bildförinställningar. Du kan dessutom välja storlek och måttenhet, format, färgrymd, upplösning och alla bildmodifierare (t.ex. för att invertera bilden) |
| [!UICONTROL Create separate folder for each asset] | Välj det här om du vill bevara mapphierarkin när du hämtar resurser. Som standard ignoreras mapphierarkin och alla resurser hämtas i en mapp på det lokala systemet. |

Alternativet för återgivningar är tillgängligt om resursen har några återgivningar. Alternativet Delresurser är tillgängligt om tillgången innehåller delresurser.

När du väljer en mapp att hämta hämtas hela resurshierarkin under mappen. Om du vill inkludera varje resurs som du hämtar (inklusive resurser i underordnade mappar som är kapslade under den överordnade mappen) i en enskild mapp väljer du **[!UICONTROL Create separate folder for each asset]**.

## Aktivera resurshämtningsserver {#enable-asset-download-servlet}

Med standardservleten i AEM kan autentiserade användare skicka godtyckligt stora, samtidiga hämtningsbegäranden för att skapa ZIP-filer med resurser som är synliga för dem och som kan överbelasta servern och nätverket. För att minska de potentiella DoS-riskerna som orsakas av den här funktionen är `AssetDownloadServlet` OSGi-komponenten inaktiverad som standard för publiceringsinstanser.

Om du vill tillåta hämtning av resurser från DAM, till exempel när du använder Assets Share Commons eller någon annan portalliknande implementering, aktiverar du servleten manuellt via en OSGi-konfiguration. Adobe rekommenderar att du anger en så låg hämtningsstorlek som möjligt utan att det påverkar kraven för den dagliga hämtningen. Ett högt värde kan påverka prestandan.

1. Skapa en mapp med en namnkonvention som anger publiceringsmiljön som mål, det vill säga `config.publish`:

   `/apps/<your-app-name>/config.publish`

1. Skapa en ny fil av typen `nt:file` med namnet i config-mappen `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`.
1. Fyll `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` med följande: Anger en maximal storlek (i byte) för hämtningen som värdet för `asset.download.prezip.maxcontentsize`. Nedanstående exempel konfigurerar den maximala storleken för ZIP-nedladdningen till högst 100 kB.

   ```java
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
>* [Hämta resurser med Adobe Assets Link inifrån de Adobe Creative Cloud-program som stöds](https://helpx.adobe.com/se/enterprise/using/manage-assets-using-adobe-asset-link.html)

