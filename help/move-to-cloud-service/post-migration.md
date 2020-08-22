---
title: Efter migreringsfas
description: Efter migreringsfas
translation-type: tm+mt
source-git-commit: 5a90db8791dd92cceb811b9ed2beda3ecb4a974d
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 100%

---


# Efter migrering {#post-migration}

Under fasen efter migrering bör du se till att tillfälliga filer rensas, granska bästa praxis för kontinuerlig utveckling och hantera loggar.

Följande verktyg är tillgängliga för att felsöka AEM as a Cloud Service-miljö:

* **Developer Console**
* **CRXDE Lite**
* **Hantera loggar**


## Developer Console {#developer-console}

Felsökning av utvecklingsmiljön hos AEM as a Cloud Service finns i Developer Console för utvecklings-, mellanlagrings- och produktionsmiljöer.

Mer information om utvecklingsverktyg finns i [Implementera för AEM as a Cloud Service](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/development-guidelines.html#aem-as-a-cloud-service-development-tools).

## CRXDE Lite {#crxde-lite}

Som användare har du åtkomst till **CRXDE Lite** i utvecklingsmiljön, men inte i mellanlagring eller produktion.

>[!IMPORTANT]
>Skrivning till oföränderliga databaser som `/libs` och `/apps` under körning ger upphov till fel. Som kund har du dessutom inte tillgång till utvecklarverktyg för mellanlagrings- och produktionsmiljöer.

Läs mer i [Utveckla med CRXDE Lite](https://docs.adobe.com/help/en/experience-manager-65/developing/devtools/developing-with-crxde-lite.html) om du vill veta hur du utvecklar ditt AEM-program med CRXDE Lite.

## Hantera loggar {#managing-logs}

Användarna kan öppna en lista över tillgängliga loggfiler för den valda miljön.

Läs [Komma åt och hantera loggar](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html) för att lära dig hur du får åtkomst till och hanterar loggar via användargränssnittet eller från API via Cloud Manager.

### Ytterligare support {#additional-support}

Om du har frågor om åtkomst till Cloud Service kontaktar du Adobe eller Adobe AEM CQ Support Portal.
