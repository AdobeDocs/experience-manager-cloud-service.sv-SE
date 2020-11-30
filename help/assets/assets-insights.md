---
title: 'Asset Insights '
description: Lär dig hur funktionen för tillgångsinsikter gör att du kan spåra användarbetyg och användningsstatistik för bilder som används på tredjepartswebbplatser, marknadsföringskampanjer och Adobe kreativa lösningar.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 26833f59f21efa4de33969b7ae2e782fe5db8a14
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 3%

---


# Asset Insights {#asset-insights}

Med tillgångsinsikter kan du spåra användarbetyg och användningsstatistik för bilder som används på tredjepartswebbplatser, marknadsföringskampanjer och Adobe kreativa lösningar. Det ger insikter om bildens prestanda och popularitet.

Assets Insights samlar in information om användaraktivitet, t.ex. hur många gånger en bild klassificeras, klickas och hur många gånger bilden läses in på webbplatsen. Det tilldelar poäng till bilder baserat på denna statistik. Du kan använda resultat och prestandastatistik för att välja populära bilder som ska ingå i kataloger, marknadsföringskampanjer och så vidare. Man kan till och med utforma arkiverings- och licensförnyelseregler baserat på denna statistik.

För att Assets Insights ska kunna samla in användningsstatistik för bilder från en webbplats måste du inkludera inbäddningskoden för bilden i webbplatskoden.

