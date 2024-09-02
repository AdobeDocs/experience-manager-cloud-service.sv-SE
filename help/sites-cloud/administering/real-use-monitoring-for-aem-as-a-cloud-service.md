---
title: Real Use Monitoring for AEM as a Cloud Service
description: Lär dig hur du använder Real Use Monitoring (RUM) för att hämta in och analysera den digitala användarupplevelsen för en webbplats eller tillämpning i realtid.
exl-id: 91fe9454-3dde-476a-843e-0e64f6f73aaf
feature: Administering
role: Admin
source-git-commit: 1bb463fe59e89e6360dceefdaaec395084fc80c5
workflow-type: tm+mt
source-wordcount: '1213'
ht-degree: 0%

---

# Real Use Monitoring Service för AEM as a Cloud Service {#real-use-monitoring-service-for-aem-as-a-cloud-service}

>[!NOTE]
>
>Tjänsten för övervakning av faktisk användning, datainsamling på klientsidan, är en automatiserad tjänst. Ingen kundinställning krävs.

>[!INFO]
>
>Övervakning på klientsidan fungerar bara för kunder med Cloud Servicen AEM (Adobe Experience Manager) version **2024.5.16461** och senare.

## Ökning {#overview}

Tjänsten RUM (Real Use Monitoring) är en teknik för prestandaövervakning som samlar in och analyserar de digitala användarupplevelserna för en webbplats eller tillämpning i realtid. Den ger synlighet i ett webbprograms realtidsprestanda och ger djupare insikter i slutanvändarens upplevelse. Tjänsten fokuserar på att optimera prestanda genom att övervaka webbplatsens engagemang, snarare än användarna själva.

Med RUM spåras nyckeltal från det att URL:en startas tills begäran skickas tillbaka till webbläsaren. Det hjälper utvecklare att förbättra programmet så att det blir enkelt att använda för slutanvändarna.

>[!INFO]
>
>&quot;Real User Monitoring&quot; har ändrats till &quot;Real Use Monitoring&quot; eftersom det bättre återspeglar tjänstens verkliga kärna.

## Vem kan utnyttja en tjänst för övervakning av verkligt bruk? {#who-can-benefit-from-rum-service}

AEM har utvecklat RUM för att hjälpa kunder och Adobe att förstå hur besökarna interagerar med AEM webbplatser. RUM kan användas för att diagnostisera prestandaproblem och mäta hur effektiva experimenten är. RUM bevarar besökarnas integritet genom stickprov - endast en liten del av alla sidvisningar övervakas - och ingen personligt identifierbar information samlas in.

## Övervakningstjänst och sekretess för användning i realtid {#rum-service-and-privacy}

Tjänsten för övervakning av verkligt bruk i AEM är utformad för att bevara besökarnas sekretess och minimera datainsamlingen. Som besökare innebär det att den webbplats som du besöker eller som är tillgänglig för Adobe inte samlar in några personuppgifter.

Som webbplatsoperatör krävs inget ytterligare deltagande för att aktivera övervakning via den här funktionen. Det finns inga ytterligare popup-formulär eller medgivandeformulär som slutanvändarna kan godkänna för aktivering av RUM.

## Datainsamling för övervakning av realanvändning {#rum-service-data-sampling}

Traditionella webbanalyslösningar försöker samla in data om varje enskild besökare. AEM RUM-tjänst hämtar bara information från en liten del av sidvyerna. Tjänsten är avsedd att samplas och anonymiseras i stället för att ersättas för analyser. Som standard har sidorna 1:100 samplingsförhållande. Webbplatsoperatorer kan för närvarande inte öka eller minska samplingsfrekvensen. För att beräkna den totala trafiken korrekt samlas data in från 1 för varje 100 sidvy, vilket ger en tillförlitlig uppskattning av den totala trafiken.

När man beslutar om uppgifterna ska samlas in, görs det i sidvy per sida och det blir praktiskt taget omöjligt att spåra interaktioner mellan flera sidor. RUM har som standard inget koncept för besökare eller sessioner, utan bara för sidvisningar.

## Vilka data samlas in? {#what-data-is-being-collected}

Tjänsten för övervakning av faktisk användning är utformad för att förhindra insamling av personligt identifierbar information. Den fullständiga uppsättningen information som samlas in av RUM anges nedan:

