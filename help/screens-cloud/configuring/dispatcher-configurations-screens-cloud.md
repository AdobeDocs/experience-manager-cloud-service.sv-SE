---
title: Dispatcher Configurations in Screens as a Cloud Service
description: På den här sidan beskrivs Dispatcher Configurations in Screens som en Cloud Service.
source-git-commit: b00856e1be8842c4e9fa6ed4ada9129926c73ef5
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---


# Dispatcher Configurations in Screens as a Cloud Service{#dispatcher-configurations-screens-cloud}

I det här avsnittet beskrivs dispatcherkonfigurationerna för skärmar som en Cloud Service.

## Distribuera konfigurationer för skärmar som en Cloud Service-distribution {#deployment}

Tillåt följande filter och cacheregler i utskickare för publiceringsinstanserna på skärmar som en Cloud Service.

### Filter {#filters}

## AEM Screens Filters

```
## # Content Configurations
/0200 { /type "allow" /method '(GET|HEAD)' /url "/content/screens/*" }
#/0201 { /type "allow" /method '(GET|HEAD)' /url "/content/experience-fragments/*" } ## uncomment this, if you're using experience-fragments
## add any other formats required for your project here
/0202 { /type "allow" /extension '(css|eot|gif|ico|jpeg|jpg|js|gif|pdf|png|svg|swf|ttf|woff|woff2|html|mp4|mov|m4v)' /path "/content/dam/*" }
/0203 { /type "allow" /method 'GET' /url "/screens/channels.json" }
## # Enable clientlibs proxy servlet
/0210 { /type "allow" /method "GET" /url "/etc.clientlibs/*" }
```

## Cache-regler {#cache-rules}

* Lägg till `/statfileslevel "10"` i `/cache`-avsnittet i `publish_farm.any`/.

   >[!NOTE]
   >Detta stöder cachelagring av upp till 10 nivåer från cache-dokumentet och gör innehållet ogiltigt när det publiceras i stället för att göra allt ogiltigt. Du kan ändra den här nivån baserat på hur detaljerad innehållsstrukturen är.

* Lägg till följande i `/invalidate`-avsnittet i `publish_farm.any`.

   ```
   /0003 {
       /glob "*.json"
       /type "allow"
   }
   ```

* Lägg till följande regler i `/rules`-avsnittet i `/cache` i publish_farm.any eller i en fil som inkluderas från `publish_farm.any`.

   ```
   ## Allow Dispatcher Cache for Screens channels
    /0002
        {
        /glob "/content/screens/*.html"
        /type "allow"
            }
   
   ## Allow Dispatcher Cache for Screens offline manifests
   
   /0003
       {
       /glob "/content/screens/*.manifest.json"
       /type "allow"
       }
   
   ## Allow Dispatcher Cache for Assets
   /0004
       {
       /glob "/content/dam/*"
       /type "allow"
       }
   
   ## Deny Screens Channels json
   /0005
       {
       /glob "/screens/channels.json"
       /type "deny"
       }
   ```
