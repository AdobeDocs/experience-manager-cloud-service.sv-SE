---
title: Förstå begäranden om Cloud Service innehåll
description: Om du har köpt innehållsförfrågningslicenser från Adobe kan du ta reda på vilka typer av innehållsförfrågningar som Adobe Experience Cloud som en tjänst mäter och varianterna med en organisations analysrapporteringsverktyg.
exl-id: 3666328a-79a7-4dd7-b952-38bb60f0967d
source-git-commit: 949f0ec1aa89fd05813bc9ffb02a75fb0ad84a32
workflow-type: tm+mt
source-wordcount: '2690'
ht-degree: 0%

---

# Begäranden om Cloud Service

## Introduktion {#introduction}

Cloud Servicens innehållsbegäranden mäts via datainsamling på serversidan. Samlingen aktiveras via CDN-logganalys.

>[!NOTE]
>För ett begränsat antal [Kunder som är tidiga](/help/release-notes/release-notes-cloud/release-notes-current.md#sites-early-adopter), aktiveras även klientsidans samling via RUM-mätning (Real User Monitoring). Du kan läsa mer i dokumentationen i [den här artikeln](#real-user-monitoring-for-aem-as-a-cloud-service).

## Förstå begäranden om Cloud Service innehåll {#understaing-cloud-service-content-requests}

Innehållsförfrågningar samlas automatiskt in på serversidan vid Adobe Experience Manager as a Cloud Service kant via automatisk analys av loggfiler som kommer från AEM as a Cloud Service CDN. Detta görs genom att isolera de förfrågningar som returnerar HTML `(text/html)` eller JSON `(application /Json)` Innehåll från CDN, baserat på flera av de regler för inkludering och uteslutning som anges nedan. En innehållsbegäran görs oberoende av det returnerade innehåll som opereras från CDN-cachen eller det innehåll som skickas tillbaka till CDN-källan (AEM).

Tjänsten Real User Monitoring (RUM) Data Service, klientsidans samling, ger en mer exakt återgivning av användarinteraktioner och säkerställer ett tillförlitligt mått på webbplatsens engagemang. Detta ger kunderna avancerade insikter om deras sidtrafik och prestanda. Detta är fördelaktigt för både kunder som använder antingen det CDN som hanteras av Adobe eller ett CDN som inte hanteras av Adobe. Dessutom kan automatisk trafikrapportering nu aktiveras för kunder som använder ett CDN som inte hanteras av Adobe, vilket eliminerar behovet av att dela trafikrapporter med Adobe.

För kunder som lägger sitt eget CDN ovanpå AEM as a Cloud Service resulterar rapportering på serversidan i siffror som inte kan användas för att jämföra med förfrågningar om licensierat innehåll. Dessa siffror måste mätas av kunden i kanten av det yttre nätverket för CDN. För dessa kunder, rapportering på klientsidan och tillhörande prestanda, [Adobe RUM Data Service](#real-user-monitoring-for-aem-as-a-cloud-service) är det rekommenderade alternativet Adobe. Se [versionsinformation](/help/release-notes/release-notes-cloud/release-notes-current.md#sites-early-adopter) om du vill ha information om hur du anmäler dig.

## Samling på serversidan {#serverside-collection}

Det finns regler för att utesluta välkända botar, inklusive välkända tjänster som regelbundet besöker webbplatsen för att uppdatera deras sökindex eller tjänst.

### Varianter på begäranden om Cloud Service {#content-requests-variances}

Innehållsförfrågningar kan innehålla avvikelser med en organisations analysrapporteringsverktyg som sammanfattas i följande tabell. I allmänhet *inte* använda analysverktyg som samlar in data via instrumentering på klientsidan för att rapportera antalet innehållsförfrågningar för en viss webbplats, helt enkelt eftersom de ofta är beroende av att användarens samtycke aktiveras, och därför saknas en betydande del av trafiken. Analysverktyg som samlar in data på serversidan i loggfiler, eller CDN-rapporter för kunder som lägger till egna CDN AEM as a Cloud Service, ger bättre antal. För rapportering om sidvyer och deras prestanda är Adobe RUM Data Service det alternativ som rekommenderas av Adobe.

| Orsak till avvikelse | Förklaring |
|---|---|
| Användarens samtycke | Analysverktyg som förlitar sig på klientens instruktioner är ofta beroende av att användarens samtycke aktiveras. Detta skulle kunna representera merparten av den trafik som inte spåras. För kunder som vill mäta innehållsförfrågningar på egen hand rekommenderar vi att man använder analysverktyg för att samla in data på serversidan eller CDN-rapporter. |
| Taggar | Alla sidor eller API-anrop som spåras som Adobe Experience Manager (AEM)-innehållsbegäranden kanske inte taggas med Analytics-spårning. |
| Tag Management Rules | Regelinställningar för tagghantering kan resultera i olika datainsamlingskonfigurationer på en sida, vilket resulterar i en kombination av avvikelser med spårning av innehållsbegäran. |
| Bots | Okända botar som inte har föridentifierats och tagits bort av AEM kan orsaka spårningsavvikelser. |
| Rapportsviter | Sidor som ingår i samma AEM och domän kan skicka data till olika rapportsviter i Analytics. |
| Övervaknings- och säkerhetsverktyg från tredje part | Övervaknings- och säkerhetssökningsverktygen kan generera innehållsförfrågningar för AEM som inte spåras i analysrapporter. |
| API-åtkomst | Programmatisk åtkomst till sidor eller till Adobe Experience Manager API:er kan generera innehållsförfrågningar för AEM som inte spåras i Analytics-rapporter. |
| Förhämtningsbegäranden | Om du använder en förhämtningstjänst för att förhandsladda sidor för att öka hastigheten kan det medföra att trafiken för innehållsförfrågningar ökar avsevärt. |
| DOS | Även om Adobe gör försök att automatiskt upptäcka och filtrera bort trafik från DDOS-attacker finns det ingen garanti för att alla möjliga DDOS-attacker identifieras. |
| Trafikblockerare | Om du använder en spårningsblockerare i en webbläsare kan det hända att vissa begäranden inte spåras. |
| Brandväggar | Brandväggar kan blockera Analytics-spårning. Detta scenario är vanligare med brandväggar. |

Se även [Licensieringspanel](/help/implementing/cloud-manager/license-dashboard.md).

### Olika typer av innehållsförfrågningar {#included-content-requests}

| Typ av begäran | Innehållsbegäran | Beskrivning |
| --- | --- | --- |
| HTTP-kod 100-299 | Ingår | Det här är vanliga förfrågningar som levererar allt eller delar av innehåll. |
| HTTP-bibliotek för automatisering | Ingår | Exempel:<br>・ Amazon CloudFront<br>・ Apache HTTP-klient<br>・ Asynkron HTTP-klient<br>・ Axios<br>・ Azureus<br>・ Rullande<br>・ GitHub-nodhämtning<br>・ Guzzle<br>・ Go-http-client<br>・ Headless Chrome<br>・ Java™ Client<br>・ Jersey<br>・ Node Oembed<br>・ okhttp<br>・ Python-förfrågningar<br>・ Reaktorenhet<br>・ Wget<br>・ WinHTTP |
| Verktyg för övervakning och hälsokontroll | Ingår | Dessa konfigureras av kunden för att övervaka en viss aspekt av webbplatsen. Exempel: tillgänglighet eller verkliga användarprestanda. Använd `/system/probes/health` slutpunkten och inte de faktiska HTML-sidorna från webbplatsen.<br>Exempel:<br>・ Amazon-Route53-Health-Check-Service<br>・ EyeMonIT_bot_version_0.1_[(https://www.eyemon.it/)](https://www.eyemon.it/)<br>・ Investis-Site24x7<br>・ Mozilla/5.0+(compatible; UptimeRobot/2.0; [https://uptimerobot.com/](https://uptimerobot.com/))<br>・ ThousandEyes-Dragonfly-x1<br>・ OmtrBot/1.0<br>・ WebMon/2.0.0 |
| `<link rel="prefetch">` förfrågningar | Ingår | För att öka hastigheten vid inläsning av nästa sida kan kunderna låta webbläsaren läsa in en uppsättning sidor innan användaren klickar på länken, så att de redan finns i cachen. *Obs! Detta ökar trafiken avsevärt*—Beroende på hur många av dessa sidor som har förhämtats. |
| Trafik som blockerar rapportering från Adobe Analytics eller Google Analytics | Ingår | Det är vanligare att besökare på webbplatser har installerat sekretessprogram (annonsblockerare osv.) som påverkar Google Analytics eller Adobe Analytics precision. AEM as a Cloud Service räknar förfrågningar på den första ingångspunkten till den infrastruktur som drivs av Adobe och inte på klientsidan. |

Se även [Licensieringspanel](/help/implementing/cloud-manager/license-dashboard.md).

### Olika typer av utelämnade innehållsbegäranden {#excluded-content-request}

| Typ av begäran | Innehållsbegäran | Beskrivning |
| --- | --- | --- |
| HTTP-kod 500+ | Exkluderad | Fel som returneras till besökaren när något går fel AEM as a Cloud Service eller kundens anpassade kod. |
| HTTP-kod 400-499 | Exkluderad | Fel returneras till besökaren när innehållet inte finns (404) eller om det finns andra innehålls- eller förfrågningsrelaterade problem. |
| HTTP-kod 300-399 | Exkluderad | Det här är bra begäranden som antingen kontrollerar om något har ändrats på servern eller omdirigerar begäran till en annan resurs. De innehåller inte själva innehållet och är därför inte fakturerbara. |
| Begäranden som går att /libs/* | Exkluderad | AEM interna JSON-begäranden, till exempel CSRF-token som inte är fakturerbar. |
| Trafik från DDOS-attacker | Exkluderad | DDOS-skydd. AEM identifierar automatiskt vissa av DDOS-attackerna och blockerar dem. DDOS-attacker om de upptäcks är inte fakturerbara. |
| AEM as a Cloud Service NewRelic-övervakning | Exkluderad | AEM as a Cloud Service global övervakning. |
| URL för att kunderna ska kunna övervaka sina Cloud Service | Exkluderad | Rekommenderad URL för extern övervakning av tillgängligheten.<br><br>`/system/probes/health` |
| AEM as a Cloud Service Pod Warm-up Service | Exkluderad | Användaragent: skyline-service-warmup/1.* |
| Välkända sökmotorer, sociala nätverk och HTTP-bibliotek (taggade med Fastly) | Exkluderad | Välkända tjänster som regelbundet besöker webbplatsen för att uppdatera sökindexet eller tjänsten:<br><br>Exempel:<br>・ AddSearchBot<br>・ AhrefsBot<br>・ Applebot<br>・ Fråga Jeeves Corporate Spider<br>・ Bingbot<br>・ BingPreview<br>・ BLEXBot<br>・ BuiltWith<br>・ Bytespider<br>・ CrawlerKengo<br>・ Facebook-extern träff<br>・ Google AdsBot<br>・ Google AdsBot Mobile<br>・ Googlebot<br>・ Googlebot Mobile<br>・ lmspider<br>・ LucidWorks<br>・ MJ12bot<br>・ Förenade kungariket<br>・ Pinterest<br>・ SemushBot<br>・ SiteImproved<br>・ StashBot<br>・ StatusCake<br>・ YandexBot |
| Uteslut Commerce integrationa frameworkar | Exkluderad | Detta är begäranden som skickas till AEM som vidarebefordras till Commerce integrationa frameworken - URL:en börjar med `/api/graphql`- för att undvika dubbelräkning kan de inte faktureras för Cloud Service. |
| Exkludera `manifest.json` | Exkluderad | Manifestet är inte ett API-anrop. Här finns information om hur du installerar webbplatser på datorer och mobiltelefoner. Adobe ska inte räkna JSON-begäran till `/etc.clientlibs/*/manifest.json` |
| Exkludera `favicon.ico` | Exkluderad | Även om det returnerade innehållet inte ska vara HTML eller JSON observerar vi att i vissa scenarier, som SAML-autentiseringsflöden, kan favoritikoner returneras eftersom HTML därför uttryckligen utesluts från räkningen. |

## Samling på klientsidan {#cliendside-collection}

## Real User Monitoring (RUM) för AEM as a Cloud Service {#real-user-monitoring-for-aem-as-a-cloud-service}

>[!INFO]
>
>Den här funktionen är bara tillgänglig för det program som används tidigt.
>Du måste använda AEM Cloud Service version **2023.11.14227** och senare för att aktivera RUM-datatjänsten.

### Ökning {#overview}

Real User Monitoring (RUM) är en typ av teknik för prestandaövervakning som samlar in och analyserar de digitala användarupplevelserna på en webbplats eller i en applikation i realtid. Den ger synlighet i ett webbprograms realtidsprestanda och ger korrekta insikter i slutanvändarens upplevelse.

Real User Monitoring (RUM, Real User Monitoring) ger djupgående insikter i nyckeltal från det att URL:en startas tills begäran skickas tillbaka till webbläsaren. Tillsammans hjälper utvecklarna att förbättra applikationen så att den blir enkel att använda för slutanvändarna.

### Vem kan utnyttja RUM Data Monitoring Service? {#who-can-benefit-from-rum-data-monitoring-service}

RUM Data Service är fördelaktigt för dem som använder Adobe CDN, eftersom det ger en mer exakt återgivning av användarinteraktioner och säkerställer ett tillförlitligt mått på webbplatsengagemanget genom att återspegla antalet sidvisningar på klientsidan som kan jämföras med befintliga CDN-loggsidor på serversidan. Dessutom kan Adobe nu effektivisera den automatiska trafikrapporteringen för kunder som använder sitt eget CDN, vilket innebär att de inte behöver dela någon trafikrapport med Adobe.

Det är också en bra möjlighet att få avancerade insikter om hur sidorna fungerar för både kunder som använder Adobe CDN och kunder som använder sitt eget CDN.

### Förstå hur datatjänsten för övervakning av verkliga användare (RUM) fungerar {#understand-how-the-rum-data-service-works}

Adobe Experience Manager använder Real User Monitoring (RUM) för att hjälpa kunder och Adobe att förstå hur besökarna interagerar med webbplatser som drivs av Adobe Experience Manager, att diagnostisera prestandaproblem och att mäta hur effektiva experimenten är. RUM bevarar besökarnas integritet genom stickprov - endast en liten del av alla sidvisningar övervakas - och alla personligt identifierbara uppgifter utesluts på ett vettigt sätt.

### Övervakning av verkliga användare (RUM) och sekretess {#rum-and-privacy}

Real User Monitoring i Adobe Experience Manager är utformat för att bevara besökarnas integritet och minimera datainsamlingen. Som besökare innebär detta att ingen personlig information samlas in av den webbplats du besöker eller görs tillgänglig för Adobe.

Som webbplatsoperatör innebär detta att inget ytterligare deltagande krävs för att aktivera övervakning via den här funktionen. Det innebär att det inte finns något extra popup-fönster där slutanvändarna kan godkänna aktivering av RUM-övervakning.

### RUM-datainsamling {#rum-data-sampling}

Traditionella webbanalyslösningar försöker samla in data om varje enskild besökare. Adobe Experience Manager Real User Monitoring hämtar bara information från en liten del av sidvyerna. Real User Monitoring (RUM) är avsett att samplas och anonymiseras i stället för att ersättas för analyser. Som standard har sidorna 1:100 samplingsförhållande. Webbplatsoperatorer kan inte konfigurera det här talet för att öka eller minska samplingsfrekvensen från och med i dag. För att uppskatta den totala trafiken korrekt samlar vi in detaljerade data från en sida för varje 100 sidvy, vilket ger en tillförlitlig uppskattning av den totala trafiken.&quot;

När man bestämmer sig för om uppgifterna ska samlas in sida för sida blir det praktiskt taget omöjligt att spåra interaktionen mellan flera sidor. RUM har inget koncept för besök, besökare eller sessioner, bara för sidvisningar. Det här är designat.

### Vilka data samlas in {#what-data-is-being-collected}

Real User Monitoring (RUM) är avsett att förhindra insamling av personligt identifierbar information. Den fullständiga uppsättningen information som kan samlas in av Adobe Experience Manager Real User Monitoring (Reell användarövervakning) visas nedan:

* Värdnamnet för den webbplats som besöktes, till exempel: `experienceleague.adobe.com`
* Den breda användaragenttyp som används för att visa sidan, till exempel: dator eller mobil
* Tidpunkten för datainsamlingen, till exempel: `2021-06-26 06:00:02.596000 UTC (in order to preserve privacy, we round all minutes to the previous hour, so that only seconds and milliseconds are tracked)`
* URL-adressen till den sida som besöktes, till exempel: `https://experienceleague.adobe.com/docs`
* Referens-URL (URL:en för sidan som länkade till den aktuella sidan, om användaren följde en länk)
* Ett slumpmässigt genererat ID för sidvyn i ett format som liknar: `2Ac6`
* Samplingsfrekvensen, t.ex. `100`. Detta innebär att bara en av hundra sidvisningar spelas in
* Kontrollpunkten eller namnet på en viss händelse i den sekvens då sidan läses in eller interagerar med den som besökare
* Källan eller identifieraren för det DOM-element som användaren interagerar med för den kontrollpunkt som nämns ovan. Detta kan till exempel vara en bild
* Målet, eller länken till en extern sida eller resurs som användaren interagerar med för den kontrollpunkt som nämns ovan. Till exempel: `https://blog.adobe.com/jp/publish/2022/06/29/media_162fb947c7219d0537cce36adf22315d64fb86e94.png`
* Prestandamätningarna Core Web Vitals (CWV), Störst Contentful Paint (LCP), First Input Delay (FID) och Cumulative Layout Shift (CLS) som beskriver besökarens upplevelsekvalitet.

### Så här konfigurerar du datatjänsten för övervakning av verkliga användare (RUM) {#how-to-set-up-them-rum-data-service}

* Om du vill delta i vårt program för tidig Adobe-användare skickar du ett mejl till `aemcs-rum-adopter@adobe.com`, tillsammans med ditt domännamn för produktions-, scen- och utvecklingsmiljön från din e-postadress som är kopplad till din Adobe ID. Adobe produktteam aktiverar sedan datatjänsten Real User Monitoring (RUM) åt dig.
* När detta är klart skapar Adobe produktteam en kanal för kundsamarbete.
* Adobe produktgrupp kommer att kontakta dig för att ge dig en URL för domännyckeln och datapanelen där du kan visa sidvyer och [Core Web Vitals (CWV)](https://web.dev/vitals/) Mätvärden som samlats in av samlingen Real User Monitoring (RUM) på klientsidan.
* Därefter får du vägledning om hur du använder domännyckeln för att få åtkomst till instrumentpanelens URL och visa mätvärdena.

### Hur data för faktisk användarövervakning (RUM) används {#how-rum-data-is-being-used}

RUM-data är fördelaktiga för följande syften:

* Identifiera och åtgärda prestandamässiga flaskhalsar för kundsajter
* Effektiv, automatisk trafikrapportering som inkluderar sidvisningar för kunder som använder sitt eget CDN, vilket innebär att de inte behöver dela någon trafikrapport med Adobe.
* För att förstå hur Adobe Experience Manager interagerar med andra skript (till exempel analyser, målgruppsanpassning eller externa bibliotek) på samma sida kan man öka kompatibiliteten.

### Begränsningar och Förstå variansen i sidvyer och prestandamått {#limitations-and-understanding-variance-in-page-views-and-performance-metrics}

Eftersom du kommer att analysera dessa data kan det finnas eller inte finnas avvikelser i sidvisningar och andra prestandamått som rapporterats av Real User Monitoring (RUM). Dessa avvikelser kan tillskrivas flera faktorer som är förenade med realtidsövervakning på klientsidan. Här är några viktiga saker som kunderna bör tänka på när de tolkar sina RUM-data:

1. **Spårarblockerare**

   * Slutanvändare som använder blockerare för spårning eller tillägg för sekretess kan hindra datainsamlingen i Real User Monitoring (RUM) eftersom dessa verktyg begränsar körningen av spårningsskript. Begränsningen kan leda till underrapporterade sidvisningar och användarinteraktioner, vilket skapar en diskrepans mellan faktisk webbplatsaktivitet och data som hämtas av RUM.

1. **Begränsningar i hämtning av API-/JSON-anrop**

   * RUM-datatjänsten fokuserar på klientupplevelsen och fångar inte upp backend-API:t eller JSON-anrop just nu. Om dessa anrop utelämnas från data från Real User Monitoring (RUM) skapas avvikelser från de innehållsförfrågningar som mäts i CDN Analytics.

### Vanliga frågor {#faq}

1. **Hur konfigurerar jag sökvägar som ska inkluderas eller exkluderas vid övervakning?**

   Kunderna kan konfigurera sökvägar så att de inkluderar eller exkluderar URL:er för övervakning genom att ställa in miljövariablerna i konfigurationen i Cloud Manager med hjälp av följande variabler: `AEM_WEBVITALS_EXCLUDE` och `AEM_WEBVITALS_INCLUDE_PATHS`

   Observera att inställningen Inkludera som standard är konfigurerad för att ange /content som mål. Det är viktigt att komma ihåg att sökvägarna som du måste konfigurera här är innehållssökvägar i systemet, inte URL-sökvägarna som visas i webbläsaren. Den här skillnaden är avgörande för att du ska kunna konfigurera och anpassa konfigurationen efter dina specifika behov.

1. **Skulle Adobe kunna spåra alla sidvisningar innan interaktionen når det kundhanterade CDN eller när interaktionen når det kundhanterade CDN?**

   Ja.

1. **Kommer kunderna att kunna integrera skript för RUM-datatjänster med tredjepartssystem som Dynatrace?**

   Ja.

1. **Samlas&quot;Interaktion med nästa målning&quot;,&quot;Time to first byte&quot; och&quot;First contentful paint&quot;, webbstatistik?**

   Interaktion med nästa målning (INP) och TTFB (Time to first byte) samlas in.  Den första innehållsmässiga målningen samlas inte in just nu.
