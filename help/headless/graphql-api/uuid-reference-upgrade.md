---
title: Uppgradera dina innehållsfragment för UUID-referenser
description: Lär dig hur du uppgraderar dina innehållsfragment för optimerade UUID-referenser i Adobe Experience Manager as a Cloud Service för leverans av headless-innehåll.
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
exl-id: 004d1340-8e3a-4e9a-82dc-fa013cea45a7
source-git-commit: f740301df609e534f1ef770921ea9431de17f846
workflow-type: tm+mt
source-wordcount: '1157'
ht-degree: 0%

---

# Uppgradera dina innehållsfragment för UUID-referenser {#upgrade-content-fragments-for-UUID-references}

>[!IMPORTANT]
>
>Olika funktioner i GraphQL API för användning med innehållsfragment är tillgängliga via Tidiga Adobe-program.
>
>Kontrollera [Versionsinformation](/help/release-notes/release-notes-cloud/release-notes-current.md) om du vill se status och hur du tillämpar den om du är intresserad.

För att optimera stabiliteten hos dina GraphQL-filter kan du uppgradera innehålls- och fragmentreferenserna i dina innehållsfragment så att de använder UUID (Universally Unique Identiters).

Ursprungligen tillhandahöll Content Fragment Models datatyperna för **Content Reference** och **Fragment Reference**. Båda dessa referenser använder en sökväg för att peka på den refererade resursen, och den här sökvägen kan bli inaktuell om resursen flyttas. Även om sådana referenser är mer än tillräckliga i de flesta scenarier, har modeller för innehållsfragment utökats så att de även innehåller referenser som baseras på ett UUID:

* **Innehållsreferens (UUID)**
* **Fragmentreferens (UUID)**.

Dessa nya referenstyper kan användas både i nya modeller för innehållsfragment och fragment samt för att utöka befintliga instanser.

Om du vill uppgradera befintliga innehållsfragment och modeller kan du köra proceduren som beskrivs här.

