---
title: Dispatcher Configurations in Screens as a Cloud Service
description: På den här sidan beskrivs Dispatcher Configurations in Screens as a Cloud Service.
exl-id: cc04b480-9310-4975-a7c2-20682c567fa4
source-git-commit: f0e9fe0bdf35cc001860974be1fa2a7d90f7a3a9
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---

# Dispatcher Configurations in Screens as a Cloud Service {#dispatcher-configurations-screens-cloud}

I det här avsnittet beskrivs dispatcherkonfigurationerna för as a Cloud Service skärmar.

## Lägga till filter och cacheregler i Dispatcher för as a Cloud Service distribution av skärmar {#deployment}

Tillåt följande filter och cacheregler i utskickare för publiceringsinstanserna på as a Cloud Service Skärmar.

### AEM Screens Filters {#filters}

```
## # Content Configurations
/0200 { /type "allow" /method '(GET|HEAD)' /url "/content/screens/*" }
#/0201 { /type "allow" /method '(GET|HEAD)' /url "/content/experience-fragments/*" } ## uncomment this, if you are using experience-fragments
## add any other formats required for your project here
/0202 { /type "allow" /extension '(css|eot|gif|ico|jpeg|jpg|js|gif|pdf|png|svg|swf|ttf|woff|woff2|html|mp4|mov|m4v)' /path "/content/dam/*" }
/0203 { /type "allow" /method 'GET' /url "/screens/channels.json" }
## # Enable clientlibs proxy servlet
/0210 { /type "allow" /method "GET" /url "/etc.clientlibs/*" }
```

### Cache-regler {#cache-rules}

* Lägg till `/statfileslevel "10"` till `/cache` avsnitt i `publish_farm.any`/.

  >[!NOTE]
  >Den här cacheregeln stöder cachelagring av upp till 10 nivåer från cachedokumentroten och gör innehållet ogiltigt när innehållet publiceras i stället för att göra allt ogiltigt. Du kan ändra den här nivån baserat på hur detaljerad innehållsstrukturen är.

* Lägg till följande i `/invalidate` avsnitt i `publish_farm.any`.

  ```
  /0003 {
      /glob "*.json"
      /type "allow"
  }
  ```

* Lägg till följande regler i `/rules` avsnitt i `/cache` i publish_farm.any eller in a file that&#39;s included from `publish_farm.any`.

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
