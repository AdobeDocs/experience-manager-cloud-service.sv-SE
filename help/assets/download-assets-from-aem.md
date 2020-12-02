---
title: Hämta resurser
description: Hämta resurser från [!DNL Adobe Experience Manager Assets] och aktivera eller inaktivera hämtningsfunktionen.
contentOwner: AG
translation-type: tm+mt
source-git-commit: b1586cd9d6b3e9da115bff802d840a72d1207e4a
workflow-type: tm+mt
source-wordcount: '865'
ht-degree: 1%

---


# Hämta resurser från [!DNL Adobe Experience Manager] {#download-assets-from-aem}

Du kan hämta resurser, inklusive statiska och dynamiska återgivningar. Du kan också skicka e-postmeddelanden med länkar till resurser direkt från [!DNL Adobe Experience Manager Assets]. Hämtade resurser paketeras i en ZIP-fil. Den komprimerade ZIP-filen har en maximal filstorlek på 1 GB för exportjobbet. Högst 500 resurser per exportjobb tillåts.

>[!NOTE]
>
>Mottagare av e-postmeddelanden måste vara medlemmar i gruppen `dam-users` för att få åtkomst till länken för ZIP-hämtning i e-postmeddelandet. För att kunna hämta resurserna måste medlemmarna ha behörighet att starta arbetsflöden som utlöser hämtning av resurser.

Det går inte att hämta resurstyperna Bilduppsättningar, Snurra uppsättningar, Blandade medieuppsättningar och Carousel-uppsättningar.

Du kan hämta Experience Manager-resurser på följande sätt:

