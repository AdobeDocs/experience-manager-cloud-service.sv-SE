---
title: Aktuell underhållsanvisning för [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell underhållsanvisning för [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: bb7d8145eb954557d185b58f884532f8f08c5a54
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 2%

---

# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs den tekniska versionsinformationen för den aktuella underhållsutgåvan av Experience Manager as a Cloud Service.

## Utgåva 13239 {#release-13239}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsutgåvan 13239, som offentliggjordes den 29 augusti 2023. Den här underhållsversionen ersätter version 13206.

2023.9.0 Funktionsaktivering innehåller alla funktioner som finns i den här underhållsversionen. Se [Roadmap för lanseringar av Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html) för mer information.

### Förbättringar {#enhancements-13239}

- GRANITE-46784: Lägg till alternativ för att inaktivera BearerAuthenticationHandler
- GRANITE-36205: Uppdatera den interna ekversionen till den senaste
- ASSETS-26713: Touch UI External Link to New Experience UI Dashboard - unified-shell-integration och UI-touch-optimerad uppgraderad
- SKYOPS-63302: Uppgradera com.adobe.granite:com.adobe.granite.auth.saml till v1.0.54
- GRANITE-46634: Uppgradera till Eventing client 1.4.0
- GRANITE-46788: Uppdatera bibliotek till Apache Commons IO 2.13.0, Commons Lang 3.13.0, Commons Code 1.16.0 och Commons Compress 1.23.0
- GRANITE-46705: Uppdatering till Apache Felix HTTP Jetty 4.1.14
- GRANITE-46631: Uppdatera Jackrabbit-version till 2.20.11
- SKYOPS-61895: Uppdatera till Jackrabbit Filevault 3.7.0

### Åtgärdade problem {#fixed-issues-13239}

- SKYOPS-63290: Korrigerad felaktig utveckling av fickor
- SKYOPS-54607: Beräkningen av Ratelimiter-serverbelastningen är inte korrekt för begäran som misslyckades
- ASSETS-27648: ContentModelIT kan inte läsa exkluderingsfiler från andra paket
- GRANITE-43744: Sling Authenticator fungerar inte korrekt om det finns en felkonfiguration med autentiseringskrav och vanity-sökväg
- GRANITE-46419: AEM integreringsproblem med Auth0 IP
- GRANITE-46292: Okta SAML-konfiguration fungerar inte efter AEM Cloud-uppdatering
- GRANITE-47059: Ta bort Granite Jetty SSL Bundle

### Kända fel {#known-issues-13239}

Ingen.

### Inbäddade tekniker {#embedded-tech-13239}

| Teknik | Version | Länk |
|---|---|---|
| AEM | 1.54-T20230817132355-3800a65 | [Oak API 1.54.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.54.0/index.html) |
| AEM SLING API | Version 2.27.2 | [API för Apache Sling 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTML | Version 1.4.20-1.4.0 | [HTML-mallens språkspecifikation](https://github.com/adobe/htl-spec) |
| Grundläggande komponenter i AEM | Version 2.23.2 | [AEM WCM-kärnkomponenter](https://github.com/adobe/aem-core-wcm-components) |
