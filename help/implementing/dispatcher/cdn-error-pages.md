---
title: Konfigurera CDN-felsidor
description: Lär dig hur du åsidosätter standardfelsidan genom att lagra statiska filer i värdbaserat lagringsutrymme som Amazon S3 eller Azure Blob Storage, och referera till dem i en konfigurationsfil som distribueras med Cloud Manager Configuration Pipeline.
feature: Dispatcher
source-git-commit: 11036c3e95f0444fc5d865232a7dccab5b7f26ae
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 0%

---


# Konfigurera CDN-felsidor {#cdn-error-pages}

>[!NOTE]
>Den här funktionen är ännu inte allmänt tillgänglig. Om du vill gå med i programmet för tidig adopter skickar du e-post `aemcs-cdn-config-adopter@adobe.com` och beskriva hur ni använder er.

Om det osannolika skulle inträffa [CDN som hanteras av Adobe](/help/implementing/dispatcher/cdn.md#aem-managed-cdn) kan inte nå AEM. CDN är som standard en unik felsida som anger att servern inte kan nås. Du kan åsidosätta standardfelsidan genom att lagra statiska filer i värdbaserat lagringsutrymme som Amazon S3 eller Azure Blob Storage och referera till dem i en konfigurationsfil som distribueras med [Konfigurationspipeline för Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#config-deployment-pipeline).

## Inställningar {#setup}

Innan du kan åsidosätta standardfelsidan måste du göra följande:

* Skapa först den här mapp- och filstrukturen i den översta mappen i Git-projektet:

```
config/
     cdn.yaml
```

* För det andra `cdn.yaml` konfigurationsfilen ska innehålla metadata och felsidans referenser, enligt beskrivningen nedan.

### Konfiguration {#configuration}

Felsidan implementeras som ett program med en sida (SPA) och refererar till en handfull egenskaper, vilket visas i exemplet nedan.  De statiska filer som URL-adresserna refererar till bör lagras hos dig på en Internettillgänglig tjänst som Amazon S3 eller Azure Blob Storage.

Konfigurationsexempel:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  experimental_errorPages:
    spa:
      title: the error page
      icoUrl: https://www.example.com/error.ico
      cssUrl: https://www.example.com/error.css
      jsUrl: https://www.example.com/error.js
```

| Namn | Tillåtna egenskaper | Betydelse |
|-----------|--------------------------|-------------|
| **spa** | title | Felsidans titel. |
|     | icoUrl | URL till en ikonfil. |
|     | cssUrl | URL till en CSS-fil. |
|     | jsUrl | URL till en JavaScript-fil. |

### Sample Generated HTML {#sample-generated-html}

Den HTML-kod som genereras av CDN och skickas till klienten, t.ex. en webbläsare, liknar (men är inte identisk med) följande kodutdrag:

```
<!DOCTYPE html>
<html lang="en">
    <head>
        ...
        <title>the error page</title>
        <link rel="icon" href="https://www.example.com/error.ico">
        <link rel="stylesheet" href="https://www.example.com/error.css">
    </head>
    <body>
        ...
        <div id="root" status="403"></div>
        <script src="https://www.example.com/error.js"> </script>
    </body>
</html>
```

### Testning {#testing}

I testsyfte anropar du den dedikerade slutpunkten med den felkod som stöds, till exempel:

```
curl "https://publish-pXXXXX-eXXXXXX.adobeaemcloud.com/cdnstatus?code=403"
```

Följande koder stöds: 403, 404, 406, 500 och 503.

På så sätt utlöser du CDN:ens felhanterare direkt för att testa det syntetiska svaret för den angivna felkoden.
