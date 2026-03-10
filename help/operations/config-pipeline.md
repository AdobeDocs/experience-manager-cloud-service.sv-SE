---
title: Använd konfigurationsförlopp
description: Lär dig hur du kan använda konfigurationspipelines för att distribuera olika konfigurationer i AEM as a Cloud Service, till exempel inställningar för vidarebefordran av loggfiler, rensningsrelaterade underhållsåtgärder och olika CDN-konfigurationer.
feature: Operations
role: Admin
exl-id: bd121d31-811f-400b-b3b8-04cdee5fe8fa
source-git-commit: 66ea803dbf8e8b12fecf6256a88c94c2ca6fa112
workflow-type: tm+mt
source-wordcount: '1445'
ht-degree: 0%

---

# Använda config pipelines {#config-pipelines}

Lär dig hur du kan använda konfigurationspipelines för att distribuera olika konfigurationer i AEM as a Cloud Service, till exempel inställningar för vidarebefordran av loggfiler, rensningsrelaterade underhållsåtgärder och olika CDN-konfigurationer.

## Ökning {#overview}

En Cloud Manager-konfigurationspipeline distribuerar konfigurationsfiler (skapade i YAML-format) till en målmiljö. Ett antal funktioner i AEM as a Cloud Service kan konfigureras på det här sättet, inklusive loggvidarebefordran, rensningsrelaterade underhållsåtgärder och flera CDN-funktioner.

