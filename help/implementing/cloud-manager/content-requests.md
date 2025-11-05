---
title: Förstå Cloud Service Content Requests
description: Om du har köpt innehållsförfrågningslicenser från Adobe kan du ta reda på vilka typer av innehållsförfrågningar som Adobe Experience Cloud som en tjänst mäter och varianterna med en organisations analysrapporteringsverktyg.
exl-id: 3666328a-79a7-4dd7-b952-38bb60f0967d
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 20bb86d83a1afeda760e7c8d88e4257b8cb65860
workflow-type: tm+mt
source-wordcount: '1918'
ht-degree: 0%

---

# Förstå förfrågningar om Cloud Service-innehåll

## Introduktion {#introduction}

Innehållsförfrågningar omfattar förfrågningar som skickas till AEM Sites. Dessa förfrågningar kan skickas via Edge Delivery Services eller kundtillhandahållna cachelagringssystem, t.ex. ett CDN-nätverk (Content Delivery Network). Dessa förfrågningar levererar strukturerade data i HTML- eller JSON-format och supportsidor (till exempel sidor och Experience Fragments) eller JSON-returer via API:er utan rubriker.

Systemet räknar innehållsbegäranden när en användare visar en sida med HTML eller JSON. Den mäter begäran vid den punkt där det första cachesystemet tar emot den. Vissa HTTP-begäranden inkluderas eller exkluderas för att räkna innehållsbegäranden. Se den fullständiga listan över HTTP [inkluderade innehållsförfrågningar](#included-content-requests) och [exkluderade innehållsförfrågningar](#excluded-content-request).

>[!NOTE]
>
>Data som visas i vyn Innehållsförfrågningar uppdateras var 24:e timme.

## Om förfrågningar om Cloud Service-innehåll {#understanding-cloud-service-content-requests}

En *sidförfrågan* refererar till en HTTP-begäran som hämtar kärnstrukturerat innehåll (till exempel HTML eller JSON) som behövs för att återge huvudsidans upplevelse. Det omfattar inte förfrågningar om resurser, t.ex. bilder eller skript.

För kunder som använder det färdiga CDN:et räknar AEM as a Cloud Service med att innehållsförfrågningar ska mätas på serversidans nivå. Detta mått utförs automatiskt och kräver inte uppföljning på klientsidan.

AEM (Adobe Experience Manager) as a Cloud Service identifierar innehållsförfrågningar baserat på de svarstyper som genereras av AEM-instansen och tas emot vid CDN. Mer specifikt räknas förfrågningar som returnerar HTML (`text/html`) eller JSON (`application/json`). Dessa format levererar vanligtvis primärt sidinnehåll för både traditionell webbplatsåtergivning och headless-leverans.

Förfrågningar om statiska resurser som JavaScript-filer, CSS-formatmallar och bilder räknas inte som innehållsförfrågningar.

>[!NOTE]
>Om en API-begäran returnerar HTML eller JSON som fungerar som sidnivåinnehåll (t.ex. vid headless-leverans), kan den ändå räknas som en innehållsbegäran beroende på sammanhanget.

Innehållsbegäranden mäts oavsett om svaret har skickats från CDN-cachen eller vidarebefordrats till den ursprungliga AEM-miljön.

<!-- REMOVED AS PER EMAIL REQUEST FROM SHWETA DUA, JULY 30, 2024 TO RICK BROUGH AND ALEXANDRU SARCHIZ   For customers employing their own CDN, client-side collection offers a more precise reflection of interactions, ensuring a reliable measure of website engagement via the [Real Use Monitoring](/help/sites-cloud/administering/real-use-monitoring-for-aem-as-a-cloud-service.md) service. This gives customers advanced insights into their page traffic and performance. While it is beneficial for all customers, it offers a representative reflection of user interactions, ensuring a reliable measure of website engagement by capturing the number of page views from the client side. 

For customers that bring their own CDN on top of AEM as a Cloud Service, server-side reporting results in numbers that cannot be used to compare with the licensed content requests. With the [Real Use Monitoring](/help/sites-cloud/administering/real-use-monitoring-for-aem-as-a-cloud-service.md), Adobe can reflect a reliable measure of website engagement. -->

### Olika typer av förfrågningar om Cloud Service-innehåll {#content-requests-variances}

Innehållsförfrågningar kan ha avvikelser inom en organisations analysrapporteringsverktyg som sammanfattas i följande tabell. I allmänhet bör du undvika att använda analysverktyg som använder klientutrustning för att rapportera antalet innehållsförfrågningar för en webbplats. Dessa verktyg saknar ofta en stor del av trafiken eftersom de kräver att användaren ger sitt medgivande. Analysverktyg som samlar in data på serversidan i loggfiler, eller CDN-rapporter för kunder som lägger till egna CDN ovanpå AEM as a Cloud Service, ger bättre antal.

| Orsak till avvikelse | Förklaring |
|---|---|
| Användarens samtycke | Analysverktyg som förlitar sig på instrumentering på klientsidan är ofta beroende av att användarens samtycke aktiveras. Det här arbetsflödet kan representera merparten av trafiken som inte spåras. För kunder som vill mäta innehållsförfrågningar på egen hand rekommenderar Adobe att ni använder analysverktyg för att samla in data från rapporter på serversidan eller CDN-rapporter. |
| Taggar | Alla sidor eller API-anrop som spåras som Adobe Experience Manager-innehållsbegäranden kanske inte taggas med Analytics-spårning. |
| Tag Management Rules | Regelinställningar för tagghantering kan resultera i olika datainsamlingskonfigurationer på en sida, vilket resulterar i en kombination av avvikelser med spårning av innehållsbegäran. |
| Bots | Okända fel som AEM inte har identifierat i förväg och tagit bort kan orsaka spårningsdiskrepanser. |
| Rapportsviter | Sidor i samma AEM-instans kan rapportera till olika analysrapportsviter. Den här processen kan dela data över flera sviter, beroende på konfiguration. |
| Övervaknings- och säkerhetsverktyg från tredje part | Övervaknings- och säkerhetssökningsverktygen (till exempel för att kontrollera drifttid eller sårbarhetsläsare) kan begära sidor och generera innehållsförfrågningar på serversidan som inte syns i analysrapporter. |
| API-åtkomst | Begäranden till AEM sidor eller innehåll via API:er (t.ex. via Adobe Experience Manager som Headless CMS) räknas fortfarande som innehållsförfrågningar, men utlöser inte analysspårning. |
| Förhämtningsbegäranden | Förhämtning (till exempel med hjälp av en servicearbetare eller kantfunktion) kan öka trafikvolymer genom att begära sidor i förväg. Dessa begäranden räknas på serversidan men kör inte kod för klientanalys. |
| DOS | Adobe använder filtrering för att upptäcka och blockera många DDoS-attacker. Vissa attackbegäranden kan dock fortfarande räknas som innehållsbegäranden innan filter tillämpas. |
| Trafikblockerare | Sekretessfunktioner i webbläsaren eller brandväggar kan förhindra att analysskript läses in. Dessa användare genererar fortfarande innehållsförfrågningar på serversidan. |
| Brandväggar | Brandväggar för företag eller regioner kan förhindra att analysanrop når Adobe-servrar, vilket kan orsaka underrapportering i analyser medan antalet servrar inte påverkas. |

Se [License Dashboard](/help/implementing/cloud-manager/license-dashboard.md) för information om hur du visar och spårar användningen av innehållsbegäran i förhållande till dina licensbegränsningar.

## Samlingsregler på serversidan {#serverside-collection}

AEM as a Cloud Service tillämpar samlingsregler på serversidan för att räkna innehållsbegäranden. Dessa regler exkluderar välkända botar (t.ex. crawler för sökmotorer) och en uppsättning övervakningstjänster som regelbundet pingar webbplatsen. Annan trafik av syntetisk eller övervakningstyp som inte finns med i den här exkluderingslistan räknas som förfrågningar om fakturerbart innehåll.

I följande tabeller visas typerna av inkluderade och exkluderade innehållsbegäranden, med korta beskrivningar av var och en.

### Olika typer av innehållsförfrågningar {#included-content-requests}

>[!NOTE]
>Om en API-begäran returnerar ett HTML-svar kan den klassificeras som en innehållsbegäran, beroende på dess användarkontext. API-förfrågningar som returnerar data som inte är användargränssnittsdata exkluderas vanligtvis.

| Typ av begäran | Innehållsbegäran | Beskrivning |
| --- | --- | --- |
| HTTP-kod 100-299 | Ingår | Innehåller lyckade begäranden som returnerar helt eller delvis HTML- eller JSON-innehåll.<br>HTTP-kod 206: Dessa begäranden levererar endast en del av det fullständiga innehållet. Till exempel en video eller stor bild. Förfrågningar med delvis innehåll inkluderas när de levererar en del av ett HTML- eller JSON-svar som används vid återgivning av sidinnehåll. |
| HTTP-bibliotek för automatisering | Ingår | Begäranden från verktyg eller bibliotek som hämtar sidinnehåll. Exempel: <br> ・ Amazon CloudFront<br> ・ Apache Http Client<br> ・ asynkron HTTP-klient <br> ・ Axios <br> ・ Azureus<br> ・ Curl<br> ・ GitHub Node Fetch<br> orist Guzzle<br> avslutad Go-http-client<br> avslutning Rubrik minus Chrome<br> avslutad Java™ Client <br> ¹ Jersey <br> bådautomated Node Node Oembed <br> avslutnings-http<br> bågförfrågningar <br> bågslut Netty<br> avslutningsmål <br> WinHTTP <br> avslutnings-HTTP <br> 7 GitHub Node Fetch <br> Netty |
| Verktyg för övervakning och hälsokontroll | Ingår | Begäranden som används för att övervaka sidors hälsa eller tillgänglighet.<br>Se [Typer av begäranden om utelämnat innehåll](#excluded-content-request).<br>Exempel: <br> ・ `Amazon-Route53-Health-Check-Service`<br> ・ EyeMonIT_bot_version_0.1_[(https://eyemonit.com/)](https://eyemonit.com/)<br> ・ Investis-Site24x7<br> ・ Mozilla/5.0+(compatible; UptimeRobot/2.0; [https://uptimerobot.com/](https://uptimerobot.com/))<br> ・ ThousandEyes-yes Dragonfly-x1<br> ・ OmtrBot/1.0<br> ・ WebMon/2.0.0 |
| `<link rel="prefetch">` förfrågningar | Ingår | När kunderna läser in innehåll i förväg eller hämtar innehåll i förväg (till exempel med `<link rel="prefetch">`) räknas dessa förfrågningar på serversidan. Se till att den här metoden kan öka trafiken, beroende på hur många av dessa sidor som är förhämtade. |
| Trafik som blockerar rapportering från Adobe Analytics eller Google Analytics | Ingår | Det är vanligare att besökare på webbplatser har installerat sekretessprogram (Ad-blockers osv.) som påverkar Google Analytics eller Adobe Analytics precision. AEM as a Cloud Service räknar förfrågningar vid den första ingångspunkten till den Adobe-styrda infrastrukturen och inte på klientsidan. |

Se även [License Dashboard](/help/implementing/cloud-manager/license-dashboard.md).

### Olika typer av utelämnade innehållsbegäranden {#excluded-content-request}

| Typ av begäran | Innehållsbegäran | Beskrivning |
| --- | --- | --- |
| HTTP-kod 500+ | Exkluderad | Fel som returneras till besökaren när något går fel på AEM as a Cloud Service eller kundens anpassade kod. |
| HTTP-kod 400-499 | Exkluderad | Fel returneras till besökaren när innehållet inte finns (404) eller om det finns andra innehålls- eller förfrågningsrelaterade problem. |
| HTTP-kod 300-399 | Exkluderad | Bra begäranden som antingen kontrollerar om något har ändrats på servern eller omdirigerar begäran till en annan resurs. De innehåller inte själva innehållet och är därför inte fakturerbara. |
| Begäranden går till `/libs/`* | Exkluderad | AEM interna JSON-begäranden, till exempel CSRF-token som inte är fakturerbar. |
| Trafik från DDOS-attacker | Exkluderad | DDOS-skydd. AEM identifierar några av DDOS-attackerna automatiskt och blockerar dem. DDOS-attacker om de upptäcks är inte fakturerbara. |
| AEM as a Cloud Service New Relic Monitoring | Exkluderad | AEM as a Cloud Service global övervakning. |
| URL till kunder som vill övervaka sina Cloud Service-program | Exkluderad | Adobe rekommenderar att du använder URL:en för att övervaka tillgänglighets- eller hälsokontrollen externt.<br><br>`/system/probes/health` |
| AEM as a Cloud Service Pod Warm-up Service | Exkluderad |
| Agent: skyline-service-warmup/1.* |
| Välkända sökmotorer, sociala nätverk och HTTP-bibliotek (taggade med Fastly) | Exkluderad | Välkända tjänster som regelbundet besöker webbplatsen för att uppdatera deras sökindex eller tjänst:<br><br>Exempel:<br> ・ AddSearchBot<br> ・ AhrefsBot<br> ・ Applebot<br> ・ Ask Jeeves Corporate Spider<br> ・ Bingbot<br> ・ BingPreview<br> ・ BLEXBot<br> ‡ BuiltWith<br> pider<br> ;CrawlerKengo<br> avslutning Facebookexternalhit<br> avslutning Google AdsBot<br> avslutning Google AdsBot Mobile<br> avslutad Googlebot<br> avslutad Googlebot Mobile<br> avslutad lspider<br> avslutad LucidWorks<br> avslutning `MJ12bot`<br> avslutning <br>  avslutande Pinterest<br> <br> avslutningsprisBot  avslutad SiteImimprove  avslutad StashBot <br> avslutad StatusCake <br> avslutad YandexBot <br> pigg ContentKing <br> avslutad Claudebot |
| Uteslut Commerce integration framework-samtal | Exkluderad | Begäranden som skickas till AEM som vidarebefordras till Commerce integration framework - URL:en börjar med `/api/graphql` - för att undvika dubbelräkning kan de inte debiteras för Cloud Service. |
| Uteslut `manifest.json` | Exkluderad | Manifestet är inte ett API-anrop. Här finns information om hur du installerar webbplatser på en dator eller mobiltelefon. Adobe ska inte räkna JSON-begäran till `/etc.clientlibs/*/manifest.json` |
| Uteslut `favicon.ico` | Exkluderad | Även om det returnerade innehållet inte ska vara HTML eller JSON har vissa scenarier, som SAML-autentiseringsflöden, observerats returnera favoritikoner som HTML. Därför exkluderas favoritikoner uttryckligen från antalet. |
| Experience Fragment (XF) - Återanvändning i samma domän | Exkluderad | Begäranden som gjorts för XF-sökvägar (till exempel `/content/experience-fragments/...`) från sidor som finns på samma domän (som identifieras av referensrubriken som matchar begärandevärden).<br><br> Exempel: En hemsida på `aem.customer.com` som drar in en XF-fil för en banderoll eller ett kort från samma domän.<br><br> ・ URL matchar /content/experience-fragments/..<br> ・ referensdomänen matchar `request_x_forwarded_host`<br><br>**Obs!** Om Experience Fragment-sökvägen är anpassad (till exempel med `/XFrags/...` eller någon sökväg utanför `/content/experience-fragments/`), kommer begäran inte att uteslutas och kan räknas, även om den är samma domän. Vi rekommenderar att Adobe standardstruktur för XF-sökväg används för att säkerställa att exkluderingslogiken tillämpas korrekt. |

## Hantera innehållsförfrågningar {#managing-content-requests}

Som vi nämnt i avsnittet [Varianter på Cloud Service-innehållsbegäranden](#content-requests-variances) kan innehållsbegäranden vara högre än förväntat på grund av ett antal orsaker, där en vanlig tråd är trafik som träffar CDN.  Det är till din fördel att som AEM-kund övervaka och hantera era innehållsförfrågningar så att de passar er licensbudget.  Hantering av innehållsbegäranden är vanligtvis en kombination av implementeringstekniker och [trafikfilterregler](/help/security/traffic-filter-rules-including-waf.md).

### Implementeringstekniker som hanterar innehållsförfrågningar {#implementation-techniques-to-manage-crs}

* Kontrollera att alla sidsvar som inte hittas levereras med HTTP-status 404.  Om de returneras med statusen 200 räknas de av mot innehållsförfrågningar.
* Vidarebefordra hälsokontroller eller övervakningsverktyg till URL:en /systems/probes/health eller använd HEAD-metoden i stället för GET för att undvika att det uppstår innehållsförfrågningar.
* Balansera era behov av aktualitet i innehållet med AEM licenskostnader för alla skräddarsydda crawler som ni har integrerat med er webbplats.  En alltför aggressiv crawler kan förbruka många innehållsförfrågningar.
* Hantera eventuella omdirigeringar som server (status 301 eller 302) i stället för på klientsidan (status 200 med javascript-omdirigering) för att undvika två separata innehållsförfrågningar.
* Kombinera eller minska API-anrop, som är JSON-svar från AEM som kan läsas in för att återge sidan.

### Trafikfilterregler för att hantera innehållsförfrågningar {#traffic-filter-rules-to-manage-crs}

* Ett vanligt robotmönster är att använda en tom användaragent.  Du måste granska implementerings- och trafikmönstren för att se om den tomma användaragenten är användbar eller inte.  Om du vill blockera den här trafiken rekommenderas [syntax](/help/security/traffic-filter-rules-including-waf.md#rules-syntax):

```
trafficFilters:
  rules:
    - name: block-missing-user-agent
      when:
        anyOf:
          - { reqHeader: user-agent, exists: false }
          - { reqHeader: user-agent, equals: '' }
      action: block
```

* Somliga botar har slagit en webbplats mycket hårt en dag och försvinner nästa dag.  Detta kan frustrera alla försök att blockera en viss IP-adress eller användaragent.  Ett allmänt tillvägagångssätt är att införa en [avgiftsbegränsningsregel](/help/security/traffic-filter-rules-including-waf.md#rate-limit-rules).  Granska [exemplen](/help/security/traffic-filter-rules-including-waf.md#ratelimiting-examples) och skapa en regel som matchar din tolerans för att få en snabb frekvens av förfrågningar.  Granska syntaxen för [villkorsstruktur](/help/security/traffic-filter-rules-including-waf.md#condition-structure) för eventuella undantag som du vill tillåta för en allmän hastighetsbegränsning.
