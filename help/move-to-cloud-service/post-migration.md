---
title: Efter migreringsfas
description: Efter migreringsfas
translation-type: tm+mt
source-git-commit: 3478827949356c4a4f5133b54c6cf809f416efef
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 1%

---


# Efter migrering {#post-migration}

Under fasen efter migrering bör du se till att tillfälliga filer rensas, granska bästa praxis för kontinuerlig utveckling och hantera loggar.

Följande verktyg är tillgängliga för att felsöka AEM som en molntjänstmiljö:

* **Developer Console**
* **CRXDE Lite**
* **Hantera loggar**


## Developer Console {#developer-console}

Felsökning av AEM som molntjänstutvecklingsmiljöer finns på Developer Console för utvecklings-, scen- och produktionsmiljöer.

Mer information om utvecklingsverktyg finns i [Implementera för AEM som en molntjänst](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/development-guidelines.html#aem-as-a-cloud-service-development-tools) .

## CRXDE Lite {#crxde-lite}

Som användare har du åtkomst till **CRXDE Lite** i utvecklingsmiljön, men inte till scenen eller produktionen.

>[VIKTIGT]
>Skrivning till oföränderliga databaser som `/libs` och `/apps` under körning ger upphov till fel. Som kund har du dessutom inte tillgång till utvecklarverktyg för staging- och produktionsmiljöer.

Läs mer i [Utveckla med CRXDE Lite](https://docs.adobe.com/help/en/experience-manager-65/developing/devtools/developing-with-crxde-lite.html) om du vill veta hur du utvecklar ditt AEM-program med CRXDE Lite.

## Hantera loggar {#managing-logs}

Användarna kan komma åt en lista över tillgängliga loggfiler för den valda miljön.

Läs [Åtkomst till och hantering av loggar](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html) för att lära dig hur du får åtkomst till och hanterar loggar via användargränssnittet eller från API via Cloud Manager.

### Ytterligare support {#additional-support}

Om du har frågor om åtkomst till molntjänsten kontaktar du Adobe eller Adobe AEM CQ Support Portal.
