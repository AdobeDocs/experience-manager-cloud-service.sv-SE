---
title: Förstå begäranden om Cloud Service innehåll
description: Om du har köpt innehållsförfrågningslicenser från Adobe kan du ta reda på vilka typer av innehållsförfrågningar som Adobe Experience Cloud som en tjänst mäter och varianterna med en organisations analysrapporteringsverktyg.
exl-id: 3666328a-79a7-4dd7-b952-38bb60f0967d
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f8b058549162b7ae3d57b1a7dd3461f738b75320
workflow-type: tm+mt
source-wordcount: '1269'
ht-degree: 0%

---

# Begäranden om Cloud Service

## Introduktion {#introduction}

Innehållsförfrågningar är förfrågningar som kommer till AEM Sites (inklusive i samband med Edge Delivery Services för AEM Sites) eller något annat kundtillhandahållet cachningssystem (som ett Content Delivery Network) för att leverera innehåll eller data i antingen HTML-format via sidvyer (till exempel sidor och upplevelsefragment) eller JSON-format via API-anrop (i headlessform). Innehållsförfrågningar räknas antingen som en sidvy eller som 5 API-anrop och mäts vid ingången till det första cachningssystem som tar emot en innehållsförfrågan. Vissa HTTP-begäranden inkluderas eller exkluderas för att räkna innehållsbegäranden. En fullständig lista över sådana inkluderade och exkluderade HTTP-begäranden, samt tekniska definitioner av dem, finns i dokumentationen.

## Förstå begäranden om Cloud Service innehåll {#understanding-cloud-service-content-requests}

För kunder som använder det färdiga CDN-numret mäts förfrågningar om Cloud Service via datainsamling på serversidan. Den här samlingen aktiveras via CDN-logganalys. Innehållsförfrågningar samlas automatiskt in på serversidan vid Adobe Experience Manager as a Cloud Service kant via automatisk analys av loggfiler från AEM as a Cloud Service CDN. Detta görs genom att isolera förfrågningarna som returnerar HTML `(text/html)` - eller JSON `(application/json)` -innehåll från CDN och baseras på flera inkluderings- och exkluderingsregler som anges nedan. En innehållsbegäran görs oberoende av det returnerade innehåll som opereras från CDN-cachen eller det innehåll som skickas tillbaka till CDN-källan (AEM avsändare).

<!-- REMOVED AS PER EMAIL REQUEST FROM SHWETA DUA, JULY 30, 2024 TO RICK BROUGH AND ALEXANDRU SARCHIZ   For customers employing their own CDN, client-side collection offers a more precise reflection of interactions, ensuring a reliable measure of website engagement via the [Real Use Monitoring](/help/sites-cloud/administering/real-use-monitoring-for-aem-as-a-cloud-service.md) service. This gives customers advanced insights into their page traffic and performance. While it is beneficial for all customers, it offers a representative reflection of user interactions, ensuring a reliable measure of website engagement by capturing the number of page views from the client side. 

For customers that bring their own CDN on top of AEM as a Cloud Service, server-side reporting results in numbers that cannot be used to compare with the licensed content requests. With the [Real Use Monitoring](/help/sites-cloud/administering/real-use-monitoring-for-aem-as-a-cloud-service.md), Adobe can reflect a reliable measure of website engagement. -->

### Varianter på begäranden om Cloud Service {#content-requests-variances}

Innehållsförfrågningar kan ha avvikelser inom en organisations analysrapporteringsverktyg som sammanfattas i följande tabell. I allmänhet använder *inte* analysverktyg som samlar in data via instrumentering på klientsidan för att rapportera antalet innehållsförfrågningar för en viss plats, helt enkelt eftersom de ofta är beroende av att användarens samtycke aktiveras, vilket innebär att en stor del av trafiken saknas. Analysverktyg som samlar in data på serversidan i loggfiler, eller CDN-rapporter för kunder som lägger till egna CDN ovanpå AEM as a Cloud Service, ger bättre antal.