* Värdnamnet för den webbplats som besöktes, till exempel: `experienceleague.adobe.com`
* Den breda användaragenttypen och det operativsystem som används för att visa sidan, till exempel: `desktop:windows` eller `mobile:ios`
* Tidpunkten för datainsamlingen, till exempel: `2021-06-26 06:00:02.596000 UTC (in order to preserve privacy, we round all minutes to the previous hour, so that only seconds and milliseconds are tracked)`
* URL:en för sidan som besöks, till exempel: `https://experienceleague.adobe.com/docs`
* Referens-URL (URL:en för sidan som länkade till den aktuella sidan, om användaren följde en länk)
* Ett slumpmässigt genererat ID för sidvyn i ett format som liknar: `2Ac6`
* Samplingsfrekvensen, t.ex. `100`, har samma vikt eller inverterad. Det betyder att bara en av hundra sidvisningar spelas in
* Kontrollpunkten, eller namnet, för en viss händelse i den sekvens då sidan läses in. Eller interagera med det som besökare
* Källan, eller identifieraren, för det DOM-element som användaren interagerar med för den kontrollpunkt som nämns ovan. Det kan till exempel vara en bild
* Målet, eller länken till en extern sida eller resurs som användaren interagerar med för den kontrollpunkt som nämns ovan. Till exempel: `https://blog.adobe.com/jp/publish/2022/06/29/media_162fb947c7219d0537cce36adf22315d64fb86e94.png`
* Prestandamätningarna Core Web Vitals (CWV), inklusive LCP (Störst Contentful Paint), FID (First Input Delay), CLS (Cumulative Layout Shift) och TTFB (Time To First Byte) som beskriver besökarens upplevelsekvalitet.

## Så fungerar övervakning av riktig användning för en kund {#how-rum-works-for-a-customer}

Övervakning av faktisk användning övervakar automatiskt klienttrafiken för att ge dig värdefulla insikter. Som Adobe-kund behöver du inte vidta några ytterligare åtgärder eftersom den här tjänsten är sömlöst integrerad i din befintliga konfiguration. Med lanseringen av General Availability (GA) drar du automatiskt nytta av den här nya funktionen.

<!-- Alexandru: hiding temporarily, until we figure out where this needs to be linked to 

If you wish to leverage more insights with this new feature to optimize your digital experiences effortlessly, please see here (link to Row 99). -->

## Hur data från övervakningstjänsten för verkligt bruk används {#how-rum-service-data-is-being-used}

RUM-data är fördelaktiga för följande syften:

* Identifiera och åtgärda prestandamässiga flaskhalsar för kundsajter
* För att effektivisera automatisk trafiksökning med sidvyer.
* För att förstå hur AEM interagerar med andra skript (till exempel analyser, målinriktning eller externa bibliotek) på samma sida, ökar kompatibiliteten.

## Begränsningar och förståelse av variationer i sidvisningar och prestandamått {#limitations-and-understanding-variance-in-page-views-and-performance-metrics}

När du analyserar RUM-data kan det finnas skillnader i sidvisningar och andra prestandamått. Dessa avvikelser kan tillskrivas flera faktorer som är förenade med realtidsövervakning på klientsidan. Här är några viktiga saker som kunderna bör tänka på när de tolkar sina RUM-data:

1. **Spårarblockerare**

   * Slutanvändare som använder blockerare för spårning eller tillägg för sekretess kan förhindra insamling av RUM-data, eftersom dessa verktyg begränsar körningen av spårningsskript. Begränsningen kan leda till underrapporterade sidvisningar och användarinteraktioner, vilket skapar en diskrepans mellan faktisk webbplatsaktivitet och data som samlats in av RUM.

1. **Begränsningar i hämtning av headless API/JSON-anrop**

   * RUM-datatjänsten fokuserar på klientupplevelsen och fångar inte upp backend-API:t eller JSON-anrop som gjorts från en AEM headless-app för tillfället. Om dessa anrop utesluts från RUM-tjänstdata skapas avvikelser från innehållsförfrågningar som mäts med CDN Analytics.

## Vanliga frågor {#faq}


1. **Kan kunder integrera skript för RUM-tjänster med tredjepartssystem som Dynatrace?**

   Ja.

1. **Samlas interaktion med nästa färg, tid till första byte och första innehållsanpassade målning in i webbinarierna?**

   Interaktion med nästa färg (INP) och TTFB (Time To First Byte) samlas in.  Den första innehållsmässiga målningen samlas inte in just nu.

1. **Sökvägen `/.rum` blockeras på min webbplats, hur ska jag åtgärda den?**

   Sökvägen `/.rum` krävs för att RUM-samlingen ska fungera. Om du använder ett CDN framför Adobe AEM as a Cloud Service måste du se till att sökvägen `/.rum` går till samma AEM som ditt andra AEM. Och se till att den inte justeras på något sätt.

1. **Räknas RUM-samlingen med innehållsförfrågningar för kontraktssyften?**

   RUM-biblioteket och RUM-samlingen räknas inte som innehållsbegäranden och ökar inte antalet rapporterade sidvisningar eller API-anrop. Dessutom är [samling på serversidan](#serverside-collection) grunden för innehållsförfrågningar för kunder som använder det färdiga CDN-nätverket med AEM as a Cloud Service.

1. **Hur avanmäler jag mig?**

   Adobe rekommenderar att man använder Real Use Monitoring (RUM) på grund av dess stora fördelar och att man kan optimera de digitala upplevelserna. Det kan ge värdefulla insikter som kan förbättra webbplatsens prestanda. Tjänsten är utformad för att vara sömlös och påverkar inte webbplatsens prestanda.

   Om du väljer bort något missar du dessa insikter. Om du råkar ut för några problem kontaktar du Adobe Support.
