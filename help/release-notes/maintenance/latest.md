---
title: Aktuell underhållsanvisning för [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell underhållsanvisning för [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 3fbdb150a9a1c133b4910603682e37f1c5d885d2
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 1%

---

# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs den tekniska versionsinformationen för den aktuella underhållsutgåvan av Experience Manager as a Cloud Service.

## Version 13804 {#release-13804}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsutgåva 13804, som offentliggjordes den 10 oktober 2023. Den här underhållsversionen är en uppdatering från den tidigare underhållsversionen 13665.

2023.10.0 Funktionsaktivering innehåller alla funktioner som finns i den här underhållsversionen. Se [Roadmap för lanseringar av Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html) för mer information.

### Förbättringar {#enhancements-13804}

* GRANITE-47238: Underhåll av granskningslogg - Töm kronjobb för att använda kundkonfigurationen.
* GRANITE-47123: Publicera (Sling) - Förbättra starttiden genom att initiera standardsökvägscachen asynkront som standard.
* GRANITE-46618: Publicera (replikering) - Förbättra starthastigheten för publiceringen genom att gruppera replikeringsstatusmeddelanden.
* GRANITE-47136: Indexering (hämtning) - Förbättra hämtningshastigheten för ny parallell indexhämtare (genom att inaktivera validering av kontrollsumma).
* GRANITE-47211: Publicera (Infra) - Förbättra frikopplingen av publiceringsskiktens distributioner (genom att lagra och hämta namn på segmentlagerrevision).
* GRANITE-47267: Uppdatering till Apache Felix Http Jetty 4.2.18 (inkluderar buggfix för parameterhantering av begäranden ([FELIX-6625](https://issues.apache.org/jira/browse/FELIX-6625)) med prestandaförbättringar för lokal utveckling och RDE-utveckling).
* GRANITE-47247: Uppdatera till Sling Servlets Resolver 2.9.14 med prestandaförbättringar för serverupplösning.

### Åtgärdade problem {#fixed-issues-13804}

* GRANITE-47376: Författare (Infra) - Korrigera för DiscoveryTopologyOdefinierade fel efter rullande omstart.
* CQ-4353436: AEM Web Console (Sling) - Tomma konfigurationer i ServiceUserMapperImpl-validerare (Principal/User) bryter AEM Instance ([SLING-11912](https://issues.apache.org/jira/browse/SLING-11912)).
* SKYOPS-63925: Transformeringsjobb - Undvik TransformJob-fel med JDK 11 - ZipException: Ogiltiga CEN-rubrikfel (med flaggan disableZip64ExtraFieldValidation JVM).
* SKYOPS-63361: Transformeringsjobb (loggning) Förbättrad loggning med transformeringsjobb (understeget CUSTOMER_EXTRACT).
* SKYOPS-64103: FACT-verktyg (loggning) - Minska eller korta av fel- och varningsmeddelanden för Clientlib-kompilering.
* SKYOPS-65109: FACT-verktyget (felhantering) - Innehållspaket med olösta beroenden resulterar i ett korrekt rapporterat fel.
* SKYOPS-65368: FACT-verktyget (felhantering) - Verktyget körs i en oändlig inkluderingscykel och kan till slut ta slut i cirkulära inbäddningar av Clientlibs.
* SKYOPS-64031: RDE - ComponentCacheImpl kan försättas i ett inkonsekvent tillstånd på grund av duplicerad ResourceResolverFactory-registrering ([SLING-12019](https://issues.apache.org/jira/browse/SLING-12019)).
* ASSETS-29105: RDE - Begränsningsprovidern saknas i SecurityProviderRegistration requiredServicePids i RDE-funktionsmodellen.
* GRANITE-44674: CoralUI - Den datepicker-funktion som krävs är felaktig.

### Kända fel {#known-issues-13804}

Ingen.

### Inbäddade tekniker {#embedded-tech-13804}

| Teknik | Version | Länk |
|---|---|---|
| AEM | 1.56-T20230927085643-189caed | [Oak API 1.56.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.56.0/index.html) |
| AEM SLING API | Version 2.27.2 | [API för Apache Sling 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTML | Version 1.4.20-1.4.0 | [HTML-mallens språkspecifikation](https://github.com/adobe/htl-spec) |
| Grundläggande komponenter i AEM | Version 2.23.4 | [AEM WCM-kärnkomponenter](https://github.com/adobe/aem-core-wcm-components) |
