---
title: Förstå förfrågningar om Cloud Service
description: Om du har köpt innehållsförfrågningslicenser från Adobe kan du ta reda på vilka typer av innehållsförfrågningar som Adobe Experience Cloud som en tjänst mäter och varianterna med en organisations analysrapporteringsverktyg.
exl-id: 3666328a-79a7-4dd7-b952-38bb60f0967d
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 16941385a05358d9a5cf3f57405b8f2174902af2
workflow-type: tm+mt
source-wordcount: '1278'
ht-degree: 0%

---

# Förstå förfrågningar om Cloud Service

## Introduktion {#introduction}

Innehållsbegäranden avser förfrågningar som görs till AEM Sites, inklusive förfrågningar som rör Edge Delivery Services eller kundtillhandahållna cachningssystem som ett Content Delivery Network. Dessa förfrågningar levererar innehåll eller data i HTML-format via sidvyer (till exempel sidor och Experience Fragments) eller i JSON-format via API-anrop utan rubriker. Innehållsförfrågningar räknas antingen som en sidvy eller som fem API-anrop och mäts vid ingången till det första cachningssystem som tar emot en innehållsförfrågan. Vissa HTTP-begäranden inkluderas eller exkluderas för att räkna innehållsbegäranden. En fullständig lista över sådana inkluderade och exkluderade HTTP-begäranden, samt tekniska definitioner av dem, finns i dokumentationen.

## Om begäranden om Cloud Service {#understanding-cloud-service-content-requests}

För kunder som använder det färdiga CDN-numret mäts förfrågningar om Cloud Service via datainsamling på serversidan. Den här samlingen aktiveras via CDN-logganalys. AEM (Adobe Experience Manager) samlar automatiskt in innehållsförfrågningar på serversidan i kanten. Den analyserar loggfiler som genererats av AEM as a Cloud Service CDN. Den här processen görs genom att isolera förfrågningarna som returnerar HTML `(text/html)` - eller JSON `(application/json)` -innehåll från CDN, och baseras på flera inkluderings- och exkluderingsregler som anges nedan. En innehållsbegäran inträffar oavsett om innehållet skickas från CDN-cachen eller returneras till CDN-ursprunget (AEM avsändare).

<!-- REMOVED AS PER EMAIL REQUEST FROM SHWETA DUA, JULY 30, 2024 TO RICK BROUGH AND ALEXANDRU SARCHIZ   For customers employing their own CDN, client-side collection offers a more precise reflection of interactions, ensuring a reliable measure of website engagement via the [Real Use Monitoring](/help/sites-cloud/administering/real-use-monitoring-for-aem-as-a-cloud-service.md) service. This gives customers advanced insights into their page traffic and performance. While it is beneficial for all customers, it offers a representative reflection of user interactions, ensuring a reliable measure of website engagement by capturing the number of page views from the client side. 

For customers that bring their own CDN on top of AEM as a Cloud Service, server-side reporting results in numbers that cannot be used to compare with the licensed content requests. With the [Real Use Monitoring](/help/sites-cloud/administering/real-use-monitoring-for-aem-as-a-cloud-service.md), Adobe can reflect a reliable measure of website engagement. -->

### Variationer i förfrågningar om Cloud Service {#content-requests-variances}

Innehållsförfrågningar kan ha avvikelser inom en organisations analysrapporteringsverktyg som sammanfattas i följande tabell. I allmänhet bör du undvika att använda analysverktyg som använder klientutrustning för att rapportera antalet innehållsförfrågningar för en webbplats. Dessa verktyg saknar ofta en stor del av trafiken eftersom de kräver att användaren ger sitt medgivande. Analysverktyg som samlar in data på serversidan i loggfiler, eller CDN-rapporter för kunder som lägger till egna CDN ovanpå AEM as a Cloud Service, ger bättre antal.

