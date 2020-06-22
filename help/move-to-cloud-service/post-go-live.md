---
title: Efter publicering-fas
description: Efter publicering-fas
translation-type: tm+mt
source-git-commit: 0565d053b6040bc99ae79823711d56eb9aecdfb3
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 82%

---


# Efter publicering {#post-go-live}

I fasen efter publicering bör du se till att tillfälliga filer rensas, granska bästa praxis för kontinuerlig utveckling och hantera loggar. 

Följande verktyg är tillgängliga för att felsöka AEM as a Cloud Service-miljö:

* **Developer Console**
* **CRX/DE Lite**
* **Hantera loggar**


## Developer Console {#developer-console}

Felsökning av utvecklingsmiljön hos AEM as a Cloud Service finns i Developer Console för utvecklings-, mellanlagrings- och produktionsmiljöer.

Mer information om utvecklingsverktyg finns i [Implementera för AEM as a Cloud Service](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/development-guidelines.html#aem-as-a-cloud-service-development-tools).

## CRX/DE Lite {#crxde-lite}

Som användare har du åtkomst till CRX/DE Lite i utvecklingsmiljön, men inte till scenen eller produktionen.

>[VIKTIGT]
>Skrivning till oföränderliga databaser som `/libs` och `/apps` under körning ger upphov till fel. Som kund har du dessutom inte tillgång till utvecklarverktyg för mellanlagrings- och produktionsmiljöer.

Refer to [Developing with CRX/DE Lite](https://docs.adobe.com/help/en/experience-manager-65/developing/devtools/developing-with-crxde-lite.html) to learn how to develop your AEM application using CRX/DE Lite.

## Hantera loggar {#managing-logs}

Användarna kan öppna en lista över tillgängliga loggfiler för den valda miljön.

Läs [Komma åt och hantera loggar](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html) för att lära dig hur du får åtkomst till och hanterar loggar via användargränssnittet eller från API via Cloud Manager.

### Ytterligare support {#additional-support}

Om du har frågor om åtkomst till Cloud Service kontaktar du Adobe eller Adobe AEM CQ Support Portal.
