---
title: Cachelagring och prestanda
description: Lär dig mer om de olika konfigurationer som är tillgängliga för att aktivera GraphQL- och innehållscachning för att optimera prestanda för implementeringen av din e-handel.
exl-id: 21ccdab8-4a2d-49ce-8700-2cbe129debc6
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 0%

---

# Cachelagring och prestanda {#caching}

## Cachelagring av komponenter och GraphQL-svar {#graphql}

AEM CIF Core Components har redan inbyggt stöd för cachelagring av GraphQL-svar för enskilda komponenter. Den här funktionen kan användas för att minska antalet GraphQL backend-anrop med stor faktor. Effektiv cachelagring kan utföras särskilt för upprepade frågor, som att hämta kategoriträdet för en navigeringskomponent eller hämta alla tillgängliga aggregations-/facets-värden som visas på produktsöknings- och kategorisidorna.

För de AEM CIF Core-komponenterna konfigureras cachelagring på komponentbasis, så det är möjligt att kontrollera om (och hur länge) GraphQL-begäranden/svar cachelagras för varje komponent. Det går också att definiera cachelagring för OSGi-tjänster med GraphQL-klienten.

### Konfiguration {#configuration}

När cachen har konfigurerats för en viss komponent börjar den lagra GraphQL-frågor och svar enligt varje cachekonfigurationspost. Storleken på cacheminnet och cachelagringstiden för varje post definieras på projektbasis, beroende t.ex. på följande:

* Hur ofta katalogdata kan ändras.
* Hur viktigt det är att en komponent alltid visar de senaste möjliga data, och så vidare.

Det finns ingen cacheogiltigförklaring, så var försiktig när du anger varaktigheten för cachen.

När cachelagring konfigureras för komponenter måste cachenamnet vara namnet på **proxy** komponenter som du definierar i ditt projekt.

Innan klienten skickar en GraphQL-begäran kontrollerar den om **exakt** samma GraphQL-begäran har redan cache-lagrats och returnerar eventuellt det cachelagrade svaret. För att matcha _måste_ exakt matchning. Det vill säga frågan, åtgärdsnamn (om det finns något), variabler (om sådana finns) _måste_ alla vara lika med den cachelagrade begäran. Alla anpassade HTTP-rubriker som kan anges _måste_ vara detsamma. Adobe Commerce `Store` header _måste_ matchar.

### Exempel {#examples}

Adobe rekommenderar att du konfigurerar viss cachelagring för söktjänsten som hämtar alla tillgängliga aggregations-/facets-värden som visas på produktsöknings- och kategorisidorna. Dessa värden ändras vanligtvis bara när ett nytt attribut läggs till i produkter, till exempel. Varaktigheten för den här cacheposten kan därför vara &quot;stor&quot; om produktattributuppsättningen inte ändras så ofta. Även om det här tävlingsbidraget är projektspecifikt rekommenderar Adobe några minuter i projektutvecklingsfaserna och några timmar i stabila produktionssystem.

Den här inställningen är vanligtvis konfigurerad med följande cachepost:

```
com.adobe.cq.commerce.core.search.services.SearchFilterService:true:10:3600
```

Ett annat exempel där cachningsfunktionen GraphQl rekommenderas är navigeringskomponenten. Orsaken är att samma GraphQL-fråga skickas till alla sidor. I det här fallet är cacheposten vanligtvis inställd på:

```
venia/components/structure/navigation:true:10:600
```

Med tanke på att [Referensarkiv för Venedig](https://github.com/adobe/aem-cif-guides-venia) används. Observera användningen av komponentens proxynamn `venia/components/structure/navigation`och **not** namnet på CIF-navigeringskomponenten (`core/cif/components/structure/navigation/v1/navigation`).

Cachelagring för andra komponenter bör definieras på projektbasis, vanligtvis i samordning med cachning som konfigurerats på Dispatcher-nivå. Kom ihåg att det inte finns någon aktiv ogiltigförklaring av dessa cacheminnen, så cachelagringstiden bör vara noggrann. Det finns inga värden för&quot;en storlek passar alla&quot; som matchar alla möjliga projekt och användningsfall. Se till att du definierar en cachelagringsstrategi på projektnivå som bäst motsvarar projektets krav.

## Dispatcher Caching {#dispatcher}

Cachelagra AEM sidor eller fragment i [AEM Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html) är den bästa metoden för alla AEM projekt. Oftast bygger det på invalideringstekniker som säkerställer att allt innehåll som ändras i AEM uppdateras korrekt i Dispatcher. Den här funktionen är väsentlig för AEM Dispatcher-cachningsstrategi.

Förutom CIF för rent AEM-hanterat innehåll kan en sida vanligtvis visa e-handelsdata som hämtas dynamiskt från Adobe Commerce via GraphQL. Även om själva sidstrukturen kanske aldrig ändras kan e-handelsinnehållet ändras. Om produktdata, till exempel namn och pris, ändras i Adobe Commerce.

För att CIF-sidor ska kunna cachelagras under en begränsad tid i AEM Dispatcher rekommenderar Adobe att du använder [Tidsbaserad cacheinvalidering](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#configuring-time-based-cache-invalidation-enablettl) (kallas TTL-baserad cachelagring) när CIF-sidor cachelagras i AEM Dispatcher. Den här funktionen kan konfigureras i AEM med den extra [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/) paket.

Med TTL-baserad cachning definierar en utvecklare vanligtvis en eller flera cachningstider för valda AEM. Den här tidslängden säkerställer att CIF-sidor bara cachas i AEM Dispatcher upp till den konfigurerade tidslängden och att innehållet uppdateras ofta.

>[!NOTE]
>
>Data på serversidan kan cachas av AEM Dispatcher, men vissa CIF-komponenter, som `product`, `productlist`och `searchresults` uppdaterar vanligtvis alltid produktpriser i en webbläsarbegäran på klienten när sidan läses in. Om du gör det kan du vara säker på att viktigt dynamiskt innehåll alltid hämtas vid sidinläsning.

## Ytterligare resurser {#additional}

* [Referensarkiv för Venedig](https://github.com/adobe/aem-cif-guides-venia)
* [Konfiguration av GraphQL-cachning](https://github.com/adobe/commerce-cif-graphql-client#caching)
* [AEM Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html)
