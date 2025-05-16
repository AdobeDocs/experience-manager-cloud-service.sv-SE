---
title: Versionsinformation om 2024.3.0-utgåvan av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Versionsinformation om 2024.3.0-utgåvan av  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: b3816929-2c0a-4d6a-b583-c928d2182ecd
feature: Release Information
role: Admin
source-git-commit: 603602dc70f9d7cdf78b91b39e3b7ff5090a6bc0
workflow-type: tm+mt
source-wordcount: '2293'
ht-degree: 0%

---

# Versionsinformation 2024.3.0 för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs versionsinformationen för funktionen för 2024.3.0-versionen av [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Härifrån kan du navigera till versionsinformation för tidigare versioner som 2021 eller 2022.
>
>Ta en titt på [Experience Manager Releases Roadmap](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=sv-SE) om du vill veta mer om kommande funktionsaktiveringar för [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Mer information om dokumentationsuppdateringar som inte är direkt relaterade till en release finns i [Senaste dokumentationsuppdateringar](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=sv-SE).

## Releasedatum {#release-date}

Releasedatum för [!DNL Adobe Experience Manager] som [!DNL Cloud Service] aktuell funktionsversion (2024.3.0) är 11 april 2024. Nästa funktionsversion (2024.4.0) är planerad till 25 april 2024.

## Versionsinformation om underhåll {#maintenance}

Du hittar den senaste underhållsversionsinformationen [här](/help/release-notes/maintenance/latest.md).

## Släpp video {#release-video}

Titta på videon med versionsöversikten för mars 2024 om du vill se en sammanfattning av funktioner som lagts till i version 2024.3.0:

>[!VIDEO](https://video.tv.adobe.com/v/3428342?quality=12)

## [!DNL Experience Manager Sites] som en [!DNL Cloud Service] {#sites}

### Nya funktioner i [!DNL Experience Manager Sites] {#sites-features}

**AEM Authoring for Edge Delivery Services**

AEM Sites kan nu användas som innehållskälla för Edge Delivery Services. Man kan hantera webbplatser i AEM med den nya universella redigeraren med sammanhangsberoende webbverktyg. På så sätt kan företag skapa högpresterande webbsidor med Edge Delivery Services och samtidigt utnyttja AEM kraftfulla funktioner för innehållshantering.

![AEM Authoring](/help/edge/assets/universal_editor_edge_delivery_services.png)

Mer information finns i [dokumentationen](/help/edge/overview.md) och i [AEM Gems - Komma igång med AEM Authoring och Edge Delivery Services](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/aem-gems-getting-started-with-aem-authoring-and-edge-delivery/m-p/652694#M43905)

**Universell redigerare för Headless-implementeringar**

Med Universell redigerare kan även fristående webbprogram använda samma intuitiva kontextbaserade WYSIWYG-redigering som tidigare bara fanns på traditionella webbplatser. Innehållsskapare kan nu visuellt komponera layouter med Content Fragments på samma sätt som komponenter på sidor.

Det som skiljer den universella redigeraren åt är dess anpassningsbarhet till olika webbarkitekturer, anpassning av rendering på både server- och klientsidan, bibehållen ramverksagnostikering och eliminering av behovet av AEM värdtjänster. Det är enkelt att integrera befintliga webbprogram med den universella redigeringsfunktionen för redigering av innehåll, vilket i första hand kräver att utvecklarna lägger in specifika dataattribut i sina markeringar.

Med den funktionen får den universella redigeraren en konsekvent redigeringsupplevelse, oavsett innehållsstruktur eller underliggande teknologi. Mer information finns i [Introduktion till den universella redigeraren](/help/implementing/universal-editor/introduction.md).

**OpenAPI:er för innehållshantering för innehållsfragment och modeller**

Utvecklare kan nu programmässigt interagera med innehållsfragment och Content Fragment-modeller och utföra CruD-åtgärder på dem med Content Management OpenAPI:er. Mer information finns i [API-dokumentation](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/)

**Stöd för hantering av flera webbplatser för Experience Fragments**

Stödet för hantering av flera webbplatser har utökats för mappstrukturer som lagrar upplevelsefragment, vilket gör det möjligt för användare att lansera en komplett innehållsstruktur med upplevelsefragment.

**Jämför innehållsfragmentversioner**

Med den nya Content Fragment Editor kan innehållsförfattare jämföra och visa skillnader mellan den aktuella versionen av ett innehållsfragment och en tidigare version.

### Tidiga Adobe-program {#sites-early-adopter}

**Generera variationer**

Utnyttja GenAI genom AEM nya funktion, [generera varianter](/help/generative-ai/generate-variations.md), som nu är tillgängliga i Cloud Service. Generera variationer hjälper er att generera och skala innehåll med hjälp av generativ AI. Kontakta ditt Adobe-kontoteam och ta del av ditt bidrag i programmet.

**Resurssökning i Content Fragment Console**

Innehållsförfattare kan nu bläddra bland, visa och vidta åtgärder för bilder och andra resurser utan att behöva lämna konsolen Innehållsfragment.

![Resurssökning](/help/sites-cloud/administering/content-fragments/assets/cf-console-assets-browse.png)

Är du intresserad av att testa funktionen och ge feedback? Skicka ett e-postmeddelande till aemcs-headless-adopter@adobe.com från ditt officiella e-post-ID om du vill veta mer om det tidiga adopterprogrammet.

## [!DNL Experience Manager Assets] som en [!DNL Cloud Service] {#assets}

### Nya funktioner i administrationsvyn {#admin-view}

**Inbyggd integrering med Adobe Express**

AEM Assets är integrerat med Adobe Express, som gör att du kan komma åt material som lagras i AEM Assets direkt inifrån Adobe Express användargränssnitt. Du kan placera innehåll som hanteras i AEM Assets på arbetsytan Express och sedan spara nytt eller redigerat innehåll i en AEM Assets-databas.

![Inkludera resurser från Assets-tillägg](/help/assets/assets/adobe-express-native-integration.png)

**Förhandsgranska återgivningar för alla videotyper som stöds**

Experience Manager Assets genererar nu förhandsgranskningsåtergivningar av alla videotyper som stöds som standard utan att en bearbetningsprofilskonfiguration krävs.

### Nya funktioner i vyn Assets {#assets-view}

**Hantera behörigheter för samlingar**

Med Assets Essentials kan administratörer hantera åtkomstnivåer för privata samlingar som är tillgängliga i databasen. Som administratör kan du skapa användargrupper och tilldela behörigheter till dessa grupper för att hantera åtkomstnivåer. Du kan även delegera behörighetshanteringsprivilegier till användargrupper.


## [!DNL Experience Manager Forms] som en [!DNL Cloud Service] {#forms}

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### Nya funktioner för AEM Forms {#forms-new-features}

* **[Adobe Experience Manager Forms Edge Delivery Services](/help/edge/docs/forms/overview.md)**: Edge Delivery Services för AEM Forms är en sammansatt uppsättning tjänster som möjliggör en snabb utvecklingsmiljö där författare snabbt kan uppdatera, publicera och öppna nya formulär. Dessa tjänster ger enastående och slagkraftiga formulärupplevelser som skapar engagemang och konverteringar. Dessa blankettupplevelser är enkla att skapa och utveckla.

  ![EDS Forms Features](/help/edge/assets/eds-forms-features.png)

Med de här tjänsterna kan du:

* Arbeta med flera innehållskällor på samma formulärwebbplats och använd de redigeringsverktyg du föredrar, som Microsoft Excel, Google Sheets eller Adaptiv Forms Editor.
* Leverera digitala registreringsupplevelser som läses in och återges snabbt och kontinuerligt med övervakning av formulärens prestanda med hjälp av RUM (Real Use Monitoring).
* Använd HTML, modern CSS och vanilj JavaScript för att skapa exceptionella upplevelser och undvika den branta inlärningskurvan i ett specifikt ramverk.


### Nya funktioner i förhandsversionen för AEM Forms {#forms-pre-release}

* **Förbättrad Visual Rule Editor för Core Component Based Adaptive Forms**: Den här versionen innebär en betydande uppgradering av den visuella regelredigeraren för adaptiva formulär baserade på kärnkomponenter. Den här versionen innebär en betydande uppgradering av den visuella regelredigeraren för adaptiva formulär baserade på kärnkomponenter. Uppdateringen fokuserar på att effektivisera interaktionen med anpassade funktioner, så att du kan skapa mer robusta och effektiva formulär.

  Nu kan du effektivisera anpassade funktionsinteraktioner genom att:

   * Använd nya kommentarer för att få tydligare funktionsdefinitioner.
   * Använd cachningsmekanismer för anpassade funktioner, vilket ger snabbare formulärprestanda.
   * Arbeta smidigt med globala objekt i anpassade funktioner.
   * Definiera och använda valfria parametrar i anpassade funktioner.

  Uppdateringen innehåller även följande förbättringar av regelredigeringsfunktionen. Du kan:

   * Implementera kraftfull&quot;when-then-else&quot;-logik för villkorlig exekvering.
   * Utnyttja moderna JavaScript-funktioner som låt- och pilfunktioner (ES10-stöd).
   * Validera eller återställ inte bara fält, utan även hela paneler och formulär, vilket ger bättre kontroll över användarinteraktioner.

  Dessa förbättringar ger en mer intuitiv och kraftfull upplevelse när man skapar regler och anpassade funktioner i den visuella regelredigeraren.

* **Skapa flera versioner av ett anpassat formulär**: Nu kan du enkelt hantera varianter av befintliga formulär. Detta förenklar versionskontrollen och underlättar jämförelse för formuläroptimering, allt i ett enda smidigt arbetsflöde.

* **Jämför anpassat formulär**: Nu kan du enkelt jämföra två formulär för att identifiera skillnader mellan två formulär. Det underlättar smidigt samarbete genom att teammedlemmarna kan jämföra revisioner och diskutera ändringar effektivt.

* **Hjälpmedelsförbättringar för signeringskomponenten Scribble**: Den här uppdateringen ger avsevärda tillgänglighetsförbättringar för komponenten Scribble Signature:

  **Förbättrad tangentbordsnavigering:**
   * Genom att trycka på Tabb kan användarna navigera bland alla interaktiva element i signaturdialogrutan.
   * Om du signerar med en pensel eller ett tangentbord och trycker på Retur stängs dialogrutan.
   * Fokuset ligger kvar på signaturkontrollen när du har signerat och klickat på OK.

  **Rensa signaturfunktion:**

   * En tydlig kryssikon för att radera signaturen är tillgänglig via tabbtangenten.
   * Dialogrutan&quot;Bekräfta signatur&quot; är också tillgänglig via tabbnavigering.

  **Förbättrade etiketter och kontroller:**
   * Etiketten för tangentbordssignaturknappen är nu tydligare och använder&quot;aria-label&quot; för att meddela funktioner (till exempel&quot;aria-label=&#39;Signera med tangentbord&#39;&quot;).
   * Förbättrad kontrast gör att alla kontroller i den klotbaserade signaturen är lätta att urskilja.
   * Knappen OK/bock visar nu när den är inaktiv.

  **Signaturfeedback för skärmläsare:**
   * När en signatur skrivs kan skärmläsaranvändare höra texten som användes för att skapa signaturen.

Denna uppdatering ger en mer heltäckande upplevelse för användare med funktionshinder genom att förbättra navigering, klarhet och feedback för komponenten Klottsignatur.

### Tidiga Adobe-program {#forms-early-adopter}

* **[Skicka ett anpassat formulär till Adobe Workfront Fusion Scenario](/help/forms/submit-adaptive-form-to-workfront-fusion.md)**: Forms as a Cloud Service har ett körklart alternativ för att enkelt ansluta ett anpassat formulär till Adobe Workfront. Detta förenklar processen att skicka in ett adaptivt formulär till ett Adobe Workfront-scenario, vilket gör att du kan utlösa ett Workfront Fusion-scenario när ett adaptivt formulär skickas in.

  <br/> ![Adobe Workfront](/help/forms/assets/adobe-workfront.png) <br/> Med Adobe Workfront Fusion Connector kan du utforma arbetsflöden som aktiveras automatiskt när ett anpassat formulär skickas. Du kan till exempel förutse ett scenario där ett arbetsflöde initieras för att tilldela en viss person uppgiften att granska inskickade data, vilket gör det möjligt att godkänna eller avvisa en ansökan baserat på den information som hämtas via det anpassade formuläret. Denna smidiga integrering ökar effektiviteten och ger en ny nivå av automatisering i arbetsflödesprocesserna.|

* **Reader Extension Service**: AEM Forms Communication API:er innehåller Reader Extension Service som gör att du kan lägga till funktioner som formulärifyllning och kommentarer i vanliga PDF-filer, vilket gör dem interaktiva för användare med kostnadsfria Adobe Reader.

* [Stöd för höger till vänster-språk](/help/forms/supporting-new-language-localization-core-components.md): Adaptiv Forms som bygger på kärnkomponenter kan nu presenteras på ett höger till vänster-språk (RTL) som arabiska, persiska och urdu. RTL-språken talas av över 2 miljarder människor globalt. Genom att använda ett formulär på RTL-språk kan ni utöka räckvidden för era adaptiva formulär så att de kan anpassas till dessa olika målgrupper och väljas ut på RTL-marknader. I vissa regioner är det också ett juridiskt mandat att tillhandahålla formulär på det lokala språket. Genom att ta hand om lokala språk kan ni inte bara öppna dörrar för en bredare publik utan också säkerställa att relevanta lagar och bestämmelser följs.

* **[Skydda dina dokument med DocAssurance-API:er (del av kommunikations-API:er)](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**: Med DocAssurance-API:erna kan du skydda känslig information genom att signera och kryptera dokumenten. Genom kryptering omvandlas innehållet i ett dokument till ett oläsligt format så att bara behöriga användare kan få åtkomst till det. Detta förstärkta skydd skyddar inte bara värdefulla data från obehöriga ögon, utan ger även sinnesro. Med signatur-API:erna kan din organisation skydda säkerheten och sekretessen för Adobe PDF-dokument som den distribuerar och tar emot. Den här tjänsten använder digitala signaturer och certifiering för att säkerställa att endast avsedda mottagare kan ändra dokument.

  Du kan skriva till `aem-forms-ea@adobe.com` från ditt officiella e-post-id för att gå med i det tidiga adopterprogrammet och begära åtkomst till funktionen.

* **[Du kan utnyttja RUM-datatjänsten](/help/implementing/cloud-manager/content-requests.md#real-user-monitoring-for-aem-as-a-cloud-service)** för att aktivera klientsidessamling för AEM as a Cloud Service.
Real Use Monitoring (RUM) Data Service ger en mer exakt återgivning av användarinteraktioner och säkerställer ett tillförlitligt mått på webbplatsengagemanget. Det är en utmärkt möjlighet att få avancerade insikter om hur sidan fungerar. Detta är fördelaktigt för kunder som använder antingen Adobe-hanterat CDN eller icke-Adobe-hanterat CDN. För kunder som använder ett icke-Adobe hanterat CDN kan nu dessutom automatiserad trafikrapportering aktiveras för dem, vilket eliminerar behovet av att dela trafikrapporter med Adobe.

  Om du är intresserad av att testa den här nya funktionen och dela med dig av dina synpunkter skickar du ett e-postmeddelande till `aemcs-rum-adopter@adobe.com` tillsammans med ditt domännamn för varje miljö som du vill aktivera RUM för från din e-postadress som är kopplad till din Adobe ID. Adobe produktteam aktiverar sedan datatjänsten Real Use Monitoring (RUM) åt dig.

## [!DNL Experience Manager] som en [!DNL Cloud Service]-grund {#foundation}

### Tidiga Adobe-program {#foundation-early-adopter}

#### Varningar om trafikfilterregler (tidig Adobe-program) {#traffic-filter-rules-alerts-early-adopter}

Med de nyligen släppta [trafikfilterreglerna](/help/security/traffic-filter-rules-including-waf.md), som innehåller de valfria brandväggsreglerna för webbprogram (WAF), kan du konfigurera vilken trafik som ska tillåtas eller nekas.

Nu kan du skicka ett e-postmeddelande till **<aemcs-cdn-config-adopter@adobe.com>** om du vill gå med i det tidiga adopterprogrammet så att du kan få meddelanden när trafikfilterreglerna aktiveras. E-postmeddelanden från Åtgärdscenter håller dig informerad när vissa trafikförhållanden inträffar så att du kan vidta lämpliga åtgärder.

#### Domänmappning (Tidigt Adobe-program) {#cdn-config-early-adopter}

Förutom de nyligen släppta [trafikfilterreglerna](/help/security/traffic-filter-rules-including-waf.md), som innehåller de valfria brandväggsreglerna för webbprogram (WAF), finns det en möjlighet att använda konfigurationsflödet för att deklarera och distribuera andra typer av CDN-konfigurationer. [Läs mer](/help/implementing/dispatcher/cdn-configuring-traffic.md) och gå med i det tidiga adopterprogrammet genom att skicka ett e-postmeddelande till **<aemcs-cdn-config-adopter@adobe.com>** för att få tillgång till:

* 301/302 serveromdirigeringar
* skicka förfrågningar till godtyckliga ursprung (t.ex. program från andra tillverkare än AEM)
* URL-omformningar
* ange eller ändra begärande- eller svarshuvuden
* anpassade felsidor när CDN inte kan nå AEM

#### Apache/Dispatcher Runtime Ing of Rewrite Maps (Early Adobe Program) {#apache-rewritemaps-early-adopter}

På liknande sätt som i AEM 6.5, kommer Apache/dispatcher att importera omskrivningskartor som placerats på en viss plats i publiceringsdatabasen och läsa in dem, utan att någon implementering av en pipeline på webbnivå krävs. Detta öppnar möjligheter för en affärsanvändare att deklarera omdirigeringar med ett användargränssnitt, som det som finns i ACS Commons Redirect Map Manager. Kontakta **<aemcs-cdn-config-adopter@adobe.com>** om du vill ha mer information.

#### Edge Side Includes (ESI) for Loading Dynamic Content (Early Adobe Program) {#esi-early-adopter}

Adobe hanterade CDN har nu stöd för Edge Side Includes (ESI), ett markeringsspråk för dynamisk sammanställning av webbinnehåll på edge-nivå. Genom att inkludera ESI-fragment kan du cachelagra hela HTML-sidan vid CDN med högre TTL-värden, samtidigt som du oftare hämtar de mindre avsnitt som kräver högre uppdateringsfrekvens (lägre TTL-värden) från ursprungsläget. Kontakta **<aemcs-cdn-config-adopter@adobe.com>** om du vill ha mer information.

#### RDE-stöd för Front-End-kod med hjälp av Site Themes och Site Templates (Early Adopter Program) {#rde-frontend-early-adopter}

[Rapid Development Environment (RDE)](/help/implementing/developing/introduction/rapid-development-environments.md) har nu stöd för klientkod baserat på [webbplatsteman](/help/sites-cloud/administering/site-creation/site-themes.md) och [webbplatsmallar](/help/sites-cloud/administering/site-creation/site-templates.md) för tidiga användare. Med RDE:er görs detta med hjälp av ett kommandoradsdirektiv i stället för en [frontendpipeline](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md). Kontakta **<aemcs-rde-support@adobe.com>** om du vill prova det och lämna feedback.

#### Förbättrad loggning för RDE (Early Adobe Program) {#rde-logging-early-adopter}

När du felsöker kod i en [Rapid Development Environment (RDE)](/help/implementing/developing/introduction/rapid-development-environments.md) kan utvecklare nu konfigurera och direktuppspela loggar mer effektivt med kommandoraden och utan att ändra OSGI-egenskaper i versionskontrollen. Funktioner:

* deklarera loggnivåer per paket eller klassnivå
* anpassa loggutdataformatet
* strömma flera loggar parallellt

Kontakta **<aemcs-rde-support@adobe.com>** om du vill prova det och lämna feedback.

## Cloud Manager {#cloud-manager}

Du hittar en fullständig lista över månadsutgåvor av Cloud Manager [här](/help/implementing/cloud-manager/release-notes/current.md).

## Migreringsverktyg {#migration-tools}

Du hittar en fullständig lista över migreringsverktygen [här](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
