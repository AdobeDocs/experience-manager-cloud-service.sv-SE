---
title: Resursinsikter
description: Spåra användarbetyg och användningsstatistik för bilder som används på tredjepartswebbplatser, marknadsföringskampanjer och Adobe kreativa lösningar.
contentOwner: AG
feature: Resursinsikter,Resursrapporter
role: Business Practitioner,Leader
exl-id: e268453b-e7c0-4aa4-bd29-2686edb5f99a
source-git-commit: 1c841eaa49eeb021fc7583c58aeaefc1236650f9
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 2%

---

# Resursinsikter {#asset-insights}

Funktionen Assets Insights gör att ni kan spåra användarbetyg och användningsstatistik för bilder som används på tredjepartswebbplatser, marknadsföringskampanjer och Adobe kreativa lösningar. Det ger insikter om bildens prestanda och popularitet.

Assets Insights samlar in information om användaraktivitet, t.ex. hur många gånger en bild klassificeras, klickas och hur många gånger bilden läses in på webbplatsen. Det tilldelar poäng till bilder baserat på denna statistik. Du kan använda resultat och prestandastatistik för att välja populära bilder som ska ingå i kataloger, marknadsföringskampanjer och så vidare. Man kan till och med utforma arkiverings- och licensförnyelseregler baserat på denna statistik.

För att Assets Insights ska kunna samla in användningsstatistik för bilder från en webbplats måste du inkludera inbäddningskoden för bilden i webbplatskoden.

