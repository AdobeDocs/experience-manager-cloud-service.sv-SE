---
title: Översikt över Edge Delivery Services
description: Lär dig hur AEM as a Cloud Service kan dra nytta av de prestanda och den perfekta poängsättningen i Lighthouse som Edge Delivery Services erbjuder.
feature: Edge Delivery Services
exl-id: 03a1aa93-d2e6-4175-9cf3-c7ae25c0d24e
role: Admin, Architect, Developer
source-git-commit: 7ad9a959592f1e8cebbcad9a67d280d5b2119866
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 3%

---


# Översikt över Edge Delivery Services {#edge-delivery-services}

Med Edge Delivery Services levererar AEM exceptionella upplevelser som skapar engagemang och konverteringar. AEM gör det genom att leverera slagkraftiga upplevelser som är snabba att skapa och utveckla. Det är en sammanslagen uppsättning tjänster som möjliggör en snabb utvecklingsmiljö där författare snabbt kan uppdatera och publicera och nya webbplatser snabbt lanseras. Med Edge Delivery Services kan du öka konverteringsgraden, minska kostnaderna och skapa extrem innehållshastighet.

Med Edge Delivery Services kan du

* Skapa snabba sajter med perfekt Lightroom Score och övervaka webbplatsens prestanda kontinuerligt med hjälp av RUM (Real Use Monitoring).
* Öka redigeringseffektiviteten genom att frikoppla innehållskällor. Nu kan du använda både WYSIWYG- och dokumentbaserad redigering. På så sätt kan du arbeta med flera innehållskällor på samma webbplats.
* Använd ett inbyggt experimentramverk som gör det möjligt att snabbt skapa tester, exekvera utan prestandapåverkan och snabbt släppa till en testvinnares produktion.

## Ökning {#overview}

Edge Delivery Services är en sammanslagen uppsättning tjänster som ger stor flexibilitet när det gäller hur du skapar innehåll på din webbplats. Du kan använda både [AEM innehållshantering](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/getting-started/concepts.html) och WYSIWYG-redigering med den [universella redigeraren](/help/sites-cloud/authoring/universal-editor/authoring.md) samt [dokumentbaserad redigering.](https://www.aem.live/docs/authoring)

Följande diagram visar hur du kan redigera innehåll i Microsoft Word (dokumentbaserad redigering) och publicera till Edge Delivery Services. Här visas även WYSIWYG-redigering med den universella redigeraren.

![Edge Delivery-arkitektur](assets/AEM-with-EDS-publishing-simple2.png)

Du kan använda innehåll direkt från Microsoft Word eller Google Docs så att dessa källor blir sidor på din webbplats. Dessutom kan rubriker, listor, bilder och teckensnittselement överföras från den ursprungliga källan till webbplatsen. Det nya innehållet läggs till omedelbart utan någon omgenereringsprocess.

Edge Delivery Services använder GitHub så att du kan hantera och distribuera kod direkt från din GitHub-databas. Du kan t.ex. skriva innehåll i antingen Google Docs eller Microsoft Word och du kan utveckla webbplatsens funktionalitet med hjälp av CSS och JavaScript i GitHub. När du är klar använder du webbläsartillägget Sidekick för att förhandsgranska och publicera innehållsuppdateringar.

Läs mer i Edge Delivery Servicens dokumentation:

* Mer information om hur du kommer igång med Edge Delivery finns i avsnittet [Skapa.](https://www.aem.live/docs/#build)
* Mer information om hur du redigerar och publicerar innehåll med Edge Delivery finns i avsnittet [Publish.](https://www.aem.live/docs/authoring)
* Mer information om hur du startar webbprojekt finns i avsnittet [Starta.](https://www.aem.live/docs/#launch)

## Edge Delivery Services och andra Adobe Experience Cloud-produkter {#edge-other-products}

Edge Delivery Services är en del av Adobe Experience Manager och som sådana Edge Delivery Services och AEM kan de finnas samtidigt på samma domän, vilket är ett vanligt användningsfall för större webbplatser. Dessutom kan innehåll från Edge Delivery Services enkelt användas på AEM Sites-sidor och vice versa.

Läs [Utvecklarhandboken Komma igång för WYSIWYG med Edge Delivery Services](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md) om du vill veta hur du startar ett eget projekt som du kan skapa med AEM och Edge Delivery Services.

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

Om ett produktproblem kräver ytterligare utredning och felsökning och måste uppfylla svars-SLT:er, kan du skicka en supportanmälan som följer den här processen med Admin Console:

1. [Efter standardsupportprocessen ](https://experienceleague.adobe.com/?support-tab=home#support) och skapar en biljett.
1. Lägg till **Edge Delivery** i biljettens titel.
1. I beskrivningen anger du följande information förutom problembeskrivningen:

   * Den publicerade webbplatsens URL. Till exempel: `www.mydomain.com`.
   * URL för den ursprungliga webbplatsen (`.hlx` URL).

## What&#39;s Next {#whats-next}

Kom igång genom att granska [Använda Edge Delivery Services.](/help/edge/using.md)
