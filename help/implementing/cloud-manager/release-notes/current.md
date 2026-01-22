---
title: Versionsinformation för Cloud Manager 2026.1.0
description: Läs om Cloud Manager 2026.1.0 i Adobe Experience Manager as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 54566e3ea99c4ac03e266eab52163a516701b611
workflow-type: tm+mt
source-wordcount: '918'
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

### Hämta din egen Git (BYOG) {#gitlab-bitbucket-azure-vsts}

<!-- BOTH CS & AMS -->

Kunderna kan nu lägga in sina Azure DevOps Git-databaser i Cloud Manager, med stöd för både moderna Azure DevOps-databaser och äldre VSTS-databaser (Visual Studio Team Services).

* För Edge Delivery Services-användare kan den inbyggda databasen användas för att synkronisera och distribuera platskod.
* För AEM as a Cloud Service- och Adobe Managed Services-användare (AMS) kan databasen länkas till både fullständiga och frontbaserade pipelines.

Stöd för fler pipelinetyper och pull-begäran-validering via pipelines för kodkvalitet kommer snart.

Se [Lägg till externa databaser i Cloud Manager](/help/implementing/cloud-manager/managing-code/external-repositories.md).

![Dialogrutan Lägg till databas](/help/implementing/cloud-manager/release-notes/assets/azure-repo.png)

<!-- If you are interested in testing this new feature and sharing your feedback, send an email to [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com) from your email address associated with your Adobe ID. Be sure to include which Git platform you want to use and whether you are on a private/public or enterprise repository structure. -->

**Frågor och svar om BYOG**

| Fråga | Svar |
|---|---|
| *Hur kan ett projekt vid behov växla tillbaka till den Adobe-hanterade Git-databasen?* | Det är enkelt att byta tillbaka. [Uppdatera pipelines](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md) så att de pekar på Adobe-databasen och tar bort den externa databasen om den inte längre behövs. |
| *Går det att konfigurera olika databaser för olika miljöer (till exempel icke-produktion kontra produktion) så att testning i icke-produktion först tillåts?* | Ja, olika databaser kan konfigureras för olika miljöer. Utvecklings- eller kodkvalitetsflödet kan till exempel peka på en extern databas medan produktionsflödet är anslutet till Adobe-databasen. Kontrollera att synkroniseringsjobbet mellan de två databaserna förblir aktivt under den här konfigurationen. |
| *Fortsätter befintliga inställningar som `IP Allow`-listor att fungera?* | Ja, befintliga `IP Allow`-listor fortsätter att fungera som vanligt. Om den externa Git-databasen skyddas av en brandvägg måste de nödvändiga [Adobe IP-adresserna läggas till i tillåtelselista](/help/implementing/cloud-manager/ip-allow-lists/introduction.md). |
| *Fungerar alla URL:er för GitLab-databasen? Databas-URL:en som används har formatet `https://gitlab_dedicated_url.com/path/repo-name.git`, vilket skiljer sig från exemplet i dokumentationen.* | Ja, alla GitLab-databaser som har stöd för API V3 eller V4 stöds, inklusive GitLab-URL:er som de som finns som värd, som den som beskrivs i [Lägg till externa databaser i Cloud Manager](/help/implementing/cloud-manager/managing-code/external-repositories.md) (`https://git-vendor-name.com/org-name/repo-name.git`). |


#### Hantera åtkomsttoken{#manage-access-tokens}

Använd **Hantera åtkomsttoken** i Cloud Manager för att visa, byta namn på och ta bort åtkomsttoken som är kopplade till externa BYOG-databaser, som GitHub Enterprise, GitLab, Bitbucket och Azure DevOps.

Se [Hantera åtkomsttoken](/help/implementing/cloud-manager/managing-code/manage-access-tokens.md).

<!-- If you are interested in testing this new feature and sharing your feedback, send an email to [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com) from your email address associated with your Adobe ID. -->


## Felkorrigeringar {#bug-fixes}

Det finns inga viktiga felkorrigeringar i Cloud Manager-utgåvan från december 2025.


<!-- ## Known issues {#known-issues} -->

