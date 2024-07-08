---
title: Övervakning av verklig användning för AEM as a Cloud Service
description: Lär dig hur du använder Real Use Monitoring (RUM) för att fånga och analysera den digitala användarupplevelsen av en webbplats eller ett program i realtid.
exl-id: 91fe9454-3dde-476a-843e-0e64f6f73aaf
feature: Administering
role: Admin
source-git-commit: 9a8adf777008b7a601abc8760cee67ec3c1816c6
workflow-type: tm+mt
source-wordcount: '1301'
ht-degree: 0%

---

# Övervakningstjänst för verklig användning för AEM as a Cloud Service {#real-use-monitoring-service-for-aem-as-a-cloud-service}

>[!NOTE]
>
>Real Use Monitoring-tjänsten, datainsamling på klientsidan, är en automatiserad tjänst. Ingen kundinställning krävs.

>[!INFO]
>
>Övervakning på klientsidan fungerar bara för kunder med AEM Cloud Service version **2024.5.16461** och senare.

## Överblick {#overview}

Tjänsten Real Use Monitoring (RUM) är en teknik för prestandaövervakning som fångar och analyserar de digitala användarupplevelserna på en webbplats eller applikation i realtid. Det ger insyn i realtidsprestanda för ett webbprogram och ger djupare insikt i slutanvändarupplevelsen. Tjänsten fokuserar på att optimera prestanda genom att övervaka webbplatsengagemang, snarare än användarna själva.

Med RUM spåras viktiga prestandamått direkt från initieringen av URL:en tills begäran skickas tillbaka till webbläsaren. Det hjälper utvecklare att förbättra applikationen för att göra den enkel att använda för slutanvändarna.

>[!INFO]
>
>&quot;Real User Monitoring&quot; har bytt namn till &quot;Real Use Monitoring&quot; eftersom det bättre återspeglar den verkliga kärnan i tjänsten.

## Vem kan dra nytta av en tjänst för övervakning av verklig användning? {#who-can-benefit-from-rum-service}

Tjänsten för övervakning av verklig användning är fördelaktig för alla kunder. Det ger en representativ återspegling av användarinteraktioner, vilket säkerställer ett tillförlitligt mått på webbplatsens engagemang genom att fånga antalet sidvisningar på klientsidan.

För alla Adobe-kunder ger den här tjänsten värdefulla insikter om användarinteraktioner. Kunder som använder sitt eget CDN kan dra nytta av förenklad trafikrapportering, eftersom Adobe nu integrerar datainsamlingen direkt, vilket eliminerar behovet av separata rapporter under förnyelsecyklerna.

## Förstå hur tjänsten för övervakning av verklig användning fungerar {#understand-how-the-rum-service-works}

Adobe Experience Manager (AEM) använder Real Use Monitoring (RUM) för att hjälpa kunder och Adobe att förstå hur besökare interagerar med AEM webbplatser. Det hjälper dem att diagnostisera prestandaproblem och mäta effektiviteten av experiment. RUM bevarar besökarnas integritet genom stickprov - endast en liten del av alla sidvisningar övervakas - och ingen personligt identifierbar information (PII) samlas in.

## Tjänst för övervakning av verklig användning och sekretess {#rum-service-and-privacy}

Tjänsten Real Use Monitoring i AEM är utformad för att bevara besökarnas integritet och minimera datainsamlingen. Som besökare innebär det att den webbplats du besöker eller som du har gjort tillgänglig för Adobe inte samlar in någon personlig information.

Som webbplatsoperatör krävs ingen ytterligare anmälan för att aktivera övervakning via den här funktionen. Det finns inget ytterligare popup- eller samtyckesformulär som slutanvändarna kan acceptera för att aktivera RUM.

## Provtagning av data för övervakning av verklig användning {#rum-service-data-sampling}

Traditionella webbanalyslösningar försöker samla in data om varje enskild besökare. AEM RUM-tjänst samlar bara in information från en liten del av sidvisningarna. Tjänsten är avsedd att samplas och anonymiseras snarare än en ersättning för analys. Som standard har sidor ett samplingsförhållande på 1:100. Webbplatsoperatörer kan för närvarande inte öka eller minska samplingsfrekvensen. För att uppskatta den totala trafiken korrekt, för varje 100 sidvisningar, samlas data in från 1, vilket ger dig en tillförlitlig uppskattning av den totala trafiken.

Som beslutet om huruvida data samlas in eller inte görs det sida för sida, och det blir praktiskt taget omöjligt att spåra interaktioner på flera sidor. RUM är utformat för att inte ha något begrepp om besökare eller sessioner, bara om sidvisningar.

## Vilka uppgifter samlas in? {#what-data-is-being-collected}

Tjänsten Real Use Monitoring är utformad för att förhindra insamling av personligt identifierbar information. Den fullständiga uppsättningen information som samlas in av RUM listas nedan:

