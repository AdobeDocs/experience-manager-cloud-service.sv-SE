---
title: Integrera AEM Assets när du skapar material för Edge Delivery Services
description: Lär dig hur du integrerar AEM Assets med Edge Delivery Services. Integreringen gör att du kan integrera AEM Assets med Microsoft Word och Google Docs, integrera AEM Assets med Universal Editor, integrera Dynamic Media med OpenAPI-funktioner med Universal Editor och integrera Dynamic Media med OpenAPI-funktioner med Microsoft Word och Google Docs.
exl-id: e58db2ce-a55a-49b3-ae8e-709b5ea8d095
source-git-commit: 105081c9124a85581240b19866adc271ea8bb190
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 0%

---

# Integrera AEM Assets när du skapar material för Edge Delivery Services {#integrate-aem-assets-while-authoring-for-edge-delivery-services}

![EDS2](/help/assets/assets/EDS2.png)

[Edge Delivery Services](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/overview) är en sammansättningsbar uppsättning tjänster som ger stor flexibilitet när det gäller att skapa och leverera innehåll på din webbplats. Du kan använda både [AEM innehållshantering](/help/sites-cloud/authoring/author-publish.md) och [WYSIWYG-redigering med den universella redigeraren samt dokumentbaserad redigering](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/authoring).

Du kan redigera innehåll i:

