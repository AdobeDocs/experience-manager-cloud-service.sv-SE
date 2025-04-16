---
title: Använda konfigurationsförlopp
description: Lär dig hur du kan använda konfigurationspipelines för att distribuera olika konfigurationer av AEM as a Cloud Service, t.ex. inställningar för vidarebefordran av loggar, rensningsrelaterade underhållsåtgärder och olika CDN-konfigurationer.
feature: Operations
role: Admin
exl-id: bd121d31-811f-400b-b3b8-04cdee5fe8fa
source-git-commit: 0b4ed7a99400bb5f91f513bbcd01862cdced03c5
workflow-type: tm+mt
source-wordcount: '991'
ht-degree: 0%

---

# Använda konfigurationsförlopp {#config-pipelines}

Lär dig hur du kan använda konfigurationspipelines för att distribuera olika konfigurationer av AEM as a Cloud Service, t.ex. inställningar för vidarebefordran av loggar, rensningsrelaterade underhållsåtgärder och olika CDN-konfigurationer.

## Ökning {#overview}

En Cloud Manager-konfigurationspipeline distribuerar konfigurationsfiler (skapade i YAML-format) till en målmiljö. Ett antal funktioner i AEM as a Cloud Service kan konfigureras på det här sättet, inklusive loggvidarebefordran, rensningsrelaterade underhållsåtgärder och flera CDN-funktioner.

