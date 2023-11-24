---
title: Använda Edge Delivery Services
description: Använda Edge Delivery Services
feature: Edge Delivery Services
exl-id: 41999302-b4c9-4f5a-b659-6e7398a3c4f4
source-git-commit: 5df61db6e0bd24d55ce73290b37ed55f167e0da2
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 1%

---

# Använda Edge Delivery Services {#usingedge}

Med Edge Delivery kan man snabbt skapa utvecklingsmiljöer där man snabbt kan uppdatera och publicera material och nya webbplatser snabbt kan lanseras. Därför kan du arbeta med flera olika innehållskällor på samma webbplats och publiceringen blir smidig och smidig oavsett vilken källa du väljer. Det tar därför bara några sekunder att gå från redigering till att se innehållet live på internet.

## Redigering {#authoring-edge}

Med Edge Delivery är det enkelt, snabbt och flexibelt att skapa. Du kan använda två olika sökvägar för att skapa i kontexten för Edge Delivery Services:

* Dokumentbaserad redigering (t.ex. Microsoft Word eller Google Docs) - [Mer information finns på den här länken](https://www.hlx.live/docs/authoring).
* Page Editor/Universal Editor - Kontakta din Adobe-säljare.

Vid dokumentbaserad redigering kan du arbeta med olika källor som Microsoft Word och Google Docs. Dokument från dessa källor blir sidor på din webbplats. Rubriker, listor, bilder, teckensnittselement och videor kan alla överföras från den ursprungliga källan till webbplatsen. Du kan lägga till metadata för SEO-syften eller använda block för att arbeta med strukturerat innehåll och lägga till funktioner.

## Publicering {#publishing-edge}

Med Edge Delivery är det smidigt att publicera innehåll oavsett innehållskälla. Processen är följande: du använder [sidekick-tillägg](#using-sidekick) för att aktivera publiceringsmekanismen så kommer ditt innehåll att vara tillgängligt live på din webbplats på några sekunder.

## Edge Delivery Services och GitHub {#github-edge}

Edge Delivery utnyttjar GitHub så att kunderna kan hantera och driftsätta kod direkt från sin GitHub-databas. Du kan till exempel skriva innehåll i antingen Google Docs eller Microsoft Word och utveckla webbplatsens funktionalitet med hjälp av CSS och JavaScript i GitHub. Webbplatser skapas automatiskt för var och en av dina grenar, från förhandsgranskning av innehåll till produktion. Alla resurser du lägger in i GitHub-databasen är tillgängliga på din webbplats utan någon byggprocess.

## Använda Sidekick {#using-sidekick}

AEM har ett verktygsfält med sammanhangsberoende alternativ så att du enkelt kan redigera, förhandsgranska och publicera innehåll. Efter [installera](https://www.hlx.live/docs/sidekick-extension) AEM kan användas antingen i projektmiljöer eller när du redigerar innehåll (till exempel i Google Docs). Beroende på miljön finns det flera tillgängliga åtgärder, som: Förhandsgranska, Läs in igen, Redigera och Publicera. Du kan också växla miljöer när du använder sidbrytaren, från förhandsgranskning till produktion och omvänt.

**Publicera**&#x200B;öppnar du sidesparken på en förhandsgranskningssida och använder åtgärden Publicera. När du har klickat på Publicera är den aktuella förhandsvisningsversionen av sidan tillgänglig i lever- och produktionsmiljöer.

## Integrera AEM Assets med dokumentbaserad framtagning {#integrate-assets-edge}

Med Edge Delivery kan du använda bilder som finns i AEM Assets-arkiv när du redigerar dokument i Microsoft Word eller Google Docs.

Alternativen för att använda bilder i dina dokument är bara tillgängliga efter [konfigurera AEM Assets-plugin-programmet för sidspark](https://www.hlx.live/developer/configuring-aem-assets-sidekick-plugin).

Sidsparkpluginen för AEM Assets ger åtkomst till:

* AEM Assets as a Cloud Service

* AEM Assets Essentials

När du har konfigurerat AEM Assets-plugin-programmet för sidspark kan du [börja använda bilder i dina Google Docs- eller Microsoft Word-dokument](https://www.hlx.live/docs/aem-assets-sidekick-plugin).

## Ytterligare läsning {#further-reading}

Mer information finns på följande sidor:

* Mer information om hur du kommer igång med Edge Delivery finns i [Bygge](https://www.hlx.live/docs/#build) i leveransdokumentationen för Edge.
* Om du vill veta hur du redigerar och publicerar innehåll med hjälp av Edge Delivery kan du läsa [Publiceringsavsnitt](https://www.hlx.live/docs/authoring).
* Mer information om hur du använder filnamnstillägget för sidosparkning finns i [Använda sidsparken](https://www.hlx.live/docs/sidekick) sida.
* AEM finns i [Sidan Authoring Concepts](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/getting-started/concepts.html)