| Orsak till avvikelse | Förklaring |
|---|---|
| Användarens samtycke | Analysverktyg som förlitar sig på instrumentering på klientsidan är ofta beroende av att användarens samtycke aktiveras. Det här arbetsflödet kan representera merparten av trafiken som inte spåras. För kunder som vill mäta innehållsförfrågningar på egen hand rekommenderar vi att man använder analysverktyg för att samla in data på serversidan eller CDN-rapporter. |
| Taggar | Alla sidor eller API-anrop som spåras som Adobe Experience Manager-innehållsbegäranden kanske inte taggas med Analytics-spårning. |
| Tag Management Rules | Regelinställningar för tagghantering kan resultera i olika datainsamlingskonfigurationer på en sida, vilket resulterar i en kombination av avvikelser med spårning av innehållsbegäran. |
| Bots | Okända fel som AEM inte har föridentifierat och tagit bort kan orsaka spårningsavvikelser. |
| Rapportsviter | Sidor som ingår i samma AEM och domän kan skicka data till olika rapportsviter i Analytics. |
| Övervaknings- och säkerhetsverktyg från tredje part | Övervaknings- och säkerhetssökningsverktygen kan generera innehållsförfrågningar för AEM som inte spåras i analysrapporter. |
| API-åtkomst | Programmatisk åtkomst till sidor eller till Adobe Experience Manager API:er kan generera innehållsförfrågningar för AEM som inte spåras i Analytics-rapporter. |
| Förhämtningsbegäranden | Om du använder en förhämtningstjänst för att förhandsladda sidor för att öka hastigheten kan det medföra att trafiken för innehållsförfrågningar ökar avsevärt. |
| DOS | Adobe gör försök att automatiskt upptäcka och filtrera bort trafik från DDOS-attacker, men det finns ingen garanti för att alla möjliga DDOS-attacker identifieras. |
| Trafikblockerare | Om du använder en spårningsblockerare i en webbläsare kan det hända att vissa begäranden inte spåras. |
| Brandväggar | Brandväggar kan blockera Analytics-spårning. Detta scenario är vanligare med brandväggar. |

Se även [License Dashboard](/help/implementing/cloud-manager/license-dashboard.md).

## Samlingsregler på serversidan {#serverside-collection}

Det finns regler för att utesluta välkända botar, inklusive välkända tjänster som regelbundet besöker webbplatsen för att uppdatera deras sökindex eller tjänst.

### Olika typer av innehållsförfrågningar {#included-content-requests}

