---
title: Developing Sites with the Front-End Pipeline
description: Med den integrerade utvecklingsmiljön får utvecklarna större oberoende och utvecklingsprocessen kan bli betydligt snabbare. I det här dokumentet beskrivs några särskilda aspekter av den inledande konstruktionsprocessen som bör anges.
exl-id: 996fb39d-1bb1-4dda-a418-77cdf8b307c5
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '1169'
ht-degree: 0%

---


# Developing Sites with the Front-End Pipeline {#developing-site-with-front-end-pipeline}

[Med frontdelspipeline](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) får frontendoututvecklarna mer oberoende och utvecklingsprocessen kan gå mycket snabbare. I det här dokumentet beskrivs hur den här processen fungerar tillsammans med vissa överväganden som du bör vara medveten om så att du kan utnyttja hela potentialen i den här processen.

>[!TIP]
>
>Om du ännu inte är bekant med hur du ska använda frontendriet och de fördelar det kan ge kan du ta en titt på [snabbplatsskapanderesan](/help/journey-sites/quick-site/overview.md) för att få ett exempel på hur du snabbt kan distribuera en ny webbplats och anpassa temat helt oberoende av serverdelsutvecklingen.

## Front-End Build Contract {#front-end-build-contract}

Ungefär som i [fullständig stackbyggmiljö](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md) har frontendpipeline en egen miljö. Utvecklarna har viss flexibilitet när det gäller att använda denna pipeline så länge som följande avtal för front-end-bygge följs.

Front-end-pipeline kräver att front-end-Node.js-projektet använder skriptdirektivet `build` för att generera det bygge som det distribuerar. Detta beror på att Cloud Manager använder kommandot `npm run build` för att generera det distribuerbara projektet för frontendbygget.

Det resulterande innehållet i mappen `dist` är det som distribueras av Cloud Manager, och som fungerar som statiska filer. Dessa filer lagras externt på AEM, men är tillgängliga via en `/content/...`-URL i den distribuerade miljön.

## Nodversioner {#node-versions}

Front-end-miljön har stöd för följande Node.js-versioner.

* 12
* 14 (standard)
* 16
* 18

Du kan använda `NODE_VERSION` [miljövariabeln ](/help/implementing/cloud-manager/environment-variables.md) för att ange önskad version.

## Enskild Source av sanning {#single-source-of-truth}

Ett allmänt bra tillvägagångssätt är att behålla en enda sanningskälla för det som används för AEM. Cloud Manager mål är att göra denna enda källa till sanning självklar. Eftersom frontdelsrörledningen tillåter avkoppling av platsen för delar av koden ligger dock ett visst extra ansvar i den korrekta konfigurationen av frontdelsrörledningarna. Man måste vara försiktig så att man inte skapar flera rörledningar som kan användas på samma plats i samma miljö.

Av denna anledning, och särskilt när flera rörledningar för framände skapas, rekommenderas att en systematisk namnkonvention upprätthålls, som följande:

* Namnet på frontmodulen, som definieras av egenskapen `name` för filen `package.json`, ska innehålla namnet på den plats som det gäller för. För en webbplats som finns på `/content/wknd` skulle namnet på frontmodulen till exempel vara `wknd-theme`.
* När en front-end-modul delar samma Git-databas med andra moduler, ska namnet på dess mapp vara lika med, eller innehålla samma namn på, front end-modulen. Om till exempel front end-modulen heter `wknd-theme` skulle namnet på den omslutande mappen vara något som liknar `wknd-theme-sources`.
* Namnet på Cloud Manager front-end-pipeline bör även innehålla namnet på front-end-modulen och även lägga till den miljö som den distribuerar till (produktion eller utveckling). För till exempel frontmodulen `wknd-theme` kan pipeline heta något som `wknd-theme-prod`.

En sådan konvention bör effektivt förhindra följande misstag i samband med driftsättningen:

* Använda en frontendmodul på fel plats
* Skapa flera frontendmoduler som använder samma plats, vilket skulle skriva över varandra
* Skapa flera rörledningar för samma källor, vilket kan orsaka konkurrensförhållanden, utan att garantera ordningen för driftsättningar

## Separation av oro {#separation-of-concerns}

