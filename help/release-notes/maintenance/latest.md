---
title: Aktuell information om underhållsversionen av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell information om underhållsversionen av  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: c1e175128ab6e4b483e3940d9bd86a06540ef40f
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 0%

---


# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs den tekniska versionsinformationen för den aktuella underhållsversionen av Experience Manager as a Cloud Service.

## Version 24464 {#release-24464}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsutgåva 24464, som offentliggjordes den 18 februari 2026. Den tidigare underhållsversionen var version 24288.

Funktionsaktiveringen i 2026.2.0 innehåller alla funktioner som finns i den här underhållsversionen. Mer information finns i [Experience Manager Releases Roadmap](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Förbättringar {#enhancements-24464}

* AEMARCH-264: Lägg till stöd för validering av villkorliga begäranden baserade på RequestEntity.
* AEMARCH-269: Visa JavaEE-validerings-API:er för OpenAPI-implementeringar.
* AEMARCH-276: Tillhandahåll stöd för i18n via RequestEntity.
* ASSETS-10995: Ange gräns för antal mediefiler i hämtningszip.
* ASSETS-50788: Uppdatera söknings-API:t så att det använder GET-API för resursmetadata.
* ASSETS-50946: Mappa begärandetext med hjälp av GET-metadatans API till JCR-metadata.
* ASSETS-55866: Undvik att skicka in nya begäranden för samma mediefil tills den tidigare bearbetningen är klar.
* ASSETS-60300: Ange API för att hämta asynkrona jobbkontext och resultat.
* ASSETS-60574: Lägg till stöd för den senaste versionen av Sling API-paketet.
* ASSETS-61049: Fortsätt med utveckling av metadatahanterarpaket.
* ASSETS-61692: Utför semantisk sökning som standard i API:t för att öppna sökning.
* ASSETS-61696: BAM-väg och MFE-wrapper i resursvyn.
* ASSETS-61854: Skicka GenStudio-lösning i aktiverings-/avaktiveringsmeddelande.
* ASSETS-61973: Skapa API i AEM för att hantera uppmaningar.
* ASSETS-62182: Asset Compute händelsehanterare för c2pa-manifest-återgivning.
* ASSETS-62311: Sökregressionsproblem.
* ASSETS-62413: Lägg till stöd för fältet customModifier i alla lager i JSON.
* ASSETS-62432: API-PR tas bort i sammanfogningsmappen.
* ASSETS-62540: Öka den användarvänliga versionen med pekfunktioner i snabbstart.
* ASSETS-62622: Hantera sökningsläge i MatchQuery.
* ASSETS-62671: Korrigera operatorn MatchQuery beginWith.
* ASSETS-62780: Växla till funktion för mapp-API.
* ASSETS-62988: Dölj c2pa-manifeståtergivningen så att den inte visas på återgivningsfliken.
* ASSETS-63336: Mallsynkronisering från AEM till DM ska bara ske för mappnamnsmetadata.
* ASSETS-63375: Lägg uppladdning av experimentella OpenAPI:er bakom funktionen toggle.
* ASSETS-63453: Kontrollera att alla användare kan läsa config för omnissearch.
* GRANITE-63744: Tillåt anslutning av asynkrona jobb till snedjobb.
* GRANITE-64567: Inaktivera semantisk sökning automatiskt för SKU-sökningar.
* GUIDES-41187: Lägg till rubriker för användning av stödlinjer.
* SITES-30452: Content API with ASO - title &amp; description ideas.
* SITES-33116: Korrigera sökvägsvalidering.
* SITES-34234: Page editor: preserve content tree state.

### Åtgärdade problem {#fixed-issues-24464}

* ASSETS-43198: E-postmeddelanden om förfallodatum för mediefiler respekterar inte användarens språkinställning.
* ASSETS-51840: Förbättrad tillgångsbearbetning.
* ASSETS-52061: Det går inte att gå tillbaka efter att du har valt en sparad sökning.
* ASSETS-53155: Förbättrat resursinnehåll.
* ASSETS-53745: Dynamiskt mediehämtningsflöde kräver att du avmarkerar originalresursen innan du väljer webbförinställning.
* ASSETS-54260: Korrigeringar av tillgångsinnehåll.
* ASSETS-54787: Förbättrat resursinnehåll.
* ASSETS-57391: Uppdateringar av medieinnehåll.
* ASSETS-59213: cq-dynamicmedia-core är beroende av det ersatta delade språkbiblioteket.
* ASSETS-59214: cq-scene7-imaging är beroende av det ersatta delade språkbiblioteket.
* ASSETS-59546: cq-remotedam-client-core är beroende av ersatt Commons-lang-bibliotek.
* ASSETS-59703: cq-dam-core är beroende av ersatt Commons-lang-bibliotek.
* ASSETS-59705: cq-dam-handler är beroende av ersatt Commons-lang-bibliotek.
* ASSETS-59707: cq-dam-indesign är beroende av ersatt Commons-lang-bibliotek.
* ASSETS-59709: cq-scene7-core är beroende av ersatt Commons-lang-bibliotek.
* ASSETS-59929: CSV från metadataexportbrytningar när fältet har radmatningstecken.
* ASSETS-60241: Det går inte att flytta asynkront jobb när mappnamnet ändras.
* ASSETS-61134: Ta bort compareVersion-taggar från PDF-filer.
* ASSETS-61309: Flytta/kopiera innehållsfragment uppdaterar inte längre interna referenser.
* ASSETS-61730: Omdirigering till direkt binär åtkomst bör respektera tillgångskodning.
* ASSETS-62358: Assets-rapportens CSV-fil visar skadade värden i innehållssökvägen.
* ASSETS-62610: Adobe Stock-licensknappen är inaktiverad i Assets-gränssnittet.
* ASSETS-62613: NPE i `downloadasset`/`saveas`.
* ASSETS-62656: Omnisearch AI-sökindikator visas felaktigt för icke-Assets-sökningar.
* GRANITE-55387: Om du korrigerar ord omgivna av citattecken tas hela ord bort.
* GRANITE-61240: RCE via lagrad XSS i lazycontainer.js.
* GRANITE-64101: OTB-index som konverterats till ES återgick till Lucene vid omstart.
* SITES-24530: Touchmålet för stängnings-/borttagningsknappar i sökmodala är inte tillräckligt stort.
* SITES-31425: Olokaliserat felmeddelande i startarbetsflödet.

### Kända fel {#known-issues-24464}

Ingen.

### Föråldrade funktioner och API:er {#deprecated-24464}

Inaktuella och borttagna funktioner och API:er i AEM as a Cloud Service beskrivs i dokumentet [Inaktuella och Borttagna funktioner och API:er](/help/release-notes/deprecated-removed-features.md).

### Säkerhetskorrigeringar {#security-24464}

AEM as a Cloud Service strävar efter att optimera säkerheten och prestandan för din plattform. Denna underhållsrelease åtgärdar 14 identifierade sårbarheter, vilket stärker vårt engagemang för robust systemskydd.

### Inbäddade tekniker {#embedded-tech-24464}

| Teknik | Version | Länk |
|---|---|---|
| AEM Oak | 1.90.0 | [Oak 1.90.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.90.0/index.html) |
| AEM SLING API | 2.27.6 | [API:t för Apache Sling 2.27.6 ](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Språkspecifikation för HTML-mall](https://github.com/adobe/htl-spec) |
| Apache HTTP-server | 2.4.65 | [Apache HTTP 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| Grundläggande komponenter i AEM | 2.30.4 | [AEM WCM Core Components](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (standard) | [Node.js-versioner som stöds](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |

