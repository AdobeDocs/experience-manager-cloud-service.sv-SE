---
title: Versionsinformation för Cloud Manager 2026.1.0
description: Läs om Cloud Manager 2026.1.0 i Adobe Experience Manager as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 2ea076c42a6406548bf48cd246227fc8ddb3a080
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 0%

---

# Versionsinformation om Cloud Manager 2026.1.0 i Adobe Experience Manager as a Cloud Service {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2025.08.0+Release -->

Läs om Cloud Manager 2026.1.0 i AEM (Adobe Experience Manager) as a Cloud Service.

Se även [aktuell versionsinformation för Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Releasedatum {#release-date}

Lanseringsdatumet för Cloud Manager 2026.1.0 i AEM as a Cloud Service är torsdagen den 22 januari 2026.

Nästa planerade version är torsdagen den 5 februari 2026.

## Nyheter - Cloud Manager {#cloud-manager-whats-new}

* **Konfigurationspipelines stöder nu hanterade hemligheter**

  Användare kan nu lägga till och hantera hemligheter direkt i Cloud Manager konfigurationspipelines. Dessa hemligheter åsidosätter på ett säkert sätt värden i pipeline-konfigurationsspecifikationen och stöder flexibla, miljöspecifika distributioner.

  ![Alternativet Visa/redigera variabler på den nedrullningsbara menyn för en vald pipeline](/help/implementing/cloud-manager/release-notes/assets/view-edit-variables-option.png)
  *Visa/redigera variabelalternativ i listrutan för en vald pipeline.*

  ![Dialogrutan Variabelkonfiguration &#x200B;](/help/implementing/cloud-manager/release-notes/assets/view-edit-variables-variablesconfig-dialogbox.png)*Dialogrutan Variabelkonfiguration.*

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

### Experience Hub Extensibility and Customization {#exp-hub-extensibility}

[Experience Hub](/help/experience-hub.md) fungerar som startpunkt för AEM och är anpassad efter organisationens behov. Berätta för Adobe om de befintliga AEM-gränssnittstilläggen så att du enkelt kan aktivera dem i Experience Hub.

![Diagram över Experience Hub arbetsflöde för utbyggbarhet och anpassning](/help/implementing/cloud-manager/release-notes/assets/experience-hub-extensibility-customization.png)

Bädda in anpassade upplevelser i Experience Hub för att utöka och personalisera organisationens kontrollpanel. Förutom Adobe inbyggda widgetar kan du lägga till egna med hjälp av ramverket [UI Extensibility](https://developer.adobe.com/uix/docs/) . Bygg JavaScript-baserade gränssnittsappar och visa upp dem för användarna för att uppfylla företagsspecifika krav och arbetsflöden.

Intresserad av betaversionen? Mejla [beta_exphubextensibility@adobe.com](mailto:beta_exphubextensibility@adobe.com) med ditt Adobe OrgID och en kort beskrivning av den anpassning du tänker skapa.

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

Det finns inga viktiga felkorrigeringar i Cloud Manager-utgåvan från december 2025.


<!-- ## Known issues {#known-issues} -->

