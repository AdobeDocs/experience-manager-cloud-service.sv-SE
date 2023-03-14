---
title: Cachelagring och prestanda
description: Lär dig mer om de olika konfigurationer som är tillgängliga för att aktivera GraphQL- och innehållscachning för att optimera prestanda för implementeringen av din e-handel.
exl-id: 21ccdab8-4a2d-49ce-8700-2cbe129debc6,8b969821-5073-4540-a997-95c74a11e4f0
source-git-commit: 05a412519a2d2d0cba0a36c658b8fed95e59a0f7
workflow-type: tm+mt
source-wordcount: '845'
ht-degree: 0%

---

# Cachelagring och prestanda {#caching}

## Cachelagring av komponenter och GraphQL-svar {#graphql}

AEM CIF Core Components har redan inbyggt stöd för cachelagring av GraphQL-svar för enskilda komponenter. Den här funktionen kan användas för att minska antalet GraphQL backend-anrop med stor faktor. Effektiv cachelagring kan utföras särskilt för upprepade frågor, som att hämta kategoriträdet för en navigeringskomponent eller hämta alla tillgängliga aggregations-/facets-värden som visas på produktsöknings- och kategorisidorna.

För de AEM CIF Core-komponenterna konfigureras cachelagring på komponentbasis, så det är möjligt att kontrollera om (och hur länge) GraphQL-begäranden/svar cachelagras för varje komponent. Det går också att definiera cachelagring för OSGi-tjänster med GraphQL-klienten.

### Konfiguration {#configuration}

När cachen har konfigurerats för en viss komponent börjar den lagra GraphQL-frågor och svar enligt varje cachekonfigurationspost. Storleken på cacheminnet och cachelagringstiden för varje post ska definieras på projektbasis, beroende t.ex. på hur ofta katalogdata kan ändras, hur viktigt det är att en komponent alltid visar de senaste möjliga data, osv. Observera att det inte finns någon cacheogiltigförklaring, så var försiktig när du anger varaktigheten för cachen.

När cachelagring konfigureras för komponenter måste cachenamnet vara namnet på **proxy** komponenter som du definierar i ditt projekt.

Innan klienten skickar en GraphQL-begäran kommer den att kontrollera om det **exakt** samma GraphQL-begäran har redan cache-lagrats och returnerar eventuellt det cachelagrade svaret. För att matcha måste GraphQL-begäran matcha exakt, dvs. frågan, åtgärdsnamnet (om det finns något), variablerna (om sådana finns) MÅSTE alla vara lika med den cachelagrade begäran och alla anpassade HTTP-rubriker som kan anges MÅSTE också vara desamma. Adobe Commerce `Store` sidhuvudet MÅSTE matcha.

### Exempel {#examples}

Vi rekommenderar att du konfigurerar viss cachelagring för söktjänsten som hämtar alla tillgängliga aggregations-/facets-värden som visas på produktsöknings- och kategorisidorna. Dessa värden ändras vanligtvis bara när ett nytt attribut läggs till i produkter, så varaktigheten för den här cacheposten kan vara&quot;stor&quot; om uppsättningen produktattribut inte ändras så ofta. Detta är projektspecifikt, men vi rekommenderar värden på några minuter i projektutvecklingsfaserna och några timmar i stabila produktionssystem.

Detta konfigureras vanligtvis med följande cachepost:

```
com.adobe.cq.commerce.core.search.services.SearchFilterService:true:10:3600
```

Ett annat exempel där cachningsfunktionen GraphQl bör användas är navigeringskomponenten eftersom den skickar samma GraphQL-fråga på alla sidor. I det här fallet är cacheposten vanligtvis inställd på:

```
venia/components/structure/navigation:true:10:600
```

När du överväger [Referensarkiv för Venedig](https://github.com/adobe/aem-cif-guides-venia) används. Observera användningen av komponentens proxynamn `venia/components/structure/navigation`och **not** namnet på CIF-navigeringskomponenten (`core/cif/components/structure/navigation/v1/navigation`).

Cachelagring för andra komponenter bör definieras på projektbasis, vanligtvis i samordning med cachning som konfigurerats på Dispatcher-nivå. Kom ihåg att det inte finns någon aktiv ogiltigförklaring av dessa cacher, så cachelagringstiden bör vara noggrann. Det finns inga värden för&quot;en storlek passar alla&quot; som matchar alla möjliga projekt och användningsexempel. Se till att du definierar en cachelagringsstrategi på projektnivå som bäst motsvarar projektets krav.

## Dispatcher Caching {#dispatcher}

Cachelagra AEM sidor eller fragment i [AEM Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html) är den bästa metoden för alla AEM projekt. Oftast bygger det på invalideringstekniker som säkerställer att allt innehåll som ändras i AEM uppdateras korrekt i Dispatcher. Detta är en viktig egenskap i AEM Dispatcher-cachningsstrategi.

Förutom rent AEM hanterat innehåll-CIF kan en sida vanligtvis visa e-handelsdata som hämtas dynamiskt från Adobe Commerce via GraphQL. Även om sidstrukturen i sig kanske aldrig ändras kan e-handelsinnehållet ändras, till exempel om vissa produktdata (namn, pris, osv.) förändringar i Adobe Commerce.

För att CIF-sidor ska kunna cachelagras under en begränsad tid i AEM dispatcher rekommenderar vi därför att du använder [Invalidering av tidsbaserad cache](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#configuring-time-based-cache-invalidation-enablettl) (kallas även TTL-baserad cachelagring) när CIF-sidor cachelagras i AEM Dispatcher. Den här funktionen kan konfigureras i AEM med den extra [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/) paket.

Med TTL-baserad cachning definierar en utvecklare vanligtvis en eller flera cachningstider för valda AEM. Detta garanterar att CIF-sidor bara cachas i AEM Dispatcher upp till den konfigurerade längden och att innehållet uppdateras ofta.

>[!NOTE]
>
>Data på serversidan kan cachas av AEM dispatcher, men vissa CIF-komponenter, som `product`, `productlist`och `searchresults` -komponenter hämtar vanligtvis alltid produktpriser på nytt i en webbläsarbegäran på klienten när sidan läses in. Detta säkerställer att viktigt dynamiskt innehåll alltid hämtas vid sidinläsning.

## Ytterligare resurser {#additional}

- [Referensarkiv för Venedig](https://github.com/adobe/aem-cif-guides-venia)
- [Konfiguration av GraphQL-cachning](https://github.com/adobe/commerce-cif-graphql-client#caching)
- [AEM Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html)
