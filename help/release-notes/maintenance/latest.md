---
title: Aktuell information om underhållsversionen av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell information om underhållsversionen av  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 467e21aff1c2164be729598d03f30f6a9e90c8aa
workflow-type: tm+mt
source-wordcount: '1758'
ht-degree: 0%

---


# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs den tekniska versionsinformationen för den aktuella underhållsversionen av Experience Manager as a Cloud Service.

## Utgåva 21331 {#21331}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsreleasen 21331, som offentliggjordes den 24 juni 2025. Den tidigare underhållsutgåvan släpptes 21193.

Funktionsaktiveringen i 2025.7.0 kommer att innehålla alla funktioner som finns i den här underhållsversionen. Mer information finns i [Experience Manager Releases Roadmap](https://experienceleague.adobe.com/sv/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Förbättringar {#enhancements-21331}

* CQ-4356522: `WorkflowResourceStatusProvider`-optimering.
* FORMS-16458: Gränssnitt för teckensnittsegenskaper (teckensnitt).
* FORMS-17707: AEP Connector fungerar inte på AEP plattformsscen.
* FORMS-19125: Stöd för automatisk fragmentmappning i AF-redigeraren.
* FORMS-19336: Sökningen har lagts till i Data Source Tree i AF-redigeraren.
* FORMS-19417: Stöd för alternativknappar i hierarkivyn.
* FORMS-19603: Stöd för mallsidor och designsidor i både regelredigeraren.
* SITES-5358: Content Fragments Rest API: Copy CFs with children.
* SITES-10575: &quot;MSM Blueprint Bloomfilter Loader&quot; försöker läsa in fler än 10000 rader.
* SITES-14542: Om du byter namn på/flyttar en källsida för live-kopia bör publiceringen av den omdöpta/flyttade sidan för live-kopia utlösas om den redan har publicerats.
* SITES-19754: Edge Delivery med Universal Editor: Lägg till ett läsbart felmeddelande när integreringen har problem.
* SITES-23499: Edge Delivery med Universal Editor: Lägg till stöd för flera fält som ska användas för blockalternativ.
* SITES-23518: Edge Delivery with Universal Editor: Add support for Edge Delivery specific asset renditions.
* SITES-24436: Content Fragments Rest API: Introducerat lokalt cacheminne för att påskynda hämtningen av dubblettreferenser.
* SITES-25155: Content Fragments Rest API: Ta bort den inaktuella frågeparametern&quot;enabledForFolder&quot; i modelllistan.
* SITES-25913: Content Fragments Rest API: tidsboxed validation of resources before starting the publish workflow.
* SITES-25976: Länkar inuti Experience Fragments som inte anpassar sig efter MSM-utrullning.
* SITES-26271: Content Fragments Rest API: växla till BFS Traversal för GET Variation-slutpunkten.
* SITES-27486: Universal Editor - AEM Integration.
* SITES-27775: Optimerad referenssökning under publicering (lat metadatainläsning).
* SITES-27782: Edge Delivery med Universal Editor: Lägg till specifik utgivar-prenumerant-implementering för att publicera innehåll i Edge Delivery (tidig åtkomst).
* SITES-27792: Edge Delivery med Universal Editor: Lägg till dedikerad mall för Edge Delivery-tjänstkonfiguration.
* SITES-28557: Content Fragments Rest API: Tillåt användning av ETags som hämtats genom att anropa `/cf/fragments/{fragmentId}` med `references=direct` för att korrigera ett innehållsfragment.
* SITES-28683: Tillåt att MSM LiveRelationship-sökningar hoppar över avancerad status.
* SITES-29601: Content Fragments Rest API: Validation for long text fields&#39; content fragment references.
* SITES-29614: Content Fragments Rest API: Hämta ett arbetsflöde med slutpunkten `/cf/workflows/{workflowInstanceId}`, där workflowInstanceIda är det ID som returnerades av publiceringsbegäran.
* SITES-29615: Content Fragments Rest API: Visa alla gruppbegäranden som skapats via POST `/cf/batch` med `GET /cf/batch`.
* SITES-29874: Content Fragments Rest API: Referenser från långa textfält i innehållsfragment hämtas och hydreras nu.
* SITES-29930: Content Fragments Rest API: add metrics for the Content Fragment Publish workflow.
* SITES-29986: Content Fragments Rest API: stöd för teknisk namngivning av CF-modell.
* SITES-30088: Content Fragments Rest API: CF Publish - hoppa över hämtning av referenser när filterReferencesByStatus är tom.
* SITES-30126: Content Fragments Rest API: prestandaförbättring för CF-publicering: ersatte kontrollen om en resurs är ett fragment med en minimal kontroll.
* SITES-30328: Edge Delivery med Universal Editor: Lägg till stöd för förhandsgranskning från Sidekick.
* SITES-30445: Content Fragments Rest API: CF Model UI-schema: lägg till ett alternativ för att styra ursprungligt läge för komprimeringsbart.
* SITES-30604: Content Fragments Rest API: stöd för användning av Model Metadata Schema i nytt användargränssnitt.
* SITES-30885: Optimerad JSON-bearbetning i beständiga frågor.
* SITES-30886: Content Fragments Rest API: GET-arbetsflöden för Content Fragment-slutpunkt baserat på fragmenthandböcker som lagras i arbetsflödets metadata.
* SITES-31005: Förbättra användargränssnittet för utfällbara projekt så att förloppet visas.
* SITES-31020: Förbättra användargränssnittet för att skapa live-kopieringsjobb så att förloppet visas.
* SITES-31111: Content Fragments Rest API: Allow variation patch API to accept Content Fragment references inside Content Fragment launches.
* SITES-31343: Content Fragments Rest API: Lägg till filtrering och sidnumrering efter datum till slutpunkt som listar gruppförfrågningar.
* SITES-31472: Delete Launch kan göra att databasen pausas om det blir en enorm starttid.
* SITES-31641: Content Fragments Rest API: Add property to model fields for storing dynamic maps related to extensions.
* SITES-31677: Anpassad arbetsyta stöder export av AEM Content fragment till Target.
* SITES-31770: Content Fragments Rest API: PATCH prestandaförbättringar.
* SITES-31782: Content Fragments Rest API: lägg till en beskrivning för lokala resurser.
* SITES-32175: Tillåt mellanliggande implementeringar för både Live Copy-skapande och MSM Page rollout.

### Åtgärdade problem {#fixed-issues-21331}

* CQ-4359756: Översättningsregler innehåller nu filteregenskaper på komponentnivå.
* CQ-4359826: Korrigerar inkonsekvent status i referenspanelen för innehållsfragment.
* CQ-4359866: Klassen LanguageUtils har nu stöd för enhetstestning utan att ytterligare beroenden läggs till.
* FORMS-13990: Forms Service API:er: Dokumentgenerering: datafältet som lämnas tomt efter att ha valts ger 200 när det förväntas vara 400.
* FORMS-14309: Forms Service API:er: Extract data Response Code Rectification.
* FORMS-18526: När en regel med flera fält i villkor kopieras ändras inte det fasta fältet.
* FORMS-18977: DOR-tjänsten skickar inte dokumentets titel.
* FORMS-19047: Översättningar saknas efter publicering av ett anpassat formulär på AEM Forms i SP22.
* FORMS-19234: Det går inte att använda tidslinjefunktionen i PDF-filer i AEM-formulär.
* FORMS-19628: I Automatiskt genererad DOR döljs även rotpanelens namn, förutom den kapslade paneltiteln.
* FORMS-19651: Korrigera regel när en knapp klickas används i binärt läge och samma knapp används i programsatsen.
* FORMS-19808: FormsPortal - Det går inte att hämta utkast när den lata inläsningen är aktiverad.
* FORMS-19887: Access-egenskapen fungerar inte i HTML5 Preview.
* SITES-15452: Unika CF-element ska inte kontrolleras mot sina kopior vid starten.
* SITES-24492: ARIA-tablisten har inget tillgängligt namn.
* SITES-24623: Content Fragments Rest API: fix ETag mismatch between endpoints for the same CF.
* SITES-24668: References Rail functionality break when zoom is added to 400%.
* SITES-24678: References Rail status message is not announby screen reader.
* SITES-24697: Skärmläsaren meddelar inte om inläsningsstatus för bildmodellen.
* SITES-24708: Filters Rail-funktionaliteten bryts när zoomningen ökas till 400 %.
* SITES-25235: Meddelandet om att läsa in innehåll i filterspår visas inte av skärmläsaren.
* SITES-25254: Vågrät rullningslist visas i Carousel Modal när innehållet visas på 320px.
* SITES-25433: Edge Delivery med Universal Editor: Korrigera återgivning av sidversioner för flerspråkiga webbplatsstrukturer.
* SITES-26064: Content Fragments Rest API: Korrigera statuskoden som returneras när ett fragment skapas och en `AccessDeniedException` hämtas i serverdelen.
* SITES-26890: När du använder tangentbord visas inte tangentbordsfokus för scopet &quot;Tabellrubriker&quot; på sidan Hantera publikation.
* SITES-29075: Översikt över Live-kopior fungerar inte för webbplatser med stora volymer.
* SITES-29514: Edge Delivery med Universal Editor: Gör GitHub/Project URL obligatorisk när du skapar en ny webbplats.
* SITES-29691: Det går inte att flytta sidan i ett specifikt startrelaterat ärende.
* SITES-29745: Content Fragments Rest API: implementera hydrering av referensvariationer i BFS-traversal.
* SITES-29748: Korrigera återgivningsvillkor för att visa hanteringspublicerings-/snabbpubliceringsåtgärder i CF-redigeraren.
* SITES-29789: Component link change issue on copied root pages.
* SITES-29987: Content Fragments Rest API: Create &amp; Edit Content Fragment Model does not support `previewUrlPattern`.
* SITES-30140: Problem med dubbla fönster när innehållsfragmentreferens skapas.
* SITES-30327: Content Fragments Rest API: publicera CF:er utan behörigheter skapar separata arbetsflöden för varje nyttolastresurs.
* SITES-30333: Läs metadata för resurser från jcr för att undvika xmp-tolkningsproblem.
* SITES-30353: GraphQL DataFetchingExceptions for &quot;src&quot; Field in AEM Content Fragments.
* SITES-30377: Edge Delivery med Universal Editor: Sanera org- och sitenames.
* SITES-30386: Edge Delivery med Universal Editor: Ta bort dubbletter, äldre UE `cors.js`.
* SITES-30583: Content Fragments Rest API: verktyget Sök och ersätt ändrar alla tecken till gemener.
* SITES-30585: Content Fragments Rest API: `previewUrlPattern` inte inställt på att skapa CFM:er med referenser.
* SITES-30634: RTE Image Alt Text &amp; Alignment fungerar inte konsekvent.
* SITES-30660: ADA Compliance Issue with Custom AEM Component.
* SITES-30695: Edge Delivery med Universal Editor: Öka rankningen för rewriter-pipeline så att den inte stör anpassad kod.
* SITES-30727: Det går inte att dra och släppa komponenter i redigeraren för produktionsförfattare.
* SITES-30752: Använd inte `If-modified-since`/`last-modified`-huvuden när du genererar beständigt frågesvar.
* SITES-30871: DOM-uppdateringar efter att efterredigeringslyssnaren har utlösts.
* SITES-30877: Felaktig status för underordnad sidutrullning.
* SITES-30899: Alternativet Senare som utrullning tillåter fortsatt utan valt datum.
* SITES-30947: Null-pekarundantag på grund av att egenskapen &quot;behavior&quot; saknas i ritningen under utrullning.
* SITES-31157: Content Fragments Rest API: patch Fails is specific case.
* SITES-31162: Content Fragments Rest API: Fix casting issue for `DateTimeField` field in `ModelFieldMapper`.
* SITES-31174: Content Fragments Rest API: taggar publicerades inte tillsammans med publiceringsbegäran.
* SITES-31272: Det går inte att skapa en Assets-språkkopia via PageManager.copy.
* SITES-31327: Content Fragments Rest API: ta bort ETag-validering i GET Fragment-begäran.
* SITES-31387: JavaScript-fel&quot;ns.ui.alert is not a function&quot; when re-enabling spökcomponent inherance.
* SITES-31454: Content Fragments Rest API: Slappna av i mönstret för fragmentreferensfält så att även UUID accepteras.
* SITES-31455: Content Fragments Rest API: fix ETag Mismatch between Endpoints for the same Content Fragment Model.
* SITES-31459: Content Fragments Rest API: CF Live copy kan inte redigeras när det finns ett innehållsreferensfält.
* SITES-31467: js-errors from contexthub.authoring-krok.js in the page editor.
* SITES-31487: Content Fragments Rest API: Allow permissions endpoint to be called for root folder.
* SITES-31621: Edge Delivery med Universal Editor: Ta bort tom rad från kalkylblad som är live-kopior.
* SITES-31676: Om du redigerar eller tar bort komponenter lämnas ett tomt utrymme längst ned på sidan.
* SITES-31822: ClassicUI Checkbox label missing &amp; Encoded HTML.
* SITES-31857: Det går inte att skapa CF i mappar med enkla citattecken.
* SITES-31888: Borttagning av innehållsfragment kan inte spridas till förhandsvisning.
* SITES-31922: Content Fragments Rest API: sidreferenser returneras inte av referenspunkten referencedBy.
* SITES-31987: Visa inte previewURL:er för innehållsfragment när de publiceras till Förhandsgranska.
* SITES-32095: Auto-Refresh Fails on afterdelete Event Listener in Live Copy.
* SITES-32237: Edge Delivery med Universal Editor: Korrigera återgivning av tomma/felformaterade textkomponenter.

### Kända fel {#known-issues-21331}

Ingen.

### Föråldrade funktioner och API:er {#deprecated-21331}

Inaktuella och borttagna funktioner och API:er i AEM as a Cloud Service beskrivs i dokumentet [Inaktuella och Borttagna funktioner och API:er](/help/release-notes/deprecated-removed-features.md).

### Säkerhetskorrigeringar {#security-21331}

AEM as a Cloud Service strävar efter att optimera säkerheten och prestandan för din plattform. Denna underhållsrelease åtgärdar 21 identifierade sårbarheter, vilket stärker vårt engagemang för robust systemskydd.

### Inbäddade tekniker {#embedded-tech-21331}

| Teknik | Version | Länk |
|---|---|---|
| AEM Oak | 1.80.0 | [Oak API 1.80.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.80.0/index.html) |
| AEM SLING API | 2.27.6 | [API:t för Apache Sling 2.27.6 ](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Språkspecifikation för HTML-mall](https://github.com/adobe/htl-spec) |
| Grundläggande komponenter i AEM | 2.29.0 | [AEM WCM Core Components](https://github.com/adobe/aem-core-wcm-components) |
