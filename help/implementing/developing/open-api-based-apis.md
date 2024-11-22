---
title: OpenAPI-baserade API:er
description: Läs om AEM as a Cloud Service stöd för OpenAPI-baserade API:er
feature: Developing
role: Admin, Architect, Developer
exl-id: 4aeafba9-8f9e-4ecb-9e37-8d048b0474cc
source-git-commit: bb125c5a20dad8afcada0e4325e4d757bfcabd7c
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 0%

---

# OpenAPI-baserade API:er {#openapi-based-apis}

>[!NOTE]
>
>OpenAPI:er är tillgängliga som en del av ett program för tidig åtkomst. Om du är intresserad av att få tillgång till dem bör du skicka ett e-postmeddelande till [aem-apis@adobe.com](mailto:aem-apis@adobe.com) med en beskrivning av ditt användningsfall.

Nyare AEM as a Cloud Service-API:er följer OpenAPI-specifikationen och producerar därmed konsekventa, väldokumenterade och användarvänliga API:er. Detaljerad information finns på följande sidor:

* En [heltäckande självstudiekurs](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis) om hur du konfigurerar och anropar OpenAPI-baserade AEM-API:er.
* Informativa [guider](https://developer.adobe.com/experience-cloud/experience-manager-apis/guides/), inklusive [API-koncept och syntax](https://developer.adobe.com/experience-cloud/experience-manager-apis/guides/how-to/).
* API-slutpunktens [referensdokumentation](https://developer.adobe.com/experience-cloud/experience-manager-apis/), där vissa API:er är OpenAPI-baserade, till exempel [den här webbplats-API:n](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/). Referensdokumentationen innehåller också en API-spelningsbakgrund, som gör det enkelt att testa en slutpunkt med en innehavartoken som genererats med Adobe Developer Console.

Ett vanligt API-exempel omfattar integrering med system som CRM eller PIM, där AEM API anropas för att hämta eller behålla data. Som en del av integreringsimplementeringen kan program prenumerera på [AEM-utsända händelser](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-eventing/overview) som kan utlösa affärslogik i Adobe App Builder eller annan infrastruktur.

De API-autentiseringstyper som stöds skiljer sig åt beroende på slutpunkten, men kan vara OAuth Server-to-Server, OAuth Web App och OAuth Single Page App (SPA).

>[!NOTE]
>
> Självstudiekursen [från början till slut](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis) rekommenderas för att lära dig hur du konfigurerar och anropar OpenAPI-baserade AEM API:er.


## Konfigurera API-åtkomst {#configuring-api-access}

Många OpenAPI-baserade AEM-API:er kräver autentisering, vilket kräver att autentiseringsuppgifter genereras med [Adobe Developer Console](https://developer.adobe.com/developer-console/docs/guides/). Konfiguration omfattar följande steg, som visas i självstudiekursen:

1. Se till att ditt AEM [produktprofiler uppdateras](/help/onboarding/aem-cs-team-product-profiles.md#aem-product-profiles) och att en lämplig tjänst är aktiverad för att komma åt det önskade API:t.
1. Skapa ett nytt projekt i Adobe Developer Console och lägg till önskade API:er i projektet, och välj även lämplig autentiseringstyp.
1. Generera autentiseringsuppgifterna, som senare kommer att användas för utbyte av en innehavartoken när API anropas.
1. Registrera klient-ID:t i miljön genom att konfigurera en YAML-fil som distribueras med Config Pipeline (eller kommandorad för RDE:er).

## Registrera ett klient-ID {#registering-a-client-id}

Klient-ID:n omfattar åtkomstpunkten i ett Adobe Developer Console-projekt för specifika AEM. Detta uppnås på följande sätt:

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
