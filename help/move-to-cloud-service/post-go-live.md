---
title: Efter publicering-fas
description: Efter publicering-fas
translation-type: tm+mt
source-git-commit: 96aa0ef43613e6ae72bf4c454be46329abb19a0c
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Efter publicering {#post-go-live}

I fasen efter publicering bör du se till att tillfälliga filer rensas, granska bästa praxis för kontinuerlig utveckling och hantera loggar. 

Följande verktyg är tillgängliga för att felsöka AEM as a Cloud Service-miljöer:

* **Developer Console**
* **CRX/DE Lite**
* **Hantera loggar**


## Developer Console {#developer-console}

Felsökning av utvecklingsmiljön hos AEM as a Cloud Service finns i Developer Console för utvecklings-, mellanlagrings- och produktionsmiljöer.

Mer information om utvecklingsverktyg finns i [Implementera för AEM as a Cloud Service](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/development-guidelines.html#aem-as-a-cloud-service-development-tools).

## CRX/DE Lite {#crxde-lite}

Som användare har du åtkomst till CRX/DE Lite i utvecklingsmiljön, men inte i mellanlagrings- eller produktionsmiljön.

>[!IMPORTANT]
>Skrivning till oföränderliga databaser som `/libs` och `/apps` under körning ger upphov till fel. Som kund har du dessutom inte tillgång till utvecklarverktyg för mellanlagrings- och produktionsmiljöer.

Läs mer i [Utveckla med CRX/DE Lite](/help/implementing/developing/tools/crxde.md) om du vill veta hur du utvecklar AEM-programmet med CRX/DE Lite.

## Hantera loggar {#managing-logs}

Användarna kan öppna en lista över tillgängliga loggfiler för den valda miljön.

Läs [Komma åt och hantera loggar](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html) för att lära dig hur du får åtkomst till och hanterar loggar via användargränssnittet eller från API via Cloud Manager.

### Ytterligare support {#additional-support}

Om du har frågor om åtkomst till Cloud Service kontaktar du Adobe eller Adobe AEM CQ Support Portal.
