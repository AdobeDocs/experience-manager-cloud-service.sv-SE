---
title: Introduktion till AEM Screens as a Cloud Service
description: Förstå AEM Screens as a Cloud Service.
exl-id: b1cc0a63-ecd3-4d89-ac49-f384cc610cdc
feature: Screens Deployments
role: Admin, Developer, User
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 2%

---


# Introduktion till AEM Screens as a Cloud Service {#introduction-screens-cloud}

Med Adobe Experience Manager (AEM) Screens as a Cloud Service kan du skapa engagerande och dynamiska digitala signeringsupplevelser som ska användas på offentliga platser. Det är nästa utveckling av AEM Screens-produkten och utgör ett stort steg framåt när det gäller användbarhet och skalbarhet.

AEM Screens as a Cloud Service är en digital signeringslösning som gör det möjligt för marknadsförare att skapa och hantera dynamiska digitala upplevelser i stor skala. Dessutom ingår olika typer av fysiska skärmar som en del av en omfattande strategi för digital marknadsföring. Det omfattar även Adobe kanalerbjudande utöver de vanliga webb- och mobilkanalerna och även digitala signeringskanaler som finns överallt hos oss. AEM Screens as a Cloud Service möjliggör mer relevanta, kontextuella, produktiva och förutsebara användarupplevelser genom en djupgående förståelse för hur innehåll skapas, hur innehåll monteras, händelsehantering utlöses och hur media spelas upp för alla konsumenter och besökare i alla offentliga miljöer.

## Komponenter på skärmar as a Cloud Service {#understanding-components}

As a Cloud Service raster har två huvudkomponenter:

* **[Innehållsleverantör](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/screens-as-cloud-service/configure-screens-cloud/using-screens-content-provider.html)**, vilket är tillägget Skärmar som körs på AEM Cloud Service eller på Adobe Managed Services (AMS). Med Screens Content Provider kan innehållsförfattaren skapa och hantera kanaler. Innehållsförfattarna kan lägga till nytt innehåll, redigera innehållet utan att behöva bekymra sig om hur de skapar displayer eller registrering. Innehållsleverantören tillhandahåller en sammanfattning av de underliggande detaljerna för utveckling av innehåll, skärmar eller spelarregistrering.

* **[Tjänsteleverantör](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/screens-as-cloud-service/configure-screens-cloud/navigating-to-screens-services-provider.html)**, som är den digitala signeringshanteringstjänsten som körs på Adobe I/O Runtime. Med Screens Services Provider kan skribenter, utvecklare och administratörer hantera skärmar och spelare för uppspelning av innehåll när innehållet har lagts till i kanalerna. Screens Services Provider informerar även koordinatorn om var och när innehållet ska spelas upp på en hög nivå.


## Arkitektöversikt {#architectural-overview}

Som as a Cloud Service AEM Screens-användare kan du lägga till och hantera innehåll i kanaler. Du kan registrera och hantera skärmar och spelare från gränssnitt som är särskilt utformade för skärmar as a Cloud Service, nämligen **Tjänsteleverantör för skärmar** och **Innehållsleverantör för skärmar**.

![bild](/help/screens-cloud/assets/architecture-screenscloud.png)
