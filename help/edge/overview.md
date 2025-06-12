---
title: Edge Delivery Services - översikt
description: Lär dig hur AEM as a Cloud Service kan dra nytta av de prestanda och den perfekta poängsättningen i Lighthouse som Edge Delivery Services erbjuder.
feature: Edge Delivery Services
exl-id: 03a1aa93-d2e6-4175-9cf3-c7ae25c0d24e
role: Admin, Architect, Developer
source-git-commit: ad9592c705c7b26292a29b43997edadfa01ccb65
workflow-type: tm+mt
source-wordcount: '1321'
ht-degree: 1%

---


# Edge Delivery Services - översikt {#edge-delivery-services}

Med Edge Delivery Services levererar AEM exceptionella upplevelser som skapar engagemang och konverteringar. AEM gör det genom att leverera slagkraftiga upplevelser som är snabba att skapa och utveckla. Det är en sammanslagen uppsättning tjänster som möjliggör en snabb utvecklingsmiljö där författare snabbt kan uppdatera och publicera och nya webbplatser snabbt lanseras. Med Edge Delivery Services kan du öka konverteringsgraden, minska kostnaderna och skapa extremt snabbt innehåll.

Med Edge Delivery Services kan man

* Skapa snabba sajter med en perfekt Lightroom Score och övervaka kontinuerligt sajtens prestanda med Operational Telemetry.
* Öka redigeringseffektiviteten genom att frikoppla innehållskällor. Nu kan du använda både AEM-redigering med den universella redigeraren och dokumentbaserad redigering. På så sätt kan du arbeta med flera innehållskällor på samma webbplats.
* Använd ett inbyggt experimentramverk som gör det möjligt att snabbt skapa tester, exekvera utan prestandapåverkan och snabbt släppa till en testvinnares produktion.

