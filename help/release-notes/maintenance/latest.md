---
title: Aktuell information om underhållsversionen av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell information om underhållsversionen av  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 6493c48797c09fa4598c2c0ff86c9cc1fafa758c
workflow-type: tm+mt
source-wordcount: '1448'
ht-degree: 0%

---


# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs den tekniska versionsinformationen för den aktuella underhållsversionen av Experience Manager as a Cloud Service.

## Utgåva 20783 {#20783}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsutgåvan 20783, som offentliggjordes den 13 maj 2025. Den tidigare underhållsutgåvan släpptes 20626.

Funktionsaktiveringen i 2025.5.0 kommer att innehålla alla funktioner som finns i den här underhållsversionen. Mer information finns i [Experience Manager Releases Roadmap](https://experienceleague.adobe.com/sv/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Förbättringar {#enhancements-20783}

* FORMS-19125: Core Component Adaptive Form editor har förbättrats med stöd för automatisk mappning av tillgängliga adaptiva formulärfragment när ett motsvarande avsnitt från datakällträdet släpps på formulärets arbetsyta. Detta ger en viktig produktivitetsfunktion från den grundläggande redigeraren till kärnkomponenterna.
* FORMS-17107: AEM Forms erbjuder nu förbättrad tolkning av anpassade funktioner på klientsidan. Detta inkluderar stöd för moderna JavaScript-funktioner (ECMAScript ES10+), t.ex. valfri kedjekoppling, och introducerar möjligheten att använda statiska importer i anpassade funktionsskript. Detta gör att utvecklare bättre kan ordna kod, använda ESM-moduler och ta bort tidigare begränsningar som uppstått med anpassade funktioner i Adaptive Forms baserat på kärnkomponenter och Edge Delivery Services, särskilt för användare som tidigare behövde tillfälliga lösningar för dessa funktioner.
* SITES-27775: Optimerad referenssökning under publicering.
* SITES-30885: Optimerad JSON-bearbetning i beständiga frågor.
* SITES-25433: Edge Delivery med Universal Editor: Stöd för helsidesrendering vid jämförelse av gamla versioner.
* SITES-27792: Edge Delivery med Universal Editor: Lägg till specifik mall för Edge Delivery Service-konfigurationer
* SITES-19754: Edge Delivery med Universal Editor: övertygande felmeddelande när installationen har brutits.
* SITES-30328: Edge Delivery med Universal Editor: Preview from Sidekick support.
* SITES-23499: Edge Delivery med Universal Editor: tillåt att flera fält används för blockalternativ.
* SITES-29987: Lägg till funktion för att ange `previewUrlPattern` när innehållsfragmentmodeller skapas.
* SITES-29874: Lägg till stöd för LongTextField-referenser i Content Fragment API.
* SITES-29601: Lägg till validering för innehållsfragment som refereras via LongText-fält.
* SITES-24623: Gör ETags som returneras av GET och SEARCH fragments API användbara för korrigering.
* SITES-28557: Tillåt URL-parametern `references` i PATCH Content Fragment.
* SITES-5358: [OpenAPI] Kopiera innehållsfragment med underordnade.
* SITES-29614: GET Workflow endpoint.
* SITES-29615: List batch requests API endpoint.
* SITES-25130: Uppgradera kärnkomponenter till 2.28.0
* SITES-10575: &quot;MSM Blueprint Bloomfilter Loader&quot; försöker läsa in >100 000 rader.
* SITES-26711: Länkar för RTE-textfält uppdateras inte så att de pekar på den aktiva kopian vid MSM-utrullning.
* SITES-25976: Länkar inuti Experience Fragments som inte anpassar sig efter MSM-utrullning.

### Åtgärdade problem {#fixed-issues-20783}

* ASSETS-50994: Inkommande trafik blockerad vid AemRequestEventFilter.
* CQ-4358591: Projekt saknas för ett fåtal språk när språkkopior skapas från platsens referenspanel med alternativet&quot;Skapa översättningsprojekt&quot;.
* CQ-4359108: XLIFF 2.0-formatet misslyckas när import/export av mänsklig översättning används.
* CQ-4358722: Lokalisering fungerar inte för äldre ISO-koder på grund av olika språkkoder i Java 11 och Java 17.
* FORMS-19808: När du sparar ett stort formulär som innehåller fragment som har aktiverats vid lazy loading kan användaren inte hämta utkast.
* FORMS-19887: Ett nedrullningsbart fält i ett XFA-formulär, som till att börja med är skrivskyddat, kan inte ändras till en öppen/redigerbar status när formuläret återges i HTML5. Fältet förblir skrivskyddat och förhindrar användarinteraktion, till skillnad från PDF-återgivning där det fungerar som förväntat.
* FORMS-19651: I Regelredigeraren fungerar inte en regel korrekt när en knappklickning används i ett binärt villkor och samma knapp används också i Då-satsen för den regeln.
* FORMS-19628: I det automatiskt genererade DoR-dokumentet (Document of Record) för Core Component-baserad Adaptive Forms döljs också rotpanelens namn felaktigt om alternativet Tillåt RTF-text för rubrik är aktiverat på rotpanelen.
* FORMS-18977: PDF-filer som genererats av DoR-tjänsten (Document of Record) saknar dokumentets titel. Detta kan leda till att tillgänglighetsstandarderna PDF/UA och WCAG 2.1 inte följs eftersom dokumenttiteln är ett obligatoriskt attribut för tillgängliga PDF-filer.
* FORMS-18526: När en regel som innehåller flera fält i villkoren kopieras från ett fält till ett annat, behåller en fast fältreferens inom dessa villkor felaktigt sin referens till det ursprungliga källfältet i stället för att uppdateras till det nya fältet där regeln kopieras.
* FORMS-19047: När ett anpassat formulär har ändrats och publicerats på nytt i AEM Forms (särskilt 6.5.22.0) kanske översättningar för vissa formulärelement, särskilt textrutor, saknas.
* FORMS-19234: Tidslinjefunktionen för PDF-filer i AEM Forms, som gör att användare kan visa information om hur PDF skapar och versionshanterar, slutar fungera efter att en PDF har överförts under avsnittet Forms och dokument.
* FORMS-18196: HTTP-API:t för synkronisering `generatePrintedOutput` (eller `generatePdfOutput`) returnerar felaktigt en 200-svarskod (Slutfört) i stället för den förväntade 400-felkoden (Ogiltig begäran) när valfria fältdata som krävs för XDP-mallen lämnas tomma i begäran.
* FORMS-19336: I Core Component Adaptive Form Editor (AF2-redigerare) fungerar inte sökfunktionen i Data Source Tree korrekt eller som förväntat, vilket hindrar användare från att enkelt hitta specifika dataelement.
* FORMS-17707: AEP-anslutningen (Adobe Experience Platform) fungerar inte korrekt när den är konfigurerad för att ansluta till AEP-plattformens scen-miljöer.
* FORMS-18526: När du kopierar en regel som har villkor som baseras på flera fält uppdateras inte ett fält som refereras inom regelns villkor eller åtgärder (som inte är det primära fält som utlöser regeln) så att det korrekt refererar till det nya fältet som regeln kopieras till. I stället fortsätter den att referera till det ursprungliga källfältet som regeln kopierades från.
* FORMS-18474: En regel som utformats för att fokusera på en viss panel eller komponent när ett visst fälts värde ändras (t.ex. fält&quot;A&quot;) aktiveras felaktigt av en ändring i något fält i formuläret. Om till exempel fält B ändras ställs fokus fortfarande in på den avsedda panelen, även om regeln bara konfigurerades för ändringar i fält A.
* GRANITE-58276: OSGi-beroendecykler förhindrar att HTL-skriptmotorfabriken fungerar korrekt.
* OAK-11673: Ökning av CPU för Oak-segment-azure v12 som orsakas av refreshLease.
* SITES-30752: Använd inte `If-modified-since`/`last-modified`-huvuden när du genererar beständigt frågesvar.
* SITES-30353: GraphQL DataFetchingExceptions for &quot;src&quot; Field in AEM Content Fragments.
* SITES-30333: Läs metadata för resurser från jcr för att undvika xmp-tolkningsproblem.
* SITES-30140: Problem med dubbla fönster när innehållsfragmentreferens skapas.
* SITES-29748: Korrigera återgivningsvillkor för att visa hanteringspublicerings-/snabbpubliceringsåtgärder i CF-redigeraren.
* SITES-15452: Unika CF-element ska inte kontrolleras mot sina kopior vid starten.
* SITES-30386: Edge Delivery med Universal Editor: duplicerad UE cors.js gör att UE duplicerar avsnitt när innehåll läggs till.
* SITES-29745: Korrigerade ett sällsynt problem där variationer av referenser inte var hydrerade.
* SITES-30585: Det går inte att ange previewUrlPattern när du skapar modeller med referenser.
* SITES-30327: När du publicerar innehållsfragment utan behörigheter skapas separata arbetsflöden för varje nyttolastresurs.
* SITES-29528: ETag kan inte användas för cachelagring på publiceringsinstansen.
* SITES-30583: Verktyget Sök och ersätt ändrar alla tecken till gemener.
* SITES-31157: Patchen misslyckas på grund av inkonsekvent ETag.
* SITES-31327: [OpenAPI] Begäran om att hämta innehållsfragment på författarinstansen kan svara med 304.
* SITES-29691: NullPointerException uppstod vid försök att flytta sidan.
* SITES-30728: OnTime/OffTime publicerar/UnPublish inte som förväntat när det är konfigurerat för resursegenskaper.
* SITES-29789: Component Link Change on Copied Root Pages in AEM.
* SITES-29191: Det går inte att lägga till fler än 20 SKU:er i produktlistkomponenten.
* SITES-30372: Smart Crop fungerar inte på huvudkomponenten för AEM Image(V2).
* SITES-28693: Teaser Component renderar trasig HTML när Title är Empty.
* SITES-28668: Det går inte att höja upp Launch med LaunchPromotionParameters.
* SITES-31005: Förbättra användargränssnittet för utrullningsjobb för att visa kunden förloppet.
* SITES-31020: Förbättra användargränssnittet för att skapa live-kopieringsjobb så att kunden ser förloppet.
* SITES-29816: &quot;Resource Not found&quot; Error while Creating Live Copy of Experience Fragment.
* SITES-29363: Knappen Återställ live-kopia fungerar inte för kapslad innehållshierarki för live-kopia.
* SKYOPS-106509: Lägg till extra öppningsflaggor som stöder GSON-reflektiv åtkomst i Java 21.

### Kända fel {#known-issues-20783}

Ingen.

### Föråldrade funktioner och API:er {#deprecated-20783}

Inaktuella och borttagna funktioner och API:er i AEM as a Cloud Service beskrivs i dokumentet [Inaktuella och Borttagna funktioner och API:er](/help/release-notes/deprecated-removed-features.md).

### Säkerhetskorrigeringar {#security-20783}

AEM as a Cloud Service strävar efter att optimera säkerheten och prestandan för din plattform. Denna underhållsrelease åtgärdar 19 identifierade sårbarheter, vilket stärker vårt engagemang för robust systemskydd.

### Inbäddade tekniker {#embedded-tech-20783}

| Teknik | Version | Länk |
|---|---|---|
| AEM Oak | 1.78.1-T20250429061757 | [Oak API 1.78.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.78.0/index.html) |
| AEM SLING API | 2.27.6 | [API:t för Apache Sling 2.27.6 ](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.26-1.4.0 | [Språkspecifikation för HTML-mall](https://github.com/adobe/htl-spec) |
| Grundläggande komponenter i AEM | 2.29.0 | [AEM WCM Core Components](https://github.com/adobe/aem-core-wcm-components) |
