---
title: Aktuell underhållsversionsinformation för  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell underhållsversionsinformation för  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 82be9b2b328343e827b90bd8266d93127757f477
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 0%

---


# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs de tekniska versionsinformationen för den aktuella underhållsutgåvan av Experience Manager as a Cloud Service.

## Utgåva 17569 {#release-17569}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsutgåvan 17569, som offentliggjordes den 27 augusti 2024. Den tidigare underhållsversionen var version 17465.

Funktionsaktiveringen i 2024.9.0 kommer att innehålla alla funktioner som finns i den här underhållsversionen. Mer information finns i [Experience Manager Releases Roadmap](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Förbättringar {#enhancements-17569}

* CQ-4353778: Översättningsprocesshändelser.
* CQ-4354583: Skicka översättningsprocesshändelser via Adobe Pipeline.
* CQ-4356479: Tillåt endast Adobe-kod att använda /adobe-serverkontexten.
* CQ-4358133: Optimera användningen av Jenkins-arbetare.
* CQ-4358226: Funktionen för att spara översättningsnyckelord fungerar inte för ett visst strängformat.
* CQ-4358270: AEM Translation Kit: 8 augusti.
* CQ-4358310: Lägg till oak-compat-query-spi-1.2 för snabbstart.
* GRANITE-36205: Automatisk uppdatering för intern ekrelease i QS.
* GRANITE-49833: Grupperingsstöd för händelseländare och proxy.
* GRANITE-52053: Ta bort användning av Commons Collections 3: Platform others.
* GRANITE-52492: Elastisk async-hämtning vid PIT-återställning.
* GRANITE-53086: Uppdatera jacoco plugin-version till 0.8.12 i AEMaaCS.
* GRANITE-53099: Uppdatering till Apache Felix HTTP Jetty 5.1.24.
* GRANITE-53125: Lägg till klassificering i CloudEvent.
* GRANITE-53328: Uppdatera Fireault till 3.8.0-T2024072611512-3cc11d50 som innehåller förbättringar av hash-loggning.
* GRANITE-53340: AEM660: Proper Versioning and branching for 660 CQ/Platform.
* GRANITE-53341: Varna inte om ACS Commons 6 används.
* GRANITE-53453: update commons-lang to 3.15.0.
* GRANITE-53473: Oföråldrade Sling-inställningar.
* GRANITE-53478: Uppdatera Fireworks till version 3.8.0.
* GRANITE-53505: Uppdatera QS till Commons-collections-3.2.2-adobe-2.
* GRANITE-53528: Uppdateringsversion av plattformsartefakter .
* GRANITE-53547: Ange ett alternativt API som undviker att använda Apache Commons Lang 2.
* GRANITE-53575: Använd BSAFE 6.2.5 i CS.
* GRANITE-53608: Uppdatera Oak till den senaste offentliga versionen (1.68.0).
* SITES-23583: Sites Evergreen-tester misslyckas i Java 17.
* SKYOPS-79535: Uppdatera till rum-skript v2.
* SKYOPS-79816: Aktivera aktiviteten Sling Feature Analyzer Task för Service User Mappings in FACT Tool.
* SKYOPS-81179: AEM bygger testning för paket som ska växlas.
* SKYOPS-81866: Rapportera varningar för paket som inte är kompatibla med Java 21.
* SKYOPS-82660: Uppdatera Sling API till 2.27.6.
* SKYOPS-82961: Uppdatera till Sling ResourceResolver 1.12.0-T20240723153354-a0270a0.
* SKYOPS-83356: Skapa en global kontrollpanel för spårning av JVM-versioner som används i AEM.
* SKYOPS-83436: Java Runtime 21-utrullning avbryter skapandet av adaptiva formulär AEM Forms.
* SKYOPS-84272: Logga den java-version som används vid start av aem.

### Åtgärdade problem {#fixed-issues-17569}

* CMGR-60225: Pipeline-körningsfel identifierades på AEM Sites CS-kund vid validering av AEM version 17486.
* GRANITE-45919: Embargoed countries in Country/Region list in Edit User Settings.
* GRANITE-51715: Det händer att väljaren inte anger markeringen i textfältet.
* GRANITE-53290: Kontrollera protokollet korrekt när du tolkar URL:en i XSS-kontrollen.
* GRANITE-53576: Felaktig definition av servicerankning i OSGi-konfigurationer.
* SKYOPS-82129: Memoryleak i Sling Models.

### Kända fel {#known-issues-17569}

Ingen.

### Ändringsmeddelande {#change-notice-17569}

* Från och med september 2024 kommer AEM as a Cloud Service att inaktivera serialiseringen av resurslösare via Sling Model Exporter-ramverket. Mer information finns i [dokumentationen](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md).

### Föråldrade funktioner och API:er {#deprecated-17569}

Observera att vi håller på att uppdatera `com.day.cq.wcm.api` och med den aktuella versionen har vi markerat `@Deprecated` som några av dess metoder och klasser. Dessa kommer att tas bort i framtida versioner, så överväg att byta till de föreslagna alternativen om du använder något av dem.

Inaktuella och borttagna funktioner och API:er i AEM as a Cloud Service beskrivs i dokumentet [Inaktuella och Borttagna funktioner och API:er](/help/release-notes/deprecated-removed-features.md).

### Säkerhetskorrigeringar {#security-17569}

AEM as a Cloud Service strävar efter att optimera säkerheten och prestandan för din plattform. Denna underhållsrelease åtgärdar fyra identifierade sårbarheter, vilket stärker vårt engagemang för robust systemskydd.

### Inbäddade tekniker {#embedded-tech-17569}

| Teknik | Version | Länk |
|---|---|---|
| AEM Oak | 1.68.0 | [Oak API 1.68.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.68.0/index.html) |
| AEM SLING API | 2.27.6 | [API:t för Apache Sling 2.27.6 ](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTML | 1.4.24-1.4.0 | [Språkspecifikation för HTML-mall](https://github.com/adobe/htl-spec) |
| Grundläggande komponenter i AEM | 2.26.0 | [AEM WCM-kärnkomponenter](https://github.com/adobe/aem-core-wcm-components) |
