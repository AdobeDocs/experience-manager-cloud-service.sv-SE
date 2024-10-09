---
title: Resursväljare för  [!DNL Adobe Experience Manager]  som en [!DNL Cloud Service]
description: Integrera resursväljare med olika program från Adobe, andra än Adobe och andra tillverkare.
role: Admin, User
exl-id: 1c0051a3-549c-4783-9fc1-594f424a70c3
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# Integrera resursväljare med Vanilla JS {#integration-using-vanilla-js}

| [Sök efter bästa praxis](/help/assets/search-best-practices.md) | [Metadata - bästa praxis](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [Dynamic Media med OpenAPI-funktioner](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets-dokumentation för utvecklare](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

Du kan integrera alla [!DNL Adobe]- och andra program än Adobe med [!DNL Experience Manager Assets]-databasen och välja resurser inifrån programmet. Se [Integrering av resursväljare med olika program](#asset-selector-integration-with-apps).

Integreringen görs genom att du importerar resursväljarpaketet och ansluter till Assets as a Cloud Service med hjälp av Vanilla JavaScript-biblioteket. Redigera en `index.html` eller en lämplig fil i programmet till:

* Definiera autentiseringsinformationen
* Åtkomst till Assets as a Cloud Service-databasen
* Konfigurera visningsegenskaperna för resursväljaren

Du kan utföra autentisering utan att definiera några IMS-egenskaper om:

* Du integrerar ett [!DNL Adobe]-program i [Enhetligt gränssnitt](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/aem-cloud-service-on-unified-shell.html?lang=en).
* Du har redan en IMS-token genererad för autentisering.

## Integrera resursväljaren med olika program {#asset-selector-integration-with-apps}

Du kan integrera resursväljaren med olika program som:

* [Integrera resursväljare med ett  [!DNL Adobe] program](/help/assets/integrate-asset-selector-adobe-app.md)
* [Integrera resursväljare med andra program än Adobe](/help/assets/integrate-asset-selector-non-adobe-app.md)
* [Integrering av Dynamic Media med OpenAPI-funktioner](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)


>[!MORELIKETHIS]
>
>* [Anpassningar av resursväljare](/help/assets/asset-selector-customization.md)
>* [Egenskaper för resursväljare](/help/assets/asset-selector-properties.md)
>* [Integrera resursväljare med Dynamic Media med OpenAPI-funktioner](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)