Om du vill att Assets Insights ska visa användningsstatistik för resurser måste du först konfigurera funktionen så att rapporteringsdata hämtas från [!DNL Adobe Analytics]. Mer information finns i [Konfigurera resursinsikter](#configure-asset-insights). Om du vill använda den här funktionen måste du köpa [!DNL Adobe Analytics] separat.

>[!NOTE]
>
>Insikter stöds och tillhandahålls endast för bilder.

## Visa statistik för en bild {#viewing-statistics-for-an-image}

Du kan visa bakgrundsmusik för resursinsikter från metadatasidan.

1. I resursanvändargränssnittet markerar du bilden och klickar sedan på **[!UICONTROL Properties]** i verktygsfältet.
1. Klicka på **[!UICONTROL Insights]** på sidan Egenskaper.
1. Granska användningsinformationen för resursen på fliken **[!UICONTROL Insights]**. Avsnittet **[!UICONTROL Score]** beskriver den totala resursanvändningen och prestandan för en tillgång.

   Användningspoäng beskriver hur många gånger resursen används i olika lösningar.

   **[!UICONTROL Impressions]**-poängen är antalet gånger som resursen läses in på webbplatsen. Siffran som visas under **[!UICONTROL Clicks]** är antalet gånger som användaren klickar på resursen.

1. Gå igenom **[!UICONTROL Usage Statistics]**-avsnittet för att ta reda på vilka enheter resursen var en del av och vilka kreativa lösningar som nyligen har använt den. Ju högre användning, desto större chans att resursen är populär bland användarna. Användningsdata visas under följande rubriker:

   * **[!UICONTROL Asset]**: Antalet gånger som tillgången ingick i en samling eller sammansatt tillgång.
   * **[!UICONTROL Web & Mobile]**: Antalet gånger som resursen ingick i webbplatser och appar.
   * **[!UICONTROL Social]**: Antalet gånger som tillgången användes i andra lösningar, t.ex. en  [!DNL Adobe Campaign].
   * **[!UICONTROL Email]**: Antalet gånger som resursen användes i e-postkampanjer.

   ![användningsstatistik](assets/usage_statistics.png)

   >[!NOTE]
   >
   >Eftersom funktionen Resursinsikter vanligtvis hämtar data från [!DNL Adobe Analytics] från lösningar regelbundet, kanske inte avsnittet Lösningar visar de senaste data. Den tidsperiod som data visas för beror på schemat för hämtningsåtgärden som Assets Insights kör för att hämta Analytics-data.

1. Om du vill visa prestandastatistik för resursen grafiskt över en tidsperiod väljer du period i **[!UICONTROL Performance Statistics]**-avsnittet. Detaljer, inklusive klick och visningar, visas som trendlinjer i ett diagram.

   ![chlimage_1-3](assets/chlimage_1-3.jpeg)

   >[!NOTE]
   >
   >Till skillnad från data i avsnittet Lösningar visar avsnittet Prestandastatistik de senaste data.

1. Om du vill hämta inbäddningskoden för resursen som du inkluderar på webbplatser för att få prestandadata klickar du **[!UICONTROL Get Embed Code]** under miniatyrbilden för resursen. <!-- For more information on how to include your Embed code in third-party web pages, see [Using Page Tracker and Embed code in web pages](/help/assets/use-page-tracker.md). -->

   ![chlimage_1-98](assets/chlimage_1-98.png)

## Visa sammanställningsstatistik för bilder {#viewing-aggregate-statistics-for-images}

Du kan visa bakgrundsmusik för alla resurser i en mapp samtidigt med **[!UICONTROL Insights View]**.

1. I resursgränssnittet navigerar du till den mapp som innehåller de resurser som du vill visa insikter för.
1. Klicka på alternativet Layout i verktygsfältet och välj sedan **[!UICONTROL Insights View]**.
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

[!DNL Experience Manager Assets] hämtar användningsdata om digitala resurser som används av tredjepartswebbplatser från  [!DNL Adobe Analytics]. Om du vill att Assets Insights ska kunna hämta data och generera insikter måste du först konfigurera funktionen så att den integreras med [!DNL Adobe Analytics].

>[!NOTE]
>
>Insikter stöds endast och tillhandahålls för bilder.

1. I [!DNL Experience Manager] klickar du på **[!UICONTROL Tools]** > **[!UICONTROL Assets]**.

   ![chlimage_1-72](assets/chlimage_1-72.png)

1. Klicka på **[!UICONTROL Insights Configuration]**-kortet.
1. Välj ett datacenter i guiden och ange dina autentiseringsuppgifter, inklusive namnet på din organisation, användarnamn och delad hemlighet.

   ![Konfigurera Adobe Analytics for Assets Insights i  [!DNL Experience Manager]](assets/insights_config2.png)

   *Bild: Konfigurera Adobe Analytics for Assets Insights i[!DNL Experience Manager]*

1. Klicka på **[!UICONTROL Authenticate]**. När [!DNL Experience Manager] har autentiserat dina inloggningsuppgifter väljer du en Adobe Analytics-rapportsserie från **[!UICONTROL Report Suite]**-listan där du vill att Assets Insights ska hämta data. Klicka på **[!UICONTROL Add]**.
1. När [!DNL Experience Manager] har konfigurerat rapportsviten klickar du på **[!UICONTROL Done]**.

### Sidspåraren {#page-tracker}

När du har konfigurerat ditt Adobe Analytics-konto genereras sidspårningskoden åt dig. Om du vill att Assets Insights ska kunna spåra [!DNL Experience Manager]-resurserna som används på tredjepartswebbplatser, inkluderar du sidspårningskoden i webbplatskoden. Använd verktyget Sidspårare i Assets för att generera sidspårningskod. <!--  For more information on how to include your Page Tracker code in third-party web pages, see [Using Page Tracker and Embed code in web pages](/help/assets/use-page-tracker.md). -->

1. I [!DNL Experience Manager] klickar du på **[!UICONTROL Tools]** > **[!UICONTROL Assets]**.

   ![chlimage_1-73](assets/chlimage_1-73.png)

1. Klicka på **[!UICONTROL Insights Page Tracker]**-kortet på sidan **[!UICONTROL Navigation]**.
1. Klicka på **[!UICONTROL Download]** om du vill hämta sidspårningskoden.

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