| Typ av begäran | Innehållsbegäran | Beskrivning |
| --- | --- | --- |
| HTTP-kod 100-299 | Ingår | Regelbundna förfrågningar som levererar allt eller delar av innehåll. |
| HTTP-bibliotek för automatisering | Ingår | Exempel:<br> ・ Amazon CloudFront<br> ・ Apache Http Client<br> ・ asynkron HTTP-klient <br> ・ Axios<br> ・ Azureus<br> ・ Curl<br> ・ GitHub Node Fetch<br> dina 7-livegel Guzzle<br> avslutad Go-http-client<br> åhHeadless Chrome{13Client Java™ Client<br> 11} bådadera Jersey <br> bådautomatiseringsnod <br> avslutaokhttp<br> båge som begär <br> bådadera Netty<br> avslutad Wget<br> avslutad WinHTTP <br> avslutad HTTP <br> avslutad GitHub Node Fetch <br> bågreaktornätverk<br> |
| Verktyg för övervakning och hälsokontroll | Ingår | Konfigureras av kunden för att övervaka en viss aspekt av webbplatsen. Exempel: tillgänglighet eller verkliga användarprestanda. Om de har specifika slutpunkter som `/system/probes/health` som mål för hälsokontroller rekommenderar Adobe att du använder `/system/probes/health`-slutpunkten och inte de faktiska HTML-sidorna från webbplatsen. [Se nedan](#excluded-content-request)<br>Exempel:<br> ・ `Amazon-Route53-Health-Check-Service`<br> ・ EyeMonIT_bot_version_0.1_[(https://eyemonit.com/)](https://eyemonit.com/)<br> ・ Investis-Site24x7<br> ・ Mozilla/5.0+(compatible; UptimeRobot/2.0; [https://uptimerobot.com/](https://uptimerobot.com/))<br> ・ Thousand Eyes-Dragonfly-x1<br> ・ OmtrBot/1.0<br> ・ WebMon/2.0.0 |
| `<link rel="prefetch">` förfrågningar | Ingår | För att öka hastigheten vid inläsning av nästa sida kan kunderna låta webbläsaren läsa in en uppsättning sidor innan användaren klickar på länken, så att de redan finns i cachen. *Obs! Den här metoden ökar trafiken avsevärt*, beroende på hur många av de här sidorna som har förhämtats. |
| Trafik som blockerar rapportering från Adobe Analytics eller Google Analytics | Ingår | Det är vanligare att besökare på webbplatser har installerat sekretessprogram (annonsblockerare osv.) som påverkar Google Analytics eller Adobe Analytics precision. AEM as a Cloud Service räknar förfrågningar på den första ingångspunkten till den infrastruktur som drivs av Adobe och inte på klientsidan. |

Se även [License Dashboard](/help/implementing/cloud-manager/license-dashboard.md).

### Olika typer av utelämnade innehållsbegäranden {#excluded-content-request}

| Typ av begäran | Innehållsbegäran | Beskrivning |
| --- | --- | --- |
| HTTP-kod 500+ | Exkluderad | Fel som returneras till besökaren när något går fel på AEM as a Cloud Service eller kundens anpassade kod. |
| HTTP-kod 400-499 | Exkluderad | Fel returneras till besökaren när innehållet inte finns (404) eller om det finns andra innehålls- eller förfrågningsrelaterade problem. |
| HTTP-kod 300-399 | Exkluderad | Bra begäranden som antingen kontrollerar om något har ändrats på servern eller omdirigerar begäran till en annan resurs. De innehåller inte själva innehållet och är därför inte fakturerbara. |
| Begäranden som går att /libs/* | Exkluderad | AEM interna JSON-begäranden, till exempel CSRF-token som inte är fakturerbar. |
| Trafik från DDOS-attacker | Exkluderad | DDOS-skydd. AEM identifierar automatiskt vissa av DDOS-attackerna och blockerar dem. DDOS-attacker om de upptäcks är inte fakturerbara. |
| AEM as a Cloud Service New Relic Monitoring | Exkluderad | AEM as a Cloud Service global övervakning. |
| URL för att kunderna ska kunna övervaka sina Cloud Service | Exkluderad | Adobe rekommenderar att du använder URL:en för att övervaka tillgänglighets- eller hälsokontrollen externt.<br><br>`/system/probes/health` |
| AEM as a Cloud Service Pod Warm-up Service | Exkluderad |
| Agent: skyline-service-warmup/1.* |
| Välkända sökmotorer, sociala nätverk och HTTP-bibliotek (taggade med Fastly) | Exkluderad | Välkända tjänster som regelbundet besöker webbplatsen för att uppdatera deras sökindex eller tjänst:<br><br>Exempel:<br> ・ AddSearchBot<br> ・ AhrefsBot<br> ・ Applebot<br> ・ Ask Jeeves Corporate Spider<br> ・ Bingbot<br> ・ BingPreview<br> ・ BLEXBot<br> ‡ BuiltWith<br> pider<br> ;CrawlerKengo<br> avslutning Facebookexternalhit<br> avslutning Google AdsBot<br> avslutning Google AdsBot Mobile<br> avslutad Googlebot<br> avslutad Googlebot Mobile<br> avslutad lspider<br> avslutad LucidWorks<br> avslutning <br> avslutning <br>  avslutande Pinterest<br> `MJ12bot`<br> avslutningsprisBot  avslutad SiteImimprove  avslutad StashBot <br> avslutad StatusCake <br> avslutad YandexBot <br> avslutad Claudebot |
| Uteslut Commerce integrationa frameworkar | Exkluderad | Begäranden som görs till AEM som vidarebefordras till Commerce integrationa frameworken - URL:en börjar med `/api/graphql` - för att undvika dubbelräkning kan de inte faktureras för Cloud Service. |
| Uteslut `manifest.json` | Exkluderad | Manifestet är inte ett API-anrop. Här finns information om hur du installerar webbplatser på en dator eller mobiltelefon. Adobe ska inte räkna JSON-begäran till `/etc.clientlibs/*/manifest.json` |
| Uteslut `favicon.ico` | Exkluderad | Även om det returnerade innehållet inte ska vara HTML eller JSON har vissa scenarier, som SAML-autentiseringsflöden, observerats returnera favoritikoner som HTML. Därför exkluderas favoritikoner uttryckligen från antalet. |
| CDN-proxy till en annan serverdel | Exkluderad | Förfrågningar som dirigeras till andra icke-AEM bakgrunder med hjälp av tekniken [CDN-väljare](/help/implementing/dispatcher/cdn-configuring-traffic.md#origin-selectors) är exkluderade eftersom de inte träffar AEM. |
