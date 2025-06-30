---
title: Integrera [!DNL AEM Assets] när du redigerar innehåll för [!DNL Edge Delivery Services]
description: Lär dig hur du integrerar  [!DNL AEM Assets] med [!DNL Edge Delivery Services]. This integration enables you to integrate [!DNL AEM Assets] med [!DNL Microsoft Word] och [!DNL Google Docs], integrate [!DNL AEM Assets] med [!DNL Universal Editor], integrate [!DNL Dynamic Media] med [!DNL Edge Delivery Services], integrate [!DNL Dynamic Media with OpenAPI capabilities] med [!DNL Universal Editor] och integrerar [!DNL Dynamic Media with OpenAPI capabilities] med [!DNL Microsoft Word] och [!DNL Google Docs].
tags: AEM Assets, Edge Delivery Services, Dynamic Media, Dynamic Media with OpenAPI capabilities, Universal Editor, Edge Delivery Services with Universal Editor
exl-id: e58db2ce-a55a-49b3-ae8e-709b5ea8d095
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 0%

---


# Integrera [!DNL AEM Assets] när du redigerar innehåll för [!DNL Edge Delivery Services] {#integrate-aem-assets-with-edge-delivery-services}

![Integrering av AEM-resurser med Universal Editor](/help/assets/assets/EDS2.png)

[[!DNL Edge Delivery Services]](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/edge-delivery/overview) är en sammansättningsbar uppsättning tjänster som ger stor flexibilitet i hur du skapar och levererar innehåll på din webbplats. Du kan använda både [AEM innehållshantering](/help/sites-cloud/authoring/author-publish.md) och [WYSIWYG med  [!DNL Universal Editor]  samt dokumentbaserad redigering](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/authoring).

Du kan redigera innehåll i:

