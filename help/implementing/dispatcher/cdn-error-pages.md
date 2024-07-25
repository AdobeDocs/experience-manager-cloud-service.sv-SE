---
title: Konfigurera CDN-felsidor
description: Lär dig hur du åsidosätter standardfelsidan genom att lagra statiska filer i värdbaserat lagringsutrymme som Amazon S3 eller Azure Blob Storage, och referera till dem i en konfigurationsfil som distribueras med Cloud Manager konfigurationsflöde.
feature: Dispatcher
exl-id: 1ecc374c-b8ee-41f5-a565-5b36445d3c7c
role: Admin
source-git-commit: 3a10a0b8c89581d97af1a3c69f1236382aa85db0
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 0%

---


# Konfigurera CDN-felsidor {#cdn-error-pages}

Om det osannolika skulle inträffa att det [Adobe-hanterade CDN](/help/implementing/dispatcher/cdn.md#aem-managed-cdn) inte kan nå AEM ursprung, visas som standard en allmän felsida utan varumärke som anger att servern inte kan nås. Du kan åsidosätta standardfelsidan genom att lagra statiska filer i värdbaserat lagringsutrymme som Amazon S3 eller Azure Blob Storage och referera till dem i en konfigurationsfil som distribueras med Cloud Manager [config pipeline.](/help/operations/config-pipeline.md#managing-in-cloud-manager)

## Inställningar {#setup}

Innan du kan åsidosätta standardfelsidan måste du göra följande:

1. Skapa en fil med namnet `cdn.yaml` eller liknande, och referera till syntaxavsnittet nedan.

1. Placera filen någonstans under en mapp på den översta nivån med namnet *config* eller liknande, enligt beskrivningen i [config pipeline-artikeln](/help/operations/config-pipeline.md#folder-structure).

1. Skapa en konfigurationspipeline i Cloud Manager, enligt beskrivningen i [konfigurationspipeline-artikeln](/help/operations/config-pipeline.md#managing-in-cloud-manager).

1. Distribuera konfigurationen.

### Syntax {#syntax}

Felsidan implementeras som ett program med en sida (SPA) och refererar till en handfull egenskaper, vilket visas i exemplet nedan.  De statiska filer som URL-adresserna refererar till bör lagras hos dig på en Internettillgänglig tjänst som Amazon S3 eller Azure Blob Storage.

Konfigurationsexempel:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  errorPages:
    spa:
      title: the error page
      icoUrl: https://www.example.com/error.ico
      cssUrl: https://www.example.com/error.css
      jsUrl: https://www.example.com/error.js
```
En beskrivning av egenskaperna ovanför datanoden finns i artikeln [config pipeline](/help/operations/config-pipeline.md#common-syntax). Egenskapsvärdet för sort ska vara *CDN* och egenskapen `version` ska vara *1*.


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

På så sätt utlöser du CDN:ens felhanterare direkt för att testa det syntetiska svaret för en viss felkod.
