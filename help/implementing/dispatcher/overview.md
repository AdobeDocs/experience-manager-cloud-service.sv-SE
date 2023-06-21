---
title: Översikt över leveransflöde
description: Översikt över leveransflöde
exl-id: fe42fb9e-cdf4-43e1-b688-7cecf4124fa5
source-git-commit: f0edd0e3deeba89dcbd2dc1a07859138b24e2220
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 1%

---

# Flöde för innehållsleverans {#content-delivery}

Den aktuella sidan innehåller information om publicering av tjänstinnehåll på AEM as a Cloud Service. Leverans av publiceringstjänstinnehåll inkluderar:

* CDN
* AEM Dispatcher
* AEM

Dataflödet är följande:

1. URL:en läggs till i webbläsaren
1. Begäran gjordes till CDN som mappats i DNS till den domänen
1. Om innehållet cachelagras fullständigt i CDN skickas det till webbläsaren av CDN
1. Om innehållet inte är fullständigt cachelagrat anropar CDN (omvänd proxy) till Dispatcher
1. Om innehållet har cache-lagrats fullständigt i Dispatcher skickas det till CDN
1. Om innehållet inte är fullständigt cachelagrat anropar Dispatcher (omvänd proxy) till AEM publicering
1. Innehållet återges av webbläsaren, som också kan cachelagra det beroende på sidhuvudena

Som standard förfaller innehållstypen HTML/text efter 300 sekunder (5 minuter) i Dispatcher-lagret, ett tröskelvärde som både Dispatcher-cachen och CDN respekterar. Under omdistributioner av publiceringstjänsten rensas Dispatcher-cachen och värms upp innan de nya publiceringsnoderna tar emot trafik.

I följande avsnitt finns mer information om innehållsleverans:
* [CDN-konfiguration](/help/implementing/dispatcher/cdn.md)
* [Cachelagring](/help/implementing/dispatcher/caching.md)


Information om replikering från författartjänsten till publiceringstjänsten finns tillgänglig [här](/help/operations/replication.md).
