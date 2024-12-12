---
title: Aktuell underhållsversionsinformation för  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell underhållsversionsinformation för  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: c8a798e1f1b7234f91682b6e5ef7072e024df022
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 0%

---


# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs de tekniska versionsinformationen för den aktuella underhållsutgåvan av Experience Manager as a Cloud Service.

## Utgåva 18751 {#18751}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsutgåvan 18751, som offentliggjordes den 11 december 2024. Den tidigare underhållsversionen var version 18598.

Funktionsaktiveringen i 2025.1.0 kommer att innehålla alla funktioner som finns i den här underhållsversionen. Mer information finns i [Experience Manager Releases Roadmap](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Förbättringar {#enhancements-18751}

* SKYOPS-88509: Java 21-stöd för AEM SDK.

### Åtgärdade problem {#fixed-issues-18751}

* ASSETS-42802: Knappen Bakåt i MFE fungerar inte alltid och extra dialogrutor visas.
* ASSETS-44148: Fast NODE_MOVED-händelse i AEM kan orsaka NPE.
* ASSETS-44418: Fast korrigeringsmiljö är inte konfigurerad på himlen.
* ASSETS-44821: Åtgärdat uppdateringshändelsefilter för att inkludera formulärurl-kodade data för överföringshändelser.
* CNTBF-298: Kopiering av fast innehåll misslyckas med UUID-konflikter.
* CNTBF-331: [content-copy-bundle] release 2.0.14.
* FORMS-16572: Ta bort arbetsflödestestningsfel för Java 21 SDK-bygge.
* GRANITE-36205: Automatisk uppdatering för intern ekrelease i QS.
* GRANITE-53704: Utvärdera Sling Discovery på databastjänsten igen.
* GRANITE-54300: Uppdatera Oak till den senaste offentliga versionen (1.70.0).
* GRANITE-54416: Uppdatera Fireworks till version 3.8.2.
* GRANITE-54462: Konfigurera SubscriberAgents att använda hc.tags för &quot;systemready&quot;.
* GRANITE-54542: Uppdatera Commons-io-beroende till 2.17.0.
* GRANITE-54658: Lägg till delayFactor och OSGi-konfigurationer i gruppstorlek för fullGC i QS.
* GRANITE-54696: Ett brett importintervall för Jackrabbit API.
* GRANITE-54803: Inaktivera ClusterAtExchange i AEM när imsauth är aktiv.
* GRANITE-55095: Uppdatera Oak till den senaste offentliga versionen (1.72.0).
* GUIDES-2006: Dokumentläget markerat som Klar återgår till Utkast innan en ny version sparas, vilket resulterar i att Klar-läget inte bevaras i några dokumentversioner.
* GUIDES-21840: I utdata från PDF saknas kapitelrubriker i innehållsförteckningen, vilket leder till en felaktig hierarki.
* GUIDES-19558: Om baslinjen har ett stort antal ämnen eller kartor kan du redigera och sedan spara en baslinje på en molnkonfiguration efter en minut.
* GUIDES-19733: Omvandling av kartor med baslinjen blir långsam och kan till slut inte läsa in listan över alla associerade ämnen och kartor.
* SITES-26798: Startar autoerbjudande uppdaterar inte kampanjstatus (kampanjdatum).
* SITES-27137: Ta bort sambandsmetriberoende från MSM-kärnan.
* SKYOPS-75446: Fast AEM returnerar ibland 404 sidor eller sidor som saknar innehåll.
* SKYOPS-76366: Inga Jetty Threadpool-värden i AEM version 15977 och senare.
* SKYOPS-82371: java.io.IOException: classFile.delete() failed.
* SKYOPS-83369: AEM kan inte startas om körningen av omvandlingsjobbet inte genererar paket.
* SKYOPS-83910: Korrigerade problem med samtidighet i SKYOPS-82371.
* SKYOPS-84821: Ange Sling Main Servletens sling.includes.checkcontenttype-konfiguration till true.
* SKYOPS-85798: Fast transformeringsjobb genererar tomma indexdefinitioner.
* SKYOPS-86251: Uppgradera till AEM Analyser Core 1.5.6 och aktivera produktpaketimportanalysatorn i transformeringsjobbet.
* SKYOPS-86710: Ta bort minify-testfel för Java 21 SDK-bygge.
* SKYOPS-86745: Uppdatera till Sling ResourceResolver 1.12.2.
* SKYOPS-89616: Det gick inte att skapa ett tekniskt konto i Adobe Developer Console.
* SKYOPS-89691: Korrigerat felaktigt artefakt-ID som används för ASM-varningar.
* SKYOPS-89699: Varningar saknas för äldre Groovy-versioner som är inbäddade i orbinson-sfären i Groovy-konsolen.
* SKYOPS-88664: Logga och skydda mot fall när den hämtade kartfilen har en linje som överstiger 1024.
* SKYOPS-89734: Release dispatcher image 2.0.235.

Mer information om de nya och förbättrade funktionerna och problemen som har åtgärdats i Experience Manager Guides finns i [Experience Manager Guides-releasemartan](https://experienceleague.adobe.com/en/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### Kända fel {#known-issues-18751}

Ingen.

### Föråldrade funktioner och API:er {#deprecated-18751}

Inaktuella och borttagna funktioner och API:er i AEM as a Cloud Service beskrivs i dokumentet [Inaktuella och Borttagna funktioner och API:er](/help/release-notes/deprecated-removed-features.md).

### Säkerhetskorrigeringar {#security-18751}

AEM as a Cloud Service strävar efter att optimera säkerheten och prestandan för din plattform. Denna underhållsrelease åtgärdar tre identifierade sårbarheter, vilket stärker vårt engagemang för robust systemskydd.

### Inbäddade tekniker {#embedded-tech-18751}

| Teknik | Version | Länk |
|---|---|---|
| AEM Oak | 1.72.0 | [Oak API 1.72.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.72.0/index.html) |
| AEM SLING API | 2.27.6 | [API:t för Apache Sling 2.27.6 ](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTML | 1.4.24-1.4.0 | [Språkspecifikation för HTML-mall](https://github.com/adobe/htl-spec) |
| Grundläggande komponenter i AEM | 2.27.0 | [AEM WCM-kärnkomponenter](https://github.com/adobe/aem-core-wcm-components) |
