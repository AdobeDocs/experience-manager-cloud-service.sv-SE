---
title: Dispatcher Configurations in Screens as a Cloud Service
description: På den här sidan beskrivs Dispatcher Configurations in Screens as a Cloud Service.
exl-id: cc04b480-9310-4975-a7c2-20682c567fa4
feature: Administering Screens
role: Admin, Developer, User
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---

# Dispatcher Configurations in Screens as a Cloud Service {#dispatcher-configurations-screens-cloud}

I det här avsnittet beskrivs dispatcherkonfigurationerna för Screens as a Cloud Service.

## Lägga till filter och cacheregler i distributionen av Dispatcher för Screens as a Cloud Service {#deployment}

Tillåt följande filter och cacheregler i utskickare för publiceringsinstanserna i Screens as a Cloud Service.

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

* Lägg till `/statfileslevel "10"` i avsnittet `/cache` i `publish_farm.any`/.

  >[!NOTE]
  >Den här cacheregeln stöder cachelagring av upp till 10 nivåer från cachedokumentroten och gör innehållet ogiltigt när innehållet publiceras i stället för att göra allt ogiltigt. Du kan ändra den här nivån baserat på hur detaljerad innehållsstrukturen är.

* Lägg till följande i avsnittet `/invalidate` i `publish_farm.any`.

  ```
  /0003 {
      /glob "*.json"
      /type "allow"
  }
  ```

* Lägg till följande regler i avsnittet `/rules` i `/cache` i publish_farm.any eller i en fil som inkluderas från `publish_farm.any`.

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
