---
title: Cachelagring och prestanda
description: Cachelagring och prestanda
translation-type: tm+mt
source-git-commit: 2997a28e79b51e88ececbd46c81dbc6a6c443e68
workflow-type: tm+mt
source-wordcount: '830'
ht-degree: 2%

---


# Cachelagring och prestanda {#caching}

## Cachelagring av komponent- och GraphQL-svar {#graphql}

AEM CIF Core Components har redan inbyggt stöd för cachelagring av GraphQL-svar för enskilda komponenter. Den här funktionen kan användas för att minska antalet GraphQL-anrop med stor faktor. Effektiv cachelagring kan utföras särskilt för upprepade frågor, som att hämta kategoriträdet för en navigeringskomponent eller hämta alla tillgängliga aggregations-/facets-värden som visas på produktsöknings- och kategorisidorna.

För AEM CIF Core Components konfigureras cachelagring på komponentbasis, så det är möjligt att kontrollera om (och hur länge) GraphQL-begäranden/svar cachelagras för varje komponent. Det går också att definiera cachelagring för OSGi-tjänster med GraphQL-klienten.

### Konfiguration

När cachen har konfigurerats för en viss komponent börjar GraphQL-frågor och svar sparas enligt varje cachekonfigurationspost. Storleken på cacheminnet och cachelagringstiden för varje post ska definieras på projektbasis, beroende t.ex. på hur ofta katalogdata kan ändras, hur viktigt det är att en komponent alltid visar de senaste möjliga data, osv. Observera att det inte finns någon cacheogiltigförklaring, så var försiktig när du anger varaktigheten för cachen.

När du konfigurerar cachelagring för komponenter måste cachenamnet vara namnet på de **proxykomponenter** som du definierar i ditt projekt.

Innan klienten skickar en GraphQL-begäran kontrollerar den om den **exakta** GraphQL-begäran redan är cachelagrad och eventuellt returnerar det cachelagrade svaret. För att matcha måste GraphQL-begäran matcha exakt, d.v.s. frågan, åtgärdsnamnet (om det finns något), variablerna (om sådana finns) MÅSTE alla vara lika med den cachelagrade begäran, och alla anpassade HTTP-rubriker som kan anges MÅSTE också vara desamma. Magento-huvudet MÅSTE till exempel matcha. `Store`

### Exempel

Vi rekommenderar att du konfigurerar viss cachelagring för söktjänsten som hämtar alla tillgängliga aggregations-/facets-värden som visas på produktsöknings- och kategorisidorna. Dessa värden ändras vanligtvis bara när ett nytt attribut läggs till i produkter, så varaktigheten för den här cacheposten kan vara&quot;stor&quot; om uppsättningen produktattribut inte ändras så ofta. Detta är projektspecifikt, men vi rekommenderar värden på några minuter i projektutvecklingsfaserna och några timmar i stabila produktionssystem.

Detta konfigureras vanligtvis med följande cachepost:

```
com.adobe.cq.commerce.core.search.services.SearchFilterService:true:10:3600
```

Ett annat exempel där cachningsfunktionen GraphQl rekommenderas att användas är navigeringskomponenten eftersom den skickar samma GraphQL-fråga på alla sidor. I det här fallet är cacheposten vanligtvis inställd på:

```
venia/components/structure/navigation:true:10:600
```

när du överväger att använda [Venias referensarkiv](https://github.com/adobe/aem-cif-guides-venia) . Observera att komponentens proxynamn används `venia/components/structure/navigation`och **inte** CIF-navigeringskomponentens (`core/cif/components/structure/navigation/v1/navigation`) namn.

Cachelagring för andra komponenter bör definieras på projektbasis, vanligen i samordning med cachning som konfigurerats på Dispatcher-nivå. Kom ihåg att det inte finns någon aktiv ogiltigförklaring av dessa cacher, så cachelagringstiden bör vara noggrann. Det finns inga värden för&quot;en storlek passar alla&quot; som matchar alla möjliga projekt och användningsexempel. Se till att du definierar en cachelagringsstrategi på projektnivå som bäst motsvarar projektets krav.

## Dispatcher cachning {#dispatcher}

Cachelagring AEM sidor eller fragment i [AEM Dispatcher](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/dispatcher.html) är en bra metod för alla AEM projekt. Oftast bygger det på invalideringstekniker som säkerställer att allt innehåll som ändras i AEM uppdateras korrekt i Dispatcher. Detta är en viktig egenskap i den AEM Dispatcher cachningsstrategin.

Förutom rent AEM hanterat innehåll-CIF kan en sida vanligtvis visa handelsdata som hämtas dynamiskt från Magento via GraphQL. Även om sidstrukturen i sig kanske aldrig ändras kan e-handelsinnehållet ändras, till exempel om vissa produktdata (namn, pris, osv.) ändras i Magento.

För att CIF-sidor ska kunna cachelagras under en begränsad tid i AEM Dispatcher rekommenderar vi därför att du använder [tidsbaserad cacheinvalidering](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#configuring-time-based-cache-invalidation-enablettl) (kallas även TTL-baserad cachelagring) när du cachelagrar CIF-sidor i AEM Dispatcher. Den här funktionen kan konfigureras i AEM med det extra [paketet ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/) .

Med TTL-baserad cachning definierar en utvecklare vanligtvis en eller flera cachningstider för valda AEM. Detta garanterar att CIF-sidor bara cachas i AEM Dispatcher upp till den konfigurerade längden och att innehållet uppdateras ofta.

>[!NOTE]
>
>Data på serversidan kan cachas av AEM dispatcher, men vissa CIF-komponenter som `product`, `productlist`och `searchresults` komponenter hämtar vanligtvis alltid produktpriser på nytt i en webbläsarbegäran på klientsidan när sidan läses in. Detta säkerställer att viktigt dynamiskt innehåll alltid hämtas vid sidinläsning.

## Ytterligare resurser

- [Referensarkiv för Venedig](https://github.com/adobe/aem-cif-guides-venia)
- [Konfiguration för GraphQL-cachelagring](https://github.com/adobe/commerce-cif-graphql-client#caching)
- [AEM Dispatcher](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/dispatcher.html)