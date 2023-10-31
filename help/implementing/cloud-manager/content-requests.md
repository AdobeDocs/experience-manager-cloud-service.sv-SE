---
title: Förstå begäranden om Cloud Service innehåll
description: Om du har köpt innehållsförfrågningslicenser från Adobe kan du ta reda på vilka typer av innehållsförfrågningar som Adobe Experience Cloud som en tjänst mäter och varianterna med en organisations analysrapporteringsverktyg.
exl-id: 3666328a-79a7-4dd7-b952-38bb60f0967d
source-git-commit: 25a4a6b9ae09cb71f50317990af1718db1e14355
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Begäranden om Cloud Service

## Varianter på begäranden om Cloud Service{#content-requests-variances}

Innehållsförfrågningar kan innehålla avvikelser med en organisations analysrapporteringsverktyg som sammanfattas i följande tabell. I allmänhet samlar analysverktyg in data via instrumentering på klientsidan <b>ska inte användas</b> att rapportera om antalet innehållsförfrågningar för en viss webbplats, helt enkelt eftersom de ofta är beroende av att slutanvändarnas samtycke aktiveras, och därför saknas en betydande del av trafiken. Analysverktyg som samlar in data på serversidan i loggfiler, eller CDN-rapporter för kunder som lägger till egna CDN AEM as a Cloud Service, ger bättre antal. Adobe RUM-datatjänsten rekommenderas som alternativ för rapportering av sidvyer och deras associerade prestanda.

| Orsak till avvikelse | Förklaring |
|---|---|
| Användarens samtycke | Analysverktyg som förlitar sig på klientverktyg är ofta beroende av att slutanvändarnas samtycke aktiveras. Detta skulle kunna representera merparten av den trafik som inte spåras. För kunder som vill mäta innehållsförfrågningar på egen hand rekommenderar vi att man använder analysverktyg för att samla in data på serversidan eller CDN-rapporter. |
| Taggar | Alla sidor eller API-anrop som spåras som Adobe Experience Manager (AEM)-innehållsbegäranden kanske inte taggas med Analytics-spårning. |
| Tag Management Rules | Regelinställningar för tagghantering kan resultera i olika datainsamlingskonfigurationer på en sida, vilket resulterar i en kombination av avvikelser med spårning av innehållsbegäran. |
| Bots | Okända botar som inte har föridentifierats och tagits bort av AEM kan orsaka spårningsavvikelser. |
| Rapportsviter | Sidor som ingår i samma AEM och domän kan skicka data till olika rapportsviter i Analytics. |
| Övervaknings- och säkerhetsverktyg från tredje part | Övervaknings- och säkerhetssökningsverktygen kan generera innehållsförfrågningar för AEM som inte spåras i analysrapporter. |
| API-åtkomst | Programmatisk åtkomst till sidor eller till Adobe Experience Manager API:er kan generera innehållsförfrågningar för AEM som inte spåras i Analytics-rapporter. |
| Förhämtningsbegäranden | Om du använder en förhämtningstjänst för att förhandsladda sidor för att öka hastigheten kan det medföra att trafiken för innehållsförfrågningar ökar avsevärt. |
| DOS | Adobe gör sitt yttersta för att automatiskt upptäcka och filtrera bort trafik från DDOS-attacker, men det finns ingen garanti för att alla möjliga DDOS-attacker identifieras |
| Trafikblockerare | Om du använder en spårningsblockerare i en webbläsare kan det hända att vissa begäranden inte spåras. |
| Brandväggar | Brandväggar kan blockera Analytics-spårning. Detta scenario är vanligare med brandväggar. |

Se även [Licensieringspanel](/help/implementing/cloud-manager/license-dashboard.md).

## Förstå begäranden om Cloud Service innehåll {#about-content-request}

Innehållsförfrågningar spåras automatiskt vid kanten av Adobe Experience Manager (AEM) as a Cloud Service, via automatiserad analys av loggfiler som kommer från det AEM as a Cloud Service CDN, där förfrågningar om att returnera HTML (text/html) eller JSON-innehåll (application/json) från CDN isoleras, och baserat på ett antal inkluderings- och exkluderingsregler som anges nedan. En innehållsbegäran sker oberoende av det returnerade innehåll som opereras från CDN-cachen eller går tillbaka till CDN-källan (AEM).

För kunder som lägger sitt eget CDN ovanpå AEM as a Cloud Service resulterar den här spårningen i siffror som inte kan användas för att jämföra med förfrågningar om licensierat innehåll, som måste mätas av kunden i kanten av det yttre CDN.

Det finns regler för att utesluta välkända botar, inklusive välkända tjänster som regelbundet besöker webbplatsen för att uppdatera deras sökindex eller tjänst.

### Olika typer av innehållsförfrågningar{#included-content-requests}