| Orsak till avvikelse | Förklaring |
|---|---|
| Användarens samtycke | Analysverktyg som förlitar sig på instrumentering på klientsidan är ofta beroende av att användarens samtycke aktiveras. Detta skulle kunna representera merparten av den trafik som inte spåras. För kunder som vill mäta innehållsförfrågningar på egen hand rekommenderar vi att man använder analysverktyg för att samla in data på serversidan eller CDN-rapporter. |
| Taggar | Alla sidor eller API-anrop som spåras som Adobe Experience Manager-innehållsbegäranden kanske inte taggas med Analytics-spårning. |
| Tag Management Rules | Regelinställningar för tagghantering kan resultera i olika datainsamlingskonfigurationer på en sida, vilket resulterar i en kombination av avvikelser med spårning av innehållsbegäran. |
| Bots | Okända botar som inte har föridentifierats och tagits bort av AEM kan orsaka spårningsavvikelser. |
| Rapportsviter | Sidor som ingår i samma AEM och domän kan skicka data till olika rapportsviter i Analytics. |
| Övervaknings- och säkerhetsverktyg från tredje part | Övervaknings- och säkerhetssökningsverktygen kan generera innehållsförfrågningar för AEM som inte spåras i analysrapporter. |
| API-åtkomst | Programmatisk åtkomst till sidor eller till Adobe Experience Manager API:er kan generera innehållsförfrågningar för AEM som inte spåras i Analytics-rapporter. |
| Förhämtningsbegäranden | Om du använder en förhämtningstjänst för att förhandsladda sidor för att öka hastigheten kan det medföra att trafiken för innehållsförfrågningar ökar avsevärt. |
| DOS | Även om Adobe gör försök att automatiskt upptäcka och filtrera bort trafik från DDOS-attacker finns det ingen garanti för att alla möjliga DDOS-attacker identifieras. |
| Trafikblockerare | Om du använder en spårningsblockerare i en webbläsare kan det hända att vissa begäranden inte spåras. |
| Brandväggar | Brandväggar kan blockera Analytics-spårning. Detta scenario är vanligare med brandväggar. |

Se även [License Dashboard](/help/implementing/cloud-manager/license-dashboard.md).

## Samlingsregler på serversidan {#serverside-collection}

Det finns regler för att utesluta välkända botar, inklusive välkända tjänster som regelbundet besöker webbplatsen för att uppdatera deras sökindex eller tjänst.

### Olika typer av innehållsförfrågningar {#included-content-requests}