En annan bra metod som gäller för varje separation av frågor är att lägga särskild vikt vid hur det kontrakt som avskiljer bekymren utformas och hanteras. När det gäller front end-rörledningen är det kontrakt som skiljer koden från resten HTML och JSON som renderas av anläggningen. Om HTML och JSON förblir stabila ger frontlinjen maximalt värde genom att göra front-end-teamet helt oberoende.

Det finns för närvarande ingen specifik funktion för att köra helstackspipeline synkront med frontendspipeline(en). Därför måste man vid frikopplingen av frontdelsutvecklingen från rörledningen i full hög lägga in extra omsorg i kontraktet som avgränsar dessa två problemområden. Kontraktet är i allmänhet det HTML och/eller JSON som Experience Manager återger. Förändringar av detta avtal måste därför vara välplanerade mellan de grupper som driver de olika rörledningarna så att de är överens om hur de ska sekvensera motsvarande ändringar.

Följande steg rekommenderas i allmänhet när det är nödvändigt att ändra HTML och/eller JSON-utdata som påverkar båda problemområdena.

1. Back-end-teamet skapar först en utvecklingsmiljö med nya HTML och/eller JSON-utdata.
   1. Via rörledningen för hela stacken distribuerar de den kod som krävs för att återge de nya HTML- och/eller JSON-utdata som önskas.
   1. Om det är i en miljö som front-end-teamet inte tidigare har åtkomst till måste följande steg utföras.
      1. URL: Front-end-teamet måste känna till URL:en för den utvecklingsmiljön.
      1. ACL: Det lokala teamet måste ges en lokal AEM med rättigheter som liknar&quot;Medarbetare&quot;.
      1. Git: Front-end-teamet måste ha en separat Git-plats för front-end-modulen som specifikt anger den utvecklingsmiljön som mål.
         * Ett vanligt tillvägagångssätt är att skapa en `dev`-gren, så att ändringarna som gjorts för utvecklingsmiljön sedan enkelt kan sammanfogas med `main`-grenen som ska distribueras till produktionsmiljön.
      1. Pipeline: Det måste finnas en frontendgrupp som distribuerar till utvecklingsmiljön. Detta tillvägagångssätt skulle distribuera frontendmodulen som vanligtvis finns i grenen `dev`, vilket beskrivs i föregående punkt.
1. Det ledande teamet får sedan CSS- och JS-koden att fungera med både gamla och nya utdata.
   1. Som vanligt för att utveckla lokalt:
      1. Kommandot `npx aem-site-theme-builder proxy` som körs i front-end-modulen startar en proxyserver som begär innehållet från en AEM, samtidigt som CSS- och JS-filerna för front-end-modulen ersätts med filerna från den lokala `dist`-mappen.
      1. Genom att konfigurera variabeln `AEM_URL` i den dolda filen `.env` kan du styra från vilken AEM som den lokala proxyservern förbrukar innehållet.
      1. Om du ändrar värdet för `AEM_URL` kan du därför växla mellan produktions- och utvecklingsmiljöerna för att justera CSS och JS så att det passar båda miljöerna.
      1. Det måste fungera med den utvecklingsmiljö som återger det nya resultatet och med den produktionsmiljö som återger det gamla resultatet.
   1. Det färdiga arbetet slutförs när den uppdaterade frontmodulen fungerar för båda miljöerna och distribueras till båda.
1. Back-end-teamet kan sedan uppdatera produktionsmiljön genom att distribuera koden som återger de nya HTML- och/eller JSON-utdata via hela stacken.
1. front-end-teamet kan sedan rensa upp sin CSS och JS och ta bort det som bara behövdes för den gamla versionen, och driftsätta den senaste uppdateringen till produktionen via front-end-flödet.

## Ytterligare resurser {#additional-resources}

* [Webbplatsteman](/help/sites-cloud/administering/site-creation/site-themes.md) - Lär dig hur AEM webbplatsteman kan användas för att anpassa webbplatsens stil och design.
* [AEM Site Theme Builder](https://github.com/adobe/aem-site-theme-builder) - Adobe tillhandahåller en AEM Site Theme Builder som en uppsättning skript för att skapa nya webbplatsteman.
