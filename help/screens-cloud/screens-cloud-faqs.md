---
title: Vanliga frågor och svar om skärmar
description: På den här sidan beskrivs as a Cloud Service frågor och svar för skärmar.
exl-id: 93f2144c-0e64-4012-88c6-86972d8cad9f
source-git-commit: cf091056bdb96917a6d22bf1197d9b34ebbf9610
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 0%

---

# Vanliga frågor och svar om skärmar {#screens-cloud-faqs}

I följande avsnitt finns svar på vanliga frågor och svar (FAQ) om as a Cloud Service skärmprojekt.

## Vad ska jag göra om AEM Screens-spelare som pekar på Skärmar as a Cloud Service inte väljer något anpassat klipp i formatet /etc.clientlibs/xxx/clientlibs/clientlib-site.lc-813643788974b0f89d686d9591526d63-lc.min.css?

AEM as a Cloud Service ändrar de långa cachenycklarna för varje distribution. AEM Screens genererar offline-cacheminnen när innehållet ändras, i stället för när Cloud Manager kör distributionen. De här långa cachenycklarna i manifesten är ogiltiga, så spelaren kan inte hämta de här *klientlibs*.

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

## Vilka bildformat rekommenderas för smidig återgivning av bilder i AEM Screens as a Cloud Service kanaler?{#screens-cloud-image-format}

Vi rekommenderar att du använder bilder i formatet `.png` och `.jpeg` i en as a Cloud Service AEM Screens-kanal för att få bästa möjliga digitala signeringsupplevelse.
Bilderna i formatet `*.tif` (taggbildfilsformat) stöds inte i AEM Screens as a Cloud Service. Om en kanal har detta bildformat återges bilden inte på spelarsidan.