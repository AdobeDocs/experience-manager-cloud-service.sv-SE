---
title: Loggvidarebefordran för AEM as a Cloud Service
description: Läs mer om vidarebefordran av loggar till Splunk och andra loggningsleverantörer på AEM as a Cloud Service
hide: true
hidefromtoc: true
source-git-commit: d41390696383f8e430bb31bd8d56a5e8843f1257
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 0%

---


# Loggvidarebefordran {#log-forwarding}

>[!NOTE]
>
>Den här funktionen har inte släppts ännu och vissa loggningsmål är kanske inte tillgängliga vid tidpunkten för lanseringen. Under tiden kan du öppna en supportanmälan och vidarebefordra loggar till **Splunk**, enligt beskrivningen i [loggningsartikel](/help/implementing/developing/introduction/logging.md).

Kunder som har en licens för en loggningsleverantör eller värd för en loggningsprodukt kan få AEM, Apache/Dispatcher och CDN-loggar vidarebefordrade till associerade loggningsmål. AEM as a Cloud Service stöder följande loggningsmål:

* Azure Blob Storage
* DataDog
* Elasticsearch eller OpenSearch
* HTTPS
* Splunk

Loggvidarebefordran konfigureras på ett självbetjäningssätt genom att en konfiguration deklareras i Git och distribueras via Cloud Manager Configuration Pipeline till dev-, stage- och produktionsmiljötyper i produktionsprogram (ej sandlådeprogram).

Observera att den nätverksbandbredd som är associerad med loggar som skickas till loggningsmålet räknas som en del av organisationens I/O-användning i nätverket.


## Hur den här artikeln ordnas {#how-organized}

Den här artikeln är organiserad på följande sätt:

* Inställningar - gemensamma för alla loggningsmål
* Målkonfigurationer för loggning - varje mål har ett något annorlunda format
* Avancerade nätverk - skicka AEM- och Apache/Dispatcher-loggar via en dedikerad utgång eller via ett VPN


## Inställningar {#setup}

1. Skapa följande mapp- och filstruktur i den översta mappen i ditt projekt i Git:

   ```
   config/
        logForwarding.yaml
   ```

1. logForwarding.yaml ska innehålla metadata och en konfiguration som liknar följande format (Splunk används som exempel).

   ```
   kind: "LogForwarding"
   version: "1"
   metadata:
     envTypes: ["dev"]
   data:
     splunk:
       default:
         enabled: true
         host: "splunk-host.example.com"
         token: "${{SPLUNK_TOKEN}}"
         index: "AEMaaCS"
   ```

   Standardnoden måste inkluderas av framtida kompatibilitetsskäl.

   Parametern kind ska anges till LogForwarding. Versionen ska anges till schemaversionen, som är 1.

   Token i konfigurationen (t.ex. `${{SPLUNK_TOKEN}}`) representerar hemligheter, som inte bör lagras i Git. Deklarera dem som Cloud Manager i stället  [Miljövariabler](/help/implementing/cloud-manager/environment-variables.md) av typen &quot;hemlighet&quot;. Se till att markera **Alla** som listvärde för fältet Service Applied, så att loggarna kan vidarebefordras till författare, publicering och förhandsgranskning.

1. För andra miljötyper än RDE (som för närvarande inte stöds) skapar du en riktad distributionskonfigurationspipeline i Cloud Manager.

   * [Se konfigurera produktionspipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md).
   * [Se konfigurera icke-produktionspipelinor](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md).

## Konfiguration för loggningsmål {#logging-destinations}

Konfigurationer för loggningsmål som stöds listas nedan tillsammans med eventuella särskilda överväganden.

### Azure Blob Storage {#azureblob}

```
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  azureBlob:
    default:
      enabled: true       
      storageAccountName: "example_acc"
      container: "aem_logs"
      sasToken: "${{AZURE_BLOB_SAS_TOKEN}}
      
```

Att tänka på:

* Autentisera med SAS-token, som ska ha en minimilängd för validering.
* SAS-token ska skapas på kontosidan, inte på behållarsidan.

### Datadog {#datadog}

```
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  dataDog:
    default:
      enabled: true       
      host: "http-intake.logs.datadoghq.eu"
      token: "${{DATADOG_API_KEY}}"
      
```

Att tänka på:

* Skapa en API-nyckel, utan någon integrering med en viss molnleverantör.


### Elasticsearch och OpenSearch {#elastic}

```
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  elasticsearch:
    default:
      enabled: true
      host: "example.com"
      user: "${{ELASTICSEARCH_USER}}"
      password: "${{ELASTICSEARCH_PASSWORD}}"
```

Att tänka på:

* För autentiseringsuppgifter måste du använda distributionsuppgifter i stället för kontoautentiseringsuppgifter. Detta är de autentiseringsuppgifter som genereras på en skärm som kan likna den här bilden:

![Elastiska autentiseringsuppgifter för distribution](/help/implementing/developing/introduction/assets/ec-creds.png)

### HTTPS {#https}

```
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  https:
    default:
      url: "https://example.com/aem_logs/aem"
      authHeaderName: "X-AEMaaCS-Log-Forwarding-Token"
      authHeaderValue: "${{HTTPS_LOG_FORWARDING_TOKEN}}"
```

### Splunk {#splunk}

```
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  splunk:
    default:
      enabled: true
      host: "splunk-host.example.com"
      token: "${{SPLUNK_TOKEN}}"
      index: "AEMaaCS"
```

<!--
### Sumo Logic {#sumologic}

   ```
   kind: "LogForwarding"
   version: "1"
   metadata:
     envTypes: ["dev"]
   data:
     splunk:
       default:
         enabled: true
         host: "https://collectors.de.sumologic.com"
         uri: "/receiver/v1/http"
         privateKey: "${{SomeOtherToken}}"
   
   ```   
-->

## Avancerat nätverksbyggande {#advanced-networking}

Om du har organisatoriska krav för att låsa trafiken till loggningsmålet kan du konfigurera vidarebefordran av loggen så att du [avancerat nätverk](/help/security/configuring-advanced-networking.md). Se mönstren för de tre avancerade nätverkstyperna nedan, som använder en valfri `port` -parametern tillsammans med `host` parameter.

### Flexibla portägg {#flex-port}

Om loggtrafiken går till en annan port än 443 (t.ex. 8443 nedan) ska du konfigurera avancerade nätverk så här:

```
{
    "portForwards": [
        {
            "name": "mylogging.service.logger.com",
            "portDest": 8443, # something other than 443
            "portOrig": 30443
        }    
    ]
}
```

och konfigurera bildspelsfilen så här:

```
kind: "LogForwarding"
version: "1"
data:
  splunk:
    default:
      host: "proxy.tunnel"
      token: "${{SomeToken}}"
      port: 30443
      index: "index_name"
```

### Dedikerad egress-IP {#dedicated-egress}

Om loggtrafiken behöver komma ut från en dedikerad IP-adress kan du konfigurera avancerade nätverk så här:

```
{
    "portForwards": [
        {
            "name": "mylogging.service.com",
            "portDest": 443, # something other than 443
            "portOrig": 30443
        }    
    ]
}
```

och konfigurera bildspelsfilen så här:

```
kind: "LogForwarding"
version: "1"
data:
  splunk:
    default:
      host: "proxy.tunnel"
      token: "${{SomeToken}}"
      port: 30443
      index: "index_name"
```

### VPN {#vpn}

Om loggtrafiken behöver gå via ett VPN-nätverk kan du konfigurera avancerade nätverk så här:

```
{
    "portForwards": [
        {
            "name": "mylogging.service.com",
            "portDest": 443, # something other than 443
            "portOrig": 30443
        }    
    ]
}
```

och konfigurera bildspelsfilen så här:

```
kind: "LogForwarding"
version: "1"
data:
  splunk:
    default:
      host: "mylogging.service.com"
      token: "${{SomeToken}}"
      port: 30443
      index: "index_name"
```
