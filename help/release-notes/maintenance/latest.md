---
title: Aktuell underhållsanvisning för [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell underhållsanvisning för [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 36fefbf74a288d60a9529f0c7273dd6b0557177b
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 1%

---

# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs den tekniska versionsinformationen för den aktuella underhållsutgåvan av Experience Manager as a Cloud Service.

## Utgåva 15939 {#release-15939}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsutgåvan 15939, som offentliggjordes den 17 april 2024. Den tidigare underhållsversionen var version 15860.

2024.4.0 Funktionsaktivering innehåller alla funktioner som finns i den här underhållsversionen. Se [Roadmap för lanseringar av Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html) för mer information.

### Förbättringar {#enhancements-15939}

* GRANITE-39892: Uppdatera distributionen för storleksgräns för kö och publicera klar.
* GRANITE-48777: Uppdatering QS till com.adobe.granite.security.user-0.4.84 klar.
* GRANITE-49421: Lagt till egenskaper för segmenttjänstens huvudnamn.
* GRANITE-49855: Skriv en funktionsmodellanalysator som inte fungerar i QuickStart-bygget om Commons.json används.
* GRANITE-47995: Tillåt att skriva om cq:isDelived.
* GRANITE-36205: Uppdatera den interna ekversionen till den senaste.
* GRANITE-50156 Bind AEMCS-tillhörighet till IMS User ID för Universal Editor.
* GRANITE-50556: Upgrade crosswalk bundle to v0.1.18.
* GRANITE-50728: Uppdatera FileVault till 3.7.3-T2024030811857-81fa88f1.
* GRANITE-50957: Uppdatera QS till com.adobe.granite.database till 1.8.114.
* GRANITE-50158: Lägg till stöd för OAuth Server i serverautentiseringsflödet i YAML-inläsaren.
* GRANITE-51327: Update Oak to the latest public release (1.62.0).
* SKYOPS-68091 Uppdatera Java 11 runtime-bilder till version 3.0.0.
* SKYOPS-70421: Uppgradera paketet org.apache.sling.servlet-help
* SKYOPS-73483: Tillåt inloggningstoken på AEM.

### Åtgärdade problem {#fixed-issues-15939}

* GRANITE-46901: Lägg till mått i meddelandeklient.
* GRANITE-48793: Uppdatera QS till com.adobe.granite.crx-explorer-1.1.28.
* GRANITE-48937: Omniseaarch fungerar inte på aem/start.html.
* GRANITE-49638: Korrigera felaktig innehållstypskonfiguration för RUM-transformatorfabriken.
* GRANITE-50141: IMSProviderImpl spammar loggen.
* SITES-20949: ComponentsIT.testEmbed failed after Youtube added reference=&quot;strict-origin-when-cross-origin&quot;.
* SITES-21233: Core Components update - Fix Accordion after upgrade to 15860.
* SKYOPS-74819: Kompatibiliteten för dubblettnycklar i Apache Commons har brutits bakåt.
* SKYOPS-67087: Clientlib-aggregering fungerar inte i vissa fall.
* CQ-4355415: AEM meddelandelänkar fungerar inte i 6.5 SP18.

### Kända fel {#known-issues-15939}

Ingen.

### Föråldrade funktioner och API:er {#deprecated-15939}

* [Borttagning av JWT-autentiseringsuppgifter i Adobe Developer Console](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md)

Titta på [Föråldrade och borttagna funktioner och API:er](/help/release-notes/deprecated-removed-features.md) för att veta vad som har tagits bort eller tagits bort på AEM as a Cloud Service.

### Inbäddade tekniker {#embedded-tech-15939}

| Teknik | Version | Länk |
|---|---|---|
| AEM | 1.62.0 | [API för Oak API 1.62.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.62.0/index.html) |
| AEM SLING API | 2.27.2 | [API för Apache Sling 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTML | 1.4.20-1.4.0 | [HTML-mallens språkspecifikation](https://github.com/adobe/htl-spec) |
| Grundläggande komponenter i AEM | 2.24.6 | [AEM WCM-kärnkomponenter](https://github.com/adobe/aem-core-wcm-components) |
