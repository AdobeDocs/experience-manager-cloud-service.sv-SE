---
title: Integrera AEM Assets med program längre fram i kedjan
description: Integrera AEM Assets med program längre fram i kedjan
role: User
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# Integrera AEM Assets med program längre fram i kedjan {#integrate-new-dynamic-media-apis}

Alla [godkända tillgångar](approved-assets.md) som finns i Experience Manager resurslager finns tillgängliga för leverans till program i senare led.

Du kan antingen integrera ditt eget anpassade användargränssnitt med Experience Manager Assets-databasen med hjälp av API:erna för sökning och leverans eller använda Adobe Micro-Frontend Resursväljare.

![Integrering med AEM Assets](assets/asset-selector-integration.png)

Med API:erna kan du söka efter godkända resurser från AEM Assets-databasen och sedan leverera resurserna till efterföljande program med en leverans-URL. Mer information finns i [Sök](/help/assets/search-assets-api.md) och [Leverans](/help/assets/deliver-assets-apis.md) API.

Adobe Micro-Frontend Asset Selector har ett användargränssnitt som enkelt kan integreras med [!DNL Experience Manager Assets as a Cloud Service] databas så att du kan bläddra bland eller söka efter godkända digitala resurser som är tillgängliga i databasen och använda dem när du redigerar program. Mer information finns i [Mikrofrontsväljare för mediefiler](/help/assets/asset-selector.md).

