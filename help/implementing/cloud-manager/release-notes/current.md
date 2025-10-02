---
title: Versionsinformation för Cloud Manager 2025.10.0
description: Läs om Cloud Manager 2025.10.0 i Adobe Experience Manager as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 4acedba631b3732b989794c648079356f9b79fdd
workflow-type: tm+mt
source-wordcount: '1286'
ht-degree: 0%

---

# Versionsinformation om Cloud Manager 2025.10.0 i Adobe Experience Manager as a Cloud Service {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2025.08.0+Release -->

Läs om Cloud Manager 2025.10.0 i AEM (Adobe Experience Manager) as a Cloud Service.

Se även [aktuell versionsinformation för Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Releasedatum {#release-date}

Lanseringsdatumet för Cloud Manager 2025.10.0 i AEM as a Cloud Service är torsdagen den 2 oktober 2025.

Nästa planerade version är torsdagen den 6 november 2025.

## Nyheter {#what-is-new}

* **AEM Cloud Health Assessment Service**

  Adobe introducerar AEM Cloud Health Assessment Service, ett automatiserat, icke-invasivt kontrollverktyg som gör att AEM as a Cloud Service-miljön förblir optimerad, säker och anpassad efter bästa praxis.

  Den här tjänsten utför följande:

   * Söker miljöer efter flaskhalsar, ineffektivitet och potentiella risker.
   * Analyserar innehållsstrukturer (utkast, live-kopior) och anpassade konfigurationer.
   * Identifierar föråldrade beroenden (AEM SDK, tredjepartsbibliotek).
   * Flaggar för problem med kodkvalitet (felaktiga anteckningar, ineffektiva mönster).
   * Tillhandahåller åtgärdsbar vägledning via instrumentpaneler som **Åtgärdscenter**.
   * Stöder proaktiv optimering genom tidig upptäckt och reparation av problem.

  Teamen kan kontinuerligt övervaka och förbättra sina AEM-miljöer för bättre prestanda, bättre säkerhet och långsiktig underhållbarhet.

  Se [Hälsoutvärdering för produktions- och scenmiljöer](/help/implementing/cloud-manager/reports/report-health-assessment.md).

* **Konfigurera stöd för pipeline**

  Config Pipelines stöds nu för sajter som byggts med Edge Delivery Services, vilket ger fler möjligheter än bara Cloud Service-miljöer. Du kan använda **Konfigurera pipelines** för att hantera inställningar som trafikfiltreringsregler och konfigurationer för WAF (Web Application Firewall), där det är tillämpligt. Se [Konfigurationer som stöds](/help/operations/config-pipeline.md#configurations).

  Edge Delivery config pipelines har också stöd för hemligheter via Cloud Manager pipeline-variabler.

  Se [Lägg till Edge Delivery-pipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-edge-delivery-pipeline.md).

* **Dialogrutan Installation av domänmappning-CDN har strömlinjeformats**

  Cloud Manager har förenklat **Mappningsdomänen till CDN**-flödet för att minska förvirring och hastighetskonfiguration. Dialogrutan framhäver nu **hanterad CDN som hanteras av Adobe** (med ett&quot;rekommenderat&quot; märke).

  ![Dialogrutan Koppla domän till CDN med alternativknappen CDN som hanteras av Adobe markerad](/help/implementing/cloud-manager/assets/cdn/map-domain-to-cdn-dialog-box-adobe-managed-cdn.png).

  Se [Lägg till en domänmappning](/help/implementing/cloud-manager/domain-mappings/add-domain-mapping.md).

  Dialogrutan innehåller också en enda, kortfattad checklista för kortet **Annan CDN-leverantör** med fokus på undervisningsinnehåll med följande:

   * Peka ditt CDN-ursprung på `publish-p<PROGRAM_ID>-e<ENV_ID>.adobeaemcloud.com`.
   * Ange **Värd/SNI** för att vidarebefordra den ursprungliga värden.
   * Lägg till `X-AEM-Edge-Key` (efter att nyckeln distribuerats i Cloud Manager).
   * Ange `X-Forwarded-Host` till din kundinriktade domän.
   * Radera andra `X-Forwarded-*`-huvuden innan du når AEM.

  ![Dialogrutan Koppla domän till CDN med alternativknappen Annan CDN-leverantör markerad](/help/implementing/cloud-manager/assets/cdn/map-domain-to-cdn-dialog-box-other-cdn-provider.png)

  <!-- (no redundant `Origin` field or "Learn more" clutter) -->Den medföljande sidfoten innehåller två praktiska länkar: exempelkonfigurationer för större CDN:er och en länk till fullständig dokumentation. En enda bekräftelseknapp - Jag har konfigurerat Mitt CDN-fyll i flödet.

  Se [CDN i AEM as a Cloud Service](/help/implementing/dispatcher/cdn.md#point-to-point-CDN).

<!--
### Staging-Only and Production-Only Pipelines {#staging-production-only-pipelines}

Support for [staging-only and production-only pipelines](/help/implementing/cloud-manager/configuring-pipelines/stage-prod-only.md) has been introduced, enabling you to split full-stack production deployment pipelines into smaller, specialized deployments.

If you are interested in testing this new feature and sharing your feedback, send an email to  `Grp-cloudmanager_splitpipelines@adobe.com` from your email address associated with your Adobe ID. -->


## Beta {#private-beta-program}

Delta i Cloud Manager betaprogram och få exklusiv tillgång till kommande funktioner innan de släpps.

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

Intresserad? Mejla [beta_quickbuild_cmpipelines@adobe.com](mailto:beta_quickbuild_cmpipelines@adobe.com) med ditt Adobe OrgID och program-ID.

<!-- You can deactivate incremental builds at the pipeline level by setting the property `CM_BUILD_DISABLE_MODULE_CACHING` to `true` (effective during the `BUILD` step). For how to add pipeline variables, see [Pipeline Variables in Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md).-->



### Enklicksåterställning för pipeline-distributioner {#one-click-rollback}

Återgå snabbt till en tidigare distribution om den senaste kundkällkoden inte fungerar som förväntat - du behöver inte köra om hela pipelinen eller återställa implementeringar manuellt.<!--https://jira.corp.adobe.com/browse/CMGR-69556 -->

![Återställ kundens källkod från miljökortet](/help/implementing/cloud-manager/release-notes/assets/restore-previous-code-deployed.png) *Miljökortet ovan med alternativet **Återställ**>**Tidigare kod som distribuerats**för en vald miljö.*

![Återställ föregående dialogruta för koddistribution](/help/implementing/cloud-manager/release-notes/assets/restore-previous-code-deployed-dialogbox.png)
*I dialogrutan **Återställ tidigare kod som distribuerats**granskar du den version som är distribuerad och den version som du vill återställa. Klicka sedan på&#x200B;**Bekräfta***.

![Återställer aktiveringen](/help/implementing/cloud-manager/release-notes/assets/restoring-previous-code-deployed-restoring.png)
*Cloud Manager återställer miljön till den tidigare versionen, bibehåller innehållet och konfigurationen intakt och markerar miljön **Återställning**tills distributionen är klar.*

![Source-kodversionen används](/help/implementing/cloud-manager/release-notes/assets/environments-view-details-sourcecodeversion.png) *Vyn Miljöinformation, som visas ovan, visar nu även den aktiva källkodsversionen som används.*

Om du är intresserad av att testa den här nya funktionen och dela med dig av dina synpunkter skickar du ett e-postmeddelande till [restorecode@adobe.com](mailto:restorecode@adobe.com) från den e-postadress som är kopplad till din Adobe ID.

Se [Återställa föregående kod som distribuerats i AEM as a Cloud Service](/help/operations/restore-previous-code-deployed.md).

Se även [Innehållsåterställning i AEM as a Cloud Service](/help/operations/restore.md).

### Specialiserad testmiljö {#specialized-test-environment}

Cloud Manager stöder nu tillägg av en ny miljötyp som kallas **Specialiserad testmiljö**. Miljön är utformad för att hjälpa team att validera funktioner under förhållanden nära produktionsförhållanden innan de publicerar. Den här miljötypen skiljer sig från *Produktion + Stage*, *Utveckling* eller *Snabb utveckling* och erbjuder ett fokuserat utrymme för att köra avancerade valideringsscenarier.

**Senaste förbättringarna**

* Nu kan du konfigurera en anpassad testmiljö på en icke-produktionsprocess via ett enklare och mer intuitivt arbetsflöde. Den strömlinjeformade installationen snabbar upp slutförandet och minskar antalet konfigurationsfel.
* **Kopiera innehåll** stöds nu i specialiserade testmiljöer. Nu kan du köra **Kopiera innehåll** säkert i isolerade testmiljöer som speglar produktionen. <!-- (CMGR‑68900) -->

Se [Lägg till en anpassad testmiljö](/help/implementing/cloud-manager/specialized-test-environment.md).

![Dialogrutan Lägg till miljö med alternativknappen Specialiserad testmiljö markerad](/help/implementing/cloud-manager/release-notes/assets/specialized-test-environment.png)

>[!NOTE]
>
>Adobe har stängt betaåtkomstbegäranden för specialiserade testmiljöer efter att ha nått ett tillräckligt antal deltagare. Funktionen förbereds nu för allmän tillgänglighet.

<!--
If you are interested in testing this new feature and sharing your feedback, send an email to [grp-earlyadopter_cs_advtestenvironment@adobe.com](mailto:grp-earlyadopter_cs_advtestenvironment@adobe.com) from your email address associated with your Adobe ID. -->


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

Det finns inga viktiga felkorrigeringar i oktober-versionen av Cloud Manager.


<!-- ## Known issues {#known-issues} -->

