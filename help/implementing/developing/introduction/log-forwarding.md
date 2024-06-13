---
title: Loggvidarebefordran för AEM as a Cloud Service
description: Läs mer om vidarebefordran av loggar till Splunk och andra loggningsleverantörer på AEM as a Cloud Service
exl-id: 27cdf2e7-192d-4cb2-be7f-8991a72f606d
feature: Developing
role: Admin, Architect, Developer
source-git-commit: e007f2e3713d334787446305872020367169e6a2
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 0%

---

# Loggvidarebefordran {#log-forwarding}

>[!NOTE]
>
>Den här funktionen har inte släppts ännu och vissa loggningsmål är kanske inte tillgängliga vid tidpunkten för lanseringen. Under tiden kan du öppna en supportanmälan och vidarebefordra loggar till **Splunk**, enligt beskrivningen i [loggningsartikel](/help/implementing/developing/introduction/logging.md).

Kunder som har en licens för en loggningsleverantör eller värd för en loggningsprodukt kan ha AEM loggar (inklusive Apache/Dispatcher) och CDN-loggar vidarebefordrade till associerade loggmål. AEM as a Cloud Service stöder följande loggningsmål:

* Azure Blob Storage
* DataDog
* Elasticsearch eller OpenSearch
* HTTPS
* Splunk

Loggvidarebefordran konfigureras på ett självbetjäningssätt genom att en konfiguration deklareras i Git och distribueras via Cloud Manager Configuration Pipeline till dev-, stage- och produktionsmiljötyper i produktionsprogram (ej sandlådeprogram).

Det finns ett alternativ för att dirigera loggarna AEM och Apache/Dispatcher via AEM avancerade nätverksinfrastruktur, som dedikerad IP-adress.

Observera att den nätverksbandbredd som är associerad med loggar som skickas till loggningsmålet räknas som en del av organisationens I/O-användning i nätverket.


## Hur den här artikeln ordnas {#how-organized}

Den här artikeln är organiserad på följande sätt:

* Inställningar - gemensamma för alla loggningsmål
* Målkonfigurationer för loggning - varje mål har ett något annorlunda format
* Loggpostformat - information om loggpostformat
* Avancerade nätverk - skicka AEM- och Apache/Dispatcher-loggar via en dedikerad utgång eller via ett VPN


## Inställningar {#setup}

1. Skapa följande mapp- och filstruktur i den översta mappen i ditt projekt i Git:

   ```
   config/
        logForwarding.yaml
   ```

1. `logForwarding.yaml` ska innehålla metadata och en konfiguration som liknar följande format (Splunk används som exempel).

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

   The **sort** parametern ska anges till `LogForwarding` versionen ska anges till schemaversionen, som är 1.

   Token i konfigurationen (t.ex. `${{SPLUNK_TOKEN}}`) representerar hemligheter, som inte bör lagras i Git. Deklarera dem som Cloud Manager i stället  [Miljövariabler](/help/implementing/cloud-manager/environment-variables.md) av typen **hemlig**. Se till att markera **Alla** som listvärde för fältet Service Applied, så att loggarna kan vidarebefordras till författare, publicering och förhandsgranskning.

   Det går att ange olika värden mellan CDN-loggar och AEM (inklusive Apache/Dispatcher) genom att inkludera ytterligare **cdn** och/eller **aem** -block efter **standard** block, där egenskaper kan åsidosätta de som definieras i **standard** block; endast egenskapen enabled krävs. Ett möjligt användningsexempel kan vara att använda ett annat Splunk-index för CDN-loggar, vilket visas i exemplet nedan.

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
          cdn:
            enabled: true
            token: "${{SPLUNK_TOKEN_CDN}}"
            index: "AEMaaCS_CDN"   
   ```

   Ett annat scenario är att inaktivera vidarebefordran av CDN-loggar eller AEM (inklusive Apache/Dispatcher). Om du till exempel bara vill vidarebefordra CDN-loggarna kan du konfigurera följande:

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
          aem:
            enabled: false
   ```

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

En SAS-token bör användas för autentisering. Den ska skapas från signatursidan för delad åtkomst, i stället för på tokensidan för delad åtkomst, och ska konfigureras med följande inställningar:

* Tillåtna tjänster: Blobb måste väljas.
* Tillåtna resurser: Objektet måste markeras.
* Tillåtna behörigheter: Skriv, Lägg till, Skapa måste vara markerat.
* Ett giltigt start- och förfallodatum/-tid.

Här följer en skärmbild av en exempelkonfiguration för SAS-token:

![Konfiguration av Azure Blob SAS-token](/help/implementing/developing/introduction/assets/azureblob-sas-token-config.png)

#### Azure Blob Storage CDN-loggar {#azureblob-cdn}

Var och en av de globalt distribuerade loggningsservrarna skapar en ny fil var sjätte sekund under `aemcdn` mapp. När filen har skapats läggs den inte längre till. Filnamnsformatet är YYY-MM-DDThh:mm:ss.sss-uniqueid.log. Exempel: 2024-03-04T10:00:00.000-WnFWYN9BpOUs2aOVn4ee.log.

Exempel:

```
aemcdn/
   2024-03-04T10:00:00.000-abc.log
   2024-03-04T10:00:00.000-def.log
```

Och sedan 30 sekunder:

```
aemcdn/
   2024-03-04T10:00:00.000-abc.log
   2024-03-04T10:00:00.000-def.log
   2024-03-04T10:00:30.000-ghi.log
   2024-03-04T10:00:30.000-jkl.log
   2024-03-04T10:00:30.000-mno.log
```

