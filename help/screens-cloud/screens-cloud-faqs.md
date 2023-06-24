---
title: Vanliga frågor och svar om skärmar
description: På den här sidan beskrivs vanliga frågor och svar om skärmar as a Cloud Service.
exl-id: 93f2144c-0e64-4012-88c6-86972d8cad9f
source-git-commit: 7260649eaab303ba5bab55ccbe02395dc8159949
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 0%

---

# Vanliga frågor och svar om skärmar {#screens-cloud-faqs}

I följande avsnitt finns svar på vanliga frågor och svar (FAQ) om as a Cloud Service skärmprojekt.

## Vad ska jag göra om AEM Screens Player som pekar på Skärmar as a Cloud Service inte väljer något anpassat klipp i formatet /etc.clientlibs/xxx/clientlibs/clientlib-site.lc-813643788974b0f89d686d9591526d63-lc.min.css?

AEM as a Cloud Service ändrar de långa cachenycklarna för varje distribution. AEM Screens genererar offline-cacheminnen när innehållet ändras, i stället för när Cloud Manager kör distributionen. De här långa cachenycklarna i manifesten är ogiltiga, så spelaren kan inte hämta *klientlibs*.

Använda `longCacheKey="none"` i `clientlib` mappen tar bort de långa cachenycklarna helt för *klientlibs*.


## Vad ska jag göra om offlinemanifestet inte innehåller alla resurser som det är tänkt? {#offline-manifest}

Offlinecache genereras med **bulk-offline-update-screens-service** tjänstanvändare. Vissa banor som inte är tillgängliga av `bulk-offline-update-screens-service`, vilket leder till att innehåll saknas i offlinematerial.

I koden, det vill säga, `ui.config or ui.apps`, skapa en OSGi-konfiguration i konfigurationsmappen med följande innehåll och ge filnamnet namnet som `org.apache.sling.jcr.repoinit.RepositoryInitializer-serviceusersandacls-content.config`

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

Vi rekommenderar att du använder bilder i formatet `.png` och `.jpeg` i en as a Cloud Service AEM Screens-kanal för bästa digitala signeringsupplevelse.
Bilderna i formatet `*.tif` (Tagg Image File-format) stöds inte i AEM Screens as a Cloud Service. Om en kanal har det här bildformatet återges inte bilden på spelarsidan.

## Vad ska jag göra om en kanal i utvecklarläget (online) inte återges i AEM Screens Player?{#screens-cloud-online-channel-blank-iframe}

Adobe rekommenderar att du använder AEM Screens cachningsfunktioner. Om du måste köra din kanal i utvecklarläge och AEM Screens Player visas på en tom skärm kontrollerar du utvecklarverktygen i Player och letar efter `X-Frame-Options` eller `frame-ancestors` fel. Upplösningen är att konfigurera Dispatcher så att innehåll som körs i iFrames tillåts. Vanligtvis fungerar följande konfiguration:

```
Header set Content-Security-Policy "frame-ancestors 'self' file: localhost:*;"
```

## Hur används registreringskodsgränsen?

Det bästa sättet är att begränsa användningen av registreringskoden. Om en registreringskod har komprometterats men har en gräns på 100 registreringar kan angriparen bara registrera upp till det numret, men inte mer. Du kan alltid uppdatera användningsgränsen när registreringskoden har skapats och vissa av kundens spelare har redan registrerats. Om kunden observerar ovanlig registreringsaktivitet för en viss registreringskod kan de sänka gränsen i realtid medan de undersöker. De kan öka antalet tillbaka om det var ett falskt larm, utan att de redan registrerade spelarna påverkas.
