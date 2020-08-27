---
title: Download assets from [!DNL Adobe Experience Manager Assets].
description: Hämta resurser [!DNL Adobe Experience Manager Assets] från och aktivera eller inaktivera hämtningsfunktionen.
contentOwner: AG
translation-type: tm+mt
source-git-commit: c4a642541a3c8f69c0efff0dbbe036374a1d6f6b
workflow-type: tm+mt
source-wordcount: '874'
ht-degree: 1%

---


# Download assets from [!DNL Adobe Experience Manager] {#download-assets-from-aem}

Du kan hämta resurser, inklusive statiska och dynamiska återgivningar. Du kan också skicka e-postmeddelanden med länkar till resurser direkt från [!DNL Adobe Experience Manager Assets]. Hämtade resurser paketeras i en ZIP-fil. Den komprimerade ZIP-filen har en maximal filstorlek på 1 GB för exportjobbet. Högst 500 resurser per exportjobb tillåts.

>[!NOTE]
>
>Mottagare av e-postmeddelanden måste vara medlemmar i gruppen för att få åtkomst till länken för ZIP-hämtning i e-postmeddelandet. `dam-users` För att kunna hämta resurserna måste medlemmarna ha behörighet att starta arbetsflöden som utlöser hämtning av resurser.

Det går inte att hämta resurstyperna Bilduppsättningar, Snurra uppsättningar, Blandade medieuppsättningar och Carousel-uppsättningar.

Du kan hämta Experience Manager-resurser på följande sätt:

