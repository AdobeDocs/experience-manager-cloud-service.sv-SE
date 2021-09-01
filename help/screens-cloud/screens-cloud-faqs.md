---
title: Skärmar som vanliga Cloud Service
description: På den här sidan beskrivs skärmar som vanliga Cloud Service.
source-git-commit: 7a26bb50a8b95a2358912249e21daeb9c5e9c1a3
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%

---


# Skärmar som vanliga Cloud Service {#screens-cloud-faqs}

I följande avsnitt finns svar på vanliga frågor (FAQ) om skärmar som ett Cloud Service-projekt.

## Vad ska jag göra om AEM Screens-spelaren som pekar på skärmar som en Cloud Service inte väljer de anpassade klientlibs i formatet /etc.clientlibs/xxx/clientlibs/clientlib-site.lc-813643788974b0f89d686d9591526d63-lc.min.css?

AEM som en Cloud Service ändras de långa cachenycklarna för varje distribution. AEM Screens genererar offline-cacheminnen när innehållet ändras, i stället för när Cloud Manager kör distributionen. De här långa cachenycklarna i manifesten är ogiltiga, så spelaren kan inte hämta de här *klientlibs*.

Om du använder `longCacheKey="none"` i din `clientlib`-mapp tas de långa cachenycklarna bort helt för dessa *klientlibs*.


## Vad ska vi göra om offlinemanifestet inte innehåller alla resurser som det är tänkt? {#offline-manifest}

Offlinecache genereras med **bulk-offline-update-screens-service**-tjänstanvändaren. Vissa sökvägar som inte är tillgängliga av `bulk-offline-update-screens-service` leder till att innehåll saknas i offlinematerial.

I koden, d.v.s. `ui.config or ui.apps`, skapar du en OSGi-konfiguration i konfigurationsmappen med följande innehåll och ger filnamnet namnet `org.apache.sling.jcr.repoinit.RepositoryInitializer-serviceusersandacls-content.config`

```
scripts=[
        "
        set principal ACL for bulk-offline-update-screens-service
                allow jcr:read on /content/mysite
                allow jcr:read on /apps/my-resources
        end
        "] 
```