>[!CAUTION]
>
>Innan du kör uppgraderingsproceduren bör du alltid [köra en torr körning](#execute-a-dry-run) för att framhäva eventuella problem med innehållet.

## Vad uppgraderas? {#what-is-upgraded}

Följande uppdateringar görs:

* Fält för datatyperna:
   * **Innehållsreferens** konverteras till **Innehållsreferens (UUID)**
   * **Fragmentreferens** konverteras till **Fragmentreferens (UUID)**
* Värdena för sökvägsbaserade referenser som finns i dessa fält ersätts med motsvarande UUID

>[!NOTE]
>
>Efter uppgraderingen är båda datatyperna fortfarande tillgängliga i modellredigeraren för innehållsfragment. Du kan skapa nya fält baserat på båda typerna (även om du förväntas använda UUID-baserade typer) och köra uppgraderingen igen om det behövs.

## Vad uppgraderas INTE {#what-is-not-upgraded}

Följande referenser har inte uppgraderats:

* Sidreferenser - UUID:n stöds inte ännu
* Alla ogiltiga referenser, till exempel där målet för sökvägen för innehållsfragment eller resurssökvägen inte finns

   * Ogiltiga referenser uppgraderas inte, som om sökvägen för innehållsfragment eller resursen är ogiltig, finns det inget motsvarande UUID att tilldela. Den ursprungliga referensen ändras inte.

   * Använd en [torr körning](#execute-a-dry-run) för att ta bort ogiltiga referenser.

  >[!NOTE]
  >
  >Om de är ogiltiga går de inte att använda, oavsett uppgraderingen.

## När du inte ska uppgradera {#when-you-should-not-upgrade}

Uppgradera inte:

* När något av dina innehållsfragment använder sidreferenser, eftersom UUID ännu inte stöds för sidreferenser

## Begränsningar för UUID-referenser {#limitations-of-uuid-references}

Följande begränsningar gäller för närvarande vid användning av referenser baserade på ett UUID:

* Modeller

   * Det går inte att skapa nya modeller för innehållsfragment med antingen UUID för innehållsfragment eller UUID-fält för innehållsreferens via OpenAPI.
   * Fältet `id` för modeller har inte ändrats till UUID-baserat. Den använder modellens base64-avkodade sökväg. Det går inte att flytta modeller, därför är det här värdet fortfarande stabilt.

* Assets

   * När du skapar ett innehållsfragment via OpenAPI måste fälttyperna `fragment-reference` eller `content-reference` användas för att ange referenser till ett fragment eller en resurs - även när du anger värdet för ett UUID-baserat referensfält.

## Upgrade Planning {#upgrade-planning}

Du måste göra några förberedelser innan du kör uppgraderingen.

### Kör en torr körning {#execute-a-dry-run}

Vi rekommenderar att *varje* gång du uppgraderar ditt innehåll utför du en torr körning. Detta skapar loggfiler med poster som markerar potentiella problem:

* Ogiltiga referenser
* Sidreferenser

Kör innehållsuppgraderingen i `dryRun`-läge för att:

* identifiera ogiltiga referenser genom att lista dem i loggfilerna
Du kan sedan åtgärda dessa referenser innan du kör den faktiska innehållsuppgraderingen.
* identifiera sidreferenser, genom att lista dem i loggfilerna
När sidreferenser upptäcks bör du [inte köra innehållsuppgraderingen](#when-you-should-not-upgrade).


### Tvinga innehåll att frysa {#enforce-a-content-freeze}

Körning av innehållsuppgraderingen ska planeras under en period då innehållet fryser.

Hur länge innehållet fryser beror på den volym innehållsfragment som uppgraderas. Uppgraderingen kan därför variera från några minuter upp till några timmar och beror också på vilka parametrar som används när innehållsuppgraderingen startar.

## Köra innehållsuppgraderingen {#running-the-content-upgrade}

Innehållsuppgraderingen kan hanteras med slutpunkten: `/libs/dam/cfm/maintenance.json`

>[!NOTE]
>
>Ditt konto behöver rollen `Administrator` för att komma åt slutpunkten.

### Starta en innehållsuppgradering {#start-a-content-upgrade}

| Slutpunkt | HTTP-begärantyp | Kommentar |
|--- |--- |--- |
| `/libs/dam/cfm/maintenance.json` | `POST` | |
| **Begär parametrar** | **Värde** | |
| åtgärd | `start` | |
| serviceTypeId | `uuidUpgradeService` | Tjänsttyps-ID (fördefinierat, fast värde). |
|  segmentSize | `1000` | Antalet innehållsfragment eller modeller som ska uppgraderas i ett segment (batch). |
| basePath | `/conf` | Ange antingen:<ul><li>roten `/conf` om du vill uppgradera alla AEM konfigurationer</li><li>en vald AEM konfigurationssökväg. som innehållsuppgraderingen körs för<br>Till exempel: `/conf/wknd-shared` uppgraderar endast en innehavare `wknd-shared`</li></ul> |
| intervall | `10` | Intervall i sekunder efter vilket nästa segment av innehållsfragment eller modeller uppgraderas. |
| läge | `replicate`, `noReplicate` | <ul><li>`replicate`: replikerar samma jobb på alla AEM Publish-instanser</li><li>`noReplicate`: kör bara jobbet AEM författarinstanser</li></ul> |
| dryRun |  `true`, `false` | <ul><li>`false`: simulera innehållsuppgraderingen, utan att spara några innehållsändringar</li><li>`true`: utför innehållsuppgraderingen och sparar innehållsändringar</li></ul> |
| **Svarsinformation** | **Värde** | |
| jobId | `UUID` |  ID:t för det jobb som kör innehållsuppgraderingen.<ul><li>Detta ID krävs i alla efterföljande anrop som rör den här körningen.</li><li>Om värdet `mode` är `replicate` måste körningen AEM Publish-instanser också vara under samma `jobId`.</li></ul> |
| parameters | Parametrarna för innehållsuppgradering | Detta inkluderar de initiala parametrarna som finns för att starta innehållsuppgraderingen och vissa interna standardinställningar. |


### Exempel på begäran om innehållsuppgradering {#example-content-upgrade-request}

+++Begäran

```http
POST http://localhost:4502/libs/dam/cfm/maintenance.json
Content-Type: application/json
Authorization: _REPLACE_WITH_VALID_AUTH_
Accept: application/json
 
{
    "action": "start",
    "serviceTypeId": "uuidUpgradeService",
    "segmentSize": 1000,
    "basePath": "/conf/wknd-shared",
    "interval": 10,
    "mode": "replicate",
    "dryRun": true
}
```

+++

+++svar

```http
HTTP/1.1 200 OK
Date: Wed, 16 Oct 2024 14:34:37 GMT
X-Content-Type-Options: nosniff
X-Frame-Options: SAMEORIGIN
Content-Type: application/json
Content-Length: 386
 
{
  "jobId": "91af43a6-63ff-45e5-ac7b-06ccf565bdfa",
  "jcr:created": 1729089277309,
  "parameters": {
    "mode": "replicate",
    "dryRun": true,
    "segmentSize": 1000,
    "serviceTypeId": "uuidUpgradeService",
    "action": "start",
    "basePath": "/conf/wknd-shared",
    "topic": "cfm/maintenance",
    "interval": 10,
    "cronSchedule": "*/10 * * * * ?"
  }
}
```

+++

### Få status för en innehållsuppgradering {#get-the-status-of-a-content-upgrade}

| Slutpunkt | HTTP-begärantyp | Kommentar |
|--- |--- |--- |
| `/libs/dam/cfm/maintenance.json` | `GET` | |
| **Begär parametrar** | **Värde** | |
| åtgärd | status | |
| jobId | `<UUID>` | `jobId` som returnerades från anropet för att starta innehållsuppgraderingen. |
| **Svarsinformation** | **Värde** | |
| status | JSON-värden | Innehåller detaljerad status för innehållsuppgraderingen:<ul><li>Uppdaterat efter varje intervall (sekunder).</li><li>Körningen av `uuidUpgradeService` har två faser:<ol><li>fas 0 för att uppgradera innehållsfragmentmodeller</li><li>fas 1 för att uppgradera innehållsfragment</li></ol></li><li>I varje fas uppdateras statistiken efter varje intervall.</li><li>&quot;jobStatus&quot;: &quot;COMPLETED&quot; anger att uppgraderingen har slutförts.</li><li>Andra statusvärden är självförklarande.</li></ul> |

### Exempel på begäran om status för innehållsuppgradering {#example-content-upgrade-status-request}

+++Begäran

```http
GET http://localhost:4502/libs/dam/cfm/maintenance.json?action=status&jobId=91af43a6-63ff-45e5-ac7b-06ccf565bdfa
Authorization: _REPLACE_WITH_VALID_AUTH_
Accept: application/json
```

+++

+++svar

```http
HTTP/1.1 200 OK
Date: Wed, 16 Oct 2024 14:35:51 GMT
X-Content-Type-Options: nosniff
X-Frame-Options: SAMEORIGIN
Content-Type: application/json
Content-Length: 1116
 
{
  "jobId": "91af43a6-63ff-45e5-ac7b-06ccf565bdfa",
  "jcr:created": 1729089277309,
  "eventProcessed": 1,
  "parameters": {
    "mode": "replicate",
    "dryRun": true,
    "segmentSize": 1000,
    "serviceTypeId": "uuidUpgradeService",
    "action": "start",
    "confPath": "/conf/wknd-shared",
    "topic": "cfm/uuid-migration",
    "interval": 10,
    "cronSchedule": "*/10 * * * * ?"
  },
  "status": {
    "jobStatus": "COMPLETED",
    "lastModified": 1729089310301,
    "currentPhaseIndex": 1,
    "phases": {
      "phase-0": {
        "bookmark": 1727183332520,
        "stats": {
          "successCount": 2,
          "skippedCount": 1,
          "errorCount": 0
        },
        "name": "modelUpgrade",
        "lastModified": 1729089290040,
        "isCompleted": true
      },
      "phase-1": {
        "bookmark": 1727183347990,
        "stats": {
          "successCount": 29,
          "skippedCount": 0,
          "errorCount": 1
        },
        "name": "cfUpgrade",
        "lastModified": 1729089310298,
        "isCompleted": true
      }
    }
  }
}
```

+++

+++Exempelloggfiler

Förutom statusen för en innehållsuppgradering som körs från HTTP-slutpunkten, innehåller AEM detaljerad information om förloppet på innehållsnivån. Till exempel:

```xml
#Successful model upgrade
com.adobe.cq.dam.cfm.impl.servicing.uuid.* Phase phase-0: resource: /conf/wknd-shared/settings/dam/cfm/models/article , status: SUCCESS, skips: [], errors: []
 
#Successful content fragment upgrade
com.adobe.cq.dam.cfm.impl.servicing.uuid.* Phase phase-1: resource: /content/dam/wknd-shared/en/magazine/san-diego-surf-spots/san-diego-surfspots , status: SUCCESS, skips: [], errors: []
 
#Unsuccessful/Skipped model upgrade
com.adobe.cq.dam.cfm.impl.servicing.uuid.* Phase phase-0: resource: /conf/wknd-shared/settings/dam/cfm/models/adventure , status: SKIPPED, skips: [Model: '/conf/wknd-shared/settings/dam/cfm/models/adventure', no upgradeable fields found], errors: []
 
#Unsuccessful content fragment upgrade
com.adobe.cq.dam.cfm.impl.servicing.uuid.* Phase phase-1: resource: /content/dam/wknd-shared/en/magazine/western-australia/western-australia-by-camper-van , status: FAILED, skips: [], errors: [Path '/content/dam/wknd-shared/en/magazine/western-australia/western-australia-by-camper-van', Variation: 'master' Field 'featuredImage', Value '/content/dam/wknd-shared/en/magazine/western-australia/adobestock_156407519.jpeg' is invalid; will not upgrade this field.] 
```

Efter bearbetningen av varje segment (grupp) av innehållsfragment och modeller loggas dessutom en ackumulerad status som sammanfattar förloppet hittills. Till exempel:

```xml
com.adobe.cq.dam.cfm.impl.servicing.PhaseChainProcessor Phase phase-x, processed a segment, stats: {successCount=29, skippedCount=0, errorCount=1}
```

+++

### Avbryta en innehållsuppgradering {#abort-a-content-upgrade}

>[!CAUTION]
>
>Avbryter en innehållsuppgradering (dvs. inte en torr körning):
>
>* återställer inte ändringar som redan gjorts
>* kan lämna innehållet i ett blandat läge
>
>Använd den här åtgärden med försiktighet.

| Slutpunkt | HTTP-begärantyp | Kommentar |
|--- |--- |--- |
| `/libs/dam/cfm/maintenance.json` | `POST` | |
| **Begär parametrar** | **Värde** | |
| åtgärd | avbryta | |
| jobId | `<UUID>` | `jobId` som returnerades från anropet för att starta innehållsuppgraderingen. |
| **Svarsinformation** | **Värde** | |
| status | JSON-värden | Innehåller detaljerad status för innehållsuppgraderingen:<ul><li>Statusen för anteckningen är &quot;jobStatus&quot;: &quot;ABORTED&quot;.<br>Efter en avbruten åtgärd kommer inga väntande datasegment att bearbetas.</li><li>Om jobStatus är &quot;COMPLETED&quot; före ett avbrott har anropet ingen effekt.</li></ul> |

### Exempel Avbryta en begäran om innehållsuppgradering {#example-abort-content-upgrade-request}

+++Begäran

```http
POST http://localhost:4502/libs/dam/cfm/maintenance.json
Content-Type: application/json
Authorization: Basic YWRtaW46YWRtaW4=
Accept: application/json
 
{
    "action": "abort",
    "jobId": "b1dbf6f9-5f59-4007-b631-01b63cd17807"
    "mode": "replicate",
}
```

+++

+++svar

```http
HTTP/1.1 200 OK
Date: Wed, 16 Oct 2024 14:39:03 GMT
 
{
  "jobId": "b1dbf6f9-5f59-4007-b631-01b63cd17807",
   ...
  "eventProcessed": 2,
  "parameters": {
    ...
    "abort": true,
    ...
  },
  "status": {
     "jobStatus": "ABORTED",
    ...
  }
}
```

+++
