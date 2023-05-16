---
title: Resursinsikter
description: Spåra användarbetyg och användningsstatistik för bilder som används på tredjepartswebbplatser, marknadsföringskampanjer och Adobe kreativa lösningar.
contentOwner: AG
feature: Asset Insights,Asset Reports
role: User,Leader
exl-id: e268453b-e7c0-4aa4-bd29-2686edb5f99a
source-git-commit: 80ac947976bab2b0bfedb4ff9d5dd4634de6b4fc
workflow-type: tm+mt
source-wordcount: '850'
ht-degree: 4%

---

# Resursinsikter {#asset-insights}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/asset-insights.html?lang=en) |
| AEM as a Cloud Service | Den här artikeln |

Funktionen Assets Insights gör att ni kan spåra användarbetyg och användningsstatistik för bilder som används på tredjepartswebbplatser, marknadsföringskampanjer och Adobe kreativa lösningar. Det ger insikter om bildens prestanda och popularitet.

Assets Insights samlar in information om användaraktivitet, t.ex. hur många gånger en bild klassificeras, klickas och hur många gånger bilden läses in på webbplatsen. Det tilldelar poäng till bilder baserat på denna statistik. Du kan använda resultat och prestandastatistik för att välja populära bilder som ska ingå i kataloger, marknadsföringskampanjer och så vidare. Man kan till och med utforma arkiverings- och licensförnyelseregler baserat på denna statistik.

För att Assets Insights ska kunna samla in användningsstatistik för bilder från en webbplats måste du inkludera inbäddningskoden för bilden i webbplatskoden.

