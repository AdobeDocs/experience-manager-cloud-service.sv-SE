---
title: Loggvidarebefordran för AEM as a Cloud Service
description: Läs om hur du vidarebefordrar loggar till loggningsleverantörer i AEM as a Cloud Service
exl-id: 27cdf2e7-192d-4cb2-be7f-8991a72f606d
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2478'
ht-degree: 0%

---

# Loggvidarebefordran {#log-forwarding}

>[!NOTE]
>
>Loggvidarebefordran är nu konfigurerat på självbetjäningssätt, vilket skiljer sig från den gamla metoden, som kräver att en Adobe Support-biljett skickas. Se avsnittet [Migrerar](#legacy-migration) om din vidarebefordran av loggen har konfigurerats av Adobe.

Kunder som har en licens hos en loggningsleverantör eller som är värd för en loggningsprodukt kan få AEM-loggar (inklusive Apache/Dispatcher) och CDN-loggar vidarebefordrade till det associerade loggningsmålet. AEM as a Cloud Service stöder följande loggningsmål:

<table>
  <tbody>
    <tr>
      <th>Loggteknik</th>
      <th>AEM</th>
      <th>Dispatcher</th>
      <th>CDN</th>
    </tr>
    <tr>
      <td>Amazon S3</td>
      <td>Ja</td>
      <td>Ja</td>
      <td style="background-color: #ffb3b3;">Framtidens</td>
    </tr>
    <tr>
      <td>Azure Blob Storage</td>
      <td>Ja</td>
      <td>Ja</td>
      <td>Ja</td>
    </tr>
    <tr>
      <td>DataDog</td>
      <td>Ja</td>
      <td>Ja</td>
      <td>Ja</td>
    </tr>
    <tr>
      <td>Dynatrace</td>
      <td>Ja</td>
      <td>Ja</td>
      <td style="background-color: #ffb3b3;">Framtidens</td>
    </tr>
    <tr>
      <td>Elasticsearch<br>OpenSearch</td>
      <td>Ja</td>
      <td>Ja</td>
      <td>Ja</td>
    </tr>
    <tr>
      <td>HTTPS</td>
      <td>Ja</td>
      <td>Ja</td>
      <td>Ja</td>
    </tr>
    <tr>
      <td>New Relic</td>
      <td>Ja</td>
      <td>Ja</td>
      <td style="background-color: #ffb3b3;">Framtidens</td>
    </tr>
    <tr>
      <td>Splunk</td>
      <td>Ja</td>
      <td>Ja</td>
      <td>Ja</td>
    </tr>
    <tr>
      <td>Sumologik</td>
      <td>Ja</td>
      <td>Ja</td>
      <td style="background-color: #ffb3b3;">Framtidens</td>
    </tr>
  </tbody>
</table>

>[!NOTE]
>
> Kommande CDN-loggtekniker planeras för framtiden. Skicka e-post till [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) för att registrera intresse.

Vidarebefordran av loggar konfigureras på ett självbetjäningssätt genom att en konfiguration deklareras i Git och kan distribueras via Cloud Manager konfigurationspipelines för utvecklings-, scen- och produktionsmiljötyper. Konfigurationsfilen kan distribueras till Rapid Development Environment (RDE) med kommandoradsverktyg.

Det finns ett alternativ för att dirigera loggarna för AEM och Apache/Dispatcher via AEM avancerade nätverksinfrastruktur, till exempel dedikerad IP-adress för utgångar.

Observera att den nätverksbandbredd som är associerad med loggar som skickas till loggningsmålet räknas som en del av organisationens I/O-användning i nätverket.

## Hur den här artikeln ordnas {#how-organized}

Den här artikeln är organiserad på följande sätt:

* Inställningar - gemensamma för alla loggningsmål
* Transport och avancerat nätverk - hänsyn bör tas till nätverksinställningarna innan loggningskonfigurationen skapas
* Målkonfigurationer för loggning - varje mål har ett något annorlunda format
* Loggpostformat - information om loggpostformat
* Migrera från äldre vidarebefordring av loggar - gå från vidarebefordran av loggfiler som tidigare konfigurerats av Adobe till självbetjäning

## Inställningar {#setup}

1. Skapa en fil med namnet `logForwarding.yaml`. Den ska innehålla metadata, enligt beskrivningen i artikeln [Configuration Pipeline](/help/operations/config-pipeline.md#common-syntax) (**kind** ska anges till `LogForwarding` och versionen ska anges till &quot;1&quot;), med en konfiguration som liknar den nedan (vi använder Splunk som exempel).

   ```yaml
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

Det går att ange olika värden mellan CDN-loggar och AEM-loggar (inklusive Apache/Dispatcher) genom att inkludera ytterligare ett **cdn**- och/eller **aem** -block efter **default** -blocket, där egenskaper kan åsidosätta dem som definieras i **default** -blocket; endast den aktiverade egenskapen krävs. Ett möjligt användningsexempel kan vara att använda ett annat Splunk-index för CDN-loggar, vilket visas i exemplet nedan.

```yaml
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

Ett annat scenario är att inaktivera vidarebefordran av CDN-loggar eller AEM-loggar (inklusive Apache/Dispatcher). Om du till exempel bara vill vidarebefordra CDN-loggarna kan du konfigurera följande:

```yaml
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

## Transport och avancerat nätverk {#transport-advancednetworking}

Vissa organisationer väljer att begränsa vilken trafik som kan tas emot av loggningsdestinationerna, andra kanske behöver använda andra portar än HTTPS (443).  I så fall måste [Avancerat nätverk](/help/security/configuring-advanced-networking.md) konfigureras innan konfigurationen för vidarebefordran av loggar distribueras.

Använd tabellen nedan för att se vad som krävs för konfigurationen av avancerat nätverk och loggning baserat på om du använder port 443 eller inte och om du behöver visa loggarna från en fast IP-adress eller inte.

<table>
  <tbody>
    <tr>
      <th>Målport</th>
      <th>Vill du att loggar ska visas från fast IP?</th>
      <th>Avancerat nätverksarbete krävs</th>
      <th>LogForwarding.yaml-portdefinition krävs</th>
    </tr>
    <tr>
      <td rowspan="2" ro>HTTPS (443)</td>
      <td>Nej</td>
      <td>Nej</td>
      <td>Nej</td>
    </tr>
    <tr>
      <td>Ja</td>
      <td>Ja, <a href="/help/security/configuring-advanced-networking.md#dedicated-egress-ip-address-dedicated-egress-ip-address">Dedikerad klänning</a></td>
      <td>Nej</td>
    <tr>
    <tr>
      <td rowspan="2">Ej standardport (t.ex. 8088)</td>
      <td>Nej</td>
      <td>Ja, <a href="/help/security/configuring-advanced-networking.md#flexible-port-egress-flexible-port-egress">Flexibel utskrift</a></td>
      <td>Ja</td>
    </tr>
    <tr>
      <td>Ja</td>
      <td>Ja, <a href="/help/security/configuring-advanced-networking.md#dedicated-egress-ip-address-dedicated-egress-ip-address">Dedikerad klänning</a></td>
      <td>Ja</td>
  </tbody>
</table>

>[!NOTE]
>Om loggarna visas från en enda IP-adress avgörs av ditt val av avancerad nätverkskonfiguration.  Dedikerade urkor måste användas för att underlätta detta.
>
> Den avancerade nätverkskonfigurationen är en [tvåstegsprocess](/help/security/configuring-advanced-networking.md#configuring-and-enabling-advanced-networking-configuring-enabling) som kräver aktivering på program- och miljönivå.

Om du har konfigurerat [Avancerat nätverk](/help/security/configuring-advanced-networking.md) för AEM-loggar (inklusive Apache/Dispatcher) kan du använda egenskapen `aem.advancedNetworking` för att vidarebefordra dem från en dedikerad IP-adress eller via ett VPN.

I exemplet nedan visas hur du konfigurerar loggning på en vanlig HTTPS-port med avancerade nätverk.

```yaml
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

För CDN-loggar kan du tillåta att IP-adresserna listas enligt beskrivningen i [Snabbt dokumentation - offentlig IP-lista](https://www.fastly.com/documentation/reference/api/utils/public-ip-list/). Om listan med delade IP-adresser är för stor kan du skicka trafik till en https-server eller (ej Adobe) Azure Blob Store där logik kan skrivas för att skicka ut loggarna från en känd IP-adress till deras slutliga mål.

>[!NOTE]
>
>Det går inte att visa CDN-loggar från samma IP-adress som dina AEM-loggar kommer från. Det beror på att loggarna skickas direkt från Fast och inte från AEM Cloud Service.
>
>Därför går det inte att använda loggvidarebefordran med VPN-konfigurationer för avancerade nätverk.

## Konfiguration för loggningsmål {#logging-destinations}

Konfigurationer för loggningsmål som stöds listas nedan tillsammans med eventuella särskilda överväganden.

### Amazon S3 {#amazons3}

Loggvidarebefordran till Amazon S3 stöder AEM- och Dispatcher-loggar, CDN-loggar stöds ännu inte.

>[!NOTE]
>
>Loggar som skrivs till S3 periodvis, var 10:e minut för varje loggfilstyp.  Detta kan resultera i en inledande fördröjning för loggar som skrivs till S3 när funktionen har växlats.  [Mer information om detta beteende](https://docs.fluentbit.io/manual/pipeline/outputs/s3#differences-between-s3-and-other-fluent-bit-outputs).

```yaml
kind: "LogForwarding"
version: "1.0"
metadata:
  envTypes: ["dev"]
data:
  awsS3:
    default:
      enabled: true
      region: "your-bucket-region"
      bucket: "your_bucket_name"
      accessKey: "${{AWS_S3_ACCESS_KEY}}"
      secretAccessKey: "${{AWS_S3_SECRET_ACCESS_KEY}}"
```

Om du vill använda S3 Log Forwarder måste du förkonfigurera en AWS IAM-användare med lämplig profil för att få åtkomst till S3-bucket.  Se [AWS IAM-användardokumentation](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html) om du vill veta mer om hur du skapar IAM-användarautentiseringsuppgifter.

IAM-principen bör tillåta användaren att använda `s3:putObject`.  Till exempel:

```json
 {
    "Version": "2012-10-17",
    "Statement": [{
        "Effect": "Allow",
        "Action": [
            "s3:PutObject"
        ],
        "Resource": "arn:aws:s3:::your_bucket_name/*"
    }]
}
```

Mer information om hur du implementerar finns i [AWS Bucket Policy Documentation](https://docs.aws.amazon.com/AmazonS3/latest/userguide/bucket-policies.html).

>[!NOTE]
>Stöd för CDN-logg för AWS S3 planeras för framtiden. Skicka ett e-postmeddelande till [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) om du vill registrera intresse.

### Azure Blob Storage {#azureblob}

```yaml
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

```text
aemcdn/
   2024-03-04T10:00:00.000-abc.log
   2024-03-04T10:00:00.000-def.log
```

Och sedan 30 sekunder:

```text
aemcdn/
   2024-03-04T10:00:00.000-abc.log
   2024-03-04T10:00:00.000-def.log
   2024-03-04T10:00:30.000-ghi.log
   2024-03-04T10:00:30.000-jkl.log
   2024-03-04T10:00:30.000-mno.log
```

Varje fil innehåller flera json-loggposter, var och en på en separat rad. Loggpostformaten beskrivs under [Loggning för AEM as a Cloud Service](/help/implementing/developing/introduction/logging.md) och varje loggpost innehåller även de ytterligare egenskaper som anges i avsnittet [Loggpostformat](#log-formats) nedan.

#### Azure Blob Storage AEM-loggar {#azureblob-aem}

AEM-loggar (inklusive Apache/Dispatcher) visas under en mapp med följande namnkonvention:

* aemaccess
* aemerror
* aemrequest
* aemdispatcher
* aemhttpdaccess
* aemhttpderror

Under varje mapp skapas en enda fil och läggs till i den. Kunderna ansvarar för att bearbeta och hantera den här filen så att den inte växer för stor.

Se loggpostformaten under [Loggning för AEM as a Cloud Service](/help/implementing/developing/introduction/logging.md). Loggposterna innehåller även de ytterligare egenskaper som nämns i avsnittet [Loggpostformat](#log-formats) nedan.

### Datadog {#datadog}

```yaml
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

#### Överväganden

* Skapa en API-nyckel, utan någon integrering med en viss molnleverantör.
* Taggegenskapen är valfri
* För AEM-loggar anges datakälltaggen för DataDig till någon av `aemaccess`, `aemerror`, `aemrequest`, `aemdispatcher`, `aemhttpdaccess` eller `aemhttpderror`
* För CDN-loggar är datakällkoden `aemcdn` angiven för Datadog
* Datadoggens servicemärke är inställd på `adobeaemcloud`, men du kan skriva över den i taggavsnittet
* Om din pipeline för dataöverföring använder datadaggar för att fastställa lämpligt index för vidarebefordringsloggar kontrollerar du att dessa taggar är korrekt konfigurerade i YAML-filen för loggvidarebefordran. Taggar som saknas kan förhindra att loggen kan tas in om pipeline är beroende av dem.

### Elasticsearch och OpenSearch {#elastic}

```yaml
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

#### Överväganden

* Som standard är porten 443. Den kan åsidosättas med en egenskap med namnet `port`
* För autentiseringsuppgifter måste du använda distributionsuppgifter i stället för kontoautentiseringsuppgifter. Detta är de autentiseringsuppgifter som genereras på en skärm som kan likna den här bilden:

![Elastic deployment credentials](/help/implementing/developing/introduction/assets/ec-creds.png)

* För AEM-loggar är `index` inställt på något av `aemaccess`, `aemerror`, `aemrequest`, `aemdispatcher`, `aemhttpdaccess` eller `aemhttpderror`
* Den valfria pipeline-egenskapen ska anges till namnet på Elasticsearch- eller OpenSearch-importflödet, som kan konfigureras för att dirigera loggposten till lämpligt index. Pipelinens processortyp måste anges till *script* och skriptspråket ska anges till *smärtfritt*. Här följer ett exempel på ett skriptfragment som dirigerar loggposter till ett index som aemaccess_dev_26_06_2024:

```text
def envType = ctx.aem_env_type != null ? ctx.aem_env_type : 'unknown';
def sourceType = ctx._index;
def date = new SimpleDateFormat('dd_MM_yyyy').format(new Date());
ctx._index = sourceType + "_" + envType + "_" + date;
```

### HTTPS {#https}

```yaml
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

#### Överväganden

* URL-strängen måste innehålla **https://**, annars misslyckas valideringen.
* URL:en kan innehålla en port. Exempel: `https://example.com:8443/aem_logs/aem`. Om ingen port ingår i URL-strängen antas port 443 (standard-HTTPS-port).

#### HTTPS CDN-loggar {#https-cdn}

Webbförfrågningar (POST) skickas kontinuerligt, med en JSON-nyttolast som är en matris med loggposter, med loggpostformatet som beskrivs under [Loggning för AEM as a Cloud Service](/help/implementing/developing/introduction/logging.md#cdn-log). Ytterligare egenskaper anges i avsnittet [Loggpostformat](#log-formats) nedan.

Det finns också en egenskap med namnet `sourcetype` som är inställd på värdet `aemcdn`.

>[!NOTE]
>
> Innan den första CDN-loggposten skickas måste HTTP-servern slutföra en engångskontroll: en begäran som skickas till sökvägen ``/.well-known/fastly/logging/challenge`` måste svara med en asterisk ``*`` i brödtexten och 200-statuskoden.

#### HTTPS AEM-loggar {#https-aem}

För AEM-loggar (inklusive apache/disacher) skickas webbförfrågningar (POST) kontinuerligt, med en JSON-nyttolast som är en matris med loggposter, med de olika loggpostformaten som beskrivs under [Loggning för AEM as a Cloud Service](/help/implementing/developing/introduction/logging.md). Ytterligare egenskaper anges i avsnittet [Loggpostformat](#log-formats) nedan.

Det finns också en egenskap med namnet `Source-Type` som är inställd på något av följande värden:

* aemaccess
* aemerror
* aemrequest
* aemdispatcher
* aemhttpdaccess
* aemhttpderror

### New Relic Log API {#newrelic-https}

Logga vidarebefordran till New Relic använder New Relic HTTPS API för förtäring.  För närvarande stöder den endast loggar från AEM och Dispatcher. CDN-loggar stöds ännu inte.

```yaml
  kind: "LogForwarding"
  version: "1"
  metadata:
    envTypes: ["dev"]
  data:
    newRelic:
      default:
        enabled: true
        uri: "https://log-api.newrelic.com/log/v1"
        apiKey: "${{NR_API_KEY}}"
```

>[!NOTE]
>
>Loggvidarebefordran till New Relic är endast tillgängligt för kundägda New Relic-konton.
>
>Stöd för CDN-logg för New Relic Log API planeras för framtiden. Skicka ett e-postmeddelande till [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) om du vill registrera intresse.
>
>New Relic tillhandahåller regionspecifika slutpunkter baserat på var ditt New Relic-konto är etablerat.  Mer information finns i [New Relic-dokumentationen](https://docs.newrelic.com/docs/logs/log-api/introduction-log-api/#endpoint).

### Dynatrace Log API {#dynatrace-https}

Logga vidarebefordran till Dynatrace använder Dynatrace HTTPS API för förtäring.  För närvarande stöder den endast loggar från AEM och Dispatcher. CDN-loggar stöds ännu inte.

Scope-attributet &quot;Ingest Logs&quot; krävs för token.

```yaml
  kind: "LogForwarding"
  version: "1"
  metadata:
    envTypes: ["dev"]
  data:
    dynatrace:
      default:
        enabled: true
        environmentId: "${{DYNATRACE_ENVID}}"
        token: "${{DYNATRACE_TOKEN}}"  
```

>[!NOTE]
>Stöd för CDN-logg för Dynatrace Log API planeras för framtiden. Skicka ett e-postmeddelande till [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) om du vill registrera intresse.

### Splunk {#splunk}

```yaml
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

#### Överväganden

* Som standard är porten 443. Den kan åsidosättas med en egenskap med namnet `port`.
* Källtypsfältet kommer att ha ett av följande värden, beroende på den specifika loggen: *aemaccess*, *aemerror*,
  *aemrequest*, *aemdispatcher*, *aemhttpdaccess*, *aemhttpderror*, *aemcdn*
* Om de nödvändiga IP-adresserna har tillåtslista och loggarna fortfarande inte levereras kontrollerar du att det inte finns några brandväggsregler som tvingar verifiering av skräpposttoken. Utför snabbt ett inledande valideringssteg där en ogiltig Splunk-token skickas avsiktligt. Om brandväggen är inställd på att avsluta anslutningar med ogiltiga Splunk-tokens, kommer valideringsprocessen att misslyckas, vilket förhindrar att loggar levereras till Splunk-instansen.

>[!NOTE]
>
> [Om du migrerar](#legacy-migration) från äldre loggvidarebefordran till den här självbetjäningsmodellen kan värdena i fältet `sourcetype` som skickas till ditt Splunk-index ha ändrats, så justera därefter.

### Sumologik {#sumologic}

Loggvidarebefordran till Sumo Logic stöder AEM- och Dispatcher-loggar. CDN-loggar stöds ännu inte.

När du konfigurerar Sumo Logic för datainmatning visas en&quot;HTTP Source Address&quot; som tillhandahåller värddatorn, receiverURI och den privata nyckeln i en enda sträng.  Till exempel:

`https://collectors.de.sumologic.com/receiver/v1/http/ZaVnC...`

Du måste kopiera det sista avsnittet i URL:en (utan föregående `/`) och lägga till det som en [&#x200B; CloudManager-miljövariabel](/help/operations/config-pipeline.md#secret-env-vars) enligt beskrivningen i avsnittet [&#x200B; Konfigurera](#setup) ovan, och sedan referera till variabeln i konfigurationen.  Ett exempel ges nedan.

```yaml
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  sumoLogic:
    default:
      enabled: true
      collectorURL: "https://collectors.de.sumologic.com/receiver/v1/http"
      privateKey: "${{SUMOLOGIC_PRIVATE_KEY}}"
      index: "aem-logs"
```

>[!NOTE]
>Stöd för CDN-logg för SumoLogic planeras för framtiden. Skicka ett e-postmeddelande till [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) om du vill registrera intresse.
>
> Du måste ha en Sumo Logic Enterprise-prenumeration för att kunna utnyttja funktionen för indexfält.  Loggarna för icke-företagsprenumerationer dirigeras till partitionen `sumologic_default` som standard.  Mer information finns i [Dokumentation för sumologisk partitionering](https://help.sumologic.com/docs/search/optimize-search-partitions/).

## Loggpostformat {#log-formats}

Se [Loggning för AEM as a Cloud Service](/help/implementing/developing/introduction/logging.md) för formatet för respektive loggtyp (CDN-loggar och AEM-loggar inklusive Apache/Dispatcher).

Eftersom loggar från flera program och miljöer kan vidarebefordras till samma loggningsmål, förutom de utdata som beskrivs i loggningsartikeln, kommer följande egenskaper att finnas i varje loggpost:

* aem_env_id
* aem_env_type
* aem_program_id
* aem_tier

Egenskaperna kan till exempel ha följande värden:

```text
aem_env_id: 1242
aem_env_type: dev
aem_program_id: 12314
aem_tier: author
```

## Migrerar från äldre loggvidarebefordran {#legacy-migration}

Innan konfigurationen av loggvidarebefordran gjordes via en självbetjäningsmodell ombads kunderna att öppna supportärenden, där Adobe initierade integreringen.

Kunder som har konfigurerats på detta sätt av Adobe får gärna anpassa sig till självbetjäningsmodellen när det passar. Det finns flera skäl till att göra den här övergången:

* En ny miljö (t.ex. en ny dev-miljö eller RDE) har etablerats.
* Ändrar din befintliga Splunk-slutpunkt eller autentiseringsuppgifter.
* Adobe konfigurerade din loggvidarebefordran innan CDN-loggar var tillgängliga och du vill få CDN-loggar.
* Ett medvetet beslut att aktivt anpassa sig till den självbetjäningsmodellen så att organisationen har kunskapen redan innan en tidskänslig förändring är nödvändig.

När du är redo att migrera konfigurerar du bara YAML-filen enligt beskrivningen i de föregående avsnitten. Använd Cloud Manager konfigurationsflöde för att distribuera till var och en av de miljöer där konfigurationen ska användas.

Vi rekommenderar, men behöver inte göra det, att en konfiguration distribueras till alla miljöer så att de alla styrs av självbetjäning. Annars kanske du glömmer vilka miljöer som har konfigurerats av Adobe jämfört med de som konfigurerats på ett självbetjäningssätt.

>[!NOTE]
>
>Värdena för fältet `sourcetype` som skickades till ditt Splunk-index kan ha ändrats, så justera därefter.
>
>När loggvidarebefordran distribueras till en miljö som tidigare konfigurerats av Adobe support kan du få dubblettloggar i upp till några timmar. Detta kommer till slut att matchas automatiskt.