| Typ av begäran | Innehållsbegäran | Beskrivning |
| --- | --- | --- |
| HTTP-kod 100-299 | Ingår | Det här är vanliga förfrågningar som levererar allt eller delar av innehåll. |
| HTTP-bibliotek för automatisering | Ingår | Exempel:<br>・ Amazon CloudFront<br>・ Apache HTTP-klient<br>・ Asynkron HTTP-klient<br>・ Axios<br>・ Azureus<br>・ Rullande<br>・ GitHub-nodhämtning<br>・ Guzzle<br>・ Go-http-client<br>・ Headless Chrome<br>・ Java™ Client<br>・ Jersey<br>・ Node Oembed<br>・ okhttp<br>・ Python-förfrågningar<br>・ Reaktorenhet<br>・ Wget<br>・ WinHTTP |
| Verktyg för övervakning och hälsokontroll | Ingår | Dessa konfigureras av kunden för att övervaka en viss aspekt av webbplatsen. Exempel: tillgänglighet eller verkliga användarprestanda. Använd `/system/probes/health` slutpunkten och inte de faktiska HTML-sidorna från webbplatsen.<br>Exempel:<br>・ Amazon-Route53-Health-Check-Service<br>・ EyeMonIT_bot_version_0.1_[(https://www.eyemon.it/)](https://www.eyemon.it/)<br>・ Investis-Site24x7<br>・ Mozilla/5.0+(compatible; UptimeRobot/2.0; [https://uptimerobot.com/](https://uptimerobot.com/))<br>・ ThousandEyes-Dragonfly-x1<br>・ OmtrBot/1.0<br>・ WebMon/2.0.0 |
| `<link rel="prefetch">` förfrågningar | Ingår | För att öka hastigheten vid inläsning av nästa sida kan kunderna låta webbläsaren läsa in en uppsättning sidor innan användaren klickar på länken, så att de redan finns i cachen. *Obs! Detta ökar trafiken avsevärt*—Beroende på hur många av dessa sidor som har förhämtats. |
| Trafik som blockerar rapportering från Adobe Analytics eller Google Analytics | Ingår | Det är vanligare att besökare på webbplatser har installerat sekretessprogram (annonsblockerare osv.) som påverkar Google Analytics eller Adobe Analytics precision. AEM as a Cloud Service räknar förfrågningar på den första ingångspunkten till den infrastruktur som drivs av Adobe och inte på klientsidan. |

Se även [Licensieringspanel](/help/implementing/cloud-manager/license-dashboard.md).

### Olika typer av utelämnade innehållsbegäranden{#excluded-content-request}

| Typ av begäran | Innehållsbegäran | Beskrivning |
| --- | --- | --- |
| HTTP-kod 500+ | Exkluderad | Fel som returneras till besökaren när något går fel AEM as a Cloud Service eller kundens anpassade kod. |
| HTTP-kod 400-499 | Exkluderad | Fel returneras till besökaren när innehållet inte finns (404) eller om det finns andra innehålls- eller förfrågningsrelaterade problem. |
| HTTP-kod 300-399 | Exkluderad | Det här är bra begäranden som antingen kontrollerar om något har ändrats på servern eller omdirigerar begäran till en annan resurs. De innehåller inte själva innehållet och är därför inte fakturerbara. |
| Begäranden som går att /libs/* | Exkluderad | AEM interna JSON-begäranden, till exempel CSRF-token som inte är fakturerbar. |
| Trafik från DDOS-attacker | Exkluderad | DDOS-skydd. AEM identifierar automatiskt vissa av DDOS-attackerna och blockerar dem. DDOS-attacker om de upptäcks är inte fakturerbara.<br><br>Automatiskt identifierade DOS-typer:<br>・ DDOSBlockedCiphersSHA<br>・ DDOSBlockedPattern<br>・ DDOSSuspiciousRequest |
| AEM as a Cloud Service NewRelic-övervakning | Exkluderad | AEM as a Cloud Service global övervakning. |
| URL för att kunderna ska kunna övervaka sina Cloud Service | Exkluderad | Rekommenderad URL för extern övervakning av tillgängligheten.<br><br>`/system/probes/health` |
| AEM as a Cloud Service Pod Warm-up Service | Exkluderad | Användaragent: skyline-service-warmup/1.* |
| Välkända sökmotorer, sociala nätverk och HTTP-bibliotek (taggade med Fastly) | Exkluderad | Välkända tjänster som regelbundet besöker webbplatsen för att uppdatera sökindexet eller tjänsten:<br><br>Exempel:<br>・ AddSearchBot<br>・ AhrefsBot<br>・ Applebot<br>・ Fråga Jeeves Corporate Spider<br>・ Bingbot<br>・ BingPreview<br>・ BLEXBot<br>・ BuiltWith<br>・ Bytespider<br>・ CrawlerKengo<br>・ Facebook-extern träff<br>・ Google AdsBot<br>・ Google AdsBot Mobile<br>・ Googlebot<br>・ Googlebot Mobile<br>・ lmspider<br>・ LucidWorks<br>・ MJ12bot<br>・ Förenade kungariket<br>・ Pinterest<br>・ SemushBot<br>・ SiteImproved<br>・ StashBot<br>・ StatusCake<br>・ YandexBot |
| Uteslut Commerce integrationa frameworkar | Exkluderad | Detta är begäranden som skickas till AEM som vidarebefordras till Commerce integrationa frameworken - URL:en börjar med `/api/graphql`- för att undvika dubbelräkning kan de inte faktureras för Cloud Service. |
| Exkludera `manifest.json` | Exkluderad | Manifestet är inte ett API-anrop. Här finns information om hur du installerar webbplatser på datorer och mobiltelefoner. Adobe ska inte räkna JSON-begäran till `/etc.clientlibs/*/manifest.json` |
| Exkludera `favicon.ico` | Exkluderad | Även om det returnerade innehållet inte ska vara HTML eller JSON observerar vi att i vissa scenarier, som SAML-autentiseringsflöden, kan favoritikoner returneras eftersom HTML därför uttryckligen utesluts från räkningen. |