Om du vill att Assets Insights ska visa användningsstatistik för resurser måste du först konfigurera funktionen att hämta rapportdata från [!DNL Adobe Analytics]. Mer information finns i [Konfigurera resursinsikter](#configure-asset-insights). Om du vill använda den här funktionen köper du [!DNL Adobe Analytics] separat.

>[!NOTE]
>
>Insikter stöds och tillhandahålls endast för bilder.

## Visa statistik för en bild {#viewing-statistics-for-an-image}

Du kan visa bakgrundsmusik för resursinsikter från metadatasidan.

1. I Assets-användargränssnittet markerar du bilden och klickar sedan på **[!UICONTROL Properties]** i verktygsfältet.
1. På sidan Egenskaper klickar du på **[!UICONTROL Insights]**.
1. Granska användningsinformationen för resursen i **[!UICONTROL Insights]** -fliken. The **[!UICONTROL Score]** I avsnittet beskrivs den totala användningen av tillgångar och prestandan för en tillgång.

   Användningspoäng beskriver hur många gånger resursen används i olika lösningar.

   The **[!UICONTROL Impressions]** poäng är antalet gånger som resursen läses in på webbplatsen. Numret som visas under **[!UICONTROL Clicks]** är antalet gånger som användaren klickar på resursen.

1. Granska **[!UICONTROL Usage Statistics]** för att ta reda på vilka enheter resursen ingick i och vilka kreativa lösningar som nyligen använde den. Ju högre användning, desto större chans att resursen är populär bland användarna. Användningsdata visas under följande rubriker:

   * **[!UICONTROL Asset]**: Antalet gånger som tillgången ingick i en samling eller sammansatt tillgång.
   * **[!UICONTROL Web & Mobile]**: Antalet gånger som resursen ingick i webbplatser och appar.
   * **[!UICONTROL Social]**: Antalet gånger som tillgången användes i andra lösningar, t.ex. en [!DNL Adobe Campaign].
   * **[!UICONTROL Email]**: Antalet gånger som resursen användes i e-postkampanjer.

   ![användningsstatistik](assets/usage_statistics.png)

   >[!NOTE]
   >
   >Eftersom funktionen Assets Insights vanligtvis hämtar data från lösningar [!DNL Adobe Analytics] Med jämna mellanrum visas kanske inte de senaste data i avsnittet Lösningar. Den tidsperiod som data visas för beror på schemat för hämtningsåtgärden som Assets Insights kör för att hämta Analytics-data.

1. Om du vill visa prestandastatistik för resursen grafiskt över en tidsperiod väljer du period i **[!UICONTROL Performance Statistics]** -avsnitt. Detaljer, inklusive klick och visningar, visas som trendlinjer i ett diagram.

   ![chlimage_1-3](assets/chlimage_1-3.jpeg)

   >[!NOTE]
   >
   >Till skillnad från data i avsnittet Lösningar visar avsnittet Prestandastatistik de senaste data.

1. Om du vill hämta inbäddningskoden för resursen som du inkluderar på webbplatser för att få prestandadata klickar du på **[!UICONTROL Get Embed Code]** under miniatyrbilden av resursen. <!-- For more information on how to include your Embed code in third-party web pages, see [Using Page Tracker and Embed code in web pages](/help/assets/use-page-tracker.md). -->

   ![chlimage_1-98](assets/chlimage_1-98.png)

## Visa sammanställd statistik för bilder {#viewing-aggregate-statistics-for-images}

Du kan visa bakgrundsmusik för alla resurser i en mapp samtidigt med **[!UICONTROL Insights View]**.

1. I Assets-användargränssnittet navigerar du till den mapp som innehåller de resurser som du vill visa insikter för.
1. Klicka på **[!UICONTROL Layout]** i verktygsfältet och välj **[!UICONTROL Insights View]**.
1. På sidan visas användningsresultat för resurserna. Jämför omdömen om de olika tillgångarna och få insikter.

<!-- TBD: Commenting as Web Console is not available. Document the appropriate OSGi config method if available in CS.

## Schedule background job {#scheduling-background-job}

Assets Insights fetches usage data for assets from Adobe Analytics report suites in a periodic manner. By default, Assets Insights runs a background job every 24 hours at 2 AM to the fetch data. However, you can modify both the frequency and the time by configuring the **[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]** service from the web console.

1. Click the [!DNL Experience Manager] logo, and go to **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
1. Open the **[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]** service configuration.

   ![chlimage_1-99](assets/chlimage_1-99.png)

1. Specify the desired scheduler frequency and the start time for the job in the property scheduler expression. Save the changes.
-->

## Konfigurera resursinsikter {#configure-asset-insights}

[!DNL Experience Manager Assets] hämtar användningsdata om digitala resurser som används av tredjepartswebbplatser från [!DNL Adobe Analytics]. Om du vill att Assets Insights ska kunna hämta data och generera insikter måste du först konfigurera funktionen så att den integreras med [!DNL Adobe Analytics].

>[!NOTE]
>
>Insikter stöds endast och tillhandahålls för bilder.

1. I [!DNL Experience Manager], klicka **[!UICONTROL Tools]** > **[!UICONTROL Assets]**.

   ![chlimage_1-73](assets/chlimage_1-73.png)

1. Klicka på **[!UICONTROL Insights Configuration]** kort.

1. Om du vill ha åtkomstinformation för webbtjänsten Analytics går du till **[!UICONTROL Analytics]** > **[!UICONTROL Admin]** > **[!UICONTROL Admin Tools]** > **[!UICONTROL Company Settings]** > **[!UICONTROL Web Services]** och kopiera **[!UICONTROL Shared Secret]** nyckel.

   I guiden väljer du **[!UICONTROL Data Center]** och ange visningsnamnet för **[!UICONTROL Company]**, webbtjänster **[!UICONTROL Username]** och klistra in **[!UICONTROL Shared Secret]** nyckel.

   Klicka på **[!UICONTROL Authenticate]**.

   ![Konfigurera Adobe Analytics for Assets Insights i [!DNL Experience Manager]](assets/analytics-insight-config.png)

   *Bild: Konfigurera Adobe Analytics for Assets Insights i[!DNL Experience Manager]*

1. När autentiseringen är klar visas rapportsviterna i listrutan. Välj Adobe Analytics **[!UICONTROL Report Suite]** där ni vill att Assets Insights ska hämta data. Klicka på **[!UICONTROL Add]**.

1. Efter [!DNL Experience Manager] ställer in din rapportsvit, klicka på **[!UICONTROL Done]**.

Mer information finns i [Adobe Analytics Web Services](https://experienceleague.adobe.com/docs/analytics/admin/company-settings/web-services-admin.html#api-access-information).

### Sidspårare {#page-tracker}

När du har konfigurerat ditt Adobe Analytics-konto genereras sidspårningskoden åt dig. Aktivera resursinsikter för att spåra [!DNL Experience Manager] resurser som används på tredjepartswebbplatser, inkluderar sidspårningskoden i webbplatskoden. Använd verktyget Sidspårare i Assets för att generera sidspårningskod. <!--  For more information on how to include your Page Tracker code in third-party web pages, see [Using Page Tracker and Embed code in web pages](/help/assets/use-page-tracker.md). -->

1. I [!DNL Experience Manager], klicka **[!UICONTROL Tools]** > **[!UICONTROL Assets]**.

   ![chlimage_1-73](assets/chlimage_1-73.png)

1. Från **[!UICONTROL Navigation]** klickar du på **[!UICONTROL Insights Page Tracker]** kort.
1. Klicka **[!UICONTROL Download]** för att hämta sidspårningskod.

<!--
Add page tracker code, CQDOC-18045, 30/07/2021
-->
I följande exempelkodfragment visas den sidspårningskod som finns på en exempelwebbsida:

```xml
 <head>
            <script type="text/javascript" src="http://localhost:4502/xxxx/etc.clientlibs/dam/clientlibs/sitecatalyst/appmeasurement.js"></script>
            <script type="text/javascript" src="http://localhost:4502/xxxx/etc.clientlibs/dam/clientlibs/foundation/assetinsights/pagetracker.js"></script>
            <script type="text/javascript">
                                assetAnalytics.attrTrackable = 'trackable';
                assetAnalytics.defaultTrackable = false;
                assetAnalytics.attrAssetID = 'aem-asset-id';
                assetAnalytics.assetImpressionPollInterval = 200; // interval in millis
                assetAnalytics.charsLimitForGET = 2000; // bytes
                assetAnalytics.dispatcher.init("assetstesting","abc.net","bee","list1","eVar3","event8","event7");
            </script>

 </head>
```



<!--

## Using demo package for Assets Insights {#using-demo-package-for-asset-insights}

Using the demo package, you can enable Adobe Assets Insights to capture data from and generate insights for a sample web page.

1. Configure Assets Insights using the instructions in [Configure Assets Insights](#configure-asset-insights).
1. Download the sample [!DNL Experience Manager Assets] package from below and install the package from CRXDE package manager.

   [Get File](assets/insightsdemo.zip)

1. Download the ZIP file containing the sample web page from below and extract on your local file system.

   [Get File](assets/demosite.zip)

1. Click the web page to open it in the web browser.

   >[!CAUTION]
   >
   >Web Page is configured to load asset from the localhost server . In case your server is running somewhere else change server address from localhost to server address in the HTML content of the web page.

   >[!NOTE]
   >
   >The external web page can be in [!DNL Experience Manager] itself.

-->

**Se även**

* [Översätt resurser](translate-assets.md)
* [HTTP API för Assets](mac-api-assets.md)
* [Resurser som stöds i filformat](file-format-support.md)
* [Söka efter resurser](search-assets.md)
* [Anslutna resurser](use-assets-across-connected-assets-instances.md)
* [Materialrapporter](asset-reports.md)
* [Metadata-scheman](metadata-schemas.md)
* [Hämta resurser](download-assets-from-aem.md)
* [Hantera metadata](manage-metadata.md)
* [Söka efter fasetter](search-facets.md)
* [Hantera samlingar](manage-collections.md)
* [Import av massmetadata](metadata-import-export.md)
