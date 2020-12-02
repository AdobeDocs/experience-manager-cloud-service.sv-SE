---
title: Exempel på ContextHub Store-kandidater
description: ContextHub innehåller flera exempel på arkivkandidater som du kan använda i dina lösningar
translation-type: tm+mt
source-git-commit: c3f69e4b03819fea9a1842a87cad38bd1e485d83
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 1%

---


# Exempel på ContextHub Store-kandidater {#sample-contexthub-store-candidates}

ContextHub innehåller flera exempel på lämpliga lagringskanaler som du kan använda i dina lösningar. Följande information tillhandahålls för varje prov:

* Var du hittar källkoden så att du kan öppna den i utbildningssyfte.
* Så här konfigurerar du de butiker du skapar från butikskandidaterna.
* Hur lagringsdata är strukturerade så att du kan komma åt dem.

>[!WARNING]
>
>Exempelbutikskandidaterna tillhandahålls som referenskonfigurationer som hjälper dig att skapa en egen dedikerad konfiguration för ditt projekt och bör därför inte användas direkt.

## aem.segmentation Sample Store Candidate {#aem-segmentation-sample-store-candidate}

Lagra för lösta och olösta ContextHub-segment. Hämtar automatiskt segment från ContextHub SegmentManager.

### Källplats {#source-location-segmentation}

`/libs/settings/cloudsettings/legacy/contexthub/segmentation`

### Basimplementering {#base-implementation-segmentation}

