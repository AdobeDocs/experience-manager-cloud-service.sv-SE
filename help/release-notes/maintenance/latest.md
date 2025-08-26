---
title: Aktuell information om underhållsversionen av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell information om underhållsversionen av  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 3067e88f8adea50f6b6b05e0466974bc57bc4a4e
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 0%

---


# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs den tekniska versionsinformationen för den aktuella underhållsversionen av Experience Manager as a Cloud Service.

## Utgåva 21994 {#21994}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsutgåvan 21994, som offentliggjordes den 19 augusti 2025. Den tidigare underhållsversionen var version 21772.

Funktionsaktiveringen i 2025.8.0 kommer att innehålla alla funktioner som finns i den här underhållsversionen. Mer information finns i [Experience Manager Releases Roadmap](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Nya funktioner  {#new-features-21994}

Ingen.

### Förbättringar {#enhancements-21994}

* GRANITE-53488: Förbättra felhanteringen för deleteconf.json-slutpunkter.
* GRANITE-59968: Tillåt att konfigurera REPLICATION_FORCE_READY_MILLIES.
* GRANITE-60183: Apache Commons-fileupload 1.6.0.
* GRANITE-60306: Apache Commons-lang to 3.18.0.
* GRANITE-60637: Apache Commons-codec to 1.19.0.
* GRANITE-60645: Apache Commons-io 2.20.0.
* GRANITE-60663: Apache Commons-text 1.14.0.
* GRANITE-60714: Mongo Java Driver 5.2.
* GRANITE-60778: Filevault 4.0.0.
* GRANITE-60823: Jackrabbit 2.22.2
* GRANITE-60967: Skapa mätvärden för att spåra kompileringstid för klientlib.
* SKYOPS-105469: Lägger till stöd för acsredirectMgr i autofix api.
* SKYOPS-113929: Lägg till mätvärden för kontroll av replikeringsberedskap.
* SKYOPS-84821: Sling engine 2.16.6.
* SKYOPS-114322: Dumpa slutkompilatorspråket på nivån till `ECMASCRIPT_2018`.

### Åtgärdade problem {#fixed-issues-21994}

* GRANITE-60167: Async index update in Skyline does not support CSV data.
* GRANITE-60532: Ändringen av värdemogglar har inte hämtats.
* SITES-34277: Åtgärda blockeringsfel i översättningsarbetsflöden för sidor.
* SKYOPS-105471: Support dambaseredirect fix for aso autofix.
* SKYOPS-109532: Lägg till borttagen länk som kommentar bakom växlingsknappen.

#### AEM Guides {#guides-21994}

* GUIDES-26688: CSS- och sidlayoutfiler i PDF-mallar har ett inkonsekvent fillåsningsbeteende, vilket gör att redigeringar kan göras även när filerna är låsta.
* GUIDES-30900: Om du kopierar en mapp med ett stort antal resurser från Assets UI kommer en API-timeout att uppstå. Åtgärden fortsätter att köras i serverdelen och slutförs efter en stund, men inget meddelande om att åtgärden lyckades eller misslyckades visas eller inget meddelande visas i användargränssnittet.
* GUIDES-29090: I utdata från PDF visas LOI (List of Index) i en icke-alfabetisk ordning och kapslade indextermer grupperas inte korrekt, vilket gör indexet svårt att navigera i.
* GUIDES-11227: Om du kopierar en DITA-karta från Assets-gränssnittet kopieras även den kopplade baslinjen till den nya kartan.
* GUIDES-31506: Hemsidan blir tom när en av filerna som listas i widgeten Senaste filer är baserad på en mall vars källmall inte innehåller någon miniatyrbild.

Mer information om de nya och förbättrade funktionerna och problemen som har åtgärdats i den här versionen finns i [Experience Manager Guides-lanseringens färdplan](https://experienceleague.adobe.com/en/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### Kända fel {#known-issues-21994}

* Apache HTTPD version 2.4.65 innehåller ändringar som kan påverka vissa konfigurationer på grund av nya begränsningar som implementeras som en del av säkerhetskorrigeringar. Dessa korrigeringar åtgärdar sårbarheter genom att säkerställa att direktiv som `RequestHeader set`, `edit` och `edit_r` som används för att ändra Content-Type-huvudet nu begränsas korrekt till begäranrubriker. Den här ändringen förhindrar oavsiktliga ändringar av svarshuvuden, särskilt för statiskt innehåll.

### Föråldrade funktioner och API:er {#deprecated-21994}

Inaktuella och borttagna funktioner och API:er i AEM as a Cloud Service beskrivs i dokumentet [Inaktuella och Borttagna funktioner och API:er](/help/release-notes/deprecated-removed-features.md).

### Säkerhetskorrigeringar {#security-21994}

AEM as a Cloud Service strävar efter att optimera säkerheten och prestandan för din plattform. Denna underhållsrelease åtgärdar två identifierade sårbarheter, vilket stärker vårt engagemang för robust systemskydd.

### Inbäddade tekniker {#embedded-tech-21994}

| Teknik | Version | Länk |
|---|---|---|
| AEM Oak | 1.84.0 | [Oak API 1.84.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.84/index.html) |
| AEM SLING API | 2.27.6 | [API:t för Apache Sling 2.27.6 ](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Språkspecifikation för HTML-mall](https://github.com/adobe/htl-spec) |
| Apache HTTP-server | 2.4.65 | [Apache HTTP 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| Grundläggande komponenter i AEM | 2.29.0 | [AEM WCM Core Components](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (standard) | [Node.js-versioner som stöds](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
