---
title: Aktuell information om underhållsversionen av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell information om underhållsversionen av  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: d73ccc454c89c7e06752de694af97ac26694be17
workflow-type: tm+mt
source-wordcount: '902'
ht-degree: 0%

---


# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs den tekniska versionsinformationen för den aktuella underhållsversionen av Experience Manager as a Cloud Service.

## Version 22450 {#22450}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsutgåvan 22450, som offentliggjordes den 16 september 2025. Den tidigare underhållsversionen var version 22171.

Funktionsaktiveringen i 2025.9.0 kommer att innehålla alla funktioner som finns i den här underhållsversionen. Mer information finns i [Experience Manager Releases Roadmap](https://experienceleague.adobe.com/sv/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Nya funktioner {#new-features-22450}

* SITES-32595: Arbetsflöden som slutförs med överhoppade eller avvisade fragment kan nu identifieras. En ny egenskap är tillgänglig i arbetsflödes-API:ts svar, med en lista över fragment som har utelämnats på grund av att de är ogiltiga eller har ogiltiga referenser.
* SITES-33642: En ny API-händelse skapas och används nu för ändrade innehållsfragment.
* SITES-33320: Nu går det att söka efter en innehållsfragmentmodell med hjälp av dess `technicalName` via söknings-API.

### Förbättringar {#enhancements-22450}

* SITES-34023: Fältet `technicalName` har lagts till i svaren för slutpunkterna för innehållsfragmentmodellen för bättre identifiering.
* SITES-32766: Content Asset References i Content Fragment Models har nu stöd för ett större antal binära filtyper.
* SITES-33974: Förbättrad OpenAPI-dokumentation som gör den mer korrekt och användarvänlig.
* SITES-9173: Cache `ContentPolicyStatus`.
* SITES-9290: Förbättra cachelagringen av `TouchEditContext`.
* SITES-33355: Öppna ny CF-redigerare för Visa nyttolast i arbetsflödeskonsolen.
* SITES-33356: Öppna ny CF-redigerare för Create CF → Öppna i TouchUI Admin UI.
* SITES-32952: Inkonsekvent hantering av standardvärden för CFM-fält när leverans-API används.
* SITES-31539: Edge Delivery med Universal Editor: Lägg till stöd för metataggar i konfigurationen för Universal Editor i `head.html`.
* SITES-20672: Edge Delivery med Universal Editor: Lägg till stöd för ytterligare kalkylblad med massmetadata vid redigering.
* SITES-32963: Edge Delivery med Universal Editor: Lägg till nya experimenteringsmetadata för optimeringsmål, automatisk allokering och självlärande.
* SITES-30847: Release Core Components 2.30.0.
* SITES-29617: Slutpunkten referencedBy har uppdaterats för att använda klassen ReferenceSearch, vilket förbättrar dess prestanda och tillförlitlighet.
* SITES-19308: Förbättrade prestanda för sidborttagningsprocessen genom att optimera referensvalideringssteget.
* SITES-34293: Implementerad lazy loading för mallresurser för att förbättra prestandan.
* SITES-33892: Lade till en funktionsväxling för att hoppa över referenskontroller för pseudosidor, vilket kan förbättra prestanda.

### Åtgärdade problem {#fixed-issues-22450}

* CQ-4360550: Korrigerat oväntat försvinnande av språkkopia efter återgång av sidflyttning i AEM Cloud-tjänsten.
* SITES-25232: Länkarna för att ange datum och tid för avslut har ingen synlig fokusindikator.
* SITES-25258: Fokus hanteras inte med den modala dialogrutan Ta bort anteckning.
* SITES-25305: Det demografiska verktygsfältet får inte fokus i en logisk ordning.
* SITES-25366: Skärmläsaren meddelar inte om inläsningsstatus för teaser modal.
* SITES-34276: Edge Delivery med Universal Editor: fix skapade automatiskt CORS-princip som inte tillämpades på publiceringsnivån.
* SITES-34811: Edge Delivery med Universal Editor: fix hlx selector läggs inte till i länkar till kalkylblad vid redigering.
* SITES-31669: Olokaliserade strängar &quot;This page redirects to&quot; i Verktyg > Sites > Launches.
* SITES-30879: Olokaliserade strängar i Sites > Page Editor > Sökkomponent.
* SITES-30959: Olokaliserade strängar i sidredigeraren > Bildkomponent.
* SITES-21743: Olokaliserad &quot;Välj ett dokument som ska visas.&quot; i Page Editor > PDF Viewer
* SITES-19785: Strängar är olokaliserade på platsen Core Components > Tabs.
* SITES-22059: Olokaliserad sträng &quot;File preview not available&quot; i Core Components site > PDF Viewer.
* SITES-33360: Olokaliserad &quot;Error during operation. Den angivna sökvägen är inte en startsträng i Startar > Redigera.
* SITES-32975: Olokaliserat datumformat i Headless UI > Launches > Compare Launch to Source.
* SITES-32973: Hardcoded strings in Headless UI > Launches > Rebase.
* SITES-13540: Unlocalized strings in Launches > Promotion.
* SITES-13085: Olokaliserade felsträngar på Sites > Startsida för skapande.
* SITES-21499: Den olokaliserade strängen är Sites > Launches > Edit.
* SITES-14961: Trunkering av datumfält i Sites >Properties > Blueprint > Rollout dialog.
* SITES-33764: Startfilter (Source Path/Workflow-created Launches) fungerar inte.
* SITES-33884:&quot;Promote current page and sub pages&quot; höjer oavsiktligt sidor som inte omfattas.
* SITES-33611: Översikt över Live-text fungerar inte för stora volymer.
* SITES-34331: 503 Timeout vid inläsning av övertäckning för utrullning för icke-admin-användare.
* SITES-34403: `NullPointerException` i `GraphqlClientImpl deactivate()` under avstängning.
* SITES-33817: Löste synkroniseringsproblem mellan gränssnittsschemat och JCR-modellen för att säkerställa konsekvens.
* SITES-31141: Innehållsreferenser som inte representeras av sökväg returneras nu korrekt i API-svaret.
* SITES-34080: Processen för att skapa innehållsfragment är nu mer robust och kommer inte att misslyckas om inga fält anges för begäran.
* SITES-30773: Det reguljära uttrycket för att söka efter ord med &quot;Sök och ersätt&quot; har förbättrats så att det matchar UTF-8-tecken.
* SITES-33742: Ett fel som gjorde att ett innehållsfragment inte kunde flyttas när arbetsflödes-API användes har åtgärdats.

### Kända fel {#known-issues-22450}

Ingen.

### Föråldrade funktioner och API:er {#deprecated-22450}

Inaktuella och borttagna funktioner och API:er i AEM as a Cloud Service beskrivs i dokumentet [Inaktuella och Borttagna funktioner och API:er](/help/release-notes/deprecated-removed-features.md).

### Säkerhetskorrigeringar {#security-22450}

AEM as a Cloud Service strävar efter att optimera säkerheten och prestandan för din plattform. Denna underhållsrelease åtgärdar 18 identifierade sårbarheter, vilket stärker vårt engagemang för robust systemskydd.

### Inbäddade tekniker {#embedded-tech-22450}

| Teknik | Version | Länk |
|---|---|---|
| AEM Oak | 1.84.0 | [Oak API 1.84.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.84/index.html) |
| AEM SLING API | 2.27.6 | [API:t för Apache Sling 2.27.6 ](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Språkspecifikation för HTML-mall](https://github.com/adobe/htl-spec) |
| Apache HTTP-server | 2.4.65 | [Apache HTTP 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| Grundläggande komponenter i AEM | 2.29.0 | [AEM WCM Core Components](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (standard) | [Node.js-versioner som stöds](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