Varje fil innehåller flera json-loggposter, var och en på en separat rad. Loggpostens format beskrivs i [loggningsartikel](/help/implementing/developing/introduction/logging.md), och varje loggpost innehåller också de ytterligare egenskaper som anges i [Loggpostformat](#log-format) nedan.

#### Loggar för Azure Blob Storage-AEM {#azureblob-aem}

AEM (inklusive Apache/Dispatcher) visas under en mapp med följande namnkonvention:

* aemaccess
* aemerror
* aemdispatcher
* httpdaccess
* httpderror

Under varje mapp skapas en enda fil och läggs till i den. Kunderna ansvarar för att bearbeta och hantera den här filen så att den inte växer för stor.

Se loggpostformaten i [loggningsartikel](/help/implementing/developing/introduction/logging.md). Loggposterna kommer även att innehålla de ytterligare egenskaper som anges i [Loggpostformat](#log-formats) nedan.


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

#### HTTPS CDN-loggar {#https-cdn}

Webbförfrågningar (POST) skickas kontinuerligt, med en JSON-nyttolast som är en matris med loggposter, med det loggpostformat som beskrivs i [loggningsartikel](/help/implementing/developing/introduction/logging.md#cdn-log). Ytterligare egenskaper anges i [Loggpostformat](#log-formats) nedan.

Det finns också en egenskap med namnet `sourcetype`, som är inställt på värdet `aemcdn`.

>[!NOTE]
>
> Innan den första posten i CDN-loggen skickas måste HTTP-servern slutföra en engångskontroll: en begäran som skickas till sökvägen ``wellknownpath`` måste svara med ``*``.


#### HTTPS-AEM {#https-aem}

För AEM loggar (inklusive apache/disacher) skickas webbförfrågningar (POST) kontinuerligt, med en json-nyttolast som är en matris av loggposter, med de olika loggpostformaten som beskrivs i [loggningsartikel](/help/implementing/developing/introduction/logging.md). Ytterligare egenskaper anges i [Loggpostformat](#log-format) nedan.

Det finns också en egenskap med namnet `sourcetype`, som är inställt på något av dessa värden:

* aemaccess
* aemerror
* aemdispatcher
* httpdaccess
* httpderror

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

## Loggpostformat {#log-formats}

Se det allmänna [loggningsartikel](/help/implementing/developing/introduction/logging.md) för formatet för varje loggtyp (CDN-loggar och AEM inklusive Apache/Dispatcher).

Eftersom loggar från flera program och miljöer kan vidarebefordras till samma loggningsmål, förutom de utdata som beskrivs i loggningsartikeln, kommer följande egenskaper att finnas i varje loggpost:

* aem_env_id
* aem_env_type
* aem_program_id
* aem_tier

Egenskaperna kan till exempel ha följande värden:

```
aem_env_id: 1242
aem_env_type: dev
aem_program_id: 12314
aem_tier: author
```

## Avancerat nätverksbyggande {#advanced-networking}

>[!NOTE]
>
>Den här funktionen är ännu inte klar för tidiga användare.


Vissa organisationer väljer att begränsa vilken trafik som kan tas emot av loggningsdestinationerna.

För CDN-loggen kan du tillåta att IP-adresserna listas enligt beskrivningen i [den här artikeln](https://www.fastly.com/documentation/reference/api/utils/public-ip-list/). Om listan med delade IP-adresser är för stor kan du skicka trafik till ett (ej Adobe) Azure Blob Store där logik kan skrivas för att skicka ut loggarna från en dedikerad IP-adress till deras slutliga mål.

För AEM (inklusive Apache/Dispatcher) kan du konfigurera vidarebefordran av loggar så att du går igenom [avancerat nätverk](/help/security/configuring-advanced-networking.md). Se mönstren för de tre avancerade nätverkstyperna nedan, som använder en valfri `port` -parametern tillsammans med `host` parameter.

### Flexibla portägg {#flex-port}

Om loggtrafiken går till en annan port än 443 (t.ex. 8443 nedan) ska du konfigurera avancerade nätverk så här:

```
{
    "portForwards": [
        {
            "name": "splunk-host.example.com",
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
      host: "${{AEM_PROXY_HOST}}"
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
            "name": "splunk-host.example.com",
            "portDest": 443, 
            "portOrig": 30443
        }    
    ]
}
```

och konfigurera bildspelsfilen så här:

```
      
kind: "LogForwarding"
version: "1"
   metadata:
     envTypes: ["dev"]
data:
  splunk:
     default:
       enabled: true
       index: "index_name" 
       token: "${{SPLUNK_TOKEN}}"  
     aem:
       enabled: true
       host: "${{AEM_PROXY_HOST}}"
       port: 30443       
     cdn:
       enabled: true
       host: "splunk-host.example.com"
       port: 443    
```

### VPN {#vpn}

Om loggtrafiken behöver gå via ett VPN-nätverk kan du konfigurera avancerade nätverk så här:

```
{
    "portForwards": [
        {
            "name": "splunk-host.example.com",
            "portDest": 443,
            "portOrig": 30443
        }    
    ]
}

kind: "LogForwarding"
version: "1"
   metadata:
     envTypes: ["dev"]
data:
  splunk:
     default:
       enabled: true
       index: "index_name" 
       token: "${{SPLUNK_TOKEN}}"  
     aem:
       enabled: true
       host: "${{AEM_PROXY_HOST}}"
       port: 30443       
     cdn:
       enabled: true
       host: "splunk-host.example.com"
       port: 443     
```
