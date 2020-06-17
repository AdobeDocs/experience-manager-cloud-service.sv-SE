---
title: Post GoLive Phase
description: Post GoLive Phase
translation-type: tm+mt
source-git-commit: 0565d053b6040bc99ae79823711d56eb9aecdfb3
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---


# Post GoLive {#post-go-live}

I fasen efter publicering bör du se till att tillfälliga filer rensas, granska bästa praxis för kontinuerlig utveckling och hantera loggar.

Följande verktyg är tillgängliga för att felsöka AEM som en Cloud Service-miljö:

* **Developer Console**
* **CRX/DE Lite**
* **Hantera loggar**


## Developer Console {#developer-console}

Det går att felsöka AEM som utvecklarmiljö i Developer Console för utvecklings-, scen- och produktionsmiljöer.

Se [Implementera för AEM som en Cloud Service](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/development-guidelines.html#aem-as-a-cloud-service-development-tools) för mer information om utvecklingsverktyg.

## CRX/DE Lite {#crxde-lite}

Som användare har du åtkomst till CRX/DE Lite i utvecklingsmiljön, men inte till scenen eller produktionen.

>[VIKTIGT]
>Skrivning till oföränderliga databaser som `/libs` och `/apps` under körning ger upphov till fel. Som kund har du dessutom inte tillgång till utvecklarverktyg för staging- och produktionsmiljöer.

Se [Utveckla med CRX/DE Lite](https://docs.adobe.com/help/en/experience-manager-65/developing/devtools/developing-with-crxde-lite.html) för att lära dig hur du utvecklar AEM-program med CRX/DE Lite.

## Hantera loggar {#managing-logs}

Användarna kan komma åt en lista över tillgängliga loggfiler för den valda miljön.

Läs [Åtkomst till och hantering av loggar](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html) för att lära dig hur du får åtkomst till och hanterar loggar via användargränssnittet eller från API via Cloud Manager.

### Ytterligare support {#additional-support}

Om du har frågor om hur du får tillgång till Cloud Service kontaktar du Adobe eller Adobe AEM CQ Support Portal.
