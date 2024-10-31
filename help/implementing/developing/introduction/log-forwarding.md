---
title: Loggvidarebefordran för AEM as a Cloud Service
description: Läs om hur du vidarebefordrar loggar till loggningsleverantörer i AEM as a Cloud Service
exl-id: 27cdf2e7-192d-4cb2-be7f-8991a72f606d
feature: Developing
role: Admin, Architect, Developer
source-git-commit: f6de6b6636d171b6ab08fdf432249b52c2318c45
workflow-type: tm+mt
source-wordcount: '1781'
ht-degree: 0%

---

# Loggvidarebefordran {#log-forwarding}

>[!NOTE]
>
>Loggvidarebefordran är nu konfigurerat på självbetjäningssätt, vilket skiljer sig från den gamla metoden, som kräver att du skickar en Adobe Support-biljett. Se avsnittet [Migrerar](#legacy-migration) om din vidarebefordran av loggen har konfigurerats av Adobe.

Kunder som har en licens hos en loggningsleverantör eller som är värd för en loggningsprodukt kan få AEM loggar (inklusive Apache/Dispatcher) och CDN-loggar vidarebefordrade till den associerade loggningsdestinationen. AEM as a Cloud Service stöder följande loggningsmål:

* Azure Blob Storage
* Datadog
* Elasticsearch eller OpenSearch
* HTTPS
* Splunk

Loggvidarebefordran konfigureras på ett självbetjäningssätt genom att en konfiguration deklareras i Git och distribueras via Cloud Manager Config Pipeline till typerna RDE, dev, stage och production i produktionsprogram (ej sandbox).

Det finns ett alternativ för att dirigera loggarna AEM och Apache/Dispatcher via AEM avancerad nätverksinfrastruktur, som dedikerad IP-adress för utgångar.

Observera att den nätverksbandbredd som är associerad med loggar som skickas till loggningsmålet räknas som en del av organisationens I/O-användning i nätverket.


## Hur den här artikeln ordnas {#how-organized}

Den här artikeln är organiserad på följande sätt:

* Inställningar - gemensamma för alla loggningsmål
* Målkonfigurationer för loggning - varje mål har ett något annorlunda format
* Loggpostformat - information om loggpostformat
* Avancerade nätverk - skicka AEM- och Apache/Dispatcher-loggar via en dedikerad utgång eller via ett VPN
* Migrera från äldre vidarebefordran av loggar - gå från vidarebefordran av loggfiler som tidigare konfigurerats av Adobe till självbetjäningsmetoden


## Inställningar {#setup}

1. Skapa en fil med namnet `logForwarding.yaml`. Den ska innehålla metadata, enligt beskrivningen i [config pipeline-artikeln](/help/operations/config-pipeline.md#common-syntax) (**kind** ska anges till `LogForwarding` och versionen ska anges till &quot;1&quot;), med en konfiguration som liknar den nedan (vi använder Splunk som exempel).

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

1. Placera filen någonstans under en mapp på den översta nivån med namnet *config* eller liknande, enligt beskrivningen i [Använda konfigurationsförlopp](/help/operations/config-pipeline.md#folder-structure).

1. För andra miljötyper än RDE (som använder kommandoradsverktyg) kan du skapa en riktad distributionskonfigurationspipeline i Cloud Manager, vilket [det här avsnittet](/help/operations/config-pipeline.md#creating-and-managing) refererar till. Observera att fullständiga stackpipelines och webbskiktspipelines inte distribuerar konfigurationsfilen.

1. Distribuera konfigurationen.

Tokens i konfigurationen (till exempel `${{SPLUNK_TOKEN}}`) representerar hemligheter som inte ska lagras i Git. Deklarera dem i stället som Cloud Manager [Hemliga miljövariabler](/help/operations/config-pipeline.md#secret-env-vars). Välj **Alla** som listvärde för fältet Tjänst används, så att loggarna kan vidarebefordras till författare, publicering och förhandsgranskningsnivåer.

Det går att ange olika värden mellan CDN-loggar och AEM (inklusive Apache/Dispatcher) genom att inkludera ytterligare ett **cdn**- och/eller **aem** -block efter **default** -blocket, där egenskaper kan åsidosätta de som definieras i **default** -blocket. Det krävs bara den aktiverade egenskapen. Ett möjligt användningsexempel kan vara att använda ett annat Splunk-index för CDN-loggar, vilket visas i exemplet nedan.

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

![Azure Blob SAS-tokenkonfiguration](/help/implementing/developing/introduction/assets/azureblob-sas-token-config.png)

Om loggarna inte har levererats efter att de tidigare fungerat korrekt kontrollerar du om den SAS-token som du konfigurerade fortfarande är giltig eftersom den kan ha gått ut.

#### Azure Blob Storage CDN-loggar {#azureblob-cdn}

Var och en av de globalt distribuerade loggningsservrarna skapar en ny fil var sjätte sekund, under mappen `aemcdn`. När filen har skapats läggs den inte längre till. Filnamnsformatet är YYY-MM-DDThh:mm:ss.sss-uniqueid.log. Exempel: 2024-03-04T10:00:00.000-WnFWYN9BpOUs2aOVn4ee.log.

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

Varje fil innehåller flera json-loggposter, var och en på en separat rad. Loggpostformaten beskrivs under [Loggning för AEM as a Cloud Service](/help/implementing/developing/introduction/logging.md) och varje loggpost innehåller även de ytterligare egenskaper som anges i avsnittet [Loggpostformat](#log-format) nedan.

#### Loggar för Azure Blob Storage-AEM {#azureblob-aem}

AEM (inklusive Apache/Dispatcher) visas under en mapp med följande namnkonvention:

* aemaccess
* aemerror
* aemrequest
* aemdispatcher
* aemhttpdaccess
* aemhttpderror

Under varje mapp skapas en enda fil och läggs till i den. Kunderna ansvarar för att bearbeta och hantera den här filen så att den inte växer för stor.

Se loggpostformaten under [Loggning för AEM as a Cloud Service](/help/implementing/developing/introduction/logging.md). Loggposterna innehåller även de ytterligare egenskaper som nämns i avsnittet [Loggpostformat](#log-formats) nedan.


### Datadog {#datadog}

```
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  datadog:
    default:
      enabled: true       
      host: "http-intake.logs.datadoghq.eu"
      token: "${{DATADOG_API_KEY}}"
      tags:
         tag1: value1
         tag2: value2
      
```

Att tänka på:

* Skapa en API-nyckel, utan någon integrering med en viss molnleverantör.
* Taggegenskapen är valfri
* För AEM loggar är datakälltaggen för DataDig inställd på något av `aemaccess`, `aemerror`, `aemrequest`, `aemdispatcher`, `aemhttpdaccess` eller `aemhttpderror`
* För CDN-loggar är datakällkoden `aemcdn` angiven för Datadog
* Datadoggens servicemärke är inställd på `adobeaemcloud`, men du kan skriva över den i taggavsnittet
* Om din pipeline för dataöverföring använder datadaggar för att fastställa lämpligt index för vidarebefordringsloggar kontrollerar du att dessa taggar är korrekt konfigurerade i YAML-filen för loggvidarebefordran. Taggar som saknas kan förhindra att loggen kan tas in om pipeline är beroende av dem.



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
      pipeline: "ingest pipeline name"
```

Att tänka på:

* Som standard är porten 443. Den kan åsidosättas med en egenskap med namnet `port`
* För autentiseringsuppgifter måste du använda distributionsuppgifter i stället för kontoautentiseringsuppgifter. Detta är de autentiseringsuppgifter som genereras på en skärm som kan likna den här bilden:

![Elastic deployment credentials](/help/implementing/developing/introduction/assets/ec-creds.png)

* För AEM loggar är `index` inställt på något av `aemaccess`, `aemerror`, `aemrequest`, `aemdispatcher`, `aemhttpdaccess` eller `aemhttpderror`
* Den valfria pipeline-egenskapen ska anges till namnet på importflödet för Elasticsearch eller OpenSearch, som kan konfigureras för att dirigera loggposten till rätt index. Pipelinens processortyp måste anges till *script* och skriptspråket ska anges till *smärtfritt*. Här följer ett exempel på ett skriptfragment som dirigerar loggposter till ett index som aemaccess_dev_26_06_2024:

```
def envType = ctx.aem_env_type != null ? ctx.aem_env_type : 'unknown';
def sourceType = ctx._index;
def date = new SimpleDateFormat('dd_MM_yyyy').format(new Date());
ctx._index = sourceType + "_" + envType + "_" + date;
```

### HTTPS {#https}

```
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  https:
    default:
      enabled: true
      url: "https://example.com/aem_logs/aem"
      authHeaderName: "X-AEMaaCS-Log-Forwarding-Token"
      authHeaderValue: "${{HTTPS_LOG_FORWARDING_TOKEN}}"
```

Att tänka på:

* URL-strängen måste innehålla **https://**, annars misslyckas valideringen.
* URL:en kan innehålla en port. Exempel: `https://example.com:8443/aem_logs/aem`. Om ingen port ingår i URL-strängen antas port 443 (standard-HTTPS-port).

#### HTTPS CDN-loggar {#https-cdn}

Webbförfrågningar (POST) skickas kontinuerligt, med en JSON-nyttolast som är en matris med loggposter, med loggpostformatet som beskrivs under [Loggning för AEM as a Cloud Service](/help/implementing/developing/introduction/logging.md#cdn-log). Ytterligare egenskaper anges i avsnittet [Loggpostformat](#log-formats) nedan.

Det finns också en egenskap med namnet `sourcetype` som är inställd på värdet `aemcdn`.

>[!NOTE]
>
> Innan den första CDN-loggposten skickas måste HTTP-servern slutföra en engångskontroll: en begäran som skickas till sökvägen ``/.well-known/fastly/logging/challenge`` måste svara med en asterisk ``*`` i brödtexten och 200-statuskoden.

#### HTTPS-AEM {#https-aem}

För AEM (inklusive apache/disacher) skickas webbförfrågningar (POST) kontinuerligt, med en JSON-nyttolast som är en matris med loggposter, med de olika loggpostformaten som beskrivs under [Loggning för AEM as a Cloud Service](/help/implementing/developing/introduction/logging.md). Ytterligare egenskaper anges i avsnittet [Loggpostformat](#log-format) nedan.

Det finns också en egenskap med namnet `Source-Type` som är inställd på något av följande värden:

* aemaccess
* aemerror
* aemrequest
* aemdispatcher
* aemhttpdaccess
* aemhttpderror

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
      index: "aemaacs"
```

Att tänka på:

* Som standard är porten 443. Den kan åsidosättas med en egenskap med namnet `port`.
* Källtypsfältet kommer att ha ett av följande värden, beroende på den specifika loggen: *aemaccess*, *aemerror*,
  *aemrequest*, *aemdispatcher*, *aemhttpdaccess*, *aemhttpderror*, *aemcdn*
* Om de nödvändiga IP-adresserna har tillåtslista och loggarna fortfarande inte levereras kontrollerar du att det inte finns några brandväggsregler som tvingar verifiering av skräpposttoken. Utför snabbt ett inledande valideringssteg där en ogiltig Splunk-token skickas avsiktligt. Om brandväggen är inställd på att avsluta anslutningar med ogiltiga Splunk-tokens, kommer valideringsprocessen att misslyckas, vilket förhindrar att loggar levereras till Splunk-instansen.


>[!NOTE]
>
> [Om du migrerar](#legacy-migration) från äldre loggvidarebefordran till den här självbetjäningsmodellen kan värdena i fältet `sourcetype` som skickas till ditt Splunk-index ha ändrats, så justera därefter.


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

Se [Loggning för AEM as a Cloud Service](/help/implementing/developing/introduction/logging.md) för formatet för respektive loggtyp (CDN-loggar och AEM loggar inklusive Apache/Dispatcher).

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

Vissa organisationer väljer att begränsa vilken trafik som kan tas emot av loggningsdestinationerna.

För CDN-loggen kan du tillåta att IP-adresserna listas enligt beskrivningen i [Snabbt dokumentation - offentlig IP-lista](https://www.fastly.com/documentation/reference/api/utils/public-ip-list/). Om listan med delade IP-adresser är för stor kan du skicka trafik till en https-server eller (ej Adobe) Azure Blob Store där logik kan skrivas för att skicka ut loggarna från en känd IP-server till den slutliga målplatsen.

Om du har konfigurerat [avancerat nätverk](/help/security/configuring-advanced-networking.md) för AEM (inklusive Apache/Dispatcher) kan du använda egenskapen advancedNetworking för att vidarebefordra dem från en dedikerad IP-adress eller via ett VPN.

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
      port: 443
      token: "${{SPLUNK_TOKEN}}"
      index: "aemaacs"
    aem:
      advancedNetworking: true
```

## Migrerar från äldre loggvidarebefordran {#legacy-migration}

Innan konfigurationen av loggvidarebefordran gjordes via en självbetjäningsmodell ombads kunderna att öppna supportärenden, där Adobe initierade integreringen.

Kunder som har konfigurerats på det sättet av Adobe får gärna anpassa sig till självbetjäningsmodellen när det passar. Det finns flera skäl till att göra den här övergången:

* En ny miljö (t.ex. en ny dev-miljö eller RDE) har etablerats.
* Ändrar din befintliga Splunk-slutpunkt eller autentiseringsuppgifter.
* Adobe hade konfigurerat vidarebefordran av loggar innan CDN-loggarna var tillgängliga och du vill få CDN-loggar.
* Ett medvetet beslut att aktivt anpassa sig till den självbetjäningsmodellen så att organisationen har kunskapen redan innan en tidskänslig förändring är nödvändig.

När du är redo att migrera konfigurerar du bara YAML-filen enligt beskrivningen i de föregående avsnitten. Använd Cloud Manager konfigurationsflöde för att distribuera till var och en av de miljöer där konfigurationen ska användas.

Vi rekommenderar, men behöver inte göra det, att en konfiguration distribueras till alla miljöer så att de alla styrs av självbetjäning. Annars kanske du glömmer vilka miljöer som har konfigurerats av Adobe jämfört med de som konfigurerats på ett självbetjäningssätt.

>[!NOTE]
>
>Värdena för fältet `sourcetype` som skickades till ditt Splunk-index kan ha ändrats, så justera därefter.

>[!NOTE]
>
>När loggvidarebefordran distribueras till en miljö som tidigare konfigurerats av Adobe support kan du få dubblettloggar i upp till några timmar. Detta kommer till slut att matchas automatiskt.

