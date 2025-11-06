---
title: Konfigurera Source
description: Lär dig hur du konfigurerar innehållskällan för din Edge Delivery-webbplats. Använd fstab.yaml med Helix 4-arkitekturen eller använd guiden i Cloud Manager (eller API:t för konfigurationstjänsten) med Helix 5-arkitekturen.
feature: Cloud Manager, Developing
role: Admin, Developer
exl-id: f82eafc0-03d0-4c69-9b28-e769a012531b
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 0%

---

# Konfigurera innehållskällan med ett klick för Edge Delivery Services {#config-content-source}

>[!IMPORTANT]
>
>*Helix* är det interna namnet på den underliggande arkitekturen som driver AEM Sites med dokumentbaserad redigering. Det är inte en funktion eller ett produktnamn. I den här artikeln hänvisar *Helix* till den arkitekturversion som används av dina Edge Delivery Sites. Helix 5 är den nuvarande versionen av den underliggande arkitekturen; Helix 4 är den tidigare versionen.

Adobe Experience Manager (AEM) Edge Delivery Services tillåter innehållsleverans från flera källor, som Google Drive, SharePoint eller AEM, via ett snabbt, globalt distribuerat gränsnätverk.

Innehållskällans konfiguration skiljer sig mellan de två arkitekturversionerna på följande sätt:

| Version | Konfigurationsmetod för innehållskälla |
| --- | --- |
| Helix 4 | YAML-fil (`fstab.yaml`) |
| Helix 5 | Konfigurationstjänstens API (*no`fstab.yaml`*) |

I den här artikeln finns omfattande konfigurationssteg, exempel och valideringsinstruktioner för båda versionerna.

**Innan du börjar**

Om du använder [ett klick i Edge Delivery i Cloud Manager](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md##one-click-edge-delivery-site) använder webbplatsen Helix 5 med en enda databas. [Följ Helix 5-instruktionerna](#config-helix5) och använd den medföljande Helix 4 YAML-versionen av instruktionerna som reserv.

**Bestäm din Helix-version**

* Helix 4 - Ditt projekt innehåller en `fstab.yaml`-fil.
* Helix 5 - Ditt projekt *använder inte* `fstab.yaml` och konfigurerades via [Cloud Manager med hjälp av den guidade guiden](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md) eller API:t.

Bekräfta via databasmetadata eller kontakta administratören om du fortfarande är osäker.

## Konfigurera innehållskällan för Helix 4

I Helix 4 definierar filen `fstab.yaml` platsens innehållskälla. Den här filen finns i roten av GitHub-databasen och mappar URL-sökvägsprefix (kallas monteringspunkter) till externa innehållskällor. Ett typiskt exempel ser ut så här:

```yaml
mountpoints:
  /: https://drive.google.com/drive/folders/your-folder-id
```

Exemplet ovan är endast för illustrationer. Den faktiska URL:en ska peka mot innehållskällan, t.ex. en Google Drive-mapp, SharePoint-katalog eller AEM-sökväg.

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

### Validering

* Klicka på **Förhandsgranska** > **Publicera** > **Testa den publicerade webbplatsen** med AEM Sidekick Chrome Extension.
* Verifiera URL: `https://main--<repo>--<org>.hlx.page/`

## Konfigurera innehållskällan för Helix 5 {#config-helix5}

Helix 5 är svarslös, använder inte `fstab.yaml` och stöder flera platser som delar samma katalog. Konfigurationen hanteras via konfigurationstjänstens API eller användargränssnittet för Edge Delivery Sites. Konfigurationen är platsnivå (inte databasnivå).

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

### Validering

* Klicka på **Förhandsgranska** > **Publicera** > **Testa den publicerade webbplatsen** med AEM Sidekick Chrome Extension.
* Verifiera URL: `https://main--<repo>--<org>.aem.page/`
* (Valfritt) Kontrollera den aktuella konfigurationen via följande `GET` API-anrop:

  ```bash
  GET /api/{program}/{programId}/site/{siteId}
  ```
