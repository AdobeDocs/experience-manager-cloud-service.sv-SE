---
title: Översikt över Edge Delivery Services
description: Lär dig hur AEM as a Cloud Service kan dra nytta av de prestanda och den perfekta poängsättningen i Lighthouse som Edge Delivery Services erbjuder.
feature: Edge Delivery Services
exl-id: 03a1aa93-d2e6-4175-9cf3-c7ae25c0d24e
role: Admin, Architect, Developer
source-git-commit: fa50e661d05a5083be3605a8c6e26450357f4aec
workflow-type: tm+mt
source-wordcount: '1425'
ht-degree: 1%

---


# Översikt över Edge Delivery Services {#edge-delivery-services}

Med Edge Delivery Services levererar AEM exceptionella upplevelser som skapar engagemang och konverteringar. AEM gör det genom att leverera slagkraftiga upplevelser som är snabba att skapa och utveckla. Det är en sammanslagen uppsättning tjänster som möjliggör en snabb utvecklingsmiljö där författare snabbt kan uppdatera och publicera och nya webbplatser snabbt lanseras. Med Edge Delivery Services kan du öka konverteringsgraden, minska kostnaderna och skapa extrem innehållshastighet.

Med Edge Delivery Services kan du

* Skapa snabba sajter med perfekt Lightroom Score och övervaka webbplatsens prestanda kontinuerligt med hjälp av RUM (Real Use Monitoring).
* Öka redigeringseffektiviteten genom att frikoppla innehållskällor. Nu kan du använda både WYSIWYG och dokumentbaserad redigering. På så sätt kan du arbeta med flera innehållskällor på samma webbplats.
* Använd ett inbyggt experimentramverk som gör det möjligt att snabbt skapa tester, exekvera utan prestandapåverkan och snabbt släppa till en testvinnares produktion.

## Flexibel reaktion på affärsbehov {#agile-reaction}

Som sedan länge känd branschledare vet Adobe hur viktigt det är att snabbt kunna skapa och publicera nytt, meningsfullt innehåll för era kunder. Marknaden har klargjort vanliga utmaningar när det gäller att skapa innehåll:

1. **Efterfrågan på innehåll fortsätter att öka.**
   * Man måste låsa upp nya skribenter för att uppfylla detta krav.
   * Processen för att skapa innehåll måste kunna skalas effektivt i hela verksamheten.
   * Författare måste kunna reagera snabbt på förändrade trender.
1. **Det finns ett behov av flerkanalsinnehåll.**
   * Layoutkontroll krävs oavsett hur materialet levereras.
   * Författare måste kunna ändra innehållslayouten direkt.
1. **Trycket ökar för att öka avkastningen på innehållet.**
   * Man måste kunna optimera innehållet.

Dessa trender har visat sig vara enhetliga i hela branschen. Oftast varierar dock de individuella kraven från projekt till projekt. Målet med alla Edge Delivery Services är att hitta den lösning som fungerar för era användare.

1. **Fokusera på värde i stället för på funktioner.** - Bestäm det optimerade arbetsflödet för dina författare i stället för att gå vilse i AEM omfattande funktionsuppsättning.
1. **Dra nytta av AEM flexibilitet.** - AEM funktioner behöver inte användas i ett vakuum. Använd de funktioner du behöver per användningstillfälle.
1. **Utnyttja dina kunskaper.** - Låt upphovspersonerna i projektet delta från början för att säkerställa att ni levererar det värde de behöver genom att implementera de funktioner som är begripliga.

Genom att fokusera på värdet för era författare kan era Edge Delivery Services uppfylla de moderna branschkrav som kreatörerna ställs inför och snabbt kunna leverera innehåll till kunderna.

## Flexibla redigeringsverktyg för kreatörer {#overview}