* [[!DNL Microsoft Word] eller [!DNL Google Docs]](#integrate-dynamic-media-with-edge-delivery-services)
* [[!DNL Universal Editor]](#integrate-aem-assets-with-universal-editor-UE)

När du har redigerat innehållet kan du publicera det på Edge Delivery Services.

## Integrerar [!DNL AEM Assets] med dokumentbaserade redigeringsflöden för [!DNL Edge Delivery Services] {#integrate-dynamic-media-with-edge-delivery-services}

När [!DNL AEM Assets] integreras med dina dokumentbaserade redigeringsverktyg, som [!DNL Microsoft Word] eller [!DNL Google Docs], innehåller det en resursväljare i utvecklingsverktyget. Använd den här resursväljaren för att komma åt [!DNL AEM Assets] och infoga godkända resurser i ditt innehåll.
Om du redan har en [!DNL Edge Delivery Services]-webbplats kan du läsa [[!DNL AEM Assets] plugin](https://github.com/adobe-rnd/aem-assets-plugin/blob/main/README.md)-dokumentationen och lära dig hur du integrerar [!DNL AEM Assets] med ditt befintliga [!DNL AEM]-projekt.
Följ följande avsnitt i [Förutsättningar](#integrate-aem-assets-with-microsoft-word-and-google-docs) och [Integrera [!DNL AEM Assets]  med dokumentbaserad redigeringsmiljö](#integrate-aem-assets-with-microsoft-word-or-google-docs-to-use-aem-assets-with-microsoft-word-or-google-docs) om du inte har någon [!DNL Edge Delivery Services]-webbplats för att publicera [!DNL AEM Assets] inkluderande innehåll som har skapats i dokumentbaserade redigeringsverktyg.

### Förutsättningar{#integrate-aem-assets-with-microsoft-word-and-google-docs}

Innan du börjar ser du till att den dokumentbaserade redigeringsmiljön är klar:

* Integrera [!DNL AEM] med ett dokumentbaserat redigeringsverktyg för att konfigurera redigeringsmiljön. Se [Komma igång - självstudiekurs för utvecklare](https://www.aem.live/developer/tutorial) om du vill veta mer om hur du konfigurerar redigeringsmiljön.

### Integrerar [!DNL AEM Assets] med dokumentbaserad redigeringsmiljö{#integrate-aem-assets-with-microsoft-word-or-google-docs-to-use-aem-assets-with-microsoft-word-or-google-docs}

Konfigurera Sidekick-plugin-programmet [!DNL AEM Assets] så att det använder resurser när du redigerar innehåll i [!DNL Microsoft Word] eller [!DNL Google Docs].

* Läs [[!DNL Adobe Experience Manager Assets Sidekick Plugin]](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-experience-manager-assets-for-website-authors) om du vill veta mer om hur du kommer åt och använder AEM Assets i Microsoft Word eller Google Docs.
* Mer konfigurationsinformation finns i [Konfigurera [!DNL Adobe Experience Manager Assets Sidekick Plugin]](https://www.aem.live/developer/configuring-aem-assets-sidekick-plugin).
  ![använd dynamiska media med openAPI-funktioner i MS Word- och Google-dokument](/help/assets/assets/my-assets-sidebar.png)

## Leverera resurser med [!DNL Dynamic Media with OpenAPI capabilities] {#integrate-Dynamic-Media-with-OpenAPI-capabilities-with-Microsoft-Word-Google-Docs-and-universal-editor}

Du kan också använda resurser som levereras med [!DNL Dynamic Media with OpenAPI capabilities]. Det ger många fördelar:

* Åtkomst till endast varumärkesgodkända resurser (bilder, videor, PDF-filer och andra resurstyper) från [!DNL AEM Assets Cloud Services].
* Styrning (referenser jämfört med kopior av resursen), som hjälper till med automatisk spridning av livscykelhändelser för resurser, som förfallodatum, borttagning och uppdateringar.
* Dynamiska bildåtergivningar och smart beskärning.
* Optimering och leverans av multimedia, som adaptiv direktuppspelad video, och ursprunglig materialleverans för PDF-filer.
* Resultatnivårapport ([begränsad tillgänglighet](/help/assets/manage-reports-assets-view.md#dynamic-media-delivery-reports)).

Mer information om funktionerna finns i dokumentationen för [[!DNL Dynamic Media with OpenAPI capabilities]](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/dynamic-media-open-apis-overview).

### Förutsättningar {#dynamic-media-with-universal-editor-and-edge-delivery-services}

Om du vill använda resursreferens måste du ha:

* Tillstånd till en Assets Cloud Service-miljö där [!DNL Dynamic Media with Open API capabilities] är aktiverat.
* En [!DNL Dynamic Media]-licens.
* [!DNL AEM Assets sidekick plugin] har aktiverats med kopieringsreferens för bildresurser aktiverat. Mer information finns i [den här dokumentationen](https://www.aem.live/developer/configuring-aem-assets-sidekick-plugin#copymode) för dokumentbaserad redigering och i [den här dokumentationen](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#extension-overview) för Universell redigeringsbaserad redigering.
* Assets som godkänts. Godkända resurser har `dam:status=Approved` via Assets Cloud Services-backend eller gränssnittsåtgärder.

### Använd resurser som levereras med [!DNL Dynamic Media with OpenAPI capabilities]{#Using-Dynamic-Media-with-edge-delivery-services}

Välj följande länkar om du vill lära dig hur du använder [!DNL Dynamic Media with OpenAPI capabilities] för att leverera bilder, videoklipp och andra resurstyper i ditt innehåll:

* [Lägg till bilder i ditt innehåll](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-image-references-when-authoring-content)
* [Lägg till videofilmer i ditt innehåll](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-video-references-when-authoring-content)
* [Lägg till icke-bild- och videomaterial som PDF, Zip-filer med mera i ditt innehåll](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-asset-references-for-pdf-zip-etc-when-authoring-content)

I den här videon får du lära dig hur du levererar resurser i ditt innehåll med hjälp av Dynamic Media med OpenAPI-funktioner.

>[!VIDEO](https://video.tv.adobe.com/v/3441155)

## Exempel på [!DNL Edge Delivery Services]-plats{#dynamic-media-with-google-docs-and-ms-word}

Se [WKND Travel](https://aem-dynamicmedia-demo--dm--hlxsites.aem.live/travel-hospitality/wknd-trvl-home), en webbplats som har skapats med dokumentbaserade redigeringsfunktioner i [!DNL Edge Delivery Services]. Webbplatsens innehåll skapas i [Google Docs](https://drive.google.com/drive/folders/1HCCHRWp4HJIXW_cUv5cRDQ5DzzqiZsXT) och [!DNL Dynamic Media with OpenAPI capabilities] används för att leverera resurser i innehållet. Efter redigeringen publiceras innehållet direkt från dokumentet. Utforska denna [Git-databas](https://github.com/hlxsites/franklin-assets-selector/tree/aem-dynamicmedia-demo/blocks) för att få information om alla viktiga filer, mappar, konfigurationer, webbplatsens format och funktionskoder som används för att skapa den dokumentbaserade redigeringsinställningen för den här [!DNL Edge Delivery Services (EDS)] -platsen.

## Integrerar [!DNL AEM Assets] med [!DNL Universal Editor]-baserade redigeringsflöden för [!DNL Edge Delivery Services] {#integrate-aem-assets-with-universal-editor-UE}

Konfigurera [!DNL Universal Editor] för integrering med [!DNL AEM Assets]. Med den här integreringen kan du använda [!DNL Dynamic Media with OpenAPI capabilities] för att leverera resurser.

* Mer information om hur du lägger till en anpassad resursväljarfunktion i [!DNL Universal Editor] finns i [Konfiguration i [!DNL Edge Delivery] Plats](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#configuration-in-edge-delivery-site). Med den anpassade resursväljaren kan du infoga resurser direkt i ditt [!DNL Universal Editor]-innehåll.
* Se [Tilläggsöversikt](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#extension-overview) om du vill veta hur du får åtkomst till [!DNL AEM Assets] och infogar resurserna när du redigerar i [!DNL Universal Editor].
