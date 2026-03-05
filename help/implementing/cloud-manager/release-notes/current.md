---
title: Versionsinformation om Cloud Manager 2026.3.0
description: Läs om Cloud Manager 2026.3.0 i Adobe Experience Manager as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: eb3e826e27e14b8b1da534440f11d43e973130ec
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 0%

---

# Versionsinformation om Cloud Manager 2026.3.0 i Adobe Experience Manager as a Cloud Service {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2025.08.0+Release -->

Läs om Cloud Manager 2026.3.0 i AEM (Adobe Experience Manager) as a Cloud Service.

Se även [aktuell versionsinformation för Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Releasedatum {#release-date}

Lanseringsdatumet för Cloud Manager 2026.3.0 i AEM as a Cloud Service är torsdagen den 5 mars 2026.

Nästa planerade version är torsdagen den 2 april 2026.


## Nyheter - Cloud Manager {#cloud-manager-whats-new}

* **Cloud Manager har nu stöd för ett** rensningsalternativ **för** innehållskopior **-importer**

  När du aktiverar **Rensa** tar Cloud Manager bort det befintliga innehållet på målplatsen innan du startar importen, så att du kan börja från en ren platta och undvika konflikter med befintligt innehåll. Om du låter **Rensa** vara inaktiverat importerar Cloud Manager det nya innehållet ovanpå det befintliga målinnehållet. Ett bekräftelsemeddelande visas innan rensningen börjar och Cloud Manager loggar rensningsåtgärden och importinformationen för spårbarhet.

  Se även [Kopiera innehåll](/help/implementing/developing/tools/content-copy.md#copy-content).

* **Stöd för UI-utbyggbarhet i AEM Experience Hub**
Stöd för gränssnittstillägg i [&#x200B; AEM Experience Hub &#x200B;](https://experience.adobe.com/experiencemanager) är nu aktiverat, vilket gör att utvecklare kan utöka gränssnittet med anpassade funktioner och widgetar som skapats med Adobe App Builder.

  Mer information finns i [AEM Experience Hub](https://developer.adobe.com/uix/docs/services/aem-experience-hub/).

* **Förbättrad stabilitet, prestanda och tillförlitlighet**

  Den här versionen innehåller optimerings- och underhållsuppdateringar som förbättrar stabiliteten, prestandan och tillförlitligheten i Cloud Manager.


## Beta {#private-beta-program}

Delta i Cloud Manager betaprogram och få exklusiv tillgång till kommande funktioner innan de släpps.

>[!IMPORTANT]
>
>Beta-releaser kan innehålla defekter och tillhandahålls i befintligt skick utan någon garanti av något slag. Adobe har ingen skyldighet att upprätthålla, korrigera, uppdatera, ändra, modifiera eller på annat sätt ge support (via Adobe Support Services eller på annat sätt) för betaversioner. Adobe rekommenderar sina kunder att iaktta försiktighet och inte förlita sig på att betaversioner fungerar eller fungerar som de ska, eller på medföljande dokumentation eller material. Funktioner och API:er i betaversionen kan ändras utan föregående meddelande. Därför är all användning av betaversioner helt och hållet på kundens egen risk.

Se även [AEM Beta-program](/help/release-notes/release-notes-cloud/release-notes-current.md#aem-beta-programs)

Följande möjligheter är för närvarande tillgängliga:
<!--
### Support for Custom Author Domains in Cloud Service

AEM Cloud Service is going to soon support one custom domain per Author environment.-->

### Cloud Manager MCP-server för AI-driven IDE{#mcp-server-for-cm}

Nu kan du prova en MCP-server (Model Context Protocol) som visar Cloud Manager Public API:er som verktyg för AI-aktiverade IDE:er (som Cursor). När du har anslutit den kan du använda konversationsprompter för att lista och hantera program, pipelines, miljöer och databaser, vilket gör att du kan gå snabbare utan att behöva lämna redigeraren.

Se dokumentationen [Använd MCP med AEM as a Cloud Service](/help/ai-in-aem/mcp-support/using-mcp-with-aem-as-a-cloud-service.md).

Se självstudien [Cloud Manager MCP Server](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/ai/mcp-server/cloud-manager#).

Intresserad av betaversionen? Mejla [GRP-AEM-CM-MCP-FEEDBACK@adobe.com](mailto:GRP-AEM-CM-MCP-FEEDBACK@adobe.com) med ditt Adobe OrgID och program-ID.


<!--
### Experience Hub Extensibility and Customization {#exp-hub-extensibility}

[Experience Hub](/help/experience-hub.md) serves as your entry point to AEM, customized for your organization's needs. Tell Adobe about your existing AEM UI Extensions so they can help you enable them in Experience Hub with minimal effort.

![Diagram of Experience Hub extensibility and customization workflow](/help/implementing/cloud-manager/release-notes/assets/experience-hub-extensibility-customization.png)

Embed custom experiences in Experience Hub to extend and personalize your organization's dashboard. In addition to Adobe's built-in widgets, add your own using the [UI Extensibility](https://developer.adobe.com/uix/docs/) framework. Build JavaScript-based UI apps and surface them to your users to meet business-specific requirements and workflows. 

Interested in the beta? Email [beta_exphubextensibility@adobe.com](mailto:beta_exphubextensibility@adobe.com) with your Adobe OrgID and a short description of the customization you intend to create.
-->

### Bygger snabbare med modulcachning {#quick-build-cm-pipelines}

En ny byggmodell kompilerar endast ändrade moduler (i stället för hela repon) med cache-lagring på modulnivå för att korta byggtiden. Det gäller för rörledningar med kodkvalitet, fullständig stapel och enbart scener.

![Dialogrutan Redigera icke-produktionspipeline som visar två alternativ för byggstrategi som är Fullständigt bygge och Smart bygge](/help/implementing/cloud-manager/release-notes/assets/non-production-pipeline-edit.png)
*Dialogrutan Redigera icke-produktionsförlopp visar två alternativ för Build Strategy som är Full Build och Smart Build.*

I dialogrutan **Lägg till/redigera pipeline**, under fliken **Source-kod**, finns ett nytt avsnitt i avsnittet **Skapa strategi** där du kan välja något av följande byggalternativ:

* **Fullständigt bygge** - Skapar alla moduler i databasen vid varje körning.
* **Smart Build** - Skapar bara moduler som ändrats sedan den senaste implementeringen, vilket förkortar den totala byggtiden.

Du styr vilka pipelines som använder **Smart build**. Under betaversionen visas det här alternativet endast för **kodkvalitet**- och **dev-distribution**-pipelines.

Intresserad? Mejla [beta_quickbuild_cmpipelines@adobe.com](mailto:beta_quickbuild_cmpipelines@adobe.com) med ditt Adobe OrgID och program-ID.

<!-- You can deactivate incremental builds at the pipeline level by setting the property `CM_BUILD_DISABLE_MODULE_CACHING` to `true` (effective during the `BUILD` step). For how to add pipeline variables, see [Pipeline Variables in Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md).-->

## Felkorrigeringar {#bug-fixes}

* Ett problem där återställningspunkter-API:t kunde returnera 500 fel när återställningspunkter hämtades har åtgärdats. Slutpunkten hanterar nu null-värden korrekt, vilket ger enhetliga och tillförlitliga svar. (CMGR-72963)
* Cloud Manager godkänner nu GitHub-databasens URL:er med eller utan suffixet `.git`, som anpassar API-beteendet med användargränssnittet och gör databasintroduktionen mer flexibel. (CMGR-73296)
* Validering av produktprofilnamn är nu inte skiftlägeskänsligt, vilket förhindrar fel när du skapar profiler med namn som bara skiljer sig åt med versaler. (CMGR-74075)
* Nu kan du utföra flera återställningsåtgärder från samma pipeline-körning, vilket möjliggör sekventiella återställningar för miljöer som Stage och Production utan att en ny pipeline-körning krävs. (CMGR-73538)


<!-- ## Known issues {#known-issues} -->

