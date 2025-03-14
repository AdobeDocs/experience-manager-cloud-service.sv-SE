---
title: Integrera AEM Assets med program längre fram i kedjan
description: Integrera AEM Assets med program längre fram i kedjan
role: User
exl-id: abd48b5d-2b43-453c-8eb6-31ff509245ca
source-git-commit: ed7331647ea2227e6047e42e21444b743ee5ce6d
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---

# Integrera AEM Assets med program längre fram i kedjan {#integrate-dynamic-media-open-apis}

| [Sök efter bästa praxis](/help/assets/search-best-practices.md) | [Metadata - bästa praxis](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [Dynamic Media med OpenAPI-funktioner](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets-dokumentation för utvecklare](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

>[!AVAILABILITY]
>
>Dynamic Media med funktionsguiden OpenAPI finns nu i PDF-format. Ladda ned hela guiden och använd Adobe Acrobat AI Assistant för att besvara dina frågor.
>
>[!BADGE Dynamic Media med OpenAPI-funktionshandboken PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/dynamic-media-with-openapi-capabilities.pdf"}

Alla [godkända resurser](/help/assets/approve-assets.md) som är tillgängliga i resurskatalogen för Experience Manager är tillgängliga för leverans till program längre fram i kedjan.

Du kan antingen integrera ditt eget anpassade användargränssnitt med Experience Manager Assets-databasen med hjälp av API:erna för sökning och leverans eller använda Adobe Micro-Frontend Resursväljare.

![Integrering med AEM Assets-databasen](assets/asset-selector-integration.png)

Med API:erna kan du söka efter godkända resurser från AEM Assets-databasen och sedan leverera resurserna till efterföljande program med en leverans-URL. Mer information finns i [API:er för sökning](/help/assets/search-assets-api.md) och [leverans](/help/assets/deliver-assets-apis.md).

Adobe Micro-Frontend Asset Selector har ett användargränssnitt som enkelt kan integreras med databasen [!DNL Experience Manager Assets as a Cloud Service] så att du kan bläddra bland eller söka efter godkända digitala resurser som är tillgängliga i databasen och använda dem i programutvecklingen. Mer information finns i [Micro-Frontend Asset Selector](/help/assets/overview-asset-selector.md).

>[!MORELIKETHIS]
>
* [Integrera resursväljare med olika program](/help/assets/integrate-asset-selector.md)
* [Egenskaper för resursväljare](/help/assets/asset-selector-properties.md)
* [Anpassning av resursväljare](/help/assets/asset-selector-customization.md)
