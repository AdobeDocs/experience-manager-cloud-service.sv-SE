---
title: OpenAPI-baserade API:er
description: Läs om AEM as a Cloud Service stöd för OpenAPI-baserade API:er
feature: Developing
role: Admin, Architect, Developer
exl-id: 4aeafba9-8f9e-4ecb-9e37-8d048b0474cc
source-git-commit: 320fe55d652b94cd63dfe82d4165c1f957653a63
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 0%

---

# OpenAPI-baserade API:er {#openapi-based-apis}

Nyare AEM as a Cloud Service-API:er följer OpenAPI-specifikationen och erbjuder därmed en konsekvent och väldokumenterad uppsättning API:er.

>[!NOTE]
>
> En [heltäckande självstudiekurs](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis) rekommenderas för att lära dig hur du konfigurerar och anropar OpenAPI-baserade AEM API:er.

För slutpunkter som kräver autentisering skiljer sig autentiseringsmetoden från slutpunkten, men kan använda OAuth Server-to-Server, OAuth Web App eller OAuth Single Page App (SPA). Autentiseringsuppgifter konfigureras via projekt i [Adobe Developer Console](https://developer.adobe.com/developer-console/).

Vanliga API-användningsfall omfattar integreringar med system som CRM eller PIM, där AEM API:er anropas för att hämta eller behålla data. Som en del av integreringsimplementeringen kan program prenumerera på [händelser som skickas från AEM](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-eventing/overview), vilket kan utlösa affärslogik i Adobe App Builder eller annan infrastruktur.

Det här dokumentet fungerar som en översikt, men mer ingående dokumentation finns på följande sidor:

* Länkarna från det OpenAPI-baserade API-avsnittet i [referensdokumentationen](https://developer.adobe.com/experience-cloud/experience-manager-apis/). Varje API:s referensdokumentation innehåller också en API-spelningsbakgrund, vilket gör det enkelt att testa en slutpunkt med en bearer-token som genererats med Adobe Developer Console.

* Informativa [guider](https://developer.adobe.com/experience-cloud/experience-manager-apis/guides/), inklusive [API-koncept och syntax](https://developer.adobe.com/experience-cloud/experience-manager-apis/guides/how-to/).

* En självstudiekurs på den översta nivån som beskriver [autentiseringsmetoder](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/openapis/overview#authentication-support) och andra koncept.

* En självstudiekurs med video som fokuserar på [hur du konfigurerar OpenAPI-baserade API:er](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/openapis/setup).

* [En självstudiekurs från början till slut](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis) om hur du konfigurerar och anropar OpenAPI:er med autentiseringsstrategin server-till-server. Liknande självstudiekurser finns också för autentiseringsmetoderna Web App och Single Page Application.

## Konfigurera API-åtkomst {#configuring-api-access}

Vissa OpenAPI-baserade AEM-API:er behöver autentiseras, vilket kräver att autentiseringsuppgifter genereras med [Adobe Developer Console](https://developer.adobe.com/developer-console/). Konfiguration omfattar följande steg:

1. Modernisering av AEM as a Cloud Service. Mer information finns i [Modernisering av AEM as a Cloud Service-miljön](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/openapis/setup?#modernization-of-aem-as-a-cloud-service-environment) - självstudiekurs.
1. Ge åtkomst till AEM API:er med produktprofiler. Produktprofiler är kopplade till de tjänster som representerar AEM användargrupper med fördefinierade åtkomstkontrollistor (ACL). Vissa tjänster är som standard associerade med specifika produktprofiler, men andra måste uttryckligen kopplas. AEM Assets API-användartjänst är till exempel inte associerad med någon [produktprofil](/help/onboarding/aem-cs-team-product-profiles.md#aem-product-profiles), så du måste aktivera den för att kunna använda AEM Assets API. Mer information finns i [Aktivera åtkomst till AEM API:er](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/openapis/setup#enable-aem-apis-access) självstudiekurs.
1. Om du vill lägga till server-till-server-autentisering måste den användare som ställer in integreringen vara organisationens systemadministratör i Adobe Admin Console eller läggas till som utvecklare i den produktprofil där tjänsten är kopplad. Mer information finns i [Aktivera åtkomst till AEM API:er](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/openapis/setup#enable-aem-apis-access) självstudiekurs.
1. Skapa ett Adobe Developer Console-projekt (ADC).
1. Konfigurera ADC-projektet. Detta genererar autentiseringsuppgifter som ska användas senare för utbyte mot en innehavartoken när API anropas.
1. Konfigurera AEM-instansen för att aktivera ADC-projektkommunikation. Detta innebär att registrera klient-ID:t i miljön genom att konfigurera och distribuera en YAML-fil, vilket beskrivs i avsnittet [Registrera ett klient-ID](#registering-a-client-id) nedan.

Detaljerade stegvisa instruktioner finns i självstudiekursen [Konfigurera OpenAPI-baserade API:er](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/openapis/setup).

### Registrera ett klient-ID {#registering-a-client-id}

Klient-ID:n omfattar API:erna i ett Adobe Developer Console-projekt för specifika AEM-miljöer. Detta uppnås på följande sätt:

1. Skapa en fil med namnet `api.yaml` eller liknande med en konfiguration som fragmentet nedan, inklusive önskade nivåer (författare, publicering, förhandsgranskning). `Client_id` värden ska komma från dina Adobe Developer Console API-projekt.

   Egenskaperna `kind`, `version` och `metadata` beskrivs i artikeln [Konfigurera pipeline](/help/operations/config-pipeline.md#common-syntax). Egenskapsvärdet `kind` ska anges till *API* och egenskapen `version` ska anges till *1*.

   ```
   kind: "API"
   version: "1"
   metadata:
     envTypes: ["dev"]
   data:
     allowedClientIDs:
       author:
         - "<client_id>"
       publish:
         - "<client_id>"
       preview:
         - "<client_id>"
   ```

1. Placera filen någonstans under en mapp på den översta nivån med namnet `config` eller liknande, enligt beskrivningen under [Konfigurera pipeline](/help/operations/config-pipeline.md#folder-structure).
1. För andra miljötyper än RDE (som använder kommandoradsverktyg) skapar du en riktad distributionskonfigurationspipeline i Cloud Manager, enligt referens i [det här avsnittet](/help/operations/config-pipeline.md#creating-and-managing) i artikeln Config Pipeline. Observera att pipelines för fullständig stapel och webbnivå inte distribuerar konfigurationsfilen.
1. Distribuera konfigurationen.