Om du vill att tillgångsinsikter ska visa användningsstatistik för resurser måste du först konfigurera funktionen för att hämta rapportdata från Adobe Analytics. Mer information finns i [Konfigurera tillgångsinsikter](#configure-asset-insights).

>[!NOTE]
>
>Insikter stöds endast och tillhandahålls för bilder.

## Visa statistik för en bild {#viewing-statistics-for-an-image}

Du kan visa poängen för resursinsikter från metadatasidan.

1. Välj bilden i användargränssnittet Resurser och tryck sedan på **[!UICONTROL Properties]** i verktygsfältet.
1. Tryck på egenskapssidan **[!UICONTROL Insights]**.
1. Granska användningsinformationen för resursen på **[!UICONTROL Insights]** fliken. I avsnittet **[!UICONTROL Score]** beskrivs den totala resursanvändningen och prestandan för en tillgång.

   Användningspoäng beskriver hur många gånger resursen används i olika lösningar.

   Poängen **[!UICONTROL Impressions]** är antalet gånger som resursen läses in på webbplatsen. Siffran som visas under **[!UICONTROL Clicks]** är antalet gånger som användaren klickar på resursen.

1. Läs igenom **[!UICONTROL Usage Statistics]** avsnittet för att ta reda på vilka enheter resursen ingick i och vilka kreativa lösningar som nyligen använt den. Ju högre användning, desto större chans att resursen är populär bland användarna. Användningsdata visas under följande rubriker:

   * **[!UICONTROL Asset]**: Antalet gånger som tillgången ingick i en samling eller sammansatt tillgång.
   * **[!UICONTROL Web & Mobile]**: Antalet gånger som resursen ingick i webbplatser och appar.
   * **[!UICONTROL Social]**: Antalet gånger som resursen användes i lösningar som Adobe Social och Adobe Campaign.
   * **[!UICONTROL Email]**: Antalet gånger som resursen användes i e-postkampanjer.

   ![användningsstatistik](assets/usage_statistics.png)

   >[!NOTE]
   >
   >Eftersom funktionen för tillgångsinsikter vanligtvis hämtar data från lösningar från Adobe Analytics regelbundet, kanske inte avsnittet Lösningar visar de senaste data. Den tidsperiod som data visas för beror på schemat för hämtningsåtgärden som resursinsikter körs för att hämta analysdata.

1. To view performance statistics for the asset graphically over a period of time, select period in the **[!UICONTROL Performance Statistics]** section. Detaljer, inklusive klick och visningar, visas som trendlinjer i ett diagram.

   ![chlimage_1-3](assets/chlimage_1-3.jpeg)

   >[!NOTE]
   >
   >Till skillnad från data i avsnittet Lösningar visar avsnittet Prestandastatistik de senaste data.

1. Om du vill hämta inbäddningskoden för resursen som du inkluderar på webbplatser för att få prestandadata trycker/klickar du **[!UICONTROL Get Embed Code]** nedanför miniatyrbilden för resursen. <!-- For more information on how to include your Embed code in third-party web pages, see [Using Page Tracker and Embed code in web pages](/help/assets/use-page-tracker.md). -->

   ![chlimage_1-98](assets/chlimage_1-98.png)

## Visa sammanställd statistik för bilder {#viewing-aggregate-statistics-for-images}

You can view scores of all assets within a folder simultaneously using **[!UICONTROL Insights View]**.

1. I resursgränssnittet navigerar du till den mapp som innehåller de resurser som du vill visa insikter för.
1. Tryck/klicka på layoutikonen i verktygsfältet och välj sedan **[!UICONTROL Insights View]**.
1. På sidan visas användningsresultat för resurserna. Jämför omdömen om de olika tillgångarna och få insikter.

## Schemalägg bakgrundsjobb {#scheduling-background-job}

Resursinsikter hämtar användningsdata för resurser från Adobe Analytics rapportsviter regelbundet. Som standard körs ett bakgrundsjobb var 24:e timme i resursinsikter för att hämta data. Du kan dock ändra både frekvens och tid genom att konfigurera **[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]** tjänsten från webbkonsolen.

1. Tap the AEM logo, and go to **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
1. Öppna **[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]** tjänstkonfigurationen.

   ![chlimage_1-99](assets/chlimage_1-99.png)

1. Ange önskad schemaläggningsfrekvens och starttid för jobbet i egenskapsschemaläggaruttrycket. Spara ändringarna.

## Konfigurera tillgångsinsikter {#configure-asset-insights}

Adobe Experience Manager (AEM) Assets hämtar användningsdata runt AEM resurser som används av tredjepartswebbplatser från Adobe Analytics. Om du vill att tillgångsinsikter ska kunna hämta dessa data och generera insikter måste du först konfigurera funktionen så att den integreras med Adobe Analytics.

>[!NOTE]
>
>Insikter stöds endast och tillhandahålls för bilder.

1. Klicka på **[!UICONTROL Tools]** > **[!UICONTROL Assets]** i AEM.

   ![chlimage_1-72](assets/chlimage_1-72.png)

1. Klicka på **[!UICONTROL Insights Configuration]** kortet.
1. Välj ett datacenter i guiden och ange dina autentiseringsuppgifter, inklusive namnet på din organisation, användarnamn och delad hemlighet.

   ![Konfigurera Adobe Analytics för Assets Insights i AEM](assets/insights_config2.png)

   *Bild: Konfigurera Adobe Analytics för Assets Insights i AEM*

1. Klicka/tryck på **[!UICONTROL Authenticate]**. När AEM har autentiserat dina inloggningsuppgifter väljer du en Adobe Analytics-rapportsvit från den plats där du vill att tillgångsinsikter ska hämta data. **[!UICONTROL Report Suite]** Klicka på **[!UICONTROL Add]**.
1. När AEM har konfigurerat rapportsviten trycker du **[!UICONTROL Done]**.

### Sidspårare {#page-tracker}

När du har konfigurerat ditt Adobe Analytics-konto genereras sidspårningskoden åt dig. Om du vill göra det möjligt för Assets Insights att spåra AEM resurser som används på tredjepartswebbplatser, inkluderar du sidspårningskoden i webbplatskoden. Använd verktyget Sidspårare i AEM Assets för att generera sidspårningskod. <!--  For more information on how to include your Page Tracker code in third-party web pages, see [Using Page Tracker and Embed code in web pages](/help/assets/use-page-tracker.md). -->

1. Klicka på **[!UICONTROL Tools]** > **[!UICONTROL Assets]** i AEM.

   ![chlimage_1-73](assets/chlimage_1-73.png)

1. På **[!UICONTROL Navigation]** sidan klickar du på **[!UICONTROL Insights Page Tracker]** kortet.
1. Klicka **[!UICONTROL Download]** för att hämta sidspårningskoden.

<!--

## Using demo package for Asset Insights {#using-demo-package-for-asset-insights}

Using the demo package, you can enable Adobe Asset Insights to capture data from and generate insights for a sample web page.

1. Configure Asset Insights using the instructions in [Configure Asset Insights](#configure-asset-insights).
1. Download the sample AEM Assets package from below and install the package from CRXDE package manager.

   [Get File](assets/insightsdemo.zip)

1. Download the ZIP file containing the sample web page from below and extract on your local file system.

   [Get File](assets/demosite.zip)

1. Click the web page to open it in the web browser.

   >[!CAUTION]
   >
   >Web Page is configured to load asset from the localhost server . In case your server is running somewhere else change server address from localhost to server address in the HTML content of the web page.

   >[!NOTE]
   >
   >The external web page can be in AEM itself.

-->
