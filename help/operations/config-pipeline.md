---
title: Använda konfigurationsförlopp
description: Lär dig hur du kan använda konfigurationspipelines för att distribuera olika konfigurationer av AEM as a Cloud Service, t.ex. inställningar för vidarebefordran av loggar, rensningsrelaterade underhållsåtgärder och olika CDN-konfigurationer.
feature: Operations
role: Admin
source-git-commit: 3a10a0b8c89581d97af1a3c69f1236382aa85db0
workflow-type: tm+mt
source-wordcount: '978'
ht-degree: 0%

---


# Använda konfigurationsförlopp {#config-pipelines}

Lär dig hur du kan använda konfigurationspipelines för att distribuera olika konfigurationer av AEM as a Cloud Service, t.ex. inställningar för vidarebefordran av loggar, rensningsrelaterade underhållsåtgärder och olika CDN-konfigurationer.

## Ökning {#overview}

En Cloud Manager-konfigurationspipeline distribuerar konfigurationsfiler (skapade i YAML-format) till en målmiljö. Ett antal funktioner i AEM as a Cloud Service kan konfigureras på det här sättet, inklusive loggvidarebefordran, rensningsrelaterade underhållsåtgärder och flera CDN-funktioner.

Konfigurationspipelines kan distribueras via Cloud Manager till olika typer av dev-, stage- och produktionsmiljöer i produktionsprogram (icke-sandlådeprogram). RDE:er stöds inte.

I följande avsnitt i det här dokumentet finns en översikt över viktig information om hur du kan använda Config-pipelines och hur konfigurationer för dem ska struktureras. Här beskrivs allmänna koncept som delas av alla eller en delmängd av de funktioner som stöds av konfigurationspipelines.

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
| [Omdirigeringar på klientsidan](/help/implementing/dispatcher/cdn-configuring-traffic.md#client-side-redirectors) | `CDN` | Deklarera 301/302-liknande omdirigeringar på klientsidan [ (endast tillgängligt för tidiga användare)](/help/release-notes/release-notes-cloud/release-notes-current.md#foundation-early-adopter) |
| [Väljare för ursprung](/help/implementing/dispatcher/cdn-configuring-traffic.md#origin-selectors) | `CDN` | Deklarera regler för att dirigera trafik till olika backend-system, inklusive program utanför Adobe |
| [CDN-felsidor](/help/implementing/dispatcher/cdn-error-pages.md) | `CDN` | Åsidosätt standardfelsidan om AEM inte kan nås och refererar till platsen för statiskt innehåll som lagras automatiskt i konfigurationsfilen |
| [CDN-rensning](/help/implementing/dispatcher/cdn-credentials-authentication.md#purge-API-token) | `CDN` | Deklarera de rensnings-API-nycklar som används för att rensa CDN |
| [Kundhanterad CDN HTTP-token](/help/implementing/dispatcher/cdn-credentials-authentication.md#purge-API-token#CDN-HTTP-value) | `CDN` | Deklarera värdet på den X-AEM-Edge-nyckel som behövs för att anropa Adobe CDN från en kundens CDN |
| [Grundläggande autentisering](/help/implementing/dispatcher/cdn-credentials-authentication.md#purge-API-token#basic-auth) | `CDN` | Deklarera användarnamn och lösenord för en grundläggande dialogruta för autentisering som skyddar vissa URL:er [ (endast tillgängligt för tidig användare)](/help/release-notes/release-notes-cloud/release-notes-current.md#foundation-early-adopter) |
| [Underhållsaktivitet för versionsrensning](/help/operations/maintenance.md#purge-tasks) | `MaintenanceTasks` | Optimera AEM genom att deklarera regler runt när innehållsversioner ska rensas |
| [Granskningslogg Rensa underhållsaktivitet](/help/operations/maintenance.md#purge-tasks) | `MaintenanceTasks` | Optimera AEM granskningslogg för bättre prestanda genom att deklarera regler runt när loggar ska rensas |
| [Loggvidarebefordran](/help/implementing/developing/introduction/log-forwarding.md) | `LogForwarding` | Inte tillgängligt ännu - Konfigurera slutpunkterna och autentiseringsuppgifterna för vidarebefordran av loggar till olika mål (t.ex. Splunk, Datadog, HTTPS) |

## Skapa och hantera konfigurationsförlopp {#creating-and-managing}

Mer information om hur du skapar och konfigurerar rörledningar finns i dokumentet [CI/CD Pipelines.](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#config-deployment-pipeline)

När du skapar en konfigurationspipeline i Cloud Manager måste du välja en **riktad distribution** i stället för **fullständig stackkod** när du konfigurerar pipeline.

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
| `kind` | En sträng som bestämmer vilken typ av konfiguration, t.ex. vidarebefordran av loggar, trafikfilterregler eller begäranomformningar | Obligatoriskt, ingen standard |
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

Mappnamnen och filnamnen under `/config` är godtyckliga. YAML-filen måste dock innehålla ett giltigt [`kind`-egenskapsvärde.](#configurations)

Konfigurationer distribueras vanligtvis till alla miljöer. Om alla egenskapsvärden är identiska för varje miljö räcker det med en YAML-fil. Det är dock vanligt att egenskapsvärden skiljer sig åt mellan olika miljöer, till exempel när en lägre miljö testas.

I följande avsnitt visas några strategier för hur du strukturerar filer.

### En enda konfigurationsfil för alla miljöer {#single-file}

Filstrukturen ser ut ungefär så här:

```text
/config
  cdn.yaml
  logForwarding.yaml
```

Använd den här strukturen när samma konfiguration är tillräcklig för alla miljöer och för alla typer av konfigurationer (CDN, loggvidarebefordran osv.). I det här scenariot skulle matrisegenskapen `envTypes` innehålla alla miljötyper.

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