Edge Delivery Services är en sammanslagen uppsättning tjänster som ger stor flexibilitet när det gäller hur du skapar innehåll på din webbplats. Du kan använda både [AEM innehållshantering](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/getting-started/concepts.html) och WYSIWYG-redigering med [den universella redigeraren](/help/sites-cloud/authoring/universal-editor/authoring.md) samt [dokumentbaserad redigering.](https://www.aem.live/docs/authoring)

Följande diagram visar hur du kan redigera innehåll i Microsoft Word (dokumentbaserad redigering) och publicera till Edge Delivery Services. Här visas även WYSIWYG redigering med Universal Editor.

![Edge Delivery-arkitektur](assets/AEM-with-EDS-publishing-simple2.png)

Edge Delivery Services använder GitHub så att du kan hantera och distribuera kod direkt från din GitHub-databas. Nytt innehåll läggs till direkt utan någon omgenereringsprocess.

### Dokumentbaserad redigering {#document-based}

Med dokumentbaserad redigering kan du använda innehåll direkt från Microsoft Word eller Google Docs så att dessa blir sidor på din webbplats. Rubriker, listor, bilder och teckensnittselement kan alla överföras från den ursprungliga källan till webbplatsen.

* Med dokumentbaserad redigering kan alla marknadsförare snabbt skapa innehåll med hjälp av kända redigeringsverktyg (Microsoft Word, Google Docs osv.).
* Det går smidigare att skapa innehåll genom att det går att skapa, granska och publicera direkt i källdokumenten.
* Eftersom kända verktyg används krävs ingen introduktion för innehållsförfattare, vilket ökar innehållets hastighet.
* Du kan utveckla webbplatsens funktionalitet med hjälp av CSS och JavaScript i GitHub.

![Dokumentbaserad redigering](assets/document-based-authoring.png)

Läs mer i den dokumentbaserade redigeringsdokumentationen:

* Mer information om hur du kommer igång med Edge Delivery finns i avsnittet [Skapa.](https://www.aem.live/docs/#build)
* Mer information om hur du redigerar och publicerar innehåll med Edge Delivery finns i avsnittet [Publish.](https://www.aem.live/docs/authoring)
* Mer information om hur du startar webbprojekt finns i avsnittet [Starta.](https://www.aem.live/docs/#launch)

### WYSIWYG Authoring {#wysiwyg-authoring}

Framtagning av material för just dig (WYSIWYG) använder den universella redigeraren, en anpassningsbar och lättanvänd plats där du kan redigera innehåll live och i sitt sammanhang med en visuell förhandsgranskning.

* Med WYSIWYG kan du effektivisera redaktionen, oavsett om du är headless eller headful.
* Ni kan dra nytta av AEM omfattande innehållshanteringsfunktioner som arbetsflöde och styrning.
* Utnyttja ett stort antal tilläggspunkter för att stödja era egna processer och integreringar.
* Du kan utveckla webbplatsens funktionalitet med hjälp av CSS och JavaScript i GitHub.

![WYSIWYG-redigering](assets/wysiwyg-authoring.png)

Läs mer i WYSIWYG dokumentation:

* En översikt över Universal Editor och WYSIWYG-redigering finns i dokumentet [WYSIWYG Content Authoring for Edge Delivery Services.](/help/edge/wysiwyg-authoring/authoring.md)
* En utvecklaröversikt finns i dokumentet [Utvecklarhandbok för att komma igång med WYSIWYG-redigering med Edge Delivery Services.](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md)

### Bestäm din redigeringsmetod {#authoring-method}

AEM flexibilitet säkerställer att alla redigeringsbehov täcks. Adobe kan hjälpa dig att avgöra vilken metod (eller vilka metoder) som bäst passar dina behov.

* Involvera alltid innehållsförfattarna i beslutet.
* Flera redigeringsmetoder kan implementeras.
* Du kan alltid ändra redigeringsmetod efter hand.
* Du får inte bestämma dig före implementeringen, utan som en del av implementeringen.

Mer information finns i dokumentet [Välja en redigeringsmetod](authoring-methods.md).

## Edge Delivery Services och andra Adobe Experience Cloud-produkter {#edge-other-products}

Edge Delivery Services är en del av Adobe Experience Manager och som sådana Edge Delivery Services och AEM kan de finnas samtidigt på samma domän, vilket är ett vanligt användningsfall för större webbplatser. Dessutom kan innehåll från Edge Delivery Services enkelt användas på AEM Sites-sidor och vice versa.

Se [Utvecklarhandboken Komma igång för WYSIWYG med Edge Delivery Services](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md) för att lära dig hur du startar ett eget projekt som du kan skapa med AEM och Edge Delivery Services.

Du kan också använda Edge Delivery Services med [Adobe Target,](https://www.aem.live/developer/target-integration) [Real Use Monitoring (RUM)](https://www.aem.live/developer/rum) för att diagnostisera användning och prestanda för dina webbplatser och [Launch.](https://experienceleague.adobe.com/en/docs/experience-platform/tags/home)

## Kom igång med Edge Delivery Services {#getting-started}

Det är enkelt att komma igång med Edge Delivery Services genom att följa självstudiekursen [Komma igång - Utvecklare.](https://www.aem.live/developer/tutorial)

## Få hjälp från Adobe {#getting-help}

Adobe har tre kanaler som kan hjälpa dig med Edge Delivery Services:

* Engagera med [communityresurser](#community-resources) för allmänna frågor.
* Gå till din [produktsamarbetskanal](#collaboration-channel) om du vill ha specifika frågor.
* [Logga en supportanmälan](#support-ticket) för att lösa viktiga och allvarliga problem.

### Använd communityresurser {#community-resources}

Adobe vill ge er bästa möjliga engagemang och stöd för Edge Delivery Services, WYSIWYG och dokumentbaserad framtagning.

* Delta i [Experience League Community](https://adobe.ly/3Q6kTKl) om du vill ställa frågor, dela med dig av feedback, starta diskussioner, söka hjälp av experter från Adobe och AEM rådgivare/grupper samt få kontakt med likasinnade individer i realtid.
* Gå med i vår [Discord-kanal,](https://discord.gg/aem-live) är en mer tillfällig plattform för realtidsinteraktioner och snabb idéutbyte.

### Så här kommer du åt din Collaboration-kanal {#collaboration-channel}

Med tanke på värdet av direktkommunikationskanalen med användare kommer alla AEM vid lanseringen att skapa en Slack-kanal för hastighet, viktiga uppdateringar och skalad rapportering om upplevelsekvalitet. Du får en inbjudan från Adobe om att gå med i en Slack-kanal som är specifik för din organisation.

Mer information finns i dokumentet [Använda Slack-roboten](https://www.aem.live/docs/slack) för mer information.

Ni kan kontakta Adobe produktteam via er tilldelade produktsamarbetskanal för att få svar på frågor om produktanvändning eller bästa praxis. Det finns inga servicenivåmål (SLT) kopplade till konversationerna via produktsamarbetskanalen.

### Logga en supportanmälan {#support-ticket}

Om ett produktproblem kräver ytterligare utredning och felsökning och måste uppfylla SLT-svarsalternativ kan du skicka in en supportanmälan.

För att kunna logga in på en supportanmälan måste du först registrera din Edge Delivery-webbplats i Cloud Manager. Du rekommenderas att registrera din webbplats hos Cloud Manager för alla AEM as a Cloud Service-användare och [ger ett antal fördelar.](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md) Se [Cloud Manager-dokumentationen](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md) för mer information om du inte redan har registrerat din webbplats.

När webbplatsen har registrerats hos Cloud Manager följer du den här processen med Admin Console för att skicka in en supportanmälan:

1. [Efter standardsupportprocessen ](https://experienceleague.adobe.com/?support-tab=home#support) och skapar en biljett.
1. Lägg till **Edge Delivery** i biljettens titel.
1. I beskrivningen anger du följande information förutom problembeskrivningen:

   * Den publicerade webbplatsens URL. Till exempel: `www.mydomain.com`.
   * URL för den ursprungliga webbplatsen (`.hlx` URL).

## What&#39;s Next {#whats-next}

Kom igång genom att granska [Använda Edge Delivery Services.](/help/edge/using.md)
