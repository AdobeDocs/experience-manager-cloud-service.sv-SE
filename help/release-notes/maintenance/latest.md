---
title: Aktuell information om underhållsversionen av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell information om underhållsversionen av  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 3686697c85273ccc13e80b8d7f4ad1ff3c79845d
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 0%

---


# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs den tekniska versionsinformationen för den aktuella underhållsversionen av Experience Manager as a Cloud Service.

## Version 21706 {#21706}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsutgåvan 21706, som offentliggjordes den 24 juli 2025. Den tidigare underhållsversionen var version 21570.

>[!NOTE]
>
>Version 21644 gjordes privat och ersattes av version 21706.

Funktionsaktiveringen i 2025.7.0 kommer att innehålla alla funktioner som finns i den här underhållsversionen. Mer information finns i [Experience Manager Releases Roadmap](https://experienceleague.adobe.com/sv/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Förbättringar {#enhancements-21706}

* ASSETS-39377: Förbättra hanteringen av 429s från fjärrlagring i Assets Bulk Importer.
* ASSETS-46026: Konfigurerbart maxdjup för metadataexporterare.
* ASSETS-49172: Resurser i dynamiska mediamallar ska ärva metadata från mappen.
* ASSETS-50209: Stöd för delsträngar i DM-mallar.
* ASSETS-52326: AEM Assets konfigurationssida som anger visningsinställningar för titlar för Assets.
* ASSETS-52805: Lägg till CSV-utdata/hämtningsstöd för ett gruppåtgärdsjobb.
* ASSETS-52873: Lägg till en ny konfiguration i mappegenskaperna för att inaktivera AI-bearbetning för den mappen.
* ASSETS-53535: Förbättrade prestanda för YouTube videoöverföring.
* ASSETS-53612: Kontroll för hybridsökning i Assets Omnisearch.
* GRANITE-60183: Uppdatera beroendet för Commons-fileupload till 1.6.0.
* GRANITE-60287: Uppdatering QS till Jackrabbit 2.2.1.
* SITES-30452: Content API with ASO - Title &amp; Description Suggquestions.
* SITES-31677: Anpassad arbetsyta stöder export av AEM Content fragment till Target.
* SKYOPS-112741: Ta bort paketet `com.adobe.granite.product.support` från AEM-CS SDK.

### Åtgärdade problem {#fixed-issues-21706}

* ASSETS-12882: UI-justeringsproblem efter att visningsförinställningar öppnats.
* ASSETS-48958: Problem med att ändra publiceringsstatus för resurssynkronisering på lokala AEM-platser.
* ASSETS-50856: `dam:processingAttempts` återställs inte vid completeUpload.
* ASSETS-51604: CSV-fil för länkdelningsrapport saknas &quot;Delad med&quot;-data.
* ASSETS-51783: Återgå till DM-konfigurationen under `/conf/global` om ingen konfiguration hittades med sökfrågan.
* ASSETS-51857: Det går inte att ordna om tillgångstabellobjekt.
* ASSETS-52169: Ny maskinvaruåtergivning från BAT ingår felaktigt i hämtningar av resurser.
* ASSETS-52229: Inkorgsmeddelanden saknas för resursrapporter i AEM as a Cloud Service.
* ASSETS-52399: Versionsfel i com.day.cq.dam.api kan få kundkoden att gå sönder.
* ASSETS-52780: Resursen kan markeras för förhandsgranskning även om den inte är aktiverad.
* ASSETS-52866: Migrerade DM-videor är fortfarande i bearbetningstillstånd i en mapp där DM Sync är inaktiverat.
* ASSETS-53237: Listrutan Färgprofil är tom i redigeraren för bildförinställningar.
* ASSETS-53240: Resursrapport - Diskanvändning misslyckas vid hämtning av resursåtergivningsstorlek från Dynamic Media.
* ASSETS-53446: Intermittent uppdatering av YouTube auth-token på grund av NPE.
* ASSETS-53827: ACL-valideringsblock sparar blandade medieuppsättningar.
* ASSETS-5403: Dynamiska medieklientlibs som används i publiceringsinstansen ska ha `allowProxy=true`.
* ASSETS-54261: Import av metadata läcker anslutningar och blockeras om filen inte kan hämtas.
* CQ-4359863: Taggsökning efter nyckelord som är i fel ordning i Content Fragment Editor/Resursredigeraren.
* CQ-4359958: Gör stöd för openapi kompatibelt med AEM 6.5.22.0 och senare.
* CQ-4360256: Inkludera serverns kontextsökväg i sökvägen för HTTP-begäranden som hanteras via serverletskontexten `/adobe`.
* CQ-4360317: Lägg till metod för inställning av Sunset-datumhuvudet när svar skapas.
* GRANITE-60311: AEM SDK Quickstart - NPE på OSGi Installer Configuration Printer.
* GS-15285: Användare visas som inaktiverade.

### Kända fel {#known-issues-21706}

Ingen.

### Föråldrade funktioner och API:er {#deprecated-21706}

Inaktuella och borttagna funktioner och API:er i AEM as a Cloud Service beskrivs i dokumentet [Inaktuella och Borttagna funktioner och API:er](/help/release-notes/deprecated-removed-features.md).

### Säkerhetskorrigeringar {#security-21706}

AEM as a Cloud Service strävar efter att optimera säkerheten och prestandan för din plattform. Denna underhållsrelease åtgärdar fyra identifierade sårbarheter, vilket stärker vårt engagemang för robust systemskydd.

### Inbäddade tekniker {#embedded-tech-21706}

| Teknik | Version | Länk |
|---|---|---|
| AEM Oak | 1.80.0 | [Oak API 1.80.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.80/index.html) |
| AEM SLING API | 2.27.6 | [API:t för Apache Sling 2.27.6 ](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Språkspecifikation för HTML-mall](https://github.com/adobe/htl-spec) |
| Apache HTTP-server | 2.4.63 | [Apache HTTP 2.4.63](https://github.com/apache/httpd/blob/2.4.63/CHANGES) |
| Grundläggande komponenter i AEM | 2.29.0 | [AEM WCM Core Components](https://github.com/adobe/aem-core-wcm-components) |
