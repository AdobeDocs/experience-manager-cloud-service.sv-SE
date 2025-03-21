---
title: Real Use Monitoring for AEM as a Cloud Service
description: Läs om Real Use Monitoring (RUM), en automatiserad tjänst som gör det möjligt att övervaka datainsamlingen på klientsidan.
exl-id: 91fe9454-3dde-476a-843e-0e64f6f73aaf
feature: Administering
role: Admin
source-git-commit: e6a610c56b9ad7a684ea9f5ef72199d3bed28cc0
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 0%

---

# Real Use Monitoring Service för AEM as a Cloud Service {#real-use-monitoring-service-for-aem-as-a-cloud-service}

>[!NOTE]
>
>Tjänsten för övervakning av faktisk användning, datainsamling på klientsidan, är en automatiserad tjänst. Ingen kundinställning krävs.

>[!INFO]
>
>Övervakning på klientsidan fungerar bara för kunder med AEM (Adobe Experience Manager) Cloud Service version **2024.5.16461** och senare.

## Ökning {#overview}

Tjänsten RUM (Real Use Monitoring) är en teknik för prestandaövervakning som övervakar klienttrafiken på en webbplats eller ett program i realtid. Den här tjänsten fokuserar på att samla in statistik och data som är viktiga för att optimera prestandan genom att övervaka webbplatsengagemang, snarare än användarna själva. Med RUM spåras nyckeltal från det att URL:en startas tills begäran skickas tillbaka till webbläsaren.

## Vem kan utnyttja en tjänst för övervakning av verkligt bruk? {#who-can-benefit-from-rum-service}

Real Use Monitoring (Reell Use Monitoring) hjälper kunder och Adobe att förstå hur slutanvändarna interagerar med AEM webbplatser. Real Use Monitoring (Övervakning av verklig användning) diagnostiserar prestandaproblem och mäter effekten av experiment. Övervakning av faktisk användning bevarar besökarnas integritet genom stickprov - endast en liten del av alla sidvisningar övervakas - och ingen personligt identifierbar information samlas in.

## Övervakningstjänst och sekretess för användning i realtid {#rum-service-and-privacy}

Tjänsten för övervakning av användning i AEM bevarar besökarnas integritet och minimerar datainsamlingen. Som besökare innebär det att den webbplats som du besöker eller gör tillgänglig för Adobe inte samlar in några personuppgifter.

Som webbplatsoperatör krävs inget ytterligare deltagande för att aktivera övervakning via den här funktionen. Det finns inga ytterligare popup-formulär eller medgivandeformulär som slutanvändarna kan godkänna för aktivering av RUM.

## Datainsamling för övervakning av realanvändning {#rum-service-data-sampling}

Traditionella webbanalyslösningar försöker samla in data om varje enskild besökare. AEM Real Use Monitoring (RUM) hämtar endast information från en liten del av sidvyerna. Tjänsten är avsedd att samplas och anonymiseras i stället för att ersättas för analyser. Som standard har sidorna 1:100 samplingsförhållande. Webbplatsoperatorer kan för närvarande inte öka eller minska samplingsfrekvensen. För att beräkna den totala trafiken korrekt samlas data in från 1 för varje 100 sidvy, vilket ger en tillförlitlig uppskattning av den totala trafiken.

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
* Prestandamätningarna [Core Web Vitals (CWV)](https://web.dev/articles/lcp) [Störst Contentful Paint (LCP)](https://web.dev/articles/lcp), [Interaction to Next Paint (INP)](https://web.dev/articles/inp) och [Cumulative Layout Shift (CLS)](https://web.dev/articles/cls) som beskriver besökarens upplevelsekvalitet.

## Så fungerar övervakning av riktig användning för en kund {#how-rum-works-for-a-customer}

Real Use Monitoring övervakar automatiskt trafiken på klientsidan. Som Adobe-kund behöver du inte vidta några ytterligare åtgärder eftersom den här tjänsten är sömlöst integrerad i din befintliga konfiguration. Med tjänsten för övervakning av faktisk användning (RUM) allmänt tillgänglig drar du automatiskt nytta av den här nya funktionen. Tjänsten för övervakning av faktisk användning visar inte några kundrelaterade mätvärden idag för övervakning. Vi arbetar på att leverera den här funktionen till dig så snart som möjligt.

<!-- Alexandru: hiding temporarily, until we figure out where this needs to be linked to 

If you wish to leverage more insights with this new feature to optimize your digital experiences effortlessly, please see here (link to Row 99). -->

## Hur Adobe använder övervakning av faktisk användning {#how-rum-data-is-being-used}

Data från övervakning av faktisk användning används för följande syften:

* Identifiera och åtgärda prestandamässiga flaskhalsar för kundsajter
* För att förstå hur AEM interagerar med andra skript (till exempel analyser, målinriktning eller externa bibliotek) på samma sida, ökar kompatibiliteten.
<!--
## Limitations and understanding variance in page views and performance metrics {#limitations-and-understanding-variance-in-page-views-and-performance-metrics}

Here are key considerations for customers to keep in mind when interpreting their RUM data:

1. **Tracker blockers**

   * End-users employing tracker blockers or privacy extensions can impede RUM data collection, as these tools restrict the tracking scripts' execution. This restriction may lead to underreported page views and user interactions, creating a discrepancy between actual site activity and the data captured by RUM.

1. **Limitations in capturing headless API/JSON calls**

   * RUM data service focuses on the client-side experience and doesn't capture the backend API or JSON calls made from a non-AEM headless app at this time. The exclusion of these calls from RUM service data creates variances from the content requests measured by CDN Analytics.
-->

## Vanliga frågor {#faq}

<!-- REMOVED THIS FAQ AS PER EMAIL REQUEST FROM SHWETA DUA, SEPTEMBER 4, 2024 TO THE DL-AEM-DOCS GROUP 
1. **Can customers integrate the RUM service scripts with third-party systems like Dynatrace?**

   Yes.
-->

1. **Samlas värdena&quot;Interaktion med nästa färg&quot;,&quot;Tid till första byte&quot; och&quot;Första innehållsanpassade målning&quot;?**

   Interaktion med nästa färg (INP) och TTFB (Time To First Byte) samlas in.  Den första innehållsmässiga målningen samlas inte in just nu.

1. **Sökvägen `/.rum` blockeras på min webbplats, hur ska jag åtgärda den?**

   Sökvägen `/.rum` krävs för att RUM-samlingen ska fungera. Om du använder ett CDN framför Adobe AEM as a Cloud Service kontrollerar du att sökvägen `/.rum` går till samma AEM-ursprung som ditt andra AEM-innehåll. Och se till att den inte justeras på något sätt.

1. **Räknas RUM-samlingen med innehållsförfrågningar för kontraktssyften?**

   RUM-biblioteket och RUM-samlingen räknas inte som innehållsbegäranden och ökar inte antalet rapporterade sidvisningar eller API-anrop. Dessutom är [samling på serversidan](#serverside-collection) grunden för innehållsförfrågningar för kunder som använder det färdiga CDN-nätverket med AEM as a Cloud Service.

1. **Hur avanmäler jag mig?**

   Adobe rekommenderar att du använder Real Use Monitoring (RUM) på grund av dess stora fördelar och att det kommer att göra det möjligt för Adobe att optimera dina digitala upplevelser genom att förbättra webbplatsens prestanda. Tjänsten är utformad för att vara sömlös och påverkar inte webbplatsens prestanda.

   Om du väljer bort detta kan det innebära att du missar en chans att förbättra trafikengagemanget på din webbplats. Om du råkar ut för några problem kontaktar du Adobe Support.