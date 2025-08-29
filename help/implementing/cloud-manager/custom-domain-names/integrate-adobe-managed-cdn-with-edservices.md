---
title: Integrera Edge Delivery Services med Adobe Managed CDN i Cloud Manager
description: null
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
source-git-commit: 71ea3b810d4145d5581c29e26db9bc157c425a15
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---


# Integrera Edge Delivery Services med Adobe Managed CDN i Cloud Manager {#integrate-adbe-cdn-with-edservices-in-cm}

Adobe Managed CDN (AMC-D) kan integreras med Edge Delivery Services för att ge dig prestandabaserade, globalt distribuerade upplevelser för Adobe Experience Manager (AEM) Sites.

Tillsammans ger de dig följande fördelar:

* En nyckelfärdig CDN i enterpriseklass som hanteras av Adobe.
* Ett modernt lager för kantleverans som snabbar upp förfrågningar, optimerar cachelagring och skyddar mot vanliga attacker.
* Ett enhetligt Cloud Manager-arbetsflöde för domänhantering, SSL-certifikat och pipeline-drivna distributioner.

<!--
Adobe's Edge Delivery Services (EDS) can take advantage of an Adobe managed CDN. EDS is a framework that optimizes website delivery for speed, simplicity, and scalability by pushing content closer to the user through edge nodes. It is not a replacement for a CDN, but rather a way to enhance content delivery, especially when you use the Adobe managed CDN. It offers you the following benefits:

* Adobe-Managed CDN: EDS can use an Adobe-managed CDN, offering features like self-service CDN management and automatic certificate renewal. 
* EDS and AEM: EDS is a feature of AEM as a Cloud Service and works alongside the AEM authoring environment. 
* Performance enhancement: EDS, in conjunction with an Adobe Managed CDN, improves website performance by caching content at edge locations closer to users, reducing latency. 
* Flexibility: EDS provides flexibility in content delivery, allowing your organization to choose between the Adobe-managed CDN or their own CDN setup, based on their needs and existing infrastructure. 
Self-Service CDN Management:
Adobe-managed CDN within EDS enables self-service configuration and management tasks like SSL certificate setup. 
 
Use Cases:
EDS with CDN integration is beneficial for various scenarios, including e-commerce storefronts and websites requiring high performance and scalability. -->

## Edge Delivery Services driftsättningsalternativ i Adobe Managed CDN i Cloud Manager {#deployment-options}

I det här avsnittet förklaras de två sätt som du kan distribuera Edge Delivery Services på Adobe Managed CDN i Cloud Manager och, precis som viktigt, hjälper dig att avgöra vilket alternativ som passar bäst för ditt användningssätt.

Edge Delivery Services kan konfigureras med något av följande två alternativ. Var och en har olika funktioner.

|  | Distributionsalternativ | Nyckeldokument | Funktion | Bäst för |
| --- | --- | --- | --- | --- |
| Alternativ 1 | *Med* en befintlig AEM as a Cloud Service-miljö (AEMaaCS) | [Konfigurera en proxy från en befintlig miljö](https://www.aem.live/docs/byo-cdn-adobe-managed#option-1-setup-a-proxy-from-an-existing-environment) | Config Pipeline är vanligtvis tillgänglig för AEMaaCS-miljöer | Team som redan kör Sites i Cloud Manager och vill ha en snabb prestandaökning med låg risk. |
| Alternativ 2 | *Utan* en befintlig AEMaaCS-miljö, som kallas fristående&quot;Edge-miljö&quot;. | [Konfigurera en Edge Delivery-webbplats utan en befintlig miljö](https://www.aem.live/docs/byo-cdn-adobe-managed#option-2-setup-an-edge-delivery-site-without-an-existing-environment) | Config Pipeline finns för närvarande bara för Edge-miljöer genom det begränsade Beta-programmet.<br>Se [Lägg till Edge Delivery Config Pipeline](help/implementing/cloud-manager/release-notes/current.md##add-eds-pipeline). | Nya byggen eller migreringar som vill ta till sig hela Edge Delivery-arkitekturen och detaljstyrd routning. |

<!-- Ultimately this URL above will need to be updated on GA -->

| Alternativ | Sammanfattning | Bäst för | Viktiga dokument |
| --- | --- | --- | --- |
| Adobe hanterad CDN-proxy | Adobe Managed CDN står framför en befintlig AEM Sites-miljö. Aktuell Sites-pipeline förblir&quot;original&quot; medan AMC-D hanterar edge-cachning och TLS-avslutning. | Team som redan kör Sites i Cloud Manager och vill ha en snabb prestandaökning med låg risk. | Konfigurera en AMC-D-proxy |
| Konfigurera pipeline med originSelectors | En dedikerad Edge Delivery Config Pipeline publicerar statiskt och dynamiskt innehåll direkt på kanten. `originSelectors` dirigerar trafik mellan AMC-D och AEM författare/publiceringsnivåer. | Nya byggen eller migreringar som vill ta till sig hela Edge Delivery-arkitekturen och detaljstyrd routning. | Konfigurera Edge Delivery pipeline |

>[!TIP]
>
>Är du osäker på vilken väg du ska välja? Se [Välj en distributionsmodell](#choose-deployment-model) nedan för riktlinjer för beslut.

## Välj en distributionsmodell {#choose-deployment-model}

Båda modellerna kan samexistera inom samma Cloud Manager-program, vilket möjliggör stegvis migrering.

| Om du.. | Använd sedan ... |
| :--- | :--- |
| Behöver en snabb och minimal driftsättning och redan är värd för webbplatser i Cloud Manager | AMC-D-proxy |
| Planera att strukturera om innehåll för Edge Delivery, eller att finjustera routningen mellan olika ursprung | Konfigurera Edge-leverans av pipeline + `originSelectors` |

## Förutsättningar {#prerequisites}

1. Anlita din webbplats i Cloud Manager - krävs för båda distributionsmodellerna. Följ en AEM webbplats.

2. Hämta din egen Git (BYOG) (tillval) - Om du lagrar webbplatskod utanför Adobe Git, slutför du BYOG-introduktionen.

3. Edge Delivery-licens - Kontrollera att ditt program är licensierat för Edge Delivery Services.


