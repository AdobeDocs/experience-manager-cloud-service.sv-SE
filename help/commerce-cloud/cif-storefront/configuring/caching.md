---
title: Cachelagring och prestanda
description: Lär dig mer om de olika konfigurationer som är tillgängliga för att aktivera GraphQL- och innehållscachning för att optimera prestanda för implementeringen av din e-handel.
exl-id: 21ccdab8-4a2d-49ce-8700-2cbe129debc6
feature: Commerce Integration Framework
role: Admin
index: false
source-git-commit: 80bd8da1531e009509e29e2433a7cbc8dfe58e60
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 0%

---


# Cachelagring och prestanda {#caching}

## Cachelagring av komponenter och GraphQL-svar {#graphql}

AEM CIF Core Components har redan inbyggt stöd för cachelagring av GraphQL-svar för enskilda komponenter. Den här funktionen kan användas för att minska antalet GraphQL backend-anrop med stor faktor. Effektiv cachelagring kan utföras särskilt för upprepade frågor, som att hämta kategoriträdet för en navigeringskomponent eller hämta alla tillgängliga aggregations-/facets-värden som visas på produktsöknings- och kategorisidorna.

För AEM CIF Core Components konfigureras cachelagring på komponentbasis, så det är möjligt att styra om (och hur länge) GraphQL-begäranden/svar cachelagras för varje komponent. Det går också att definiera cachelagring för OSGi-tjänster med GraphQL-klienten.

### Konfiguration {#configuration}

När cachen har konfigurerats för en viss komponent börjar den lagra GraphQL-frågor och svar enligt varje cachekonfigurationspost. Storleken på cacheminnet och cachelagringstiden för varje post definieras på projektbasis, beroende t.ex. på följande:

* Hur ofta katalogdata kan ändras.
* Hur viktigt det är att en komponent alltid visar de senaste möjliga data, och så vidare.

Det finns ingen cacheogiltigförklaring, så var försiktig när du anger varaktigheten för cachen.

När du konfigurerar cachelagring för komponenter måste cachenamnet vara namnet på de **proxy**-komponenter som du definierar i ditt projekt.

Innan klienten skickar en GraphQL-begäran kontrollerar den om **exakt** samma GraphQL-begäran redan har cache-lagrats och returnerar eventuellt det cachelagrade svaret. GraphQL-begäran _måste_ matcha varandra exakt. Det vill säga att frågan, åtgärdsnamnet (om det finns något), variablerna (om det finns) _måste_ alla vara lika med den cachelagrade begäran. Alla anpassade HTTP-huvuden som kan anges _måste_ också vara samma. Adobe Commerce `Store`-huvudet _måste_ matcha till exempel.

### Exempel {#examples}

Adobe rekommenderar att du konfigurerar viss cachelagring för söktjänsten som hämtar alla tillgängliga aggregations-/ansiktsvärden som visas på produktsöknings- och kategorisidorna. Dessa värden ändras vanligtvis bara när ett nytt attribut läggs till i produkter, till exempel. Varaktigheten för den här cacheposten kan därför vara &quot;stor&quot; om produktattributuppsättningen inte ändras så ofta. Även om det här tävlingsbidraget är projektspecifikt rekommenderar Adobe värden på några minuter i projektutvecklingsfaser och några timmar i stabila produktionssystem.

Den här inställningen är vanligtvis konfigurerad med följande cachepost:

```text
com.adobe.cq.commerce.core.search.services.SearchFilterService:true:10:3600
```

Ett annat exempel där cachningsfunktionen GraphQl rekommenderas är navigeringskomponenten. Orsaken är att samma GraphQL-fråga skickas till alla sidor. I det här fallet är cacheposten vanligtvis inställd på:

```text
venia/components/structure/navigation:true:10:600
```

Tänk på att [Venias referensarkiv](https://github.com/adobe/aem-cif-guides-venia) används. Observera användningen av komponentproxynamnet `venia/components/structure/navigation` och **inte** namnet på CIF-navigeringskomponenten (`core/cif/components/structure/navigation/v1/navigation`).

Cachelagring för andra komponenter bör definieras på projektbasis, vanligen i samordning med cachning som konfigurerats på Dispatcher-nivå. Kom ihåg att det inte finns någon aktiv ogiltigförklaring av dessa cacheminnen, så cachelagringstiden bör vara noggrann. Det finns inga värden för&quot;en storlek passar alla&quot; som matchar alla möjliga projekt och användningsfall. Se till att du definierar en cachelagringsstrategi på projektnivå som bäst motsvarar projektets krav.

## Dispatcher Caching {#dispatcher}

Cachelagring av AEM-sidor eller -fragment i [AEM Dispatcher](https://experienceleague.adobe.com/en/docs/experience-manager-dispatcher/using/dispatcher) är bästa sättet för alla AEM-projekt. Oftast bygger det på invalideringstekniker som säkerställer att allt innehåll som ändras i AEM uppdateras korrekt i Dispatcher. Den här funktionen är central i AEM Dispatcher cachningsstrategi.

Förutom rent AEM-hanterat innehåll i CIF kan en sida vanligtvis visa e-handelsdata som hämtas dynamiskt från Adobe Commerce via GraphQL. Även om själva sidstrukturen kanske aldrig ändras kan e-handelsinnehållet ändras. Om produktdata, till exempel namn och pris, ändras i Adobe Commerce.

För att CIF-sidor ska kunna cachelagras under en begränsad tid i AEM Dispatcher rekommenderar Adobe att du använder [tidsbaserad cacheinvalidering](https://experienceleague.adobe.com/en/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration#configuring-time-based-cache-invalidation-enablettl) (kallas TTL-baserad cachelagring) när du cachelagrar CIF-sidor i AEM Dispatcher. Den här funktionen kan konfigureras i AEM med det extra [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/) -paketet.

Med TTL-baserad cachning definierar en utvecklare vanligtvis en eller flera cachningstider för utvalda AEM-sidor. Med den här tidslängden kan du vara säker på att CIF-sidor bara cachelagras i AEM Dispatcher upp till den konfigurerade tidslängden och att innehållet uppdateras regelbundet.

>[!NOTE]
>
>Data på serversidan kan cachas av AEM Dispatcher, men vissa CIF-komponenter som `product`, `productlist` och `searchresults` hämtar vanligtvis alltid produktpriser i en webbläsarbegäran på klientsidan när sidan läses in. På så sätt säkerställer du att viktigt dynamiskt innehåll alltid hämtas vid sidinläsning.

## Ytterligare resurser {#additional}

* [Referensarkiv för Venedig](https://github.com/adobe/aem-cif-guides-venia)
* [GraphQL cachelagringskonfiguration](https://github.com/adobe/commerce-cif-graphql-client#caching)
* [AEM Dispatcher](https://experienceleague.adobe.com/en/docs/experience-manager-dispatcher/using/dispatcher)
