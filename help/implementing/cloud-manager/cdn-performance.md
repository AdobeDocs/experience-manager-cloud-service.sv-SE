---
title: Kontrollpanel för CDN-prestanda
description: Lär dig hur Cloud Manager utvärderar prestanda för leveransnätverk (CDN) och vad du kan lära dig av kontrollpanelen.
exl-id: ecd8c1ca-873f-4e73-ad73-b5f7561eb109
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 0%

---

# Kontrollpanel för CDN-prestanda {#cdn-performance}

Lär dig hur Cloud Manager utvärderar prestanda för leveransnätverk (CDN) och vad du kan lära dig av kontrollpanelen.

## Ökning {#overview}

Alla Cloud Manager-program har en kontrollpanel för CDN-prestanda. Den här kontrollpanelen ger en övergripande poäng för CDN-prestanda tillsammans med trender, varningar och förslag på förbättringar efter behov.

![Kontrollpanel för CDN-prestanda](assets/cdn-performance-dashboard.png)

## Åtkomst till kontrollpanelen {#accessing}

CDN-kontrollpanelen finns på översiktssidan för alla program.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.

1. På konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)** trycker eller klickar du på det program vars CDN-kontrollpanel du vill visa.

   ![Sidan Mina program](assets/my-programs.png)

1. På sidan **Programöversikt** i ditt program kan du bläddra nedåt under korten **Miljöer** och **Pipelines** för att se kortet **Prestanda**.

   ![Prestanda](assets/cdn-performance-overview.png)

## Använda kontrollpanelen {#using}

Kontrollpanelen ger en övergripande poäng för CDN-prestanda tillsammans med trender, varningar och förslag på förbättringar efter behov.

![Kontrollpanel för CDN-prestanda](assets/cdn-performance-dashboard.png)

Om du vill ha mer information om CDN-prestanda och förslag på hur du kan förbättra den trycker eller klickar du på **Visa trend**.

![Resultattrend](assets/cdn-performance-trend.png)

Tryck eller klicka på **Visa** nedanför diagrammet om du vill ändra tidsrymden för diagrammet.

Om du vill ha förslag på hur du kan förbättra CDN-prestanda väljer du fliken **Recommendations**.

![CDN-rekommendationer](assets/cdn-performance-recommendations.png)

Tryck eller klicka på markören bredvid en rekommendation i listan för att visa information om vilka åtgärder som ska vidtas för att förbättra och orsaken till problemet.

## Träffdefinition i cache {#cache-hit}

Träffgraden i cacheminnet är ett mått på hur många innehållsbegäranden som ett cacheminne kan fylla, jämfört med hur många begäranden det tar emot. Ju högre frekvens en cache-träff har, desto bättre prestanda blir ett CDN.

>[!TIP]
>
>Adobe rekommenderar att användare siktar på en cacheträffkvot på 99 %.

```text
Cache Hit Ratio = Cache Hits / (Hits + Misses + Passes + Other)
```

* **Träff** - Data begärs från cacheminnet och hittas.
* **Fröken** - Data begärs från cacheminnet, men kan inte hittas.
* **Steg** - Data begärs från cacheminnet och är inställda på att inte cachelagra dessa data i något fall.
* **Annat** - Alla dataförfrågningar från cachen som inte matchar något annat fall.

Cachelagringsstatistik uppdateras var 24:e timme.

>[!TIP]
>
>Mer information om hur Cloud Manager och CDN interagerar med Dispatcher finns i dokumentet [Caching in AEM as a Cloud Service.](/help/implementing/dispatcher/caching.md)
