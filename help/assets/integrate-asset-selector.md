---
title: Integrera resursväljare med Vanilla JS
description: Integrera resursväljare med olika program från Adobe, andra företag än Adobe och tredje part.
role: Admin, User
exl-id: 1c0051a3-549c-4783-9fc1-594f424a70c3
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---

# Integrera resursväljare med Vanilla JS {#integration-using-vanilla-js}

Du kan integrera alla [!DNL Adobe]- eller icke-Adobe-program med [!DNL Experience Manager Assets]-databaser och välja resurser inifrån programmet. Se [Integrering av resursväljare med olika program](#asset-selector-integration-with-apps).

Integreringen görs genom att du importerar resursväljarpaketet och ansluter till Assets as a Cloud Service med Vanilla JavaScript-biblioteket. Redigera en `index.html` eller en lämplig fil i programmet till:

* Definiera autentiseringsinformationen
* Öppna Assets as a Cloud Service-arkivet
* Konfigurera visningsegenskaperna för resursväljaren

Du kan utföra autentisering utan att definiera några IMS-egenskaper om:

* Du integrerar ett [!DNL Adobe]-program i [Enhetligt gränssnitt](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/aem-cloud-service-on-unified-shell.html?lang=sv-SE).
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
>* [Integrera resursväljare med dynamiska media med OpenAPI-funktioner](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)