* Värdnamnet för den webbplats som besöks, till exempel: `experienceleague.adobe.com`
* Den breda typen av användaragent och det operativsystem som används för att visa sidan, till exempel: `desktop:windows` eller `mobile:ios`
* Tidpunkten för datainsamlingen, till exempel: `2021-06-26 06:00:02.596000 UTC (in order to preserve privacy, we round all minutes to the previous hour, so that only seconds and milliseconds are tracked)`
* Webbadressen till sidan som besöks, till exempel: `https://experienceleague.adobe.com/docs`
* Hänvisnings-URL:en (webbadressen till sidan som länkade till den aktuella sidan, om användaren följde en länk)
* Ett slumpmässigt genererat ID för sidvisningen i ett format som liknar: `2Ac6`
* Vikten eller inversen av samplingsfrekvensen, till exempel: `100`. Det betyder att endast en av hundra sidvisningar registreras
* Kontrollpunkten, eller namnet, för en viss händelse i sekvensen när sidan läses in. Eller interagera med den som besökare
* Källan, eller identifieraren, för DOM-elementet som användaren interagerar med för kontrollpunkten som nämns ovan. Det kan till exempel vara en bild
* Målet, eller länken till en extern sida eller resurs som användaren interagerar med för kontrollpunkten som nämns ovan. Till exempel: `https://blog.adobe.com/jp/publish/2022/06/29/media_162fb947c7219d0537cce36adf22315d64fb86e94.png`
* Prestandamåtten Core Web Vitals (CWV), inklusive Largest Contentful Paint (LCP), First Input Delay (FID), Cumulative Layout Shift (CLS) och Time To First Byte (TTFB) som beskriver besökarens upplevelsekvalitet.

## Så här fungerar övervakning av verklig användning för en kund {#how-rum-works-for-a-customer}

Real Use Monitoring övervakar automatiskt trafik på klientsidan för att ge dig värdefulla insikter. Som Adobe-kund behöver du inte vidta några ytterligare åtgärder, eftersom den här tjänsten är sömlöst integrerad i din befintliga installation. Med distributionen av allmän tillgänglighet (GA) kan du automatiskt dra nytta av den här nya funktionen.

<!-- Alexandru: hiding temporarily, until we figure out where this needs to be linked to 

If you wish to leverage more insights with this new feature to optimize your digital experiences effortlessly, please see here (link to Row 99). -->

## Hur data från tjänsten för övervakning av verklig användning används {#how-rum-service-data-is-being-used}

RUM-data är fördelaktiga för följande ändamål:

* För att identifiera och åtgärda flaskhalsar i prestanda för kundwebbplatser
* För att effektivisera automatiserad trafiksökning som inkluderar sidvisningar.
* För att förstå hur AEM interagerar med andra skript (t.ex. analys, målinriktning eller externa bibliotek) på samma sida, för att öka kompatibiliteten.

## Begränsningar och förstå varians i sidvisningar och prestandamått {#limitations-and-understanding-variance-in-page-views-and-performance-metrics}

När du analyserar RUM-data kan det finnas variationer i sidvisningar och andra prestandamått. Dessa avvikelser kan tillskrivas flera faktorer som är inneboende i övervakning i realtid på klientsidan. Här är viktiga överväganden för kunder att tänka på när de tolkar sina RUM-data:

1. **Blockerare av spårare**

   * Slutanvändare som använder spårningsblockerare eller sekretesstillägg kan hindra RUM-datainsamling, eftersom dessa verktyg begränsar spårningsskriptens exekvering. Den här begränsningen kan leda till underrapporterade sidvisningar och användarinteraktioner, vilket skapar en diskrepans mellan den faktiska webbplatsaktiviteten och de data som samlas in av RUM.

1. **Begränsningar vid insamling av headless API/JSON-anrop**

   * RUM-datatjänsten fokuserar på klientsidan och samlar för närvarande inte in serverdels-API:t eller JSON-anrop som görs från en icke-AEM headless-app. Uteslutningen av dessa anrop från RUM-tjänstdata skapar avvikelser från de innehållsbegäranden som mäts av CDN Analytics.

## FAQ {#faq}


1. **Kan kunder integrera RUM-tjänstskripten med system från tredje part som Dynatrace?**

   Ja.

1. **Samlas &quot;Interaktion till nästa målning&quot;, &quot;Tid till första byte&quot; och &quot;Första innehållsrika målning&quot; in webbvitala mätvärden?**

   Interaction to next paint (INP) och Time To First Byte (TTFB) samlas in.  Den första innehållsrika färgen samlas inte in vid denna tidpunkt.

1. **Sökvägen `/.rum` är blockerad på min webbplats, hur ska jag fixa?**

   Sökvägen `/.rum` krävs för att RUM-insamling ska fungera. Om du har ett CDN framför det som Adobe tillhandahåller som en del av AEM as a Cloud Service måste du se till att `/.rum` sökvägen vidarebefordras till samma AEM ursprung som resten av ditt AEM. Och se till att den inte är justerad på något sätt.

1. **Räknas RUM-insamling in i innehållsförfrågningar för avtalsändamål?**

   RUM-biblioteket och RUM-samlingen räknas inte som innehållsbegäranden och ökar inte det rapporterade antalet sidvisningar eller API-anrop. För kunder som använder CDN direkt med AEM as a Cloud Service [är dessutom insamling](#serverside-collection) på serversidan grunden för innehållsförfrågningar.

1. **Hur kan jag avregistrera mig?**

   Adobe rekommenderar att du använder Real Use Monitoring (RUM) på grund av dess betydande fördelar och att det kan göra det möjligt för er att optimera era digitala upplevelser. Det kan ge värdefulla insikter som kan bidra till att förbättra webbplatsens prestanda. Tjänsten är utformad för att vara sömlös och har ingen inverkan på din webbplats prestanda.

   Att välja bort innebär att du missar dessa insikter. Om du stöter på problem kan du kontakta Adobe Support.