Förkandidaten för aem.segmentation-arkivet är [`ContextHub.Store.PersistedJSONPStore`](contexthub-api.md#contexthub-store-persistedjsonpstore).

### Konfiguration {#configuration-segmentation}

När du skapar en `aem.segmentation`-butik behöver du inte ange en detaljerad konfiguration. Standardkonfigurationen anger platsen för ContextHub-segmentdefinitionerna.

```xml
{
   "service":{
      "jsonp":false,
      "timeout":1000,
      "path":"/etc/segmentation/contexthub.segment.js"
   }
}
```

## contexthub.geolocation Sample Store Candidate {#contexthub-geolocation-sample-store-candidate}

Exempelarkivkandidaten `contexthub.geolocation` använder Google Maps för att hämta och lagra information om klientplatsen.

### Källplats {#source-location-geolocation}

`/libs/settings/cloudsettings/legacy/contexthub/geolocation`

### Basimplementering {#base-implementation-geolocation}

Butikskandidaten `contexthub.geolocation` utökar [`ContextHub.Store.PersistedJSONPStore`](contexthub-api.md#contexthub-store-persistedjsonpstore).

### Konfiguration {#configuration-geolocation}

Standardkonfigurationen anger information om Google-tjänsten och de inledande latitud- och longitudkoordinaterna.

```javascript
{
        "service": {
            "jsonp": false,
            "timeout": 1000,
            "ttl": 1800000,
            "secure": false,
            "host": "maps.googleapis.com",
            "port": 80,
            "path": "/maps/api/geocode/json"
        },

        "eventDeferring": 16,

        "html5coordinatesDiscoveryAPI": {
            "timeout": 30000,
            "ttl": 900000,
            "highAccuracy": false
        },

        "initialValues": {
            "latitude": 37.331375,
            "longitude": -121.893992
        }
    }
```

### Dataobjekt {#data-items-geolocation}

I butiken används ett dataträd som liknar följande exempel:

```javascript
{
   "latitude":"37.331375",
   "longitude":"-121.893992"
}
```

>[!NOTE]
>
>En säkerhetsprincip som introducerades i Chrome 50.x kräver att alla geopositioneringsrelaterade anrop görs via en skyddad anslutning. AEM tvingar därför även https-användning för API-anrop för geopositionering om AEM körs över https. I annat fall används http för att följa principen om samma ursprung.
>
>Mer information om ändringen i Chrome finns i [det här Google-blogginlägget](https://developers.google.com/web/updates/2016/04/geolocation-on-secure-contexts-only).

## contexthub.surferinfo Sample Store Candidate {#contexthub-surferinfo-sample-store-candidate}

Lagrar information om den aktuella klientmiljön, t.ex. enhet, fönster, webbläsare, datum och tid.

### Källplats {#source-location-surferinfo}

`/libs/settings/cloudsettings/legacy/contexthub/surferinfo`

### Basimplementering {#base-implementation-surferinfo}

Butikskandidaten `contexthub.surferinfo` utökar [`ContextHub.Store.PersistedStore`](contexthub-api.md#contexthub-store-persistedstore).

### Konfiguration {#configuration-surferinfo}

Standardkonfigurationen ärvs från `ContextHub.Store.PersistedStore`.

### Dataobjekt {#data-items-surferinfo}

Lager som använder den här butikskandidaten har ett dataträd som liknar följande exempel:

```javascript
{
   "display":{
      "resolution":{
         "width":1440,
         "height":900
      },
      "devicePixelRatio":1,
      "colorDepth":24,
      "nrOfColors":16777216,
      "pixelsPerInch":96,
      "orientation":{
         "mode":"landscape",
         "direction":"normal"
      }
   },
   "window":{
      "dimension":{
         "width":1395,
         "height":652
      },
      "percentageUsage":0.7
   },
   "browser":{
      "version":"39.0",
      "family":"Firefox",
      "userAgent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10.9; rv:39.0) Gecko/20100101 Firefox/39.0"
   },
   "device":{
      "category":"Desktop",
      "type":"Desktop",
      "model":"PC",
      "version":""
   },
   "isMobile":true,
   "os":{
      "name":"Mac OS X",
      "version":"10"
   },
   "year":2015,
   "month":7,
   "day":22,
   "hour":14,
   "minutes":1
}
```

## granite.emulators Exempelarkivkandidaten {#granite-emulators-sample-store-candidate}

I `granite.emulators`-exempelarkivkandidaten lagras information om klientenheter.

### Källplats {#source-location-emulators}

`/libs/settings/cloudsettings/legacy/contexthub/emulators`

### Basimplementering {#base-implementation-emulators}

Butikskandidaten `granite.emulators` utökar [`ContextHub.Store.PersistedStore`](contexthub-api.md#contexthub-store-persistedstore).

### Konfiguration {#configuration-emulators}

Standardkonfigurationen innehåller en array med namnet `defaultEmulators` som innehåller information om olika enheter. När du skapar en butik kan du ange olika enhetsprofiler i egenskapen Detaljkonfiguration efter behov, med det format som visas i följande exempel:

```javascript
{
   "defaultEmulators":[
        {
            "id": "iphone-6",
            "title": "iPhone 6",
            "type": "mobile",
            "platform": "iOS",
            "platformVersion": "8.1.3",
            "width": 750,
            "height": 1334,
            "canRotate": true,
            "orientation": "Portrait",
            "device-pixel-ratio": 2
        },
        {
            "id": "iphone-6-plus",
            "title": "iPhone 6 Plus",
            "type": "mobile",
            "platform": "iOS",
            "platformVersion": "8.1.3",
            "width": 1080,
            "height": 1920,
            "canRotate": true,
            "orientation": "Portrait",
            "device-pixel-ratio": 3
        },
        {
            "id": "galaxy-s4",
            "title": "Samsung Galaxy S4",
            "type": "mobile",
            "platform": "Android",
            "platformVersion": "4.4.2 KitKat",
            "width": 1080,
            "height": 1920,
            "canRotate": true,
            "orientation": "Portrait",
            "device-pixel-ratio": 3
        }
    ]
}
```

### Dataobjekt {#data-items-emulators}

Lagringsdataträdet liknar följande exempel:

```javascript
{
   "devices":[
      {"id":"native",
      "title":"Native",
      "type":"screen",
      "width":1395,
      "height":374,
      "orientation":"Landscape",
      "platform":"Mac OS X",
      "platformVersion":"10",
      "canRotate":false
      },
      {"id":"ipad-3",
      "title":"iPad 3 / 4 / Air",
      "type":"tablet",
      "platform":"iOS",
      "platformVersion":"8.1.3",
      "width":1536,
      "height":2048,
      "canRotate":true,
      "orientation":"Portrait",
      "device-pixel-ratio":2
      },
      {"id":"iphone-6",
      "title":"iPhone 6",
      "type":"mobile",
      "platform":"iOS",
      "platformVersion":"8.1.3",
      "width":750,
      "height":1334,
      "canRotate":true,
      "orientation":"Portrait",
      "device-pixel-ratio":2
      },
      {"id":"galaxy-s4",
      "title":"Samsung Galaxy S4",
      "type":"mobile",
      "platform":"Android",
      "platformVersion":"4.4.2 KitKat",
      "width":1080,
      "height":1920,
      "canRotate":true,
      "orientation":"Portrait",
      "device-pixel-ratio":3
      }
   ],
   "currentDeviceId":"native",
   "orientations":[
      {"id":"landscape",
      "title":"Landscape"
      },
      {"id":"portrait",
       "title":"Portrait"
      }
   ],
   "currentDevice":{
      "id":"native",
      "title":"Native",
      "type":"screen",
      "width":1395,
      "height":374,
      "orientation":"Landscape",
      "platform":"Mac OS X",
      "platformVersion":"10",
      "canRotate":false
   }
}
```

## granite.profile Sample Store Candidate {#granite-profile-sample-store-candidate}

Lagrar information om den aktuella användaren.

### Källplats {#source-location-profile}

`/libs/settings/cloudsettings/legacy/contexthub/profile`

### Basimplementering {#base-implementation-profile}

Butikskandidaten `granite.profile` utökar [`ContextHub.Store.PersistedJSONPStore`](contexthub-api.md#contexthub-store-persistedjsonpstore).

### Konfiguration {#configuration-profile}

Följande standardkonfiguration används. Du bör inte ändra den här konfigurationen.

```javascript
{
   "service":{
      "jsonp":false,
      "timeout":1000,
      "path":"${contexthub:/store/profile/path}.infinity.json"
   },
   "initialValues":{"path":"/home/users/a/anonymous"}
}
```

### Dataobjekt {#data-items-profile}

Lager som använder den här butikskandidaten har ett dataträd som liknar följande exempel:

```javascript
{
   "displayName":"anonymous",
   "path":"/home/users/6/6zavE_DGre6Ad9Y5E0Ba",
   "avatar":"/etc/designs/default/images/social/avatar.png",
   "authorizableId":"anonymous"
}
```
