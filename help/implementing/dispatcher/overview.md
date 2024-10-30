---
title: Översikt över leveransflöde
description: Läs mer om dataflödet för innehållsleverans och hur du publicerar ditt innehåll
exl-id: fe42fb9e-cdf4-43e1-b688-7cecf4124fa5
feature: Dispatcher
role: Admin
source-git-commit: d58055cd0ed2451b5e8063fbb4e7269885d0787c
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# Leveransflöde {#content-delivery}

Den aktuella sidan innehåller information om publicering av tjänstinnehåll i AEM as a Cloud Service. Leverans av Publish-tjänstinnehåll omfattar:

* CDN
* AEM Dispatcher
* AEM

Dataflödet är följande:

1. URL:en läggs till i webbläsaren
1. Begäran gjordes till CDN som mappats i DNS till den domänen
1. Om innehållet cachelagras fullständigt i CDN skickas det till webbläsaren av CDN
1. Om innehållet inte är fullständigt cachelagrat anropar CDN (omvänd proxy) till Dispatcher
1. Om innehållet cachelagras helt på Dispatcher skickar Dispatcher det till CDN
1. Om innehållet inte är fullständigt cachelagrat anropar Dispatcher (omvänd proxy) till AEM
1. Innehållet återges av webbläsaren, som också kan cachelagra det beroende på sidhuvudena

Som standard förfaller innehållstypen HTML/text efter 300 sekunder (5 minuter) i Dispatcher-lagret, vilket är ett tröskelvärde som både Dispatcher cache och CDN respekterar. Under omdistributioner av publiceringstjänsten rensas Dispatcher-cachen och värms upp innan de nya publiceringsnoderna tar emot trafik.

I följande avsnitt finns mer information om innehållsleverans:
* [CDN-konfiguration](/help/implementing/dispatcher/cdn.md)
* [Cachning](/help/implementing/dispatcher/caching.md)

Mer information om replikering från författartjänsten till publiceringstjänsten finns i [Replikering](/help/operations/replication.md).
