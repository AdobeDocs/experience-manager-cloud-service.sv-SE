---
title: Integrera med Adobe Analytics
description: 'Integrera med Adobe Analytics '
translation-type: tm+mt
source-git-commit: 6754693da488b0bc44a71aa9f0402fc1308b703a
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 12%

---


# Integrera med Adobe Analytics{#integrating-with-adobe-analytics}

Genom att integrera Adobe Analytics och AEM som en molntjänst kan du spåra din webbsidesaktivitet:

* Med en Adobe Analytics-konfiguration kan AEM autentisera med Adobe Analytics.
* Ett ramverk identifierar de data som skickas till rapportsviten för Adobe Analytics.

Informationen innehåller t.ex. sid- och användardata:

* data som AEM-komponenter samlar in
* länkklick
* videoanvändningsinformation
* antalet sidbesök från Adobe Analytics

På sidorna nedan kan du konfigurera integreringen. Observera att Launch från Adobe är de facto-verktyget för att instrumentera en AEM-webbplats med analysfunktioner (JS-bibliotek). Därför går det att integrera AEM som en molntjänst med Launch och Adobe Analytics hand i hand.

* [Ansluta till Adobe Analytics och skapa ramverk](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/adobeanalytics-connect.html) - Observera att&quot;Analysramverk&quot; är äldre i AEM och att det inte går att skapa dem i AEM som en molntjänst eftersom det kräver det klassiska användargränssnittet. Launch från Adobe bör användas i stället, både för variabelmappning och för distribution av JS-bibliotek till sidor.
* [Integrera Launch från Adobe](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/integrations/adobe-launch-integration-tutorial-understand.html)
* [Integrera AEM med Adobe Launch via Adobe I/O](https://helpx.adobe.com/experience-manager/using/aem_launch_adobeio_integration.html)
* [Om AEM-integrering med Launch från Adobe, Analytics och Target](https://helpx.adobe.com/experience-manager/kt/integration/using/aem-launch-integration-tutorial-understand.html)
* [Konfigurera länkspårning för Adobe Analytics](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/adobeanalytics-link.html)
* [Mappa komponentdata med Adobe Analytics-egenskaper](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/adobeanalytics-mapping.html)
* [Konfigurera videospårning för Adobe Analytics](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/adobeanalytics-video.html)
* [Adobe-klassificeringar](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/adobeanalytics-classifications.html)

>[!CAUTION]
>
>Adobe Experience Manager som molntjänstkunder som inte har något befintligt Analytics-konto kan begära åtkomst till Analytics Foundation Pack för Experience Cloud.  Detta Foundation Pack ger volymbegränsad användning av Analytics.

>[!NOTE]
>
>IMS-konfigurationen (tekniska konton) för Launch från Adobe är förkonfigurerad i AEM som en molntjänst. Användare behöver inte skapa den här konfigurationen.

## Ytterligare information {#further-information}

Se:

* [Utöka Adobe Analytics-integreringen](https://docs.adobe.com/content/help/en/experience-manager-65/developing/extending-aem/extending-analytics/extending-analytics.html) för information om hur du utvecklar komponenter som samlar in användardata och anpassar Adobe Analytics-ramverket. Observera att&quot;Analysramverk&quot; är äldre i AEM och att det inte går att skapa dem i AEM som en molntjänst eftersom det kräver det klassiska användargränssnittet. Launch från Adobe bör användas i stället, både för variabelmappning och för distribution av JS-bibliotek till sidor.
* Kunskapsbasartikeln, [Adobe Analytics-integrering - felsökningsproblem](https://helpx.adobe.com/experience-manager/kb/sitecatalystintegrationtroubleshooting.html), innehåller information om hur du felsöker Adobe Analytics-integreringen.

>[!NOTE]
>
>Om du använder Adobe Analytics med en anpassad proxykonfiguration måste du [konfigurera två OSGi-paket](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/configuring/configuring-osgi.html) (till exempel med webbkonsolen) som krävs för proxykonfigurationerna i **Apaches HTTP-klient**. Båda är obligatoriska eftersom vissa funktioner i AEM använder 3.x-API:erna, medan andra använder 4.x-API:erna. Konfigurera:
>
>* **Day Commons HTTP Client 3.1** för att konfigurera 3.x API;
   >  till exempel [https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
   >
   >
* **Proxykonfiguration** för Apache HTTP Components för att konfigurera 4.x API;
   >  till exempel [https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>


