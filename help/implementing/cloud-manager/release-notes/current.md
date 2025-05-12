---
title: Versionsinformation för Cloud Manager 2025.5.0
description: Läs om Cloud Manager 2025.5.0 i Adobe Experience Manager as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: effa19a98d59993e330e925fb933a436ff9d20d7
workflow-type: tm+mt
source-wordcount: '781'
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

### Ändra innehållskällan med ett klick för Edge Delivery Services

Adobe Experience Manager (AEM) Edge Delivery Services tillåter innehållsleverans från flera källor, som Google Drive, SharePoint eller AEM, via ett snabbt, globalt distribuerat gränsnätverk.

Innehållskällans konfiguration skiljer sig åt mellan Helix 4 och Helix 5 på följande sätt:

| Version | Konfigurationsmetod |
| --- | --- |
| Helix 4 | YAML-fil (`fstab.yaml`) |
| Helix 5 | Konfigurationstjänstens API (*no`fstab.yaml`*) |

I den här artikeln finns omfattande konfigurationssteg, exempel och valideringsinstruktioner för båda versionerna.

B **innan du börjar**

Om du använder [en klickning på Edge Delivery i Cloud Manager](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md##one-click-edge-delivery-site) är webbplatsen Helix 5 med en enda databas. Följ Helix 5-instruktionerna och använd den medföljande Helix 4 YAML-versionen som reserv.

**Bestäm din Helix-version**

* Helix 4 - Ditt projekt innehåller en `fstab.yaml`-fil.
* Helix 5 - Ditt projekt *använder inte* `fstab.yaml` och konfigurerades via Edge Delivery Services gränssnitt eller API.

Bekräfta via databasmetadata eller kontakta administratören om du fortfarande är osäker.

#### Konfigurera innehållskällan (Helix 4)

I Helix 4 definieras innehållskällan i en YAML-konfigurationsfil med namnet `fstab.yaml` som finns i GitHub-databasens rot.

##### YAML-filformat

Filen `fstab.yaml` definierar monteringspunkter (URL-sökvägsprefix mappade till innehållskällans URL:er) som i följande exempel (endast i illustrationssyfte):

```yaml
mountpoints:
  /: https://drive.google.com/drive/folders/your-folder-id
```

##### Ändra innehållskällan

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

#### Konfigurera innehållskälla (Helix 5)

Helix 5 är svarslös, använder inte `fstab.yaml` och stöder flera platser som delar samma katalog. Konfigurationen hanteras via konfigurationstjänstens API eller Edge Delivery Services UI. Konfigurationen är platsnivå (inte databasnivå).

##### Konceptskillnader

| Proportioner | Helix 4 | Helix 5 |
| --- | --- | --- |
| Konfigurationsfil | `fstab.yaml` | API- eller gränssnittskonfiguration |
| Monteringspunkter | YAML-definierad | Inte obligatoriskt (implicit rot) |

##### Ändra innehållskällan

Använd API:t för konfigurationstjänsten.

1. Autentisera via en API-nyckel eller åtkomsttoken.
1. Gör följande `PUT` API-anrop:

   ```bash
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

### Lägg till Edge Delivery Pipeline {#add-eds-pipeline}

**Pipelines** stöds nu för webbplatser som byggts med Edge Delivery Services, vilket gör att den här funktionen kan användas även i andra miljöer än Cloud Service. Du kan använda **pipelines** för att hantera inställningar som trafikfiltreringsregler och konfigurationer för WAF (Web Application Firewall), där det är tillämpligt. Se [Konfigurationer som stöds](/help/operations/config-pipeline.md#configurations).

<!-- ![Add Edge Delivery pipeline in Add Pipeline drop-down list](/help/implementing/cloud-manager/release-notes/assets/add-edge-delivery-pipeline.png) -->

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

<!--
## Bug fixes

* Issue

* Issue

* Issue
-->

<!-- ## Known issues {#known-issues} -->

