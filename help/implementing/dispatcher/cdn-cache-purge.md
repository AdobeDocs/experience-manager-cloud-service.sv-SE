---
title: Rensa CDN-cachen
description: Lär dig hur du tar bort cachelagrade objekt från CDN-cachen i Adobe genom att konfigurera rensnings-API-token som sedan kan användas i API-anrop.
feature: CDN Cache
exl-id: 4d091677-b817-4aeb-b131-7a5407ace3e0
role: Admin
source-git-commit: e5e0606c83f144f92f9ae57e5380a30389e8df1b
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---

# Rensa CDN-cachen {#cdn-purge-cache}

När du rensar bort ett objekt från CDN-cachen i Adobe tas det bort, vilket resulterar i framtida förfrågningar som fortsätter till ursprungsläget som en cache-fil som inte kan hanteras från cachen.
Med AEM as a Cloud Service kan du konfigurera en rensnings-API-token, som sedan kan användas i rensnings-API-anrop. Läs [Konfigurera CDN-autentiseringsuppgifter och autentisering](/help/implementing/dispatcher/cdn-credentials-authentication.md#purge-API-token) om du vill veta mer om hur du konfigurerar den här token med Cloud Manager Config Pipeline Authentication-direktiv.

Det finns tre rensningsvariationer som stöds:

* [Rensa en enda URL](#single-purge) - rensa en enskild resurs åt gången.
* [Töm av surrogatnyckel](#surrogate-key-purge) - Töm flera resurser samtidigt.
* [Fullständig rensning](#full-purge) - rensa alla resurser.

Alla rensningsvariationer har följande gemensamt:

* HTTP-metoden måste anges till `PURGE`.
* URL:en kan vara vilken domän som helst som är associerad med den AEM tjänsten som rensningsbegäran är avsedd för.
* `X-AEM-Purge-Key` måste anges i en HTTP-rubrik.

>[!CAUTION]
>Tömning av CDN-cachen, särskilt med den hårda flaggan, ökar trafiken vid källan och kan leda till ett driftstopp om det inte körs som det ska.

Du kan referera till [en självstudie](https://experienceleague.adobe.com/sv/docs/experience-manager-learn/cloud-service/caching/how-to/purge-cache) som fokuserar på att konfigurera rensningsnycklar och utföra rensning av CDN-cache.

## Rensa en URL {#single-purge}

Du kan rensa en enskild resurs åt gången på följande sätt:

```
curl
-X PURGE "https://publish-p1234-e5467.adobeaemcloud.com/resource-path" \
-H 'X-AEM-Purge-Key: <my_purge_key>' \
-H 'X-AEM-Purge: soft'
```

Som framgår av exemplet ovan kan du **alternativt** ange om CDN ska utföra en **hård** rensning (standard) eller en **mjuk** tömning av de cachelagrade objekten.

Med standardinställningen för strikt rensning blir innehållet omedelbart otillgängligt för nya begäranden tills innehållet hämtas från ursprungsläget. Mjuk rensning gör att innehållet blir inaktuellt, men skickar det ändå till kunderna så att de inte behöver vänta tills innehållet hämtas från originalet.

## Rensa Surrogate-nyckel {#surrogate-key-purge}

Surrognycklar är unika identifierare som du använder för att rensa en uppsättning innehåll. De tillämpas på innehåll genom att ett `Surrogate-Key`-huvud läggs till i svaret. En eller flera surrogatnycklar kan refereras i ett rensnings-API-anrop.

```
curl
-X PURGE "https://publish-p1234-e5467.adobeaemcloud.com" \
-H 'X-AEM-Purge-Key: <my_purge_key>' \
-H "Surrogate-Key: my-surrogate-key"
-H "X-AEM-Purge: soft" #optional
```

`Surrogate-Key` avgränsas med blanksteg. På samma sätt som för en enskild URL-tömning kan du konfigurera antingen en hård eller en mjuk tömning.

## Helt tömt {#full-purge}

Du kan tömma alla cachelagrade resurser helt enligt följande:

```
curl
-X PURGE "https://publish-p1234-e5467.adobeaemcloud.com" \
-H 'X-AEM-Purge-Key: <my_purge_key>' \
-H "X-AEM-Purge: all"
```

Observera att rubriken `X-AEM-Purge` måste innehålla värdet all.

## Interaktion med kundhanterad CDN

Om det finns ett [kundhanterat CDN](/help/implementing/dispatcher/cdn.md#point-to-point-CDN) måste även `X-Forwarded-Host` och `X-AEM-Edge-Key` anges:

```
curl
-X PURGE "https://publish-p1234-e5467.adobeaemcloud.com/resource-path" \
-H 'X-AEM-Purge-Key: <my_purge_key>' \
-H 'X-AEM-Edge-Key: <my_edge_key>' \
-H 'X-Forwarded-Host: <my_forwarded_domain>'
```


## Interaktion med Apache/Dispatcher-lager {#apache-layer}

Som beskrivs under [Leveransflöde för innehåll](/help/implementing/dispatcher/overview.md) hämtar CDN innehåll från lagret Apache/Dispatcher, om cachen har gått ut. Detta innebär att du måste se till att det även finns en ny version av innehållet på Dispatcher innan du rensar bort en resurs på CDN. Mer information finns också i [Invalidering av Dispatcher-cache](/help/implementing/dispatcher/caching.md#disp).