>[!TIP]
>
>**Vill du prova på saker direkt?**
>
>Om du vill komma igång direkt kan du påbörja ditt eget Edge Delivery Services-projekt med AEM-redigering på mindre än 30 minuter genom att [checka ut självstudiekursen på aem.live.](https://www.aem.live/developer/ue-tutorial)

## Flexibel reaktion på affärsbehov {#agile-reaction}

Adobe är sedan länge en känd branschledare och vet hur viktigt det är att snabbt kunna skapa och publicera nytt, meningsfullt innehåll för era kunder. Marknaden har klargjort vanliga utmaningar när det gäller att skapa innehåll:

1. **Efterfrågan på innehåll fortsätter att öka.**
   * Man måste låsa upp nya skribenter för att uppfylla detta krav.
   * Processen för att skapa innehåll måste kunna skalas effektivt i hela verksamheten.
   * Författare måste kunna reagera snabbt på förändrade trender.
1. **Det finns ett behov av flerkanalsinnehåll.**
   * Layoutkontroll krävs oavsett hur materialet levereras.
   * Författare måste kunna ändra innehållslayouten direkt.
1. **Trycket ökar för att öka avkastningen på innehållet.**
   * Man måste kunna optimera innehållet.

Dessa trender har visat sig vara enhetliga i hela branschen. De individuella kraven varierar dock oundvikligen mellan olika projekt. Målet med alla Edge Delivery Services-projekt är att fokusera på att hitta den lösning som fungerar för era användare.

1. **Fokusera på värde i stället för på funktioner.** - Bestäm det optimerade arbetsflödet för dina författare i stället för att gå vilse i AEM omfattande funktionsuppsättning.
1. **Utnyttja AEM flexibilitet.** - AEM-funktioner behöver inte användas i ett vakuum. Använd de funktioner du behöver per användningstillfälle.
1. **Utnyttja dina kunskaper.** - Låt upphovspersonerna i projektet delta från början för att säkerställa att ni levererar det värde de behöver genom att implementera de funktioner som är begripliga.

Genom att fokusera på värdet för era författare kan ert Edge Delivery Services-projekt uppfylla de moderna branschkrav som era kreatörer ställs inför och snabbt leverera innehåll till dina kunder.

## Flexibla redigeringsverktyg för kreatörer {#overview}

Edge Delivery Services är en sammansättningsbar uppsättning tjänster som ger stor flexibilitet när det gäller hur du skapar innehåll på din webbplats. Du kan använda både [AEM innehållshantering](/help/sites-cloud/authoring/author-publish.md) och innehållsredigering med den [universella redigeraren](/help/sites-cloud/authoring/universal-editor/authoring.md) samt [dokumentbaserad redigering.](https://www.aem.live/docs/authoring)

I följande diagram visas hur du kan redigera innehåll i Microsoft Word (dokumentbaserad redigering) och publicera till Edge Delivery Services tillsammans med AEM innehållsredigering med den universella redigeraren.

![Edge Delivery-arkitektur](assets/AEM-with-EDS-publishing-simple2.png)

Edge Delivery Services använder GitHub så att du kan hantera och distribuera kod direkt från din GitHub-databas. Nytt innehåll läggs till direkt utan någon omgenereringsprocess.

### AEM Authoring with the Universal Editor{#wysiwyg-authoring}

Universell redigerare är en anpassningsbar plats där du kan redigera innehåll live och i sitt sammanhang med hjälp av en visuell förhandsgranskning.

* Med AEM kan du arbeta effektivare - både utan ramar och utan papper.
* Du kan utnyttja AEM omfattande funktioner för innehållshantering, inklusive arbetsflöde och styrning.
* Utnyttja ett stort antal tilläggspunkter för att stödja era egna processer och integreringar.
* Du kan utveckla webbplatsens funktionalitet med hjälp av CSS och JavaScript i GitHub.

![AEM-redigering med Universal Editor](assets/wysiwyg-authoring.png)

Kom igång med AEM-redigering med Universal Editor och Edge Delivery Services:

* En översikt över AEM-redigering med den universella redigeraren finns i dokumentet [Skapa med AEM för Edge Delivery Services](https://www.aem.live/docs/aem-authoring) i aem.live-dokumentationen.
* En utvecklaröversikt finns i dokumentet [Getting Started - Universal Editor Developer Tutorial](https://www.aem.live/developer/ue-tutorial) i aem.live-dokumentationen.

### Dokumentbaserad redigering {#document-based}

Med dokumentbaserad redigering kan du använda innehåll direkt från Microsoft Word eller Google Docs så att dessa källor blir sidor på din webbplats. Rubriker, listor, bilder och teckensnittselement kan alla överföras från den ursprungliga källan till webbplatsen.

* Med dokumentbaserad redigering kan alla marknadsförare snabbt skapa innehåll med kända redigeringsverktyg (Microsoft Word, Google Docs osv.).
* Det går smidigare att skapa innehåll genom att det går att skapa, granska och publicera direkt i källdokumenten.
* Eftersom kända verktyg används krävs ingen introduktion för innehållsförfattare, vilket ökar innehållets hastighet.
* Du kan utveckla webbplatsens funktionalitet med hjälp av CSS och JavaScript i GitHub.

![Dokumentbaserad redigering](assets/document-based-authoring.png)

Läs mer i den dokumentbaserade redigeringsdokumentationen:

* Mer information om hur du kommer igång med Edge Delivery finns i avsnittet [Build i aem.live-dokumentationen.](https://www.aem.live/docs/#build)
* Mer information om hur du redigerar och publicerar innehåll med Edge Delivery finns i avsnittet [Publicera i dokumentationen för aem.live.](https://www.aem.live/docs/authoring)
* Mer information om hur du startar webbprojekt på rätt sätt finns i avsnittet [Starta i dokumentationen för aem.live](https://www.aem.live/docs/#launch)

### Bestäm din redigeringsmetod {#authoring-method}

AEM flexibilitet säkerställer att alla redigeringsbehov täcks. Adobe kan hjälpa dig att avgöra vilken metod (eller vilka metoder) som bäst passar dina behov.

* Involvera alltid innehållsförfattarna i beslutet.
* Flera redigeringsmetoder kan implementeras.
* Du kan alltid ändra redigeringsmetod efter hand.
* Ni behöver inte fatta beslut före implementeringen, utan snarare som en del av implementeringen.

## Edge Delivery Services och andra Adobe Experience Cloud-produkter {#edge-other-products}

Edge Delivery Services ingår i Adobe Experience Manager. Därför kan Edge Delivery Services och AEM Sites finnas parallellt på samma domän, vilket är ett vanligt användningsexempel för större webbplatser. Dessutom kan dina AEM Sites-sidor enkelt förbruka innehåll från Edge Delivery Services, och det motsatta är också sant.

Läs dokumentet [Komma igång - Universal Editor Developer Tutorial](https://www.aem.live/developer/ue-tutorial) i aem.live-dokumentationen om du vill veta hur du startar ett eget projekt som du kan skapa med AEM och Edge Delivery Services.

Du kan också använda Edge Delivery Services med [Adobe Target](https://www.aem.live/developer/target-integration), [Operational Telemetry](https://www.aem.live/developer/rum) för att diagnostisera användning och prestanda för dina webbplatser och [Launch.](https://experienceleague.adobe.com/sv/docs/experience-platform/tags/home)

## Få hjälp från Adobe {#getting-help}

Adobe har tre kanaler som kan hjälpa dig med Edge Delivery Services:

* Engagera med [communityresurser](#community-resources) för allmänna frågor.
* Gå till din [produktsamarbetskanal](#collaboration-channel) om du vill ha specifika frågor.
* [Logga en supportanmälan](#support-ticket) för att lösa viktiga och allvarliga problem.

### Använd communityresurser {#community-resources}

Adobe ger dig det bästa användarinteraktionen och stödet för Edge Delivery Services, AEM-redigering med den universella redigeraren och dokumentbaserad redigering.

* Delta i [Experience League Community](https://adobe.ly/3Q6kTKl) för att ställa frågor, dela med dig av feedback, starta diskussioner, söka hjälp av Adobe experter och AEM Advisors/Champs samt få kontakt med likasinnade individer i realtid.
* Gå med i [Discord-kanalen](https://discord.gg/aem-live), en mer tillfällig plattform för realtidsinteraktioner och snabbt idéutbyte.

### Så här kommer du åt din Collaboration-kanal {#collaboration-channel}

Med tanke på värdet av direktkommunikationskanalen med användare skapar alla AEM-projekt vid lanseringen en Slack-kanal för snabbhet, viktiga uppdateringar och skalad rapportering om upplevelsekvalitet. Du får en inbjudan från Adobe om att gå med i en Slack-kanal som är specifik för din organisation.

Mer information finns i dokumentet [Använda Slack Bot](https://www.aem.live/docs/slack) för mer information.

Ni kan samarbeta med Adobe produktteam via er tilldelade produktsamarbetskanal för att få svar på frågor om produktanvändning eller bästa praxis. Det finns inga servicenivåmål (SLT) kopplade till konversationerna via produktsamarbetskanalen.

### Logga en supportanmälan {#support-ticket}

{{support-ticket}}
