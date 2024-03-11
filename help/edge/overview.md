---
title: Komma igång med AEM och Edge Delivery Services
description: Lär dig hur AEM as a Cloud Service kan dra nytta av de prestanda och den perfekta poängsättningen i Lighthouse som Edge Delivery Services erbjuder.
feature: Edge Delivery Services
exl-id: 03a1aa93-d2e6-4175-9cf3-c7ae25c0d24e
source-git-commit: d91254b52c257a3758da200a2c74b736ca457884
workflow-type: tm+mt
source-wordcount: '874'
ht-degree: 2%

---


# Komma igång med AEM och Edge Delivery Services {#aem-edge}

Med Edge Delivery Services levererar AEM exceptionella upplevelser som skapar engagemang och konverteringar. AEM gör det genom att leverera slagkraftiga upplevelser som är snabba att skapa och utveckla. Det är en sammanslagen uppsättning tjänster som möjliggör en snabb utvecklingsmiljö där författare snabbt kan uppdatera och publicera och nya webbplatser snabbt lanseras. Med Edge Delivery Services kan du öka konverteringsgraden, minska kostnaderna och skapa extrem innehållshastighet.

Med Edge Delivery Services kan du

* Skapa snabba sajter med perfekt Lightroom Score och övervaka webbplatsens prestanda kontinuerligt med hjälp av RUM (Real User Monitoring).
* Öka redigeringseffektiviteten genom att frikoppla innehållskällor. När du är klar kan du använda både AEM och dokumentbaserad redigering. På så sätt kan du arbeta med flera innehållskällor på samma webbplats.
* Använd ett inbyggt experimentramverk som gör det möjligt att snabbt skapa tester, exekvera utan prestandapåverkan och snabbt släppa till en testvinnares produktion.

## Översikt över Edge Delivery Services {#edge-overview}

Följande diagram visar hur du kan redigera innehåll i Microsoft Word (dokumentbaserad redigering) och publicera till Edge Delivery Services. Den visar också den AEM publiceringsmetoden med Universal Editor.

![Edge Delivery Architecture](assets/AEM-with-EDS-publishing-simple2.png)

Edge Delivery Services är en sammansatt uppsättning tjänster som ger stor flexibilitet när det gäller hur du skapar innehåll på din webbplats. Som tidigare nämnts kan du använda båda [AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/getting-started/concepts.html) med [Redigering i Universal Editor](/help/implementing/universal-editor/introduction.md) och [Dokumentbaserad redigering.](https://www.aem.live/docs/authoring)

Du kan till exempel använda innehåll direkt från Microsoft Word eller Google Docs. Det innebär att dokument från dessa källor kan bli sidor på din webbplats. Dessutom kan rubriker, listor, bilder och teckensnittselement överföras från den ursprungliga källan till webbplatsen. Det nya innehållet läggs till omedelbart utan någon omgenereringsprocess.

Edge Delivery Services använder GitHub så att kunder kan hantera och driftsätta kod direkt från sina GitHub-databaser. Du kan t.ex. skriva innehåll i antingen Google Docs eller Microsoft Word och du kan utveckla webbplatsens funktionalitet med hjälp av CSS och JavaScript i GitHub. När du är klar kan du använda webbläsartillägget Sidekick för att förhandsgranska och publicera innehållsuppdateringar.

Läs mer i Edge Delivery Servicens dokumentation:

* Mer information om hur du kommer igång med Edge Delivery finns i [Build-sektionen.](https://www.aem.live/docs/#build)
* Om du vill veta hur du redigerar och publicerar innehåll med hjälp av Edge Delivery kan du läsa [Publicera.](https://www.aem.live/docs/authoring)
* Information om hur du startar webbprojekt på rätt sätt finns i [Startsektion.](https://www.aem.live/docs/#launch)

## Edge Delivery Services och andra Adobe Experience Cloud-produkter {#edge-other-products}

Edge Delivery Services är en del av Adobe Experience Manager och som sådana Edge Delivery Services och AEM kan finnas samtidigt i samma domän. Detta är ett vanligt användningsexempel för större webbplatser. Dessutom kan innehåll från Edge Delivery Services enkelt användas på AEM Sites-sidor och omvänt.

Se [Guiden Komma igång för utvecklare för AEM med Edge Delivery Services](/help/edge/edge-dev-getting-started.md) om du vill lära dig hur du påbörjar ett eget projekt att skapa med AEM och Edge Delivery Services.

Du kan också använda Edge Delivery Services med Adobe Target, Analytics och Launch.

## Få åtkomst till Edge Delivery Services {#getting-access}

Det är enkelt att komma igång med Edge Delivery Services. Kom igång genom att följa [Komma igång - självstudiekurs för utvecklare.](https://www.aem.live/developer/tutorial)

## Få hjälp från Adobe {#adobe-gethelp}

Du kan kontakta Adobe produktteam via den tilldelade produktsamarbetskanalen (se nedan för mer information) för att få svar på frågor om produktanvändning eller bästa praxis. Det finns inga servicenivåmål (SLT) kopplade till konversationerna via produktsamarbetskanalen. Om ett produktproblem kräver ytterligare utredning och felsökning, och måste uppfylla SLT-svarsalternativ, kan du skicka ett supportärende efter [supportprocessen.](https://experienceleague.adobe.com/?support-tab=home#support)

Adobe har tre kanaler som kan hjälpa dig med Edge Delivery Services:

* Engagera med communityresurser för allmänna frågor
* Gå till produktsamarbetskanalen för specifika frågor
* Logga en supportanmälan för att lösa viktiga och kritiska problem

### Använd communityresurser {#community-resource}

Adobe vill ge dig bästa möjliga engagemang och stöd för Edge Delivery Services och dokumentbaserad redigering.

* Delta i [Experience League Community](https://adobe.ly/3Q6kTKl) ställa frågor, dela med dig av feedback, inleda diskussioner, söka hjälp av experter och AEM rådgivare/grupper från Adobe samt få kontakt med likasinnade individer i realtid.
* Gå med i vår [Discord channel,](https://discord.gg/aem-live) en mer tillfällig plattform för interaktion i realtid och snabbt idéutbyte.

### Så här kommer du åt din produktsamarbetskanal {#collab-channel}

Med tanke på värdet av direktkommunikationskanalen med kunder kommer alla AEM vid lanseringen att skapa en Slack-kanal för snabbhet, viktiga uppdateringar och skalad rapportering om upplevelsekvalitet. Du får en inbjudan från Adobe om att gå med i en Slack-kanal som är specifik för din organisation.

Mer information finns i [Använda Slack Bot](https://www.aem.live/docs/slack) för mer information.

### Logga en supportanmälan {#support-ticket}

Steg för att logga en supportanmälan via Admin Console:

1. [Efter standardsupportprocessen](https://experienceleague.adobe.com/?support-tab=home#support) skapa en biljett.
1. Lägg till **Edge Delivery** i biljettens titel.
1. Ange följande information i beskrivningen:

   * Den publicerade webbplatsens URL. Till exempel: `www.mydomain.com`.
   * URL för den ursprungliga webbplatsen (`.hlx` URL).

## What&#39;s Next {#whats-next}

Kom igång genom att granska [Använda Edge Delivery Services](/help/edge/using.md).
