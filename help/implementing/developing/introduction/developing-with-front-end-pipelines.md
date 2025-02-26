---
title: Utveckla sajter med frontpipeline
description: Framtidsförloppet ökar utvecklarnas oberoende och snabbar upp utvecklingsprocessen. I den här artikeln beskrivs viktiga aspekter av frontprocessen för att säkerställa optimala prestanda och effektivitet.
exl-id: 996fb39d-1bb1-4dda-a418-77cdf8b307c5
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 635fd7736d26b95acc4389c519edf495694b1a94
workflow-type: tm+mt
source-wordcount: '1126'
ht-degree: 0%

---


# Utveckla webbplatser med den integrerade pipeline som behövs {#developing-site-with-front-end-pipeline}

[front-end-pipeline](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) ger gränssnittsutvecklare större oberoende och snabbar upp utvecklingen avsevärt. I den här artikeln beskrivs hur processen fungerar och viktiga saker som hjälper dig att få ut det mesta av den belyses.

>[!TIP]
>
>Om du ännu inte är bekant med hur du använder frontendspipelinen och dess fördelar kan du läsa guiden [Skapa snabbwebbplats](/help/journey-sites/quick-site/overview.md). Det innehåller ett exempel på hur du snabbt distribuerar en ny webbplats och anpassar dess tema oberoende av serverutvecklingen.

## Förstå processen för pipeline-framtagning och bygge i AEM Cloud Manager {#front-end-build-contract}

Ungefär som i [fullständig stackbyggmiljö](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md) har frontendpipeline en egen miljö. Utvecklarna har viss flexibilitet i den här pipeline-hanteringen, förutsatt att de följer det första byggavtalet.

front-end-pipelinen kräver att front-end-projektet `Node.js` använder skriptdirektivet `build` för att generera det bygge som det distribuerar. Detta krav finns eftersom Cloud Manager använder kommandot `npm run build` för att generera det distribuerbara projektet för front-end-bygget.

Det resulterande innehållet i mappen `dist` är det som distribueras av Cloud Manager, vilket fungerar som statiska filer. Dessa filer lagras externt på AEM, men är tillgängliga via en `/content/...`-URL i den distribuerade miljön.

## Node.js-versioner som stöds {#node-versions}

Klientmiljön stöder följande `Node.js`-versioner:

* 23
* 22
* 20
* 18
* 16
* 14 (standard)
* 12

Du kan använda `NODE_VERSION` [miljövariabeln ](/help/implementing/cloud-manager/environment-variables.md) för att ange önskad version.

## Bästa tillvägagångssätt för att namnge och hantera rörledningar för slutanvändare i AEM {#single-source-of-truth}

Ett bra tillvägagångssätt för AEM är att behålla en enda, tydlig källa till sanning. Cloud Manager har till syfte att förstärka denna princip. Men eftersom frontdelsflödet tillåter att delar av koden frikopplas är det viktigt med rätt konfiguration. Undvik konflikter genom att se till att flera frontendledningar inte distribueras till samma plats i samma miljö.

Därför rekommenderar Adobe att du upprätthåller en systematisk namnkonvention, särskilt när flera rörledningar för framände skapas. Du kan använda följande rekommendationer:

* Namnet på frontmodulen, som definieras av egenskapen `name` för filen `package.json`, ska innehålla namnet på den plats som det gäller för. För en webbplats som finns på `/content/wknd` skulle namnet på frontmodulen till exempel vara `wknd-theme`.
* När en front-end-modul delar samma Git-databas med andra moduler, ska namnet på dess mapp vara lika med, eller innehålla samma namn på, front end-modulen. Om till exempel front end-modulen heter `wknd-theme` skulle namnet på den omslutande mappen vara något som liknar `wknd-theme-sources`.
* Namnet på Cloud Manager front-end-pipeline bör även innehålla namnet på front-end-modulen och även lägga till den miljö som den distribuerar till (produktion eller utveckling). För till exempel frontmodulen `wknd-theme` kan pipeline heta något som `wknd-theme-prod`.

En sådan konvention förhindrar följande misstag vid distribution:

* Använder en frontendmodul på fel plats.
* Skapa flera frontendmoduler som tillämpar samma plats, vilket skulle skriva över varandra.
* Att skapa flera rörledningar för samma källor, vilket skulle kunna orsaka konkurrensförhållanden, utan att garantera ordningen för driftsättningar.

