---
title: Aktuell underhållsanvisning för [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell underhållsanvisning för [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: d07fc976fe9c8e7872468048f80e525fe8484339
workflow-type: tm+mt
source-wordcount: '2584'
ht-degree: 0%

---

# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs den tekniska versionsinformationen för den aktuella underhållsutgåvan av Experience Manager as a Cloud Service.

## Utgåva 15787 {#release-15787}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsutgåvan 15787, som offentliggjordes den 4 april 2024. Den tidigare underhållsversionen var version 15575.

2024.3.0 Funktionsaktivering innehåller alla funktioner som finns i den här underhållsversionen. Se [Roadmap för lanseringar av Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html) för mer information.

### Förbättringar {#enhancements-15787}

* SITES-19059 - Content Fragments - OpenAPI - Allow defaultValue for enum fields
* SITES-2013 - Innehållsfragment - OpenAPI - WCMScriptHelper bör avbryta återgivningen om det inte finns någon ServletResolver
* SITES-19926 - Content Fragments - OpenAPI - Improvements to OnOffTriggerProcessor
* SITES-17945 - Content Fragments - OpenAPI - Hämta senast ändrade metadata för varje version
* SITES-17298 - Content Fragments - OpenAPI - Content Fragment Models Permissions
* SITES-14255 - Innehållsfragment - OpenAPI - Verifiera textfältets unika karaktär om en unik flagga har angetts i fragmentmodellen
* SITES-15557 - Content Fragments - OpenAPI - Allow defaultValue for enum fields
* SITES-1559 - Content Fragments - OpenAPI - Update CF List API to allow fetching only direct child content fragments (BE)
* SITES-16052 - Innehållsfragment - OpenAPI - Lägg till URL:en för den instans där en resurs kan förbrukas
* SITES-17944 - Innehållsfragment - OpenAPI - Korrekt JCR-åtkomstkontrollista mappas till CF-behörighetsslutpunkt
* SITES-17513 - Kontrollplan för innehållsfragment - Avpublicera innehållsfragment
* SITES-8831 - Content Fragment Control Plane - PUT - Uppdatera ett fragment med fullständig information
* SITES-8836 - Content Fragments - OpenAPI - Control Plane - GET References - Get parent references of a fragment (by UUID)
* SITES-8986 - Content Fragments - OpenAPI - Publish Content Fragment Model
* SITES-18073 - Content Fragments - OpenAPI - PreviewURL Pattern for a CFM
* SITES-15242 - Content Fragments - OpenAPI - Utöka publiceringshändelserna för att ge information om nivån
* SITES-18702 - Content Fragments - OpenAPI - [Backend] Publicera på mappnivå
* SITES-20020 - Content Fragments - OpenAPI - Remove `X-Adobe-Accept-Unsupported-API` före GA
* SITES-16066 - Content Fragments - Fragment Editor - Change asset selector JS URL
* SITES-19326 - Content Fragments - Fragment Editor - Uppdatera länkar i Assets UI för att öppna CF i ny CF Editor
* SITES-10515 - Content Fragments - GraphQL API - GraphQL - Prestandaproblem i AbstractFetcher vid inläsning av referensfragment
* SITES-17364 - Content Fragments - GraphQL API - Return Full Name for the Modified by and Published by properties
* SITES-19165 - Content Fragments - GraphQL API - Tillåt att globala modeller används, refereras och kan frågas i alla GraphQL slutpunkter
* SITES-17768 - Content Fragments - GraphQL API - Expose Dynamic Media URL for images via _dmS7Url
* SITES-11057 - Core Backend - Undvik att läsa in alla versioner när du öppnar tidslinjen > Versioner
* SKYOPS-63033 - HTTPD - Trimma tomma utrymmen i variabler för avsändarmiljö
* SKYOPS-65518 - HTTPD - Verifieraren misslyckas om det finns ogiltiga filnamn i dispatchermappen
* SITES-19626 - Launches - Merge DAM-CFM lastUpdate fields into main
* SITES-19251 - Quick Site - Creation Wizard - Support sites admin ui side rail när temareferensen inte är lika med platsnamnet
* SITES-15430 - Universal Editor - Universal Editor under AEM Domain
* CQ-4344966 - WCM - Translation - Create Basic Framework for Structure Update of sites and Update existing one for assets
* CQ-4347312 - WCM - Översättning - Skapa arbetsflöde för att associera&quot;cq:translationsourcejcruuid&quot; i befintliga käll- och språkkopior
* CQ-4354509 - WCM - Översättning - Publicera översättningsjobbhändelser [OSGi EventAdmin]
* SITES-16318 - Crosswalk - AEM-baserad redigering med Edge Delivery Services
* FORMS-9889: Användaren kan lägga till POST-URL:en och molnkonfigurationen när åtgärden Skicka för REST-slutpunkten konfigureras
* I regelredigeraren kan användare:
   * FORMS-12160: Validera ett fält, en panel eller ett formulär i avsnittet Sedan i villkoret När.
   * FORMS-12570: Återställ ett fält, en panel eller ett formulär i avsnittet Sedan i villkoret När.
   * FORMS-11541: Använd fältobjekt och globala objekt i regelredigeraren via anpassade funktioner.
   * FORMS-11714: Definiera parametrar som valfria i den anpassade funktionen. Som standard är parametrar som deklarerats i anpassade funktioner obligatoriska.
   * FORMS-11756: Använd cachelagring för anpassade funktioner för att förbättra svarstiden när du hämtar den anpassade funktionslistan i regelredigeraren.
   * FORMS-12053: Lägg till en else-programsats i When-villkoret för att implementera kapslade villkor.
   * FORMS-11269: Använd moderna ES10 JavaScript-funktioner som låt- och pilfunktioner i den anpassade funktionen för kärnkomponentbaserade formulär.

* FORMS-9014: Olika tillgänglighetsrelaterade förbättringar av signeringskomponenten för klottrar


### Åtgärdade problem {#fixed-issues-15787}

* Olika problem med tillgänglighet och internationalisering har åtgärdats
* SITES-16966 - AEM: Unlocalized &quot;Not Versioned!&quot; sträng i Sites > Restore > Restore Tree
* SITES-16208 - ContentFragmentModelIdentifier visar en vilseledande titelegenskap
* SITES-18024 - När If-Match-huvudet saknas måste svaret vara 428
* SITES-18003 - Användaren som skapade en version returneras inte korrekt
* SITES-17937 - Händelsen Skapa innehållsfragment skickas innan författarpoderna har synkroniserats
* SITES-18029 - Bearbetningsflödet för händelser hänger när det samtidigt meddelas av JCR-observationer
* SITES-17882 - Ta bort maxlängden för fragmenttextfält från schemat
* SITES-19252 - Åtgärda inkonsekvenser relaterade till HTTP-statuskoden 406 och 415
* SITES-16964 - [Backend] Sorteringen efter &quot;Ändrad av&quot; fungerar inte korrekt
* SITES-17519 - egenskapsredigeraren för webbplatssidan - Det långa sidnamnet gör att knapparna inte kan klickas
* SITES-16852 - Publish API publicerar referenser med statusen NEW
* SITES-18833 - Unikhetsbegränsning i ej synliga i OpenAPI-slutpunkter
* SITES-15553 - Det gick inte att läsa in sidpanelen i XF om URL:en innehåller en väljare
* SITES-14340 - NPE i VersioningTimelineEventProvider.accept
* SITES-1605 - [Webbplatser] DeletePageCommand ger NPE om källsökvägen är null
* SITES-16308 - [GB18030]: Ett varningsmeddelande visas när en ny platsmapp med namnet GB18030-tecken skapas
* SITES-16304 - [GB18030]: Ett varningsmeddelande visas när du skapar en ny Experience Fragments-mapp med namnet GB18030-tecken
* SITES-8769 - Förbättra StyleImpl-prestanda
* CQ-4343815 - Campaign - Targeting - Standardvarianten för ett teaser har en tom URL
* CQ-4355889 - Campaign - Targeting - Create Audience request misslyckas med IMS Config.
* SITES-12460 - Kampanjintegrering - Kampanj/AEM Cloud Service-integrering fungerar inte
* SITES-11571 - Innehållsfragment - GraphQL API - PersistedQueryServlet ska skicka 400-tal på URL:er med felaktigt format
* SITES-19946 - Innehållsfragment - GraphQL API - Modeller skannas inte längre vid start
* SITES-1605 - Core Backend - DeletePageCommand returnerar NPE om källsökvägen är null
* SITES-5429 - Core Backend - ChildrenListServlet itemResourceType tillåter direkt körning av kod
* SITES-15553 - Experience Fragments - Det gick inte att läsa in XF:s sidopanel om URL:en innehåller en väljare
* SITES-13666 - Headless - Admin - Felloggen är falskt positiv &quot;com.adobe.cq.dam.cfm.headless.ui.impl.models.CFHomeCardModelImpl Config Id får inte vara null&quot;
* SITES-17164 - sidredigeraren - [Cloud, 6.5 Forms] Förhandsgranskningen i AF-temeredigeraren är bruten
* SITES-14340 - Sites Admin UI - NPE in VersioningTimelineEventProvider.accept
* SKYOPS-68611 - Sling - repoinit - Port sling repoinit Skapa sökvägskorrigering i underhållsgrenen
* CQ-4354678 - WCM - Översättning - Översättningsjobb exporterar översatt innehåll
* CQ-4355167 - WCM - Översättning - Inte popup-fönster visas när ett översättningsjobb markeras som slutfört eller arkiv
* CQ-4355913 - WCM - Översättning - Språkkort för översättningsprojekt som inte fungerar
* GRANITE-47694 - Arbetsflöde - Det går inte att hämta underaktiviteter i ett arbetsflöde i molnet för icke-adminanvändare
* ASSETS-31097 - Assets Cloud - Loggar som fyllts med indexgenererade varningar för /bin/numberofentitiesinfolders.json
* ASSETS-35860 - Assets Cloud - felaktig tidszonskonvertering i AEM Assets kolumnvy
* SITES-15260 - Classic UI (äldre) - Bulkedit lägger till tomma egenskaper på sidan om arkimport används
* SITES-16834 - Classic UI (Legacy) - texten saknas efter textredigering i gruppredigeraren när det finns kommatecken i texten
* SITES-17767 - Content Fragments - Admin - Stöd för tillåtna cf-modeller även för mappar utan jcr:content-nod
* SITES-17683 - Content Fragments - Core Backend - Content Fragments are not serializable with Jackson exporting
* SITES-18797 - Content Fragments - Core Backend - GraphQL Results Duplicated after Index customization
* SITES-18076 - Content Fragments - Core Backend - Multi-value text has invalid @TypeHint
* SITES-17856 - Content Fragments - Models &amp; Model Editor - CF Models visas inte om config inte är en mapp
* SITES-17071 - Core Backend - Den specifika sidan visar inte version på tidslinjen
* SITES-17285 - Core Components - Inline Image Crop is different on Author and Publish in AEMaCS
* SITES-19187 - Core Components - Två metoder för att placera resurser i en bildkomponent ger olika resultat i dialogrutan
* SITES-2007 - Core Components - Inline Image Crop - beskärning är fel och bilderna är suddiga
* SITES-17211 - Experience Fragments - Experience Fragments component path picker dialog that displays fragments that are deleted
* SITES-17894 - Launches - Promotion of nested launches reverts launch content to a version from its ancestor
* SITES-16042 - MSM - Live-kopior - Anteckningar visas felaktigt i Livecopy efter utrullningar
* SITES-16691 - MSM - Live-kopior - När kunden väljer utrullning eller utrullning från rollout-ikonen för en komponent är knappen&quot;continue&quot; nedtonad.
* SITES-16733 - MSM - Live-kopior - indexsida för utkast kan inte rullas ut när rep:policy tillämpas på noden
* SITES-17155 - MSM - Live-kopior - Sidhuvuden och sidfötter översätts tillbaka till engelska när LiveCopy byter namn
* SITES-17492 - MSM - Live-kopior - AEM Page Live Copy Layout Inconsistent
* SITES-19316 - MSM - Live-kopior - referenslänken till upplevelsefragment uppdateras inte i språkversionen
* SITES-19347 - MSM - Live Copies - Prod Author slowmessages - pods restarten frekvent - Health Notifications
* SITES-19790 - MSM - Live-kopior - Felaktig förhandsvisningsinformation efter att LiveCopy skapades
* SITES-20086 - MSM - Live Copies - MSM-utrullning för CF i Assets kommer att lansera alla live-kopior även om en live-kopia väljs för lansering
* SITES-2008 - MSM - Live Copies - Blank Page Issue Post XF Rollout in Properties - AEM as a Cloud Service
* SITES-16854 - sidredigeraren - Drop target overlay omfattar parsys in components with &quot;Select panel&quot; feature
* CQ-4355563 - Projekt - Sökvägsparametern är fel. Fyller i &quot;?appId=aemshell&quot; för sökskript för projektinkorg
* SITES-16876 - Quick Site - Theme Deployment - CSS and JS missing on preview pages 2
* SITES-18418 - Sites Admin UI - Funktionen Visa/dölj för sökvägswidgeten fungerar inte som den ska när fält krävs
* SITES-19534 - Sites Admin UI - Det går inte att öppna dialogrutan Effektiv behörighet efter uppgradering AEM 6.5.19
* SITES-19203 - Mallredigerare - Redigerbar mallpolicy Feljusterad text och Format överlappar borttagningsknappen
* CQ-4354881 - WCM - Översättning - Sökvägen för innehållsfragment anges till källa (en-us) när innehållsfragment översätts som en del av en sida
* CQ-4355289 - WCM - Översättning - Endast de första 40 elementen visas i Cloud Service för översättning
* CQ-4355866 - WCM - Översättning - Arbetsflöde för översättning orsakar fel för befintliga sidor
* CQ-4355797 - Arbetsflöde - Det går inte att använda OTB-arbetsflödessteg
* GRANITE-48938 - Arbetsflöde - Författaren som visas i ett väntande publiceringstillstånd för resurser. Problem i den nya beständiga nyttolastmappningscachen.
* GRANITE-49036 - Arbetsflöde - Föreslå funktioner | Möjlighet att schemalägga och konfigurera rensning av arbetsflödespaket
* SITES-17393 - Arbetsflödestillägg - Publicera innehållsträdet misslyckas när arbetsflödets startprogram för cq:Tag används
* SITES-17759 - Workflow Extensions - Tree-Activation-Workflow for tags not working in AEMaaCS
* FORMS-12411: På Android-enheter visas `Maximum Number of Characters Validation` fungerar inte för TextBox-komponenten Adaptiv form.
* FORMS-13377: När en användare försöker lägga till det anpassade teckensnittet och köra pipeline för att konfigurera det misslyckas det med felet ContainersNotReady
* FORMS-13267: När en användare lägger till en komponent för listrutor med adaptiva formulär, genereras inte ID:t för listrutan
* FORMS-13544: När en användare lägger till en adaptiv formulärbehållarkomponent med en guidelayout fungerar den inte korrekt vid formulärutveckling
* FORMS-13091, FORMS-13414: Om användaren försöker konfigurera en anpassad domän-URL i Azure Blob-lagringen misslyckas den
* FORMS-13595: När en användare försöker spara formuläret på en annan plats kan användaren inte se knapparna Välj mapp och Avbryt om webbläsarupplösningen är inställd på 100 %. Alternativet är dock synligt när upplösningen är inställd på 75 %
* FORMS-10952: När en användare lägger till en adaptiv formulärlistrutekomponent i ett adaptivt formulär och använder egenskapen Ange alternativ baserat på olika anpassade regler, fungerar egenskapen Ange alternativ bara för den sista regeln
* FORMS-11471: Den lata inläsningen av ett fragment misslyckas när anropet &quot;emitter.json&quot; misslyckas på grund av ett nätverksavbrott.
* FORMS-11786: När en användare växlar mellan månader i kalenderwidgeten visas en extra rad i datumväljarkomponenten.
* FORMS-12093, FORMS-12093: När en användare markerar kryssrutan Adaptivt formulär för att skicka ett formulär, är det felaktiga värdet med ett extra  `\` lagras i textrutan
* FORMS-11993: När en användare klickar på en bild med komponenten &quot;Ta ett foto&quot; i den bifogade filen på en iOS-enhet läggs alla bilder till i mappen med samma namn
* FORMS-12555: När en användare försöker integrera AEM Forms till en utskicksplattform med en AEM publicerad URL, lägger AEM Forms inte till method=post när sidan återges. Problemet inträffar trots att POST har angetts i skicka-åtgärden med URL:en. Det gör att e-postplattformen inte kan identifiera detta som ett formulär
* FORMS-12938: HTML 5-formulären fungerar inte eller läses in korrekt i Microsoft Edge-webbläsaren med kompatibilitetsläget IE
* FORMS-12032: När en användare skickar ett formulär pekar sökvägen för åtgärden skicka inte korrekt
* FORMS-12445: Fel värden hämtas i formulärdatamodellen när alternativknapparnas ordning har ändrats och formuläret publiceras.
* FORMS-12947: När en användare lägger till ett nytt språk i ett befintligt lexikon misslyckas sammanfogningen eller lägger inte till
* FORMS-11363: När en användare skickar ett formulär via Workspace uppstår ett visningsproblem i tabellerna när det återges
* FORMS-11756: När en användare lägger till JavaScript-funktioner för ES6, till exempel `let` och `const` i anpassade funktioner kan regelredigeraren inte öppnas. Den här underhållsversionen har stöd för ES10
* FORMS-13164: Om användaren skapar ett PDF läggs oväntade tomma rader till efter överföringen
* FORMS-13789: När en användare försöker generera flera PDF misslyckas API:t för utdatabatsen
* FORMS-11483: När en användare konverterar PDF till PDF/A-2B eller PDF/A-3B misslyckas konverteringen och ett valideringsfel visas
* FORMS-10501: När en användare anropar HSM certifieras dokumenten, men LTV aktiveras inte
* FORMS-11546: När en formulärförfattare använder upprepade paneler i ett adaptivt formulär saknas attributet ARIA i HTML-taggarna. Detta förbättrar tillgängligheten för upprepade paneler i adaptiv form
* FORMS-11826: På grund av matchande etiketter i Arial®, som är märkta med och Arial®, kan skärmläsarna inte skilja mellan dessa. För att lösa problemet ersätts etiketten &quot;aria-marked-by&quot; med &quot;aria-describedby&quot; för formulärfälten. (F) Detta förbättrar tillgängligheten för Adaptive Forms
* FORMS-12626, FORMS-13094: Användare kan inte komma åt verktygsfältet via tangentbordet för att spara eller redigera innehåll på formulärredigeringssidan. Det här tillgänglighetsproblemet har åtgärdats
* FORMS-13102: Under formulärredigeringsprocessen saknar ikonerna på Forms- och dokumentsidan beskrivande funktioner för personer med olika funktionshinder. Det här tillgänglighetsproblemet har åtgärdats

### Kända fel {#known-issues-15787}

* SITES-17934 - Content Fragments - Preview misslyckas på grund av DoS-skydd för stora fragmentträd. Se [kB](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-23945)

### Föråldrade funktioner och API:er {#deprecated-15787}

* [Borttagning av JWT-autentiseringsuppgifter i Adobe Developer Console](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md)

Titta på [Föråldrade och borttagna funktioner och API:er](/help/release-notes/deprecated-removed-features.md) för att veta vad som har tagits bort eller tagits bort på AEM as a Cloud Service.

### Ändringsmeddelande {#change-notice-15787}

**Åtgärder krävs**

#### Ange CM Java-versionen till 11 {#set-java-version-11}

Den nya versionen av aem-sdk-api innehåller klasser som kompilerats med ett Java 11-mål, vilket inte är kompatibelt med JDK version 1.8 som är standard i Creative Manager Build-miljön. Denna uppdatering kräver att Maven körs med JDK 11.

Vi rekommenderar att man lägger till en `.cloudmanager/java-version` till roten av Git-rapporten med innehållet: `11`. Se [Bygg miljö / Ställa in JDK-versionen av Maven](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#alternate-maven-jdk-version).


### Inbäddade tekniker {#embedded-tech-15787}

| Teknik | Version | Länk |
|---|---|---|
| AEM | 1.60-T20240131102219-0cde853 | [Oak API 1.60.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.60.0/index.html) |
| AEM SLING API | Version 2.27.2 | [API för Apache Sling 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTML | Version 1.4.20-1.4.0 | [HTML-mallens språkspecifikation](https://github.com/adobe/htl-spec) |
| Grundläggande komponenter i AEM | Version 2.24.4 | [AEM WCM-kärnkomponenter](https://github.com/adobe/aem-core-wcm-components) |
