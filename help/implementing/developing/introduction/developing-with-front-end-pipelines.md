---
title: Developing Sites with the Front-End Pipeline
description: Med den integrerade utvecklingsmiljön får utvecklarna större oberoende och utvecklingsprocessen kan bli betydligt snabbare.
exl-id: 996fb39d-1bb1-4dda-a418-77cdf8b307c5
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '1024'
ht-degree: 0%

---

# Developing Sites with the Front-End Pipeline {#developing-site-with-front-end-pipeline}

[Med den främre rörledningen](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) fler oberoende ges till gränssnittsutvecklare och utvecklingsprocessen kan gå mycket snabbare. I det här dokumentet beskrivs hur den här processen fungerar tillsammans med vissa överväganden som du bör vara medveten om för att få ut mesta möjliga av processen.

>[!TIP]
>
>Om du inte känner till hur du använder frontendriet och vilka fördelar det kan ge kan du titta på [Skapa snabbt webbplatser](/help/journey-sites/quick-site/overview.md) som ett exempel på hur du snabbt distribuerar en ny webbplats och anpassar dess tema helt oberoende av serverutvecklingen.

## En källa för sanning {#single-source-of-truth}

Ett allmänt bra tillvägagångssätt är att behålla en enda sanningskälla för det som används för AEM. Cloud Managers mål är att göra den enda källan till sanning uppenbar. Eftersom frontdelsrörledningen tillåter avkoppling av platsen för delar av koden ligger dock ett visst extra ansvar i den korrekta konfigurationen av frontdelsrörledningarna. Man måste vara försiktig så att man inte skapar flera rörledningar som kan användas på samma plats i samma miljö.

Av denna anledning, och särskilt när flera rörledningar för framände skapas, rekommenderas att en systematisk namnkonvention upprätthålls, som följande:

* Namnet på frontmodulen, som definieras av `name` egenskapen för `package.json` filen, ska innehålla namnet på den plats den gäller för. För en plats som finns på `/content/wknd`, namnet på frontmodulen skulle vara ungefär som `wknd-theme`.
* När en frontendmodul delar samma Git-databas med andra moduler bör namnet på dess mapp vara lika med, eller innehålla samma namn för, frontendmodulen. Om till exempel front end-modulen har ett namn `wknd-theme`, skulle namnet på den omslutande mappen vara något som `wknd-theme-sources`.
* Namnet på Cloud Managers frontendpipeline bör även innehålla namnet på den främre slutmodulen och även lägga till miljön som den distribuerar till (produktion eller utveckling). Till exempel för frontmodulen med namnet `wknd-theme`kan rörledningen heta något som `wknd-theme-prod`.

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
      1. URL: Utvecklingsteamet måste känna till URL:en för den utvecklingsmiljön.
      1. ACL: front-end-teamet måste få en lokal AEM med rättigheter som liknar&quot;Medarbetare&quot;.
      1. Git: front-end-teamet måste ha en separat Git-plats för front-end-modulen som är särskilt inriktad på den utvecklingsmiljön.
         * Ett vanligt tillvägagångssätt är att skapa en `dev` så att de ändringar som gjorts för utvecklingsmiljön sedan enkelt kan sammanfogas i `main` filial som ska distribueras till produktionsmiljön.
      1. Rörledning: front-end-teamet måste ha en front-end-pipeline som distribueras till utvecklingsmiljön. Den rörledningen distribuerar den frontdelsmodul som vanligtvis finns i `dev` gren, enligt beskrivningen i föregående punkt.
1. Det ledande teamet får sedan CSS- och JS-koden att fungera med både gamla och nya utdata.
   1. Som vanligt för att utveckla lokalt:
      1. The `npx aem-site-theme-builder proxy` -kommandot som körs i front end-modulen startar en proxyserver som begär innehållet från en AEM-miljö och ersätter CSS- och JS-filerna för front end-modulen med de som finns i den lokala `dist` mapp.
      1. Konfigurera `AEM_URL` variabeln i det dolda `.env` kan styra från vilken AEM som den lokala proxyservern använder innehållet.
      1. Ändra värdet för detta `AEM_URL` gör det därför möjligt att växla mellan produktions- och utvecklingsmiljöer för att justera CSS och JS så att den passar båda miljöerna.
      1. Det måste fungera med den utvecklingsmiljö som återger det nya resultatet och med den produktionsmiljö som återger det gamla resultatet.
   1. Det färdiga arbetet slutförs när den uppdaterade frontmodulen fungerar för båda miljöerna och distribueras till båda.
1. Back-end-teamet kan sedan uppdatera produktionsmiljön genom att distribuera koden som återger de nya HTML- och/eller JSON-utdata via hela stacken.
1. front-end-teamet kan sedan rensa upp sin CSS och JS och ta bort det som bara behövdes för den gamla versionen, och driftsätta den senaste uppdateringen till produktionen via front-end-flödet.

## Ytterligare resurser {#additional-resources}

* [Webbplatsteman](/help/sites-cloud/administering/site-creation/site-themes.md) - Lär dig hur AEM teman kan användas för att anpassa webbplatsens stil och design.
* [AEM Site Theme Builder](https://github.com/adobe/aem-site-theme-builder) - Adobe tillhandahåller en AEM Site Theme Builder som en uppsättning skript för att skapa nya webbplatsteman.
