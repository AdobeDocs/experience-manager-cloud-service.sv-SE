---
title: Screens - frågor och svar
description: På den här sidan beskrivs Screens as a Cloud Service frågor och svar.
exl-id: 93f2144c-0e64-4012-88c6-86972d8cad9f
feature: Administering Screens
role: Admin, Developer, User
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---

# Screens - frågor och svar {#screens-cloud-faqs}

I följande avsnitt finns svar på vanliga frågor och svar om Screens as a Cloud Service projekt.

## Vad ska jag göra om AEM Screens Player som pekar på Screens as a Cloud Service inte väljer något anpassat klipp i formatet /etc.clientlibs/xxx/clientlibs/clientlib-site.lc-813643788974b0f89d686d9591526d63-lc.min.css?

AEM as a Cloud Service ändrar de långa cachenycklarna vid varje driftsättning. AEM Screens genererar offline-cacheminnen när innehållet ändras, i stället för när Cloud Manager kör distributionen. De här långa cachenycklarna i manifesten är ogiltiga, så spelaren kan inte hämta *clientlibs*.

Om du använder `longCacheKey="none"` i din `clientlib`-mapp tas de långa cachenycklarna bort helt för *clientlibs*.


## Vad ska jag göra om offlinemanifestet inte innehåller alla resurser som det är tänkt? {#offline-manifest}

Offlinecache genereras med tjänstanvändaren **bulk-offline-update-screens-service**. Vissa sökvägar, som inte är tillgängliga för `bulk-offline-update-screens-service`, leder till att innehåll saknas i offlinematerial.

I koden, det vill säga `ui.config or ui.apps`, skapar du en OSGi-konfiguration i konfigurationsmappen med följande innehåll och ger filnamnet namnet `org.apache.sling.jcr.repoinit.RepositoryInitializer-serviceusersandacls-content.config`

```
scripts=[
        "
        set principal ACL for bulk-offline-update-screens-service
                allow jcr:read on /content/mysite
                allow jcr:read on /apps/my-resources
        end
        "] 
```

## Vilka bildformat rekommenderas för smidig återgivning av bilder i en as a Cloud Service AEM Screens-kanal?{#screens-cloud-image-format}

Adobe rekommenderar att du använder bilder i formatet `.png` och `.jpeg` i en as a Cloud Service AEM Screens-kanal för att få bästa möjliga digitala signeringsupplevelse.
Bilderna i formatet `*.tif` (taggbildsfilformat) stöds inte i AEM Screens as a Cloud Service. Om en kanal har det här bildformatet återges inte bilden på spelarsidan.

## Vad ska jag göra om en kanal i utvecklarläget (online) inte återges i AEM Screens Player?{#screens-cloud-online-channel-blank-iframe}

Adobe rekommenderar att du använder AEM Screens cachningsfunktioner. Om du måste köra din kanal i utvecklarläge och AEM Screens Player visar en tom skärm, kontrollerar du utvecklarverktygen i Player och letar efter `X-Frame-Options`- eller `frame-ancestors`-fel. Upplösningen är att konfigurera Dispatcher så att innehåll som körs i iFrames tillåts. Vanligtvis fungerar följande konfiguration:

```
Header set Content-Security-Policy "frame-ancestors 'self' file: localhost:*;"
```

## Hur används registreringskodsgränsen?

Det bästa sättet är att begränsa användningen av registreringskoden. Om en registreringskod har komprometterats men har en gräns på 100 registreringar kan angriparen bara registrera upp till det numret, men inte fler. Du kan alltid uppdatera användningsgränsen när registreringskoden har skapats och vissa av kundens spelare har redan registrerats. Om kunden observerar onormal registreringsaktivitet för en viss registreringskod kan de sänka gränsen i realtid medan de undersöker saken. De kan öka antalet tillbaka om det var ett falskt larm, utan att de redan registrerade spelarna påverkas.
