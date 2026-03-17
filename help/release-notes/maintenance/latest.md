---
title: Aktuell information om underhållsversionen av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell information om underhållsversionen av  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: b83d8736d47778ed133e0cc07207e02e581bbc69
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 1%

---


# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs den tekniska versionsinformationen för den aktuella underhållsversionen av Experience Manager as a Cloud Service.

## Utgåva 24893 {#release-24893}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsutgåva 24893, som offentliggjordes den 17 mars 2026. Den tidigare underhållsversionen var version 24678.

Funktionsaktiveringen i 2026.3.0 kommer att innehålla alla funktioner som finns i den här underhållsversionen. Mer information finns i [Experience Manager Releases Roadmap](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Förbättringar {#enhancements-24893}

* CNTBF-613: Det gick inte att registrera nodtyperna eftersom åtkomst nekas (JCR-101).
* GRANITE-53957: Uppgradera Azure SDK V8 till V12 för ekblobazure.
* GRANITE-57035: Använd Bouncy Castle som standardsäkerhetsprovider.
* GRANITE-59249: Undvik att registrera en säkerhetsprovider i JVM.
* GRANITE-61564: Visningsinställningar på `/security/users.html` kan inte öppnas för administratörer.
* GRANITE-64748: OIDC: konfigurerbar `sling.oauth-request-key`-cookie upphör att gälla.
* SITES-39767: Stöd för ett enda värde via request attribute (CSP).
* SKYOPS-129301: Ange API:erna jar javadoc-kompatibilitetsnivån till 17.
* GRANITE-64962: Uppdatera Apache Jackrabbit Oak till 1.92.0.
* GRANITE-64963: Uppdatera Apache Jackrabbit Filevault till 4.2.0.
* GRANITE-64764: Uppdatera Apache Commons-text till version 1.15.0.
* SKYOPS-131412: Uppdatera Apache Commons till 1.6.0.
* SKYOPS-131432: Uppdatera Felix SCR till 2.2.14.
* SKYOPS-131907: Uppdatera Sling API-region till 1.1.10.
* SKYOPS-131938: Uppdatera GSON till 2.13.2.
* SKYOPS-132173: Uppdatera Apache Commons-kodeken till 1.21.0.
* SKYOPS-132182: Uppdatera Sling-klientorganisationen till 1.1.8.
* SKYOPS-132267: Uppdatera org.osgi.service.component till 1.5.1.
* SKYOPS-132272: Uppdatera Sling-funktionsmodellen till 2.0.4.
* SKYOPS-133689: Uppdatera Dispatcher till Apache httpd 2.4.66.

### Åtgärdade problem {#fixed-issues-24893}

* GRANITE-64443: `workflow.core` tar bort inaktuell export av `log4j`.
* GRANITE-64543: Svaret på behörighetsbegränsningar ska matcha API-kontraktet.

#### AEM Guides {#guides-24893}

* GUIDES-38412: När du redigerar en Schematron `(*.sch)`-fil och använder funktionen för att söka och ersätta, visas panelen för att söka och ersätta delvis utanför skärmen längst ned, vilket förhindrar åtkomst till dess inmatningsfält och kontroller.
* GUIDES-37806: När samma ämne återanvänds för flera kartor med olika villkorliga förinställningar skrivs ämnesinnehållet över när den senaste kartan publiceras på Salesforce, vilket resulterar i att felaktiga data visas för användare av tidigare publicerade kartor.
* GUIDES-39394: När en bild som initialt hanteras som en språkspecifik resurs med en viss version (till exempel under `/en/`) flyttas till en global mapp med en uppdaterad version och baslinjeexport utförs, fortsätter den nya baslinjen att referera till inaktuella språkspecifika versioner av den bilden, vilket leder till en misslyckad baslinjeexport.
* GUIDES-39054: När du skapar en dynamisk baslinje slutar ibland redigeraren att svara på flera samtidiga API-begäranden, vilket gör att alla andra åtgärder avbryts.
* GUIDES-37781: När du tilldelar en användare till en granskningsåtgärd visas alla användare i listrutan i stället för endast de som är kopplade till de valda projekten, vilket resulterar i ogiltiga användaralternativ.
* GUIDES-39385: När du öppnar en rapport för en karta uppstår en fördröjning i inläsningen av filterpanelen.

Mer information om de nya och förbättrade funktionerna och problemen som har åtgärdats i den här versionen finns i [Experience Manager Guides-lanseringens färdplan](https://experienceleague.adobe.com/en/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### Kända fel {#known-issues-24893}

Ingen.

### Föråldrade funktioner och API:er {#deprecated-24893}

Inaktuella och borttagna funktioner och API:er i AEM as a Cloud Service beskrivs i dokumentet [Inaktuella och Borttagna funktioner och API:er](/help/release-notes/deprecated-removed-features.md).

### Säkerhetskorrigeringar {#security-24893}

AEM as a Cloud Service strävar efter att optimera säkerheten och prestandan för din plattform. Denna underhållsrelease åtgärdar nio identifierade sårbarheter, vilket stärker vårt engagemang för robust systemskydd.

### Inbäddade tekniker {#embedded-tech-24893}

| Teknik | Version | Länk |
|---|---|---|
| AEM Oak | 1.92.0 | [Oak 1.92.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.92.0/index.html) |
| AEM SLING API | 2.27.6 | [API:t för Apache Sling 2.27.6 ](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Språkspecifikation för HTML-mall](https://github.com/adobe/htl-spec) |
| Apache HTTP-server | 2.4.66 | [Apache HTTP 2.4.66](https://apache.googlesource.com/httpd/+/refs/tags/2.4.66/CHANGES) |
| Grundläggande komponenter i AEM | 2.30.4 | [AEM WCM Core Components](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (standard) | [Node.js-versioner som stöds](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