* [Experience Manager användargränssnitt](#download-in-aem)
* Användargränssnittet Resurslänkdelning
* [Kommandon för resursdelning](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* [Varumärkesportal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/introduction/brand-portal.html)
* [Datorprogram](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#download-assets)

## Hämta resurser med AEM gränssnitt {#download-in-aem}

Asynkron nedladdningstjänst ger ett ramverk för smidig nedladdning av stora resurser. Mindre filer hämtas från användargränssnittet i realtid. De stora filerna hämtas asynkront och användarna informeras om att de har slutförts via Experience Manager-meddelanden i Inkorgen. Se [mer om inkorg](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/sites/authoring/getting-started/inbox.html)för Experience Manager.

![Hämta meddelande](assets/download-notification.png)

*Bild: Hämta meddelanden via[!DNL Experience Manager]Inkorgen.*

Asynkrona nedladdningar aktiveras i något av följande fall:

* Om det finns mer än 10 resurser eller mer än 100 MB att hämta.
* Om nedladdningen tar mer än 30 sekunder att förbereda.

Så här hämtar du resurser:

1. I [!DNL Experience Manager] användargränssnittet klickar du **[!UICONTROL Assets]** > **[!UICONTROL Files]**.
1. Navigera till de resurser du vill hämta. Markera mappen eller välj en eller flera resurser i mappen. On the toolbar, click **[!UICONTROL Download]**.

   ![Tillgängliga alternativ vid hämtning av resurser från [!DNL Experience Manager Assets]](/help/assets/assets/asset-download1.png)

   *Bild: Alternativ i dialogrutan Hämta.*

1. I dialogrutan Hämta väljer du de hämtningsalternativ som du vill använda.

   | Hämtningsalternativ | Beskrivning |
   |---|---|
   | **[!UICONTROL Create separate folder for each asset]** | Välj det här alternativet om du vill inkludera varje resurs som du hämtar, inklusive resurser, i underordnade mappar som är kapslade under resursens överordnade mapp i en mapp på den lokala datorn. När det här alternativet *inte* är markerat ignoreras mapphierarkin som standard och alla resurser hämtas till en mapp på den lokala datorn. |
   | **[!UICONTROL Email]** | Välj det här alternativet om du vill att ett e-postmeddelande ska skickas till mottagaren. Standardmallar för e-post finns på följande platser:<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> Mallar som du anpassar under distributionen finns på följande platser: <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul>Du kan lagra klientspecifika anpassade mallar på följande platser:<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> |
   | **[!UICONTROL Asset(s)]** | Välj det här alternativet om du vill hämta resursen i dess ursprungliga form utan några återgivningar.<br>Alternativet Delresurser är tillgängligt om den ursprungliga tillgången har delresurser. |
   | **[!UICONTROL Rendition(s)]** | En återgivning är den binära representationen av en resurs. Resurser har en primär representation - den som utgörs av den överförda filen. De kan ha valfritt antal representationer. <br> Med det här alternativet kan du välja de återgivningar du vill hämta. Vilka återgivningar som är tillgängliga beror på vilken resurs du har valt. |
   | **[!UICONTROL Smart Crops]** | Välj det här alternativet om du vill hämta alla smarta beskärningsåtergivningar för den valda resursen inifrån [!DNL Experience Manager]. En ZIP-fil med renderingarna Smart Crop skapas och hämtas till din lokala dator. |
   | **[!UICONTROL Dynamic Rendition(s)]** | Välj det här alternativet om du vill generera en serie alternativa återgivningar i realtid. När du väljer det här alternativet väljer du också de återgivningar som du vill skapa dynamiskt genom att välja i listan [Bildförinställning](/help/assets/dynamic-media/image-presets.md) . <br>Du kan dessutom välja storlek och måttenhet, format, färgrymd, upplösning och alla valfria bildmodifierare, t.ex. invertering av bilden. Alternativet är bara tillgängligt om du har [!DNL Dynamic Media] aktiverat. |

1. In the dialog box, click **[!UICONTROL Download]**.

## Aktivera resurshämtningsserver {#enable-asset-download-servlet}

Med standardservleten i [!DNL Experience Manager] kan autentiserade användare skicka godtyckligt stora, samtidiga hämtningsbegäranden för att skapa ZIP-filer med resurser. Förberedelsen kan påverka prestanda eller till och med överbelasta servern och nätverket. För att minska sådana potentiella DoS-liknande risker som den här funktionen medför inaktiveras `AssetDownloadServlet` OSGi-komponenten för publiceringsinstanser.

Om du vill tillåta hämtning av resurser från DAM, till exempel när du använder Assets Share Commons eller någon annan portalliknande implementering, aktiverar du servleten manuellt via en OSGi-konfiguration. Adobe rekommenderar att du anger en så låg hämtningsstorlek som möjligt utan att det påverkar den dagliga hämtningen. Ett högt värde kan påverka prestandan.

1. Skapa en mapp med en namnkonvention som anger publiceringsmiljön som mål, det vill säga `config.publish`:

   `/apps/<your-app-name>/config.publish`

1. Skapa en ny fil av typen `nt:file` med namnet i config-mappen `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`.
1. Fyll `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` med följande: Anger en maximal storlek (i byte) för hämtningen som värdet för `asset.download.prezip.maxcontentsize`. Nedanstående exempel konfigurerar den maximala storleken för ZIP-nedladdningen till högst 100 kB.

   ```java
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

## Inaktivera resurshämtningsserver {#disable-asset-download-servlet}

Du `Asset Download Servlet` kan inaktivera funktionen på en [!DNL Experience Manager] publiceringsinstans genom att uppdatera dispatcherns konfiguration för att blockera eventuella hämtningsbegäranden. Servern kan även inaktiveras manuellt via OSGi-konsolen direkt.

1. Om du vill blockera resurshämtningsbegäranden via en dispatcherkonfiguration redigerar du `dispatcher.any` konfigurationen och lägger till en ny regel i [filteravsnittet](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#defining-a-filter).

   `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

>[!MORELIKETHIS]
>
>* [Hämta DRM-skyddade resurser](drm.md)
>* [Hämta resurser med skrivbordsappen Experience Manager på Win eller Mac](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html)
>* [Hämta resurser med Adobe Assets Link inifrån de Adobe Creative Cloud-appar som stöds](https://helpx.adobe.com/se/enterprise/using/manage-assets-using-adobe-asset-link.html)

