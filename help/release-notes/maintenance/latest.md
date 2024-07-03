---
title: Aktuell underhållsanvisning för [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell underhållsanvisning för [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: f4b2ea5dac880738e6412541f06b85a6a83ccf40
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 0%

---

# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs de tekniska versionsinformationen för den aktuella underhållsutgåvan av Experience Manager as a Cloud Service.

## Utgåva 16799 {#release-16799}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsutgåvan 16799, som offentliggjordes den 18 juni 2024. Den tidigare underhållsversionen var version 16544.

2024.6.0 Funktionsaktivering innehåller alla funktioner som finns i den här underhållsversionen. Se [Roadmap för lanseringar av Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) för mer information.

### Förbättringar {#enhancements-16799}

* ASSETS-31977: Förbättrade åtgärder för att flytta, kopiera och ta bort resurser.
* ASSETS-33618: Funktioner för automatisk transkription och översättning av videoklipp i Dynamic Media.
* ASSETS-35185: Godkännandeåtgärd för ContentHub och DM och lägg till egenskaper i egenskaperna damAssetLucene.
* ASSETS-35533: Lägg till DRM- och CAI-egenskaper i index damAssetLucene.
* ASSETS-37280: Sekventiell jobbhantering för översättning när källunderrubriken (vtt) fortfarande bearbetas.
* ASSETS-37559: Förbättrad händelse för borttagning av resurser.
* ASSETS-37723: Implementera resurspublicerad händelse.
* ASSETS-37724: Implementera opublicerad händelse för resurs.
* ASSETS-38614: Förbättringar i användargränssnittet för Share Link.
* ASSETS-39601: Använd valideringsregex automatiskt på resursens LiveCycle-namn.
* ASSETS-39454: Uppgradera till visningsprogram för 2024.5.0 i Quickstart.
* CNTBF-184: Supportsökvägar under `/conf` i innehållsomflödning.

### Åtgärdade problem {#fixed-issues-16799}

* ASSETS-37335: Om du redigerar sökpanelen i filtret avmarkeras alla rutor.
* ASSETS-38069: AEM DAM PDF Preview Issue on Timeline Filter Selection.
* ASSETS-38215: Adobe Stock-licensknapp är nedtonad i AEM as a Cloud Service for enterprise-prenumeration.
* ASSETS-38578: Felaktiga hyperlänkar i Assets Link Share Report.
* ASSETS-38678: Visningsinställningarna är brutna i samlingsinformationen.
* ASSETS-39071: Webboptimerad leverans kan generera ett undantag om den ursprungliga återgivningens mimeType är null.
* ASSETS-39316: Sortering efter namn fungerar inte i samlingar.
* ASSETS-39377: Massimport från OneDrive kan misslyckas om du får ett baktryck från fjärr-API.
* ASSETS-39428: Återgivningsproblem i gränssnittet för copyrighthantering.
* CQ-4357150: Guava i cq-content-sync bundle.
* GRANITE-52573: Begäranden som innehåller dubbla snedstreck `//` nekas med statuskod 400.
* SCRNS-4194: Ta bort beroendet av Google Guava API:er.
* SCRNS-4360: Publish-knappen Hantera publikation och Snabb saknas för användare som inte är administratörer i innehållsleverantören för kanaler.
* SCRNS-4323: Hide/Disable launches from screens.html.
* FORMS-14844: Adaptiv Forms tillåter att formulär skickas trots att reCAPTCHA-verifiering misslyckas.
* FORMS-14984: Forms med CAPTCHA hoppar över validering om &quot;submitMetaData&quot; saknas i skickade data.
* FORMS-14477: Alternativen &quot;Är efter&quot; och &quot;Är före&quot; i regelredigeraren fungerar inte i datumväljarens validering.
* FORMS-14019: Regelredigerarens &quot;Invoke Service&quot;-funktion fungerar inte i Universal Editor.
* FORMS-14336: När inget formulärfält är markerat ska redigeraren öppnas med fokus på hela formulärelementet.
* FORMS-15061: Loader-cirkeln kvarstår oändligt när alternativet invoke service används i regelredigeraren.

### Kända fel {#known-issues-16799}

>[!NOTE]
> AEM Engineering har identifierat en regression för startfunktioner som påverkar aktuella AEM från och med 16461. På grund av den här regressionen kommer nya startprogram (som skapats efter att nya versioner har tillämpats) som innehåller sidor som inte är djupa inte att befordras korrekt på grund av saknade konfigurationer.
> Om dina miljöer påverkas finns ett gränssnittsskript som identifierar och uppdaterar saknade konfigurationer tillgängliga via kundsupport (intern referens, SITES-22457).
> En mer långsiktig korrigering kommer att göras tillgänglig som säkerställer att nya startprogram skapas med alla de rätta konfigurationerna. Till dess finns även en intern korrigeringsversion tillgänglig vid behov.

#### Forms

* När du installerar AEM SDK och lägger till `AEM Forms add-on v2024.05.04.00-240400`startar inte Docker-tjänsten. Dockningstjänsten krävs för att generera arkivhandlingar i en lokal utvecklingsmiljö. Så här åtgärdar du problemet:
   1. Ladda ned [snabbkorrigering](/help/forms/assets/sdk_hotfix.zip). När du laddar ned snabbkorrigeringen kan du `.zip` mappen hämtas.
   1. Extrahera den hämtade snabbkorrigeringen till en mapp.
   1. Ersätt äldre `sdk.sh` och `sdk.bat` filer med nyare filer i den mapp som extraherats i steg 2.

### Ändringsmeddelande {#change-notice-16799}

* Den här versionen innehåller följande nya produktindexversioner:
   * **damAssetLucene-11**
   * **fragments-11**

  Anpassade versioner av tidigare indexversioner sammanfogas automatiskt med den nya produktindexversionen. Använd ytterligare anpassade uppdateringar för den sammanfogade versionen.

* Från och med september 2024 kommer AEM as a Cloud Service att inaktivera serialiseringen av resurslösare via Sling Model Exporter-ramverket. Se [dokumentationen](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md) för mer information.

### Föråldrade funktioner och API:er {#deprecated-16799}

Om du vill veta vad som är föråldrat eller borttaget i AEM as a Cloud Service går du till [Föråldrade och borttagna funktioner och API:er](/help/release-notes/deprecated-removed-features.md).

### Inbäddade tekniker {#embedded-tech-16799}

| Teknik | Version | Länk |
|---|---|---|
| AEM Oak | 1.64.0 | [Oak API 1.64.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.64.0/index.html) |
| AEM SLING API | 2.27.2 | [API för Apache Sling 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTML | 1.4.22-1.4.0 | [HTML-mallens språkspecifikation](https://github.com/adobe/htl-spec) |
| Grundläggande komponenter i AEM | 2.25.4 | [AEM WCM-kärnkomponenter](https://github.com/adobe/aem-core-wcm-components) |
