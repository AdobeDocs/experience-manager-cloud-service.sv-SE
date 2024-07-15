---
title: Integrera AEM Assets med program längre fram i kedjan
description: Integrera AEM Assets med program längre fram i kedjan
role: User
source-git-commit: 540aa876ba7ea54b7ef4324634f6c5e220ad19d3
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# Integrera AEM Assets med program längre fram i kedjan {#integrate-dynamic-media-open-apis}

Alla [godkända resurser](approve-assets.md) som är tillgängliga i resurskatalogen för Experience Manager är tillgängliga för leverans till program längre fram i kedjan.

Du kan antingen integrera ditt eget anpassade användargränssnitt med Experience Manager Assets-databasen med hjälp av API:erna för sökning och leverans eller använda Adobe Micro-Frontend Resursväljare.

![Integrering med AEM Assets-databasen](assets/asset-selector-integration.png)

Med API:erna kan du söka efter godkända resurser från AEM Assets-databasen och sedan leverera resurserna till efterföljande program med en leverans-URL. Mer information finns i [API:er för sökning](/help/assets/search-assets-api.md) och [leverans](/help/assets/deliver-assets-apis.md).

Adobe Micro-Frontend Asset Selector har ett användargränssnitt som enkelt kan integreras med databasen [!DNL Experience Manager Assets as a Cloud Service] så att du kan bläddra bland eller söka efter godkända digitala resurser som är tillgängliga i databasen och använda dem i programutvecklingen. Mer information finns i [Micro-Frontend Asset Selector](/help/assets/asset-selector.md).

