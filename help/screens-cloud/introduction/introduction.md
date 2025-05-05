---
title: Introduktion till AEM Screens as a Cloud Service
description: Förstå AEM Screens as a Cloud Service.
exl-id: b1cc0a63-ecd3-4d89-ac49-f384cc610cdc
feature: Screens Deployments
role: Admin, Developer, User
source-git-commit: 53086e2ec6d9d962a8f1cb1cc40f0601da74ac63
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 1%

---


# Introduktion till AEM Screens as a Cloud Service {#introduction-screens-cloud}

Med Adobe Experience Manager (AEM) Screens as a Cloud Service kan du skapa engagerande och dynamiska digitala signeringsupplevelser som ska användas på offentliga platser. Det är nästa utveckling av AEM Screens-produkten och utgör ett stort steg framåt när det gäller användbarhet och skalbarhet.

AEM Screens as a Cloud Service är en digital signeringslösning som gör att marknadsförare kan skapa och hantera dynamiska digitala upplevelser i stor skala. Dessutom ingår olika typer av fysiska skärmar som en del av en omfattande strategi för digital marknadsföring. Det omfattar även Adobe kanalerbjudande utöver de vanliga webb- och mobilkanalerna och även digitala signeringskanaler som finns överallt hos oss. AEM Screens as a Cloud Service ger en mer relevant, kontextuell, produktiv och förutseende användarupplevelse genom en djupgående förståelse för hur innehåll skapas, hur innehåll monteras, hur händelsehantering utlöses och hur media spelas upp för alla konsumenter och besökare i alla offentliga miljöer.

## Komponenter i Screens as a Cloud Service {#understanding-components}

Screens as a Cloud Service har två huvudkomponenter:

* **[Innehållsleverantör](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/screens-as-cloud-service/configure-screens-cloud/using-screens-content-provider.html?lang=sv-SE)**, som är Screens-tillägget som körs på AEM Cloud Service eller på Adobe Managed Services (AMS). Med Screens Content Provider kan innehållsförfattaren skapa och hantera kanaler. Innehållsförfattarna kan lägga till nytt innehåll, redigera innehållet utan att behöva bekymra sig om hur de skapar displayer eller registrering. Innehållsleverantören tillhandahåller en sammanfattning av de underliggande detaljerna för utveckling av innehåll, skärmar eller spelarregistrering.

* **[Tjänsteleverantör](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/screens-as-cloud-service/configure-screens-cloud/navigating-to-screens-services-provider.html?lang=sv-SE)**, som är den digitala signeringshanteringstjänsten som körs på Adobe I/O Runtime. Med Screens Services Provider kan skribenter, utvecklare och administratörer hantera displayer och spelare för uppspelning av innehåll när innehållet har lagts till i kanalerna. Dessutom informerar Screens tjänsteleverantör koordinatorn om var och när innehåll ska spelas upp på en hög nivå.


## Arkitektöversikt {#architectural-overview}

Som AEM Screens-as a Cloud Service-användare kan du lägga till och hantera innehåll i kanaler. Du kan registrera och hantera skärmar och spelare från gränssnitt som utformats speciellt för Screens as a Cloud Service, nämligen **Screens Services Provider** och **Screens Content Provider**.

![Arkitekturöversikt](/help/screens-cloud/assets/architecture-screenscloud.png)