## Koordinera frontend- och backend-utveckling för stabilitet i AEM {#separation-of-concerns}

En viktig bästa metod för varje separat problem är att utforma och hantera kontraktet noggrant och definiera gränserna mellan dem. I den rörliga delen är detta avtal HTML och JSON-utdata från webbplatsen. Genom att bevara stabiliteten i dessa utdata kan du säkerställa att frontend-pipelinen ger maximalt värde så att front-end-teamet kan arbeta oberoende av varandra.

Det finns för närvarande ingen inbyggd funktion för att köra rörledningen i full hög synkront med frontdelsrörledningarna. Därför är det viktigt att noggrant hantera avtalet som definierar deras gränser när man separerar frontend-utvecklingen från den kompletta rörledningen. Kontraktet består vanligtvis av HTML eller JSON, eller båda, som återges av Experience Manager. Alla ändringar av detta avtal bör samordnas noggrant mellan grupper som hanterar olika rörledningar för att säkerställa en smidig övergång och korrekt sekvensering av uppdateringarna.

Följande steg rekommenderas i allmänhet när du ändrar HTML- eller JSON-utdata, särskilt när båda områdena påverkas.

1. Back-end-teamet skapar först en utvecklingsmiljö med nya HTML- eller JSON-utdata.
   1. Med hjälp av den fullständiga pipeline-funktionen distribuerar de koden som krävs för att återge nya HTML- eller JSON-utdata, eller båda, som önskas.
   1. Om det gäller en miljö som front end-teamet inte tidigare hade tillgång till måste följande steg utföras.
      1. URL: Front-end-teamet måste känna till URL:en för den utvecklingsmiljön.
      1. ACL: front-end-teamet måste få en lokal AEM-användare med rättigheter som liknar&quot;Contributors&quot;.
      1. Git: Front-end-teamet måste ha en separat Git-plats för front-end-modulen som specifikt anger den utvecklingsmiljön som mål.

         Ett vanligt tillvägagångssätt är att skapa en `dev`-gren för att hantera ändringar som gjorts i utvecklingsmiljön. Den här metoden tillåter en enklare sammanslagning tillbaka till grenen `main`, som används för distribution till produktionsmiljön.

      1. Pipeline: Det måste finnas en frontendgrupp som distribuerar till utvecklingsmiljön. Detta tillvägagångssätt skulle distribuera frontendmodulen som vanligtvis finns i grenen `dev`, vilket beskrivs i föregående punkt.
1. Det ledande teamet får sedan CSS- och JS-koden att fungera med både gamla och nya utdata.
   1. Om du vill utveckla lokalt gör du som vanligt följande:
      1. Kommandot `npx aem-site-theme-builder proxy` startar en proxyserver som hämtar innehåll från en AEM-miljö. Den ersätter CSS- och JS-filerna för den främre modulen med dessa filer från den lokala `dist`-mappen.
      1. Genom att konfigurera variabeln `AEM_URL` i den dolda filen `.env` kan du styra från vilken AEM-miljö den lokala proxyservern ska använda innehållet.
      1. Om du ändrar värdet för `AEM_URL` kan du därför växla mellan produktions- och utvecklingsmiljöerna för att justera CSS och JS så att det passar båda miljöerna.
      1. Det måste fungera med den utvecklingsmiljö som återger det nya resultatet och med den produktionsmiljö som återger det gamla resultatet.
   1. Det färdiga arbetet slutförs när den uppdaterade frontmodulen fungerar för båda miljöerna och distribueras till båda.
1. Back-end-teamet kan sedan uppdatera produktionsmiljön genom att distribuera koden som återger nya HTML- eller JSON-utdata, eller både och, via pipeline i full stack.
1. front-end-teamet kan rensa upp sin CSS och JS, ta bort element som bara behövs för det gamla resultatet och distribuera den slutliga uppdateringen till produktionen med hjälp av front-end-pipeline.

## Ytterligare resurser {#additional-resources}

* Lär dig hur AEM webbplatsteman kan användas för att anpassa webbplatsens stil och design.

  Se [Webbplatsteman](/help/sites-cloud/administering/site-creation/site-themes.md).

* Adobe tillhandahåller en AEM Site Theme Builder som en uppsättning skript för att skapa nya webbplatsteman.

  Se [AEM Site Theme Builder](https://github.com/adobe/aem-site-theme-builder)


