---
title: Översikt över leveransflöde
description: Översikt över leveransflöde
translation-type: tm+mt
source-git-commit: 0080ace746f4a7212180d2404b356176d5f2d72c
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 1%

---


# Flöde för innehållsleverans {#content-delivery}

Den aktuella sidan innehåller information om publicering av tjänstinnehåll i AEM som en Cloud Service. Leverans av publiceringstjänstinnehåll inkluderar:

* CDN
* AEM
* AEM publicera

Dataflödet är följande:

1. URL:en läggs till i webbläsaren
1. Begäran gjordes till CDN som mappats i DNS till den domänen
1. Om innehållet cachelagras fullständigt i CDN skickas det till webbläsaren av CDN
1. Om innehållet inte är fullständigt cachelagrat anropar CDN (omvänd proxy) till dispatchern
1. Om innehållet är fullständigt cachelagrat när avsändaren skickar det till CDN
1. Om innehållet inte är fullständigt cachelagrat anropar avsändaren (omvänd proxy) till AEM publicering
1. Innehållet återges av webbläsaren, som också kan cachelagra det beroende på sidhuvudena

Som standard förfaller innehållstypen HTML/text efter 300-talet (5 minuter) i dispatcherlagret, vilket är ett tröskelvärde som både dispatcher cache och CDN respekterar. Under omdistributioner av publiceringstjänsten rensas dispatchercachen och varnas därefter innan den nya publiceringsnoden tar emot trafik.

Avsnitten nedan innehåller mer detaljerad information om innehållsleverans, inklusive CDN-konfiguration och cachning.

Information om replikering från författartjänsten till publiceringstjänsten finns [här](/help/operations/replication.md).
