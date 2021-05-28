---
title: Efter publicering-fas
description: Efter publicering-fas
exl-id: f9b0b2fa-e29c-4faa-a5e7-e5edd04b25ca
source-git-commit: dfbd0f38017d02810da05ccadbc5f2fbd5826aa3
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 73%

---

# Efter publicering {#post-go-live}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_troubleshooting"
>title="AEM"
>abstract="Granska metodtips för kontinuerlig utveckling och hantera loggar tillsammans med verktyg som Developer Console och CRXDE Lite för att få hjälp med felsökning av AEM"
>additional-url="https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html" text="Komma åt och hantera loggar"
>additional-url="https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/development-guidelines.html#aem-as-a-cloud-service-development-tools" text="AEM som verktyg för Cloud Service Development"


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

>[!CONTEXTUALHELP]
>id="aemcloud_golive_support"
>title="Hjälp och support"
>abstract="Kontakta vårt AEM supportteam för att få klargöranden eller för att ta itu med eventuella frågor."
>additional-url="https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html" text="Stöd för Experience Cloud"

Om du har frågor om åtkomst till Cloud Service kontaktar du Adobe eller [Support för Experience Cloud](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html) om du vill ha mer information.
