---
title: Versionsinformation för Cloud Manager 2025.9.0
description: Läs om Cloud Manager 2025.9.0 i Adobe Experience Manager as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 2b82e3b848be828fbf8c316244031a0e06f512ca
workflow-type: tm+mt
source-wordcount: '1125'
ht-degree: 0%

---

# Versionsinformation om Cloud Manager 2025.9.0 i Adobe Experience Manager as a Cloud Service {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2025.08.0+Release -->

Läs om Cloud Manager 2025.9.0 i AEM (Adobe Experience Manager) as a Cloud Service.

Se även [aktuell versionsinformation för Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Releasedatum {#release-date}

Lanseringsdatumet för Cloud Manager 2025.9.0 i AEM as a Cloud Service är torsdagen den 4 september 2025.

Nästa planerade version är torsdagen den 2 oktober 2025.

## Nyheter {#what-is-new}

* **Förnya Adobe-hanterade domänvalideringscertifikat manuellt**

  Nu kan du manuellt förnya DV-certifikat (Adobe-managed Domain Validation) från Cloud Manager eller det offentliga API:t för att uppdatera certifikat proaktivt. <!-- CMGR-68738 -->

  ![Förnya SSL-certifikat](/help/implementing/cloud-manager/release-notes/assets/ssl-certificate-adobedv-renew.png)

* **Stöd har nu lagts till för Azure DevOps för privata databaser**

  Dokumentationsuppdateringarna innehåller konfigurationssteg för Bring Your Own Git with Azure DevOps och pull request validation. Se [Lägg till externa databaser i Cloud Manager](/help/implementing/cloud-manager/managing-code/external-repositories.md).

* **Dra in begärandekontroller för privata databaser**

  Cloud Manager har nu stöd för konfigureringspipelines med privata databaser över GitHub, Bitbucket, Azure DevOps och GitLab. Se [Pull Request Checks for Private Repositories](/help/implementing/cloud-manager/managing-code/github-check-config.md).

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

### Lägg till Edge Delivery config pipeline {#add-eds-pipeline}

Config Pipelines stöds nu för sajter som byggts med Edge Delivery Services, vilket ger fler möjligheter än bara Cloud Service-miljöer. Du kan använda **Konfigurera pipelines** för att hantera inställningar som trafikfiltreringsregler och konfigurationer för WAF (Web Application Firewall), där det är tillämpligt. Se [Konfigurationer som stöds](/help/operations/config-pipeline.md#configurations).

**Senaste förbättringar**

* Edge Delivery config pipelines har nu stöd för hemligheter via Cloud Manager pipeline-variabler.
* Edge Delivery Services-pipelines visar nu **Konfiguration** i kolumnen **Distribuerad kod**, vilket möjliggör omedelbar identifiering av distributioner som bara är konfigurerade. <!-- CMGR‑69681 -->
* Cloud Manager visar **Lägg till Edge Delivery Pipeline** när ett program innehåller minst en Edge Delivery Services-webbplats och en mappad domän. I annat fall visas alternativet inaktiverat och ett verktygstips förklarar saknade krav. <!-- CMGR‑69680 -->
* På fliken **Edge Delivery** visas en ny **Edge Delivery pipelines**-widget med namn, status, databas och gren för varje pipeline. <!-- (CMGR-69052) -->

  ![Edge Delivery pipeline-widget med pipeline-namn, status, databas och gren](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-widget.png)

* Panelen **Filter** lägger till ett avsnitt av typen **Leverans**. Den innehåller kryssrutorna **Leverans** och **Publiceringsleverans** för Edge. <!-- (CMGR-69682) -->

  ![Filterpanelen visar den nya leveranstypen för Edge-leverans och Publicera leverans](/help/implementing/cloud-manager/release-notes/assets/filter-delivery-type.png)

![Lägg till Edge Delivery-pipeline i den nedrullningsbara listan Lägg till pipeline](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-add.png) *Lägger till en Edge Delivery-pipeline från sidan **Programöversikt**,**Pipelines**-kort.*

![Lägg till dialogrutan för Edge Delivery-pipeline](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-add-dialogbox.png) *Lägg till Edge Delivery-dialogrutan för pipeline.*

Se [Lägg till Edge Delivery Pipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-edge-delivery-pipeline.md)

Om du är intresserad av att testa den här nya funktionen och dela med dig av dina synpunkter skickar du ett e-postmeddelande till [grp-aemeds-config-pipeline-adopter@adobe.com](mailto:grp-aemeds-config-pipeline-adopter@adobe.com) från den e-postadress som är kopplad till din Adobe ID.

## Felkorrigeringar {#bug-fixes}

Det finns inga viktiga felkorrigeringar i september-versionen av Cloud Manager.


<!-- ## Known issues {#known-issues} -->