* [Experience Manager användargränssnitt](#download-in-aem)
* Användargränssnittet Resurslänkdelning
* [Kommandon för resursdelning](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* [Varumärkesportal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html)
* [Datorprogram](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#download-assets)

## Hämta resurser med AEM gränssnitt {#download-in-aem}

Asynkron nedladdningstjänst ger ett ramverk för smidig nedladdning av stora resurser. Mindre filer hämtas från användargränssnittet i realtid. De stora filerna hämtas asynkront och användarna informeras om att de har slutförts via Experience Manager-meddelanden i Inkorgen. Se [förstå Experience Manager inbox](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/getting-started/inbox.html).

![Hämta meddelande](assets/download-notification.png)

*Bild: Ladda ned meddelanden via  [!DNL Experience Manager] Inkorgen.*

Asynkrona nedladdningar aktiveras i något av följande fall:

* Om det finns mer än 10 resurser eller mer än 100 MB att hämta.
* Om nedladdningen tar mer än 30 sekunder att förbereda.

Så här hämtar du resurser:

1. I [!DNL Experience Manager]-användargränssnittet klickar du på **[!UICONTROL Assets]** > **[!UICONTROL Files]**.
1. Navigera till de resurser du vill hämta. Markera mappen eller välj en eller flera resurser i mappen. Klicka på **[!UICONTROL Download]** i verktygsfältet.

   ![Tillgängliga alternativ vid hämtning av resurser från  [!DNL Experience Manager Assets]](/help/assets/assets/asset-download1.png)

   *Bild: Alternativ i dialogrutan Hämta.*

1. I dialogrutan Hämta väljer du de hämtningsalternativ som du vill använda.

   | Hämtningsalternativ | Beskrivning |
   |---|---|
   | **[!UICONTROL Create separate folder for each asset]** | Välj det här alternativet om du vill inkludera varje resurs som du hämtar, inklusive resurser, i underordnade mappar som är kapslade under resursens överordnade mapp i en mapp på den lokala datorn. När det här alternativet är *inte* markerat ignoreras mapphierarkin som standard och alla resurser hämtas till en mapp på den lokala datorn. |
   | **[!UICONTROL Email]** | Välj det här alternativet om du vill att ett e-postmeddelande ska skickas till mottagaren. Standardmallar för e-post finns på följande platser:<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> Mallar som du anpassar under distributionen finns på följande platser: <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul>Du kan lagra klientspecifika anpassade mallar på följande platser:<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> |
   | **[!UICONTROL Asset(s)]** | Välj det här alternativet om du vill hämta resursen i dess ursprungliga form utan några återgivningar.<br>Alternativet Delresurser är tillgängligt om den ursprungliga tillgången har delresurser. |
   | **[!UICONTROL Rendition(s)]** | En återgivning är den binära representationen av en resurs. Resurser har en primär representation - den som utgörs av den överförda filen. De kan ha valfritt antal representationer. <br> Med det här alternativet kan du välja de återgivningar du vill hämta. Vilka återgivningar som är tillgängliga beror på vilken resurs du har valt. |
   | **[!UICONTROL Smart Crops]** | Välj det här alternativet om du vill hämta alla smarta beskärningsåtergivningar för den valda resursen från [!DNL Experience Manager]. En ZIP-fil med renderingarna Smart Crop skapas och hämtas till din lokala dator. |
   | **[!UICONTROL Dynamic Rendition(s)]** | Välj det här alternativet om du vill generera en serie alternativa återgivningar i realtid. När du väljer det här alternativet väljer du också de återgivningar som du vill skapa dynamiskt genom att välja i listan [Bildförinställning](/help/assets/dynamic-media/image-presets.md). <br>Du kan dessutom välja storlek och måttenhet, format, färgrymd, upplösning och alla valfria bildmodifierare, t.ex. invertering av bilden. Alternativet är bara tillgängligt om du har [!DNL Dynamic Media] aktiverat. |

1. Klicka på **[!UICONTROL Download]** i dialogrutan.

## Aktivera resurshämtningsserver {#enable-asset-download-servlet}

Med standardservleten i [!DNL Experience Manager] kan autentiserade användare utfärda godtyckligt stora, samtidiga hämtningsbegäranden för att skapa ZIP-filer med resurser. Förberedelsen kan påverka prestanda eller till och med överbelasta servern och nätverket. För att minska sådana potentiella DoS-liknande risker som orsakas av den här funktionen är `AssetDownloadServlet` OSGi-komponenten inaktiverad för publiceringsinstanser.

Om du vill tillåta hämtning av resurser från DAM, till exempel när du använder Assets Share Commons eller någon annan portalliknande implementering, aktiverar du servleten manuellt via en OSGi-konfiguration. Adobe rekommenderar att du anger en så låg hämtningsstorlek som möjligt utan att det påverkar den dagliga hämtningen. Ett högt värde kan påverka prestandan.

1. Skapa en mapp med en namnkonvention som anger publiceringskörningsläget som mål, det vill säga `config.publish`:

   `/apps/<your-app-name>/config.publish`

1. Skapa en ny fil av typen `nt:file` med namnet `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` i konfigurationsmappen.
1. Fyll i `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` med följande: Anger en maximal storlek (i byte) för hämtningen som `asset.download.prezip.maxcontentsize`. Nedanstående exempel konfigurerar den maximala storleken för ZIP-nedladdningen till högst 100 kB.

   ```java
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

## Inaktivera resurshämtningsservlet {#disable-asset-download-servlet}

`Asset Download Servlet` kan inaktiveras för en [!DNL Experience Manager]-publiceringsinstans genom att uppdatera dispatcherkonfigurationen för att blockera eventuella hämtningsbegäranden. Servern kan även inaktiveras manuellt via OSGi-konsolen direkt.

1. Om du vill blockera resurshämtningsbegäranden via en dispatcherkonfiguration redigerar du konfigurationen `dispatcher.any` och lägger till en ny regel i [filteravsnittet](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#configuring).

   `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

>[!MORELIKETHIS]
>
>* [Hämta DRM-skyddade resurser](drm.md)
>* [Hämta resurser med skrivbordsappen Experience Manager på Win eller Mac](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html)
>* [Hämta resurser med Adobe Assets Link inifrån de Adobe Creative Cloud-appar som stöds](https://helpx.adobe.com/se/enterprise/using/manage-assets-using-adobe-asset-link.html)