* [Microsoft Word eller Google Docs](#integrate-aem-assets-with-document-based-authoring-tools)
* [Universal Editor](#integrate-aem-assets-with-universal-editor)

När du har redigerat innehållet kan du publicera det på Edge Delivery Services.

## Integrera AEM Assets med dokumentbaserade redigeringsflöden för Edge Delivery Services {#integrate-aem-assets-with-document-based-authoring-tools}

AEM Assets integration med dokumentbaserade redigeringsverktyg som Microsoft Word och Google Docs ger dig en resursväljare direkt i redigeraren. Använd den här resursväljaren för att komma åt AEM Assets och infoga godkända resurser i dokumentet.

Om du redan har en Edge Delivery Services-webbplats kan du läsa [AEM Assets plugin](https://github.com/adobe-rnd/aem-assets-plugin/blob/main/README.md) för att integrera AEM Assets med ditt befintliga AEM. Om du inte har någon Edge Delivery Services-webbplats kan du läsa avsnitten [Förutsättningar](#integrate-aem-assets-with-microsoft-word-and-google-docs) och [Integrera AEM Assets med dokumentbaserad redigeringsmiljö](#integrate-aem-assets-with-microsoft-word-or-google-docs-to-use-aem-assets-with-microsoft-word-or-google-docs) nedan.

### Förutsättningar{#integrate-aem-assets-with-microsoft-word-and-google-docs}

Innan du börjar ser du till att den dokumentbaserade redigeringsmiljön är klar:

* Integrera AEM med ett dokumentbaserat redigeringsverktyg för att konfigurera redigeringsmiljön. Se [Komma igång - självstudiekurs för utvecklare](https://www.aem.live/developer/tutorial) för att konfigurera redigeringsmiljön.

### Integrera AEM Assets med dokumentbaserad redigeringsmiljö{#integrate-aem-assets-with-microsoft-word-or-google-docs-to-use-aem-assets-with-microsoft-word-or-google-docs}

Konfigurera plugin-programmet AEM Assets Sidekick för att använda resurser när du redigerar innehåll i Microsoft Word eller Google Docs.

* Se [Adobe Experience Manager Assets Sidekick Plugin](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-experience-manager-assets-for-website-authors) om du vill veta mer om hur du kommer åt och använder AEM Assets i Microsoft Word eller Google Docs.
* Mer konfigurationsinformation finns i [Konfigurera Adobe Experience Manager Assets Sidekick Plugin](https://www.aem.live/developer/configuring-aem-assets-sidekick-plugin).
  ![min-assets-sidebar](/help/assets/assets/my-assets-sidebar.png)

## Leverera material med hjälp av Dynamic Media med OpenAPI-funktioner {#integrate-Dynamic-Media-with-OpenAPI-capabilities-with-Microsoft-Word-Google-Docs-and-universal-editor}

Du kan också använda resurser som levereras via DM med OpenAPI-funktioner. Det ger många fördelar:

* Tillgång till varumärkesgodkända mediefiler (bilder, videor, PDF och andra typer av mediefiler) från AEM Assets Cloud Service.
* Styrning (referenser jämfört med kopior av resursen), som hjälper till med automatisk spridning av livscykelhändelser för resurser, som förfallodatum, borttagning och uppdateringar.
* Dynamiska bildåtergivningar och smart beskärning.
* Optimering och leverans av multimedia, som adaptiv direktuppspelad video, och ursprunglig medieleverans för PDF.
* Resultatnivårapport ([begränsad tillgänglighet](/help/assets/manage-reports-assets-view.md#dynamic-media-delivery-reports)).

Mer information om funktionerna finns i dokumentationen för [Dynamic Media med OpenAPI-funktioner](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/dynamic-media-open-apis-overview).

### Förutsättningar {#prerequisites-for-dm-with-openapi-capabilities-to-use-aem-assets}

Om du vill använda resursreferens måste du ha:

* Tillstånd till en Assets-Cloud Service där Dynamic Media med Open API-funktioner är aktiverat.
* En Dynamic Media-licens.
* AEM Assets-pluginen för sidspark har aktiverats med kopieringsreferens för bildresurser. Mer information finns i [this](https://www.aem.live/developer/configuring-aem-assets-sidekick-plugin#copymode) för dokumentbaserad redigering och i [this](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#extension-overview) för Universal Editor-baserad redigering.
* Assets som godkänts. Godkända resurser har `dam:status=Approved` via Assets Cloud Services backend eller UI-åtgärder.

### Använd material som levereras med Dynamic Media med OpenAPI-funktioner{#how-to-use-Dynamic-Media-with-OpenAPI-assets}

Information om hur du använder material som levereras med Dynamic Media med OpenAPI-funktioner när du redigerar innehåll finns i:

* [Använda bildreferenser](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-image-references-when-authoring-content)
* [Använda videoreferenser](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-video-references-when-authoring-content)
* [Använda resursreferenser för icke-bild- och videomaterial som PDF, Zip-filer med mera](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-asset-references-for-pdf-zip-etc-when-authoring-content)

I den här videon får du lära dig hur du levererar resurser med Dynamic Media med OpenAPI-funktioner.

>[!VIDEO](https://video.tv.adobe.com/v/3441155)

## Exempelwebbplats för Edge Delivery Services{#example-of-an-Edge-Delivery-Services-site}

Se [WKND Travel](http://bit.ly/3DExLnf). Den här webbplatsen har byggts med Edge Delivery Servicens dokumentbaserade redigeringsfunktioner. Webbplatsens innehåll skapas i [Google Docs](https://drive.google.com/drive/folders/1HCCHRWp4HJIXW_cUv5cRDQ5DzzqiZsXT) med hjälp av Dynamic Media med OpenAPI-funktioner för leverans av resurser. När innehållet har skapats publiceras det direkt från dokumentet. För den här dokumentbaserade redigeringsinställningen lagras alla viktiga filer, mappar, konfigurationer, webbplatsens format och funktionskoder i den här [Git-databasen](https://github.com/hlxsites/franklin-assets-selector/tree/aem-dynamicmedia-demo/blocks).

## Integrera AEM Assets med universella redigeringsbaserade arbetsflöden för Edge Delivery Services {#integrate-aem-assets-with-universal-editor}

Konfigurera Universal Editor för integrering med AEM Assets. Tack vare den här integreringen kan du använda Dynamic Media med OpenAPI-funktioner för att leverera resurser.

* Se [Konfiguration i Edge Delivery Site](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#configuration-in-edge-delivery-site) om du vill lägga till en anpassad resursväljarfunktion i Universal Editor. Med den anpassade resursväljaren kan du infoga resurser direkt i det universella redigeringsinnehållet.
* Se [Tilläggsöversikt](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#extension-overview) om du vill lära dig hur du får åtkomst till AEM Assets och infogar resurser när du redigerar i Universell redigerare.