Konfigurationspipelines kan distribueras via Cloud Manager till olika typer av dev-, stage- och produktionsmiljöer. Konfigurationsfilerna kan distribueras till Rapid Development Environment (RDE) med [kommandoradsverktyg](/help/implementing/developing/introduction/rapid-development-environments.md#deploy-config-pipeline).

I följande avsnitt i det här dokumentet ges en översikt över viktig information om hur du kan använda konfigureringspipelines och hur konfigurationer för dem ska struktureras. Här beskrivs allmänna koncept som delas av alla eller en delmängd av de funktioner som stöds av konfigurationspipelines.

* [Konfigurationer som stöds](#configurations) - En lista över konfigurationer som kan distribueras med konfigurationspipelines
* [Skapar och hanterar konfigurationsförgreningar](#creating-and-managing) - Så här skapar du en konfigurationsförlopp.
* [Vanlig syntax](#common-syntax) - Syntax delad mellan konfigurationer
* [Mappstruktur](#folder-structure) - Beskriver de strukturkonfigurationströrningar som förväntas för konfigurationerna
* [Hemliga miljövariabler](#secret-env-vars) - Exempel på hur du använder miljövariabler för att inte avslöja hemligheter i dina konfigurationer

## Konfigurationer som stöds {#configurations}

I följande tabell finns en omfattande lista över sådana konfigurationer med länkar till dedikerad dokumentation som beskriver dess distinkta konfigurationssyntax och annan information.

| Typ | YAML `kind`-värde | Beskrivning |
|---|---|---|
| [Trafikfilterregler, inklusive WAF](/help/security/traffic-filter-rules-including-waf.md) | `CDN` | Deklarera regler för att blockera skadlig trafik |
| [Begär omformningar](/help/implementing/dispatcher/cdn-configuring-traffic.md#request-transformations) | `CDN` | Deklarera regler för att omforma formen på trafikförfrågan |
| [Svarsomvandlingar](/help/implementing/dispatcher/cdn-configuring-traffic.md#response-transformations) | `CDN` | Deklarera regler för att omforma formen på svaret för en given begäran |
| [Omdirigeringar på serversidan](/help/implementing/dispatcher/cdn-configuring-traffic.md#server-side-redirectors) | `CDN` | Deklarera 301/302-liknande serversidesomdirigeringar |
| [Väljare för ursprung](/help/implementing/dispatcher/cdn-configuring-traffic.md#origin-selectors) | `CDN` | Deklarera regler för att dirigera trafik till olika backend-system, inklusive program från andra företag än Adobe |
| [CDN-felsidor](/help/implementing/dispatcher/cdn-error-pages.md) | `CDN` | Åsidosätt standardfelsidan om det inte går att nå AEM-originalet och referera till platsen för statiskt innehåll som lagras automatiskt i konfigurationsfilen |
| [CDN-rensning](/help/implementing/dispatcher/cdn-credentials-authentication.md#purge-API-token) | `CDN` | Deklarera de rensnings-API-nycklar som används för att rensa CDN |
| [Kundhanterad CDN HTTP-token](/help/implementing/dispatcher/cdn-credentials-authentication.md#purge-API-token#CDN-HTTP-value) | `CDN` | Deklarera värdet på den X-AEM-Edge-nyckel som behövs för att anropa Adobe CDN från en kundens CDN |
| [Grundläggande autentisering](/help/implementing/dispatcher/cdn-credentials-authentication.md#purge-API-token#basic-auth) | `CDN` | Deklarera användarnamn och lösenord för en grundläggande autentiseringsdialogruta som skyddar vissa URL:er. |
| [Underhållsaktivitet för versionsrensning](/help/operations/maintenance.md#purge-tasks) | `MaintenanceTasks` | Optimera AEM-databasen genom att deklarera regler för när innehållsversioner ska rensas |
| [Granskningslogg Rensa underhållsaktivitet](/help/operations/maintenance.md#purge-tasks) | `MaintenanceTasks` | Optimera AEM granskningslogg för bättre prestanda genom att ange regler för när loggarna ska rensas |
| [Loggvidarebefordran](/help/implementing/developing/introduction/log-forwarding.md) | `LogForwarding` | Konfigurera slutpunkterna och autentiseringsuppgifterna för vidarebefordran av loggar till olika mål, inklusive Azure Blob Storage, DataDig, HTTPS, Elasticsearch, Splunk) |

## Skapa och hantera konfigurationsförlopp {#creating-and-managing}

Mer information om hur du skapar och konfigurerar pipelines finns i [CI/CD-pipelines](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#config-deployment-pipeline).

När du skapar en konfigurationspipeline i Cloud Manager måste du välja en **riktad distribution** i stället för **fullständig stackkod** när du konfigurerar pipeline.

Som tidigare nämnts distribueras konfigurationen för RDE med [kommandoradsverktyg](/help/implementing/developing/introduction/rapid-development-environments.md#deploy-config-pipeline) i stället för en pipeline.


## Vanlig syntax {#common-syntax}

Varje konfigurationsfil börjar med egenskaper som liknar följande exempelkodfragment:

```yaml
  kind: "LogForwarding"
  version: "1"
  metadata:
    envTypes: ["dev"]
```

| Egenskap | Beskrivning | Standard |
|---|---|---|
| `kind` | En sträng som avgör vilken typ av konfiguration, till exempel vidarebefordran av loggfiler, trafikfilterregler eller begäranomvandlingar | Obligatoriskt, ingen standard |
| `version` | En sträng som representerar schemaversionen | Obligatoriskt, ingen standard |
| `envTypes` | Den här strängmatrisen är en underordnad egenskap för noden `metadata`. Möjliga värden är dev, stage, prod eller valfri kombination och avgör för vilka miljötyper konfigurationen ska bearbetas. Om matrisen till exempel bara innehåller `dev` läses konfigurationen inte in i scen- eller produktmiljöer, även om konfigurationen distribueras där. | Alla miljötyper (dev, stage, prod) |

Du kan använda verktyget `yq` för att lokalt validera YAML-formateringen av konfigurationsfilen (till exempel `yq cdn.yaml`).

## Mappstruktur {#folder-structure}

En mapp med namnet `/config` eller liknande bör finnas högst upp i trädet, med en eller flera YAML-filer någonstans i ett träd nedanför.

Till exempel:

```text
/config
  cdn.yaml
```

eller

```text
/config
  /dev
    cdn.yaml
```

Mappnamnen och filnamnen under `/config` är godtyckliga. YAML-filen måste dock innehålla ett giltigt [`kind`-egenskapsvärde ](#configurations).

Konfigurationer distribueras vanligtvis till alla miljöer. Om alla egenskapsvärden är identiska för varje miljö räcker det med en YAML-fil. Det är dock vanligt att egenskapsvärden skiljer sig åt mellan olika miljöer, till exempel när en lägre miljö testas.

I följande avsnitt visas några strategier för hur du strukturerar filer.

### En enda konfigurationsfil för alla miljöer {#single-file}

Filstrukturen ser ut ungefär så här:

```text
/config
  cdn.yaml
  logForwarding.yaml
```

Använd den här strukturen när samma konfiguration räcker för alla miljöer och för alla typer av konfigurationer (CDN, loggvidarebefordran osv.). I det här scenariot skulle matrisegenskapen `envTypes` innehålla alla miljötyper.

```yaml
   kind: "cdn"
   version: "1"
   metadata:
     envTypes: ["dev", "stage", "prod"]
```

Om du använder miljövariabler av hemlig typ kan [hemliga egenskaper](#secret-env-vars) variera per miljö, vilket visas i referensen `${{SPLUNK_TOKEN}}`

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

### En separat fil per miljötyp {#file-per-env}

Filstrukturen ser ut ungefär så här:

```text
/config
  cdn-dev.yaml
  cdn-stage.yaml
  cdn-prod.yaml
  logForwarding-dev.yaml
  logForwarding-stage.yaml
  logForwarding-prod.yaml
```

Använd den här strukturen när det kan finnas skillnader i egenskapsvärden. I filerna förväntar man sig att arrayvärdet `envTypes` motsvarar suffixet, till exempel
`cdn-dev.yaml` och `logForwarding-dev.yaml` med värdet `["dev"]`, `cdn-stage.yaml` och `logForwarding-stage.yaml` med värdet `["stage"]` och så vidare.

### En mapp per miljö {#folder-per-env}

I den här strategin finns det en separat `config`-mapp per miljö med en separat pipeline deklarerad i Cloud Manager för varje.

Detta är särskilt användbart om du har flera utvecklingsmiljöer där varje miljö har unika egenskapsvärden.

Filstrukturen ser ut ungefär så här:

```text
/config/dev1
  cdn.yaml
  logForwarding.yaml
/config/dev2
  cdn.yaml
  logForwarding.yaml
/config/prod  
  cdn.yaml
  logForwarding.yaml
```

En variant av detta tillvägagångssätt är att ha en separat gren per miljö.

## Hemliga miljövariabler {#secret-env-vars}

Så att känslig information inte behöver lagras i källkontrollen stöder konfigurationsfiler Cloud Manager-miljövariabler av typen **secrets**. För vissa konfigurationer, inklusive vidarebefordran av loggar, är hemliga miljövariabler obligatoriska för vissa egenskaper.

Utdraget nedan är ett exempel på hur den hemliga miljövariabeln `${{SPLUNK_TOKEN}}` används i konfigurationen.

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

Mer information om hur du använder miljövariabler finns i dokumentet [Cloud Manager-miljövariabler](/help/implementing/cloud-manager/environment-variables.md).
