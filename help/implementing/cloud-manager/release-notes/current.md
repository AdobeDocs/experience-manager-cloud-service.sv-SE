---
title: Versionsinformation för Cloud Manager 2025.5.0
description: Läs om Cloud Manager 2025.5.0 i Adobe Experience Manager as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 12388df411b9bf0693358a82de17fec90d83877a
workflow-type: tm+mt
source-wordcount: '1050'
ht-degree: 0%

---

# Versionsinformation om Cloud Manager 2025.5.0 i Adobe Experience Manager as a Cloud Service {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2025.03.0+Release -->

Läs om Cloud Manager 2025.5.0 i AEM (Adobe Experience Manager) as a Cloud Service.

Se även [aktuell versionsinformation för Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Releasedatum {#release-date}

Lanseringsdatumet för Cloud Manager 2025.5.0 i AEM as a Cloud Service är torsdagen den 8 maj 2025.

Nästa planerade version är torsdagen den 5 juni 2025.

## Nyheter {#what-is-new}

### Konfigurera innehållskällan med ett klick för Edge Delivery Services

Adobe Experience Manager (AEM) Edge Delivery Services tillåter innehållsleverans från flera källor, som Google Drive, SharePoint eller AEM, via ett snabbt, globalt distribuerat gränsnätverk.

Innehållskällans konfiguration skiljer sig åt mellan Helix 4 och Helix 5 på följande sätt:

| Version | Konfigurationsmetod för innehållskälla |
| --- | --- |
| Helix 4 | YAML-fil (`fstab.yaml`) |
| Helix 5 | Konfigurationstjänstens API (*no`fstab.yaml`*) |

I den här artikeln finns omfattande konfigurationssteg, exempel och valideringsinstruktioner för båda versionerna.

**Innan du börjar**

Om du använder [en klickning på Edge Delivery i Cloud Manager](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md##one-click-edge-delivery-site) är webbplatsen Helix 5 med en enda databas. Följ Helix 5- instruktionerna och använd den medföljande Helix 4 YAML- versionen av instruktionerna som reserv.

**Bestäm din Helix-version**

* Helix 4 - Ditt projekt innehåller en `fstab.yaml`-fil.
* Helix 5 - Ditt projekt *använder inte* `fstab.yaml` och konfigurerades via Edge Delivery Services gränssnitt eller API.

Bekräfta via databasmetadata eller kontakta administratören om du fortfarande är osäker.

#### Konfigurera innehållskällan för Helix 4

I Helix 4 definierar filen fstab.yaml innehållskällan för platsen. Den här filen finns i roten av GitHub-databasen och mappar URL-sökvägsprefix (kallas monteringspunkter) till externa innehållskällor. Ett typiskt exempel ser ut så här:

```yaml
mountpoints:
  /: https://drive.google.com/drive/folders/your-folder-id
```

Det här exemplet är endast för illustrationer. Den faktiska URL:en ska peka mot innehållskällan, t.ex. en Google Drive-mapp, SharePoint-katalog eller AEM-sökväg.

**Så här konfigurerar du innehållskällan för Helix 4:**

Stegen varierar beroende på vilket källsystem du använder.

* **Google Drive**

   1. Skapa en Google Drive-mapp.
   1. Dela mappen med `helix@adobe.com`.
   1. Hämta länken för den delningsbara mappen.
   1. Uppdatera din `fstab.yaml` så som visas i följande:

      ```yaml
      mountpoints: 
          /: https://drive.google.com/drive/folders/<folder-id>
      ```

   1. Verkställ och skicka ändringar till GitHub.

* **SharePoint**

   1. Skapa en SharePoint-mapp eller ett dokumentbibliotek.
   1. Dela åtkomst med `helix@adobe.com`.
   1. Hämta mappens URL.
   1. Uppdatera din `fstab.yaml` så som visas i följande:

      ```yaml
      mountpoints:
        /: https://<tenant>.sharepoint.com/sites/<site>/Shared%20Documents/<folder>
      ```

   1. Verkställ och skicka ändringar till GitHub.

* **AEM**

   1. Identifiera AEM innehållssökväg.
   1. Använd AEM innehållsexportadress enligt följande:

      ```yaml
      mountpoints:
        /: https://author.<your-aem-instance>.com/bin/franklin.delivery/<org>/<repo>/main
      ```

   1. Verkställ och skicka ändringar till GitHub.

##### Validering

* Klicka på **Förhandsgranska** > **Publicera** > **Testa den publicerade webbplatsen** med AEM Sidekick Chrome Extension.
* Verifiera URL: `https://main--<repo>--<org>.hlx.page/`

#### Konfigurera innehållskällan för Helix 5

Helix 5 är svarslös, använder inte `fstab.yaml` och stöder flera platser som delar samma katalog. Konfigurationen hanteras via konfigurationstjänstens API eller Edge Delivery Services UI. Konfigurationen är platsnivå (inte databasnivå).

Följande skillnader är konceptuella:

| Proportioner | Helix 4 | Helix 5 |
| --- | --- | --- |
| Konfiguration | Klart till `fstab.yaml` | Klar via API:t eller användargränssnittet i stället för YAML. |
| Monteringspunkter | Definieras i `fstab.yaml`. | Krävs inte. Roten är implicit känd. |

**Konfigurera innehållskällan för Helix 5:**

1. Använd konfigurationstjänstens API för att autentisera via en API-nyckel eller åtkomsttoken.
1. Gör följande `PUT` API-anrop:

   ```bash {.line-numbering}
   PUT /api/{program}/{programId}/site/{siteId}
   Content-Type: application/json
   
   {
     "sitename": "my-site",
     "branchName": "main",
     "version": "v5",
     "repo": "my-content-repo-link"
   }
   ```

1. Validera svar (förväntat: HTTP 200 OK).

##### Validering

* Klicka på **Förhandsgranska** > **Publicera** > **Testa den publicerade webbplatsen** med AEM Sidekick Chrome Extension.
* Verifiera URL: `https://main--<repo>--<org>.aem.page/`
* (Valfritt) Kontrollera den aktuella konfigurationen via följande `GET` API-anrop:

  ```bash
  GET /api/{program}/{programId}/site/{siteId}
  ```

<!--
* **AI-powered build summaries now available for internal use**

    Internal users can now use AI-powered build summaries to simplify build log analysis. The feature provides actionable recommendations and helps identify the root causes of build failures.

    ![Build Summary dialog box](/help/implementing/cloud-manager/release-notes/assets/build-summary.png)
-->


## Program för tidig användning {#early-adoption}

Delta i Cloud Manager Tidiga Adobe-program och få exklusiv tillgång till kommande funktioner innan de släpps.

Följande tidiga möjligheter för användare finns för närvarande:

### Lägg till Edge Delivery Config Pipeline {#add-eds-pipeline}

Config Pipelines stöds nu för sajter som byggts med Edge Delivery Services, vilket ger fler möjligheter än bara Cloud Service-miljöer. Du kan använda **Konfigurera pipelines** för att hantera inställningar som trafikfiltreringsregler och konfigurationer för WAF (Web Application Firewall), där det är tillämpligt. Se [Konfigurationer som stöds](/help/operations/config-pipeline.md#configurations).

![Lägg till Edge Delivery-pipeline i listrutan Lägg till pipeline](/help/implementing/cloud-manager/release-notes/assets/add-edge-delivery-pipeline.png)

Om du är intresserad av att testa den här nya funktionen och dela med dig av dina synpunkter skickar du ett e-postmeddelande till [grp-aemeds-config-pipeline-adopter@adobe.com](mailto:grp-aemeds-config-pipeline-adopter@adobe.com) från den e-postadress som är kopplad till din Adobe ID.

### Ta med din egen Git - nu med stöd för Azure DevOps {#gitlab-bitbucket-azure-vsts}

<!-- BOTH CS & AMS -->

Kunderna kan nu lägga in sina Azure DevOps Git-databaser i Cloud Manager, med stöd för både moderna Azure DevOps-databaser och äldre VSTS-databaser (Visual Studio Team Services).

* För Edge Delivery Services-användare kan den inbyggda databasen användas för att synkronisera och distribuera platskod.
* För AEM as a Cloud Service- och Adobe Managed Services-användare (AMS) kan databasen länkas till både fullständiga och frontbaserade pipelines.

Stöd för fler pipelinetyper och pull-begäran-validering via pipelines för kodkvalitet kommer snart.

Se [Lägg till externa databaser i Cloud Manager](/help/implementing/cloud-manager/managing-code/external-repositories.md).

![Dialogrutan Lägg till databas](/help/implementing/cloud-manager/release-notes/assets/azure-repo.png)

Om du är intresserad av att testa den här nya funktionen och dela med dig av dina synpunkter skickar du ett e-postmeddelande till [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com) från den e-postadress som är kopplad till din Adobe ID. Ta med vilken Git-plattform du vill använda och om du har en privat/offentlig eller företagsdatabasstruktur.

#### Vanliga frågor och svar om hur du tar med din egen Git

| Fråga | Svar |
|---|---|
| *Hur kan ett projekt vid behov växla tillbaka till den Adobe-hanterade Git-databasen?* | Det är enkelt att byta tillbaka. [Uppdatera pipelines](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md) så att de pekar på Adobe-databasen och tar bort den externa databasen om den inte längre behövs. |
| *Går det att konfigurera olika databaser för olika miljöer (till exempel icke-produktion kontra produktion) så att testning i icke-produktion först tillåts?* | Ja, olika databaser kan konfigureras för olika miljöer. Utvecklings- eller kodkvalitetsflödet kan till exempel peka på en extern databas medan produktionsflödet är anslutet till Adobe-databasen. Kontrollera att synkroniseringsjobbet mellan de två databaserna förblir aktivt under den här konfigurationen. |
| *Fortsätter befintliga inställningar som IP tillåtelselista att fungera?* | Ja, befintlig IP-tillåtelselista fortsätter att fungera som vanligt. Om den externa Git-databasen skyddas av en brandvägg måste de nödvändiga [Adobe IP-adresserna läggas till i tillåtelselista](/help/implementing/cloud-manager/ip-allow-lists/introduction.md). |
| *Fungerar alla URL:er för GitLab-databasen? Databas-URL:en som används har formatet `https://gitlab_dedicated_url.com/path/repo-name.git`, vilket skiljer sig från exemplet i dokumentationen.* | Ja, alla GitLab-databaser som har stöd för API V3 eller V4 stöds, inklusive GitLab-URL:er som de som finns som värd, som den som beskrivs i [Lägg till externa databaser i Cloud Manager](/help/implementing/cloud-manager/managing-code/external-repositories.md) (`https://git-vendor-name.com/org-name/repo-name.git`). |


<!--
## Bug fixes

* Issue

* Issue

* Issue
-->

<!-- ## Known issues {#known-issues} -->