| Typ av begäran | Innehållsbegäran | Beskrivning |
| --- | --- | --- |
| HTTP-kod 100-299 | Ingår | Det här är vanliga förfrågningar som levererar allt eller delar av innehåll. |
| HTTP-bibliotek för automatisering | Ingår | Exempel:<br> ・ Amazon CloudFront<br> ・ Apache Http Client<br> ・ asynkron Http-klient<br> ・ Axios<br> ・ Azureus<br> ・ Curl<br> ・ GitHub Node Fetch<br> ‡ Guzzle<br> avslutad Go-http-client<br> avslutning minus Chrome<br> avslutad Java™ Klient <br> avslutning Jersey <br> bådadera Node Oembed <br> avslutad http <br> bågförfrågan <br> bågförfrågningar <br> avslutad Wget <br> avslutad WinHTTP |
| Verktyg för övervakning och hälsokontroll | Ingår | Dessa konfigureras av kunden för att övervaka en viss aspekt av webbplatsen. Exempel: tillgänglighet eller verkliga användarprestanda.Om dessa är avsedda för specifika slutpunkter som /system/probes/health för hälsokontroller rekommenderar vi att du använder `/system/probes/health`-slutpunkten och inte de faktiska HTML-sidorna från webbplatsen.[Se nedan](#excluded-content-request)<br>Exempel:<br> ・ Amazon-Route53-Health-Check-Service<br> ・ EyeMonIT_bot_version_0.1_[(https://www.eyemon.it/)](https://www.eyemon.it/)<br> ・ Investis-Site24x7<br> ・ Mozilla/5.0+(compatible; UptimeRobot/2.0; [8} https://uptimerobot.com/](https://uptimerobot.com/))<br> ・ ThousandEyes-Dragonfly-x1<br> ・ OmtrBot/1.0<br> ・ WebMon/2.0.0 |
| `<link rel="prefetch">` förfrågningar | Ingår | För att öka hastigheten vid inläsning av nästa sida kan kunderna låta webbläsaren läsa in en uppsättning sidor innan användaren klickar på länken, så att de redan finns i cachen. *Obs! Detta ökar trafiken avsevärt*, beroende på hur många av dessa sidor som har förhämtats. |
| Trafik som blockerar rapportering från Adobe Analytics eller Google Analytics | Ingår | Det är vanligare att besökare på webbplatser har installerat sekretessprogram (annonsblockerare osv.) som påverkar Google Analytics eller Adobe Analytics precision. AEM as a Cloud Service räknar förfrågningar på den första ingångspunkten till den infrastruktur som drivs av Adobe och inte på klientsidan. |

Se även [License Dashboard](/help/implementing/cloud-manager/license-dashboard.md).

### Olika typer av utelämnade innehållsbegäranden {#excluded-content-request}

| Typ av begäran | Innehållsbegäran | Beskrivning |
| --- | --- | --- |
| HTTP-kod 500+ | Exkluderad | Fel som returneras till besökaren när något går fel på AEM as a Cloud Service eller kundens anpassade kod. |
| HTTP-kod 400-499 | Exkluderad | Fel returneras till besökaren när innehållet inte finns (404) eller om det finns andra innehålls- eller förfrågningsrelaterade problem. |
| HTTP-kod 300-399 | Exkluderad | Det här är bra begäranden som antingen kontrollerar om något har ändrats på servern eller omdirigerar begäran till en annan resurs. De innehåller inte själva innehållet och är därför inte fakturerbara. |
| Begäranden som går att /libs/* | Exkluderad | AEM interna JSON-begäranden, till exempel CSRF-token som inte är fakturerbar. |
| Trafik från DDOS-attacker | Exkluderad | DDOS-skydd. AEM identifierar automatiskt vissa av DDOS-attackerna och blockerar dem. DDOS-attacker om de upptäcks är inte fakturerbara. |
| AEM as a Cloud Service New Relic Monitoring | Exkluderad | AEM as a Cloud Service global övervakning. |
| URL för att kunderna ska kunna övervaka sina Cloud Service | Exkluderad | Vi rekommenderar att du använder URL för att externt övervaka tillgänglighets- eller hälsokontrollen.<br><br>`/system/probes/health` |
| AEM as a Cloud Service Pod Warm-up Service | Exkluderad |
| Agent: skyline-service-warmup/1.* |
| Välkända sökmotorer, sociala nätverk och HTTP-bibliotek (taggade med Fastly) | Exkluderad | Välkända tjänster som regelbundet besöker webbplatsen för att uppdatera deras sökindex eller tjänst:<br><br>Exempel:<br> ・ AddSearchBot<br> ・ AhrefsBot<br> ・ Applebot<br> ・ Ask Jeeves Corporate Spider<br> ・ Bingbot<br> ・ BingPreview<br> ・ BLEXBot<br> ‡ BuiltWith<br> pider<br> ;CrawlerKengo<br> avslutning Facebookexternalhit<br> avslutning Google AdsBot<br> avslutning Google AdsBot Mobile<br> avslutad Googlebot<br> kommande Googlebot Mobile<br> avslutad lspider<br> senare LucidWorks<br> avslutad MJ 12bot<br> avslutning <br> avslutning Pinterest<br> avslutningsprisBot <br> avslutad SiteImprove<br> avslutad StashBot <br> avslutad StatusCake <br> avslutad YandexBot |
| Uteslut Commerce integrationa frameworkar | Exkluderad | Det här är begäranden som skickas till AEM som vidarebefordras till Commerce integrationa frameworken - URL:en börjar med `/api/graphql` - för att undvika dubbelräkning kan de inte faktureras för Cloud Service. |
| Uteslut `manifest.json` | Exkluderad | Manifestet är inte ett API-anrop. Här finns information om hur du installerar webbplatser på datorer och mobiltelefoner. Adobe ska inte räkna JSON-begäran till `/etc.clientlibs/*/manifest.json` |
| Uteslut `favicon.ico` | Exkluderad | Även om det returnerade innehållet inte ska vara HTML eller JSON observerar vi att i vissa scenarier, som SAML-autentiseringsflöden, kan favoritikoner returneras eftersom HTML därför uttryckligen utesluts från räkningen. |