För **Publicera leveransprojekt** -projekt kan konfigurationspipelines distribueras via Cloud Manager till olika typer av dev-, stage- och produktionsmiljöer. Konfigurationsfilerna kan distribueras till Rapid Development Environment (RDE) med [kommandoradsverktyg](/help/implementing/developing/introduction/rapid-development-environments.md#deploy-config-pipeline). Använd en riktad distribution av typen [**Publish Delivery Pipeline**](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#targeted-deployment) ([Production](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#targeted-deployment) eller [Non-Production](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#targeted-deployment)) när du behöver konfigurera trafik för en domän som är kopplad till en Publish Delivery-miljö.

Konfigurationspipelines kan också distribueras via Cloud Manager för **Edge Delivery** -projekt. Använd en [**Edge Delivery-pipeline**](/help/implementing/cloud-manager/configuring-pipelines/configuring-edge-delivery-pipeline.md) när domänen är kopplad till en **Edge Delivery-webbplats**.

I följande avsnitt i det här dokumentet ges en översikt över viktig information om hur du kan använda konfigureringspipelines och hur konfigurationer för dem ska struktureras. Här beskrivs allmänna koncept som delas av alla eller en delmängd av de funktioner som stöds av konfigurationspipelines.

* [Konfigurationer som stöds](#configurations) - En lista över konfigurationer som kan distribueras med konfigurationspipelines.
* [Skapa och hantera konfigurationspipelines](#creating-and-managing) - Så här skapar du en konfigurationspipeline
* [Vanlig syntax](#common-syntax) - Syntax delad mellan konfigurationer.
* [Mappstruktur](#folder-structure) - Beskriver de strukturkonfigurationströrningar som förväntas för konfigurationerna.
* [Hemliga miljövariabler](#secret-env-vars) - Exempel på hur du använder miljövariabler för att inte avslöja hemligheter i dina konfigurationer.
* [Hemliga pipeline-variabler](#secret-pipeline-vars) - Exempel på hur du använder miljövariabler för att inte avslöja hemligheter i dina konfigurationer före Edge Delivery Services-projekt.

## Konfigurationer som stöds {#configurations}

I följande tabell finns en omfattande lista över sådana konfigurationer med länkar till dedikerad dokumentation som beskriver dess distinkta konfigurationssyntax och annan information.

| Typ | YAML `kind`-värde | Beskrivning | Publicera leverans | Edge Delivery |
|---|---|---|---|---|
| [Trafikfilterregler, inklusive WAF](/help/security/traffic-filter-rules-including-waf.md) | `CDN` | Deklarera regler för att blockera skadlig trafik | X | X |
| [Begär omformningar](/help/implementing/dispatcher/cdn-configuring-traffic.md#request-transformations) | `CDN` | Deklarera regler för att omforma formen på trafikförfrågan | X | X |
| [Svarsomvandlingar](/help/implementing/dispatcher/cdn-configuring-traffic.md#response-transformations) | `CDN` | Deklarera regler för att omforma formen på svaret för en given begäran | X | X |
| [Omdirigeringar på serversidan](/help/implementing/dispatcher/cdn-configuring-traffic.md#server-side-redirectors) | `CDN` | Deklarera 301/302-liknande serversidesomdirigeringar | X | X |
| [Väljare för ursprung](/help/implementing/dispatcher/cdn-configuring-traffic.md#origin-selectors) | `CDN` | Deklarera regler för att dirigera trafik till olika backend-system, inklusive program från andra företag än Adobe | X | X |
| [CDN-felsidor](/help/implementing/dispatcher/cdn-error-pages.md) | `CDN` | Åsidosätt standardfelsidan om det inte går att nå AEM-originalet och referera till platsen för statiskt innehåll som lagras automatiskt i konfigurationsfilen | X |  |
| [CDN-rensning](/help/implementing/dispatcher/cdn-credentials-authentication.md#purge-API-token) | `CDN` | Deklarera de rensnings-API-nycklar som används för att rensa CDN | X |  |
| [Kundhanterad CDN HTTP-token](/help/implementing/dispatcher/cdn-credentials-authentication.md#purge-API-token#CDN-HTTP-value) | `CDN` | Deklarera värdet på den X-AEM-Edge-nyckel som behövs för att anropa Adobe CDN från en kundens CDN | X |  |
| [Grundläggande autentisering](/help/implementing/dispatcher/cdn-credentials-authentication.md#purge-API-token#basic-auth) | `CDN` | Deklarera användarnamn och lösenord för en grundläggande autentiseringsdialogruta som skyddar vissa URL:er. | X | X |
| [Underhållsaktivitet för versionsrensning](/help/operations/maintenance.md#purge-tasks) | `MaintenanceTasks` | Optimera AEM-databasen genom att deklarera regler för när innehållsversioner ska rensas | X |  |
| [Granskningslogg Rensa underhållsaktivitet](/help/operations/maintenance.md#purge-tasks) | `MaintenanceTasks` | Optimera AEM granskningslogg för bättre prestanda genom att ange regler för när loggarna ska rensas | X |  |
| [Underhållsaktivitet för tömning av arbetsflöde](/help/operations/maintenance.md) | `MaintenanceTasks` | Minimera antalet arbetsflödesinstanser för att öka arbetsflödesmotorns prestanda.<br><br>Se även [Regelbunden rensning av arbetsflödesinstanser](/help/sites-cloud/administering/workflows-administering.md#regular-purging-of-workflow-instances) | X |  |
| [Loggvidarebefordran](/help/implementing/developing/introduction/log-forwarding.md) | `LogForwarding` | Konfigurera slutpunkterna och autentiseringsuppgifterna för vidarebefordran av loggar till olika mål, inklusive Azure Blob Storage, DataDig, HTTPS, Elasticsearch, Splunk | X | X |
| [Registrerar ett klient-ID](/help/implementing/developing/open-api-based-apis.md) | `API` | Omvandla Adobe Developer Console API-projekt till en viss AEM-miljö genom att registrera klient-ID:t. Krävs för användning av OpenAPI-baserade API:er som kräver autentisering | X |  |

## Skapa och hantera konfigureringspipelines {#creating-and-managing}

Mer information om hur du skapar och konfigurerar **konfigurationspipelines för publiceringsleverans** finns i [CI/CD-pipelines](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#config-deployment-pipeline). När du skapar en konfigurationspipeline i Cloud Manager måste du välja en **riktad distribution** i stället för **fullständig stackkod** när du konfigurerar pipeline. Som tidigare nämnts distribueras konfigurationen för RDE med [kommandoradsverktyg](/help/implementing/developing/introduction/rapid-development-environments.md#deploy-config-pipeline) i stället för en pipeline.

Mer information om hur du skapar och konfigurerar **Edge Delivery**-konfigurationspipelines finns i artikeln [Lägg till en Edge Delivery-pipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-edge-delivery-pipeline.md) .

## Vanlig syntax {#common-syntax}

Varje konfigurationsfil börjar med egenskaper som liknar följande exempelkodfragment:

```yaml
   kind: "CDN"
   version: "1"
   metadata: ...
   data: ...
```

| Egenskap | Beskrivning | Standard |
|---|---|---|
| `kind` | En sträng som avgör vilken typ av konfiguration, till exempel vidarebefordran av loggfiler, trafikfilterregler eller begäranomvandlingar | Obligatoriskt, ingen standard |
| `version` | En sträng som representerar schemaversionen | Obligatoriskt, ingen standard |
| `metadata` | (Valfritt) Detta innehåller en matris med strängar `envTypes` som avgör för vilka miljötyper konfigurationen bearbetas. För **Publicera leverans** är möjliga värden `dev`, `stage` och `prod`. För **Edge Delivery** ska endast värdet `prod` användas. Om matrisen till exempel bara innehåller `dev` läses konfigurationen inte in i scen- eller produktmiljöer, även om konfigurationen distribueras där. | Alla miljötyper, dvs. (dev, stage, prod) för Publish Delivery eller bara för Edge Delivery. |

Du kan använda verktyget `yq` för att lokalt validera YAML-formateringen av konfigurationsfilen (till exempel `yq cdn.yaml`).

## Publicera leverans {#yamls-for-aem}

**Konfigurationer för publiceringsleverans** distribueras till en målmiljö. När du arbetar i flera miljöer kan du ordna de olika filerna på olika sätt. Om matrisen till exempel bara innehåller `dev` läses konfigurationen inte in i scen- eller produktmiljöer, även om konfigurationen distribueras där.

```yaml
   kind: "CDN"
   version: "1"
   metadata:
    envType: ["dev"]
```

### Mappstruktur {#folder-structure}

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

Mappnamnen och filnamnen under `/config` är godtyckliga. YAML-filen måste dock innehålla ett giltigt [`kind`-egenskapsvärde &#x200B;](#configurations).

Konfigurationer distribueras vanligtvis till alla miljöer. Om alla egenskapsvärden är identiska för varje miljö räcker det med en YAML-fil. Det är dock vanligt att egenskapsvärden skiljer sig åt mellan olika miljöer, till exempel när en lägre miljö testas.

I följande avsnitt visas några strategier för hur du strukturerar filer.

### En enda konfigurationsfil för alla miljöer {#single-file}

Filstrukturen liknar följande:

```text
/config
  cdn.yaml
  logForwarding.yaml
```

Använd den här strukturen när samma konfiguration räcker för alla miljöer och för alla typer av konfigurationer (CDN, loggvidarebefordran osv.). I det här scenariot skulle matrisegenskapen `envTypes` innehålla alla miljötyper.

```yaml
   kind: "CDN"
   version: "1"
   metadata:
     envTypes: ["dev", "stage", "prod"]
```

Med hjälp av miljövariabler av hemlig typ (eller pipeline-variabler) kan [hemliga egenskaper](#secret-env-vars) variera per miljö, vilket visas i följande `${{SPLUNK_TOKEN}}`-referens.

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

Filstrukturen liknar följande:

```text
/config
  cdn-dev.yaml
  cdn-stage.yaml
  cdn-prod.yaml
  logForwarding-dev.yaml
  logForwarding-stage.yaml
  logForwarding-prod.yaml
```

Använd den här strukturen när det kan finnas skillnader i egenskapsvärden. I filerna förväntar man sig att arrayvärdet `envTypes` motsvarar suffixet. Till exempel `cdn-dev.yaml` och `logForwarding-dev.yaml` med värdet `["dev"]`, `cdn-stage.yaml` och `logForwarding-stage.yaml` med värdet `["stage"]` och så vidare.

### En mapp per miljö {#folder-per-env}

I den här strategin finns det en separat `config`-mapp per miljö med en separat pipeline deklarerad i Cloud Manager för varje.

Detta är särskilt användbart om du har flera utvecklingsmiljöer där varje miljö har unika egenskapsvärden.

Filstrukturen liknar följande:

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

## Edge Delivery Services {#yamls-for-eds}

Edge Delivery config-pipelines har inte separata miljöer för utveckling, staging och produktion. I Publicera leverans-miljöer ändrar du förloppet genom nivåerna dev, stage och prod. En Edge Delivery-konfigurationspipeline tillämpar däremot konfigurationen direkt på alla domänmappningar som är registrerade i Cloud Manager för en Edge Delivery-plats.


Distribuera en enkel filstruktur som:

```text
/config
  cdn.yaml
  logForwarding.yaml
```

Om en regel måste skilja sig åt mellan olika Edge Delivery-webbplatser kan du använda syntaxen *when* för att skilja reglerna från varandra. Observera till exempel att domänen matchar dev.example.com i kodutdraget nedan, som kan särskiljas från domänen `www.example.com`.

```
kind: "CDN"
version: "1"
data:
  trafficFilters:
    rules:
    # Block simple path
    - name: block-path
      when:
        allOf:
          - reqProperty: domain
            equals: "dev.example.com"
          - reqProperty: path
            equals: '/block/me'
      action: block
```

Om du inkluderar metadatafältet *envTypes* bör bara värdet **prod** användas (det går också bra att utelämna metadatafältet envTypes). Endast värdet *publish* ska användas för **tier** reqProperty.

## Hemliga miljövariabler {#secret-env-vars}

Så att känslig information inte behöver lagras i källkontrollen stöder konfigurationsfiler Cloud Manager-miljövariabler av typen **secrets**. För vissa konfigurationer, inklusive vidarebefordran av loggar, är hemliga miljövariabler obligatoriska för vissa egenskaper.

Observera att hemliga miljövariabler används för publiceringsleveransprojekt. Se avsnittet Hemliga rörvariabler för Edge Delivery Services-projekt.

Följande kodutdrag är ett exempel på hur den hemliga miljövariabeln `${{SPLUNK_TOKEN}}` används i konfigurationen.

```
kind: "LogForwarding"
version: "1"
data:
  splunk:
    default:
      enabled: true
      host: "splunk-host.example.com"
      token: "${{SPLUNK_TOKEN}}"
      index: "AEMaaCS"
```

Mer information om hur du använder miljövariabler finns i [Cloud Manager miljövariabler](/help/implementing/cloud-manager/environment-variables.md).

## Hemliga pipeline-variabler {#secret-pipeline-vars}

Använd Cloud Manager pipeline-variabler av typen **secrets** för Edge Delivery Services Projects så att känslig information inte behöver lagras i källkontrollen. *Använd*-valrutan bör använda alternativet **distribuera**.

Syntaxen är identisk med fragmentet som visades i föregående avsnitt.

Mer information om hur du använder pipeline-variabler finns i [Förloppsvariabler i Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md).
