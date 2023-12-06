---
title: Aktuell underhållsanvisning för [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell underhållsanvisning för [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 2677e8fbdf6b21ce2d1d848000401c826bc5f289
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 1%

---

# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs den tekniska versionsinformationen för den aktuella underhållsutgåvan av Experience Manager as a Cloud Service.

## Utgåva 14538 {#release-14538}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsreleasen 14538, som offentliggjordes den 6 december 2023. Den här underhållsversionen är en uppdatering från den tidigare underhållsversionen 14227.

2023.12.0 Funktionsaktivering innehåller alla funktioner som finns i den här underhållsversionen. Se [Roadmap för lanseringar av Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html) för mer information.

### Förbättringar {#enhancements-14538}

* GRANITE-46723: Användarsynkronisering - SAML-migrering från standardsynkronisering till IDP-baserad synkronisering.
* OAK-10311: Replikering - Optimera blobbjämförelse för att minska replikeringstiden för stora grupper resurser i AEM.
* OAK-10511: Replikering - Minska antalet nätverksrundresor för att minska replikeringstiden för stora resurser i AEM.
* GRANITE-48334: Utgivare - samlingsskript saknas för RUM.

### Åtgärdade problem {#fixed-issues-14538}

* CQ-4354867: ToggleCondition-referensen refererar till ett fält som inte finns i InstanceActionServlet.
* CQ-4349948: Lokalisering av strängar för &#39;Profilegenskaper&#39; i Redigera användarinställningar under Verktyg → Säkerhet → Användare.
* GRANITE-44541: Lokalisering av feldialogrutor när du lägger till en privat nyckelfilskärm i Redigera användare > Nyckelbehållare under Verktyg → Säkerhet → Användare.
* GRANITE-45341: Lokalisering av lyckade/misslyckade strängar för aktivering/inaktivering av användaråtgärd under Verktyg → Säkerhet → Användare.
* GRANITE-46650: Lokalisering av felmeddelandet &quot;UserId/Password mismatch&quot;. -sträng under Verktyg → Dokumentskydd → Användare skapar dialogruta.
* GRANITE-47764: Uppdatering till Sling Models API 1.5.0: Inmatning till en statisk variabel i en Sling Model orsakar kompileringsfel (SLING-11507).
* GRANITE-48452: Skickar tomma klienter med statuskod 200.
* GRANITE-48410: ResourceResolver är inte stängd.
* ASSETS-31297: Förhindra att kopierade resurser tas bort från dynamiska medier.
* ASSETS-30811: Referensuppdateringar för Blocktag-tjänstbindning.
* GRANITE-46418: Update Sling-händelser i AEM: GaugeSupport har en oändlig rekursion i registerWithSuffix (SLING-11918).

### Kända fel {#known-issues-14538}

Ingen.

### Inbäddade tekniker {#embedded-tech-14538}

| Teknik | Version | Länk |
|---|---|---|
| AEM | 1.58-T20231123092841-619e1bd | [API för Oak API 1.58.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.58.0/index.html) |
| AEM SLING API | Version 2.27.2 | [API för Apache Sling 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTML | Version 1.4.20-1.4.0 | [HTML-mallens språkspecifikation](https://github.com/adobe/htl-spec) |
| Grundläggande komponenter i AEM | Version 2.23.4 | [AEM WCM-kärnkomponenter](https://github.com/adobe/aem-core-wcm-components) |
