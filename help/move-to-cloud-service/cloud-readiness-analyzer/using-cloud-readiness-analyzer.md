---
title: Använda Cloud Readiness Analyzer
description: Använda Cloud Readiness Analyzer
translation-type: tm+mt
source-git-commit: 317dd08600df9c7127cf8502341f93758ac8ce0b
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---


# Använda Cloud Readiness Analyzer {#using-cloud-readiness-analyzer}

## Viktigt att tänka på när du använder molnberedskapsanalysen {#imp-considerations}

Följ avsnittet nedan om du vill veta mer om de viktiga sakerna att tänka på när du kör Cloud Readiness Analyzer (CRA):

* CRA stöds på AEM-källinstanser med version 6.1 och senare.
* CRA kan köras i alla miljöer. För att öka avkänningshastigheten och undvika flaskhalsar i affärskritiska instanser rekommenderar vi att du kör programmet i källförfattarens miljöer som ligger så nära produktionsmiljöer som möjligt när det gäller anpassningar, konfigurationer, innehåll och användarprogram. Den kan också köras på en klon av publiceringsmiljön.

## Tillgänglighet {#availability}

Cloud Readiness Analyzer (CRA) kan hämtas som en zip-fil från Software Distribution Portal. Du kan installera paketet via Package Manager på din källinstans av Adobe Experience Manager (AEM).

>[!NOTE]
>Hämta Cloud Readiness Analyzer (CRA) från väntande.

## Köra Cloud Readiness Analyzer {#running-tool}

Följ det här avsnittet för att lära dig hur du kör Cloud Readiness Analyzer:

1. Välj Adobe Experience Manager och navigera till verktyg -> **Åtgärder** -> **Cloud Readiness Analyzer**.

### Visa resultaten {#viewing-the-results}

Det finns två sätt att visa CRA-utdata:

1. Använd den ordnade rapporten (tillgänglig i AEM version 6.3 och senare)Se CRA Document Planning and Status för att beskriva viktiga nivåer i rapporten

Så här visar du CRA-utdata (kan användas med AEM version 6.1 och senare):

1. Navigera till AEM Web Console genom att gå till.

1. Välj Status - Cloud Readiness Analyzer enligt bilden nedan.