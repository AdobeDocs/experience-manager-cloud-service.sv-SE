---
title: Rensa CDN-cachen
description: Lär dig hur du tar bort cachelagrade objekt från CDN-cachen i Adobe genom att konfigurera rensnings-API-token som sedan kan användas i API-anrop.
feature: Dispatcher
source-git-commit: 114098a75d84a3da4cc582288ffa162cd960a0e6
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# Rensa CDN-cachen {#cdn-purge-cache}

>[!NOTE]
>Den här funktionen är ännu inte allmänt tillgänglig. Om du vill gå med i programmet för tidig adopter skickar du e-post `aemcs-cdn-config-adopter@adobe.com`.

När du rensar bort ett objekt från CDN-cachen i Adobe tas det bort, vilket resulterar i framtida förfrågningar som fortsätter till ursprungsläget som en cache-fil som inte kan hanteras från cachen.
Med AEM as a Cloud Service kan du konfigurera en rensnings-API-token, som sedan kan användas i API-anrop. Läs [Konfigurera CDN-autentiseringsuppgifter och autentiseringsartikel](/help/implementing/dispatcher/cdn-credentials-authentication.md#purge-API-token) om du vill lära dig hur du konfigurerar den här token med hjälp av autentiseringsdirektiven för Configuration Pipeline i Cloud Manager.

Det finns tre rensningsvariationer som stöds:

* [Rensa en URL](#single-purge) - rensa en enskild resurs åt gången.
* [Rensa efter surrogatnyckel](#surrogate-key-purge) - tömma flera resurser samtidigt.
* [Helt tömt](#full-purge) - tömma alla resurser.

Alla rensningsvariationer har följande gemensamt:

* HTTP-metoden måste anges till `PURGE`.
* URL:en kan vara vilken domän som helst som är associerad med den AEM tjänsten som rensningsbegäran är avsedd för.
* The `X-AEM-Purge-Key` måste anges i en HTTP-rubrik.

>[!CAUTION]
>Tömning av CDN-cachen, särskilt med den hårda flaggan, ökar trafiken vid källan och kan leda till ett driftstopp om det inte körs som det ska.

## Rensa en URL {#single-purge}

Du kan rensa en enskild resurs åt gången på följande sätt:

```
curl
-X PURGE "https://publish-p1234-e5467.adobeaemcloud.com/resource-path" \
-H 'X-AEM-Purge-Key: <my_purge_key>' \
-H 'X-AEM-Purge: soft'
```

Så som visas i exemplet ovan kan du **valfritt** ange om CDN ska utföra en **hård** rensa (standard) eller **mjuk** tömma de cachelagrade objekten.

Med standardinställningen för strikt rensning blir innehållet omedelbart otillgängligt för nya begäranden tills innehållet hämtas från ursprungsläget. Mjuk rensning gör att innehållet blir inaktuellt, men skickar det ändå till kunderna så att de inte behöver vänta tills innehållet hämtas från originalet.

## Rensa Surrogate-nyckel {#surrogate-key-purge}

Surrognycklar är unika identifierare som du använder för att rensa en uppsättning innehåll. De tillämpas på innehållet genom att lägga till en `Surrogate-Key` till svaret. En eller flera surrogatnycklar kan refereras i ett rensnings-API-anrop.

```
curl
-X PURGE "https://publish-p1234-e5467.adobeaemcloud.com" \
-H 'X-AEM-Purge-Key: <my_purge_key>' \
-H "Surrogate-Key: my-surrogate-key"
-H "X-AEM-Purge: soft" #optional
```

The `Surrogate-Key`(s) avgränsas med blanksteg. På samma sätt som för en enskild URL-tömning kan du konfigurera antingen en hård eller en mjuk tömning.

## Helt tömt {#full-purge}

Du kan tömma alla cachelagrade resurser helt enligt följande:

```
curl
-X PURGE "https://publish-p1234-e5467.adobeaemcloud.com" \
-H 'X-AEM-Purge-Key: <my_purge_key>' \
-H "X-AEM-Purge: all"
```

Var medveten om att `X-AEM-Purge` måste innehålla värdet all.

## Interaktion med lagret Apache/Dispatcher {#apache-layer}

Enligt beskrivningen i [Content Delivery Flow - artikel](/help/implementing/dispatcher/overview.md)hämtar CDN-innehållet från lagret Apache/Dispatcher, om cachen har gått ut. Detta innebär att du måste se till att det även finns en ny version av innehållet tillgänglig på Dispatcher innan du rensar bort en resurs på CDN. Mer information finns även i [Invalidering av Dispatcher-cache](/help/implementing/dispatcher/caching.md#disp).
