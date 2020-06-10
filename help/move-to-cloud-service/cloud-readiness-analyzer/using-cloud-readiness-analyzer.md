---
title: Använda Cloud Readiness Analyzer
description: Använda Cloud Readiness Analyzer
translation-type: tm+mt
source-git-commit: 3d818278c53f3d3b4c5b53aa5b78d06d876bf05f
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---


# Använda Cloud Readiness Analyzer {#using-cloud-readiness-analyzer}

## Viktigt att tänka på när du använder molnberedskapsanalysen {#imp-considerations}

Följ avsnittet nedan om du vill veta mer om de viktiga sakerna att tänka på när du kör Cloud Readiness Analyzer (CRA):

* CRA stöds på AEM-källinstanser med version 6.1 och senare.
* CRA kan köras i alla miljöer.

   >[!NOTE]
   >För att öka avkänningsfrekvensen och undvika flaskhalsar i affärskritiska instanser rekommenderar vi att CRA körs i källförfattarens stagningsmiljöer som ligger så nära produktionsmiljöer som möjligt när det gäller anpassningar, konfigurationer, innehåll och användarprogram. Den kan också köras på en klon av publiceringsmiljön.

## Tillgänglighet {#availability}

Cloud Readiness Analyzer (CRA) kan hämtas som en zip-fil från Software Distribution Portal. Du kan installera paketet via Package Manager på din källinstans av Adobe Experience Manager (AEM).

>[!NOTE]
>Hämta Cloud Readiness Analyzer (CRA) från *väntande*.

## Köra Cloud Readiness Analyzer {#running-tool}

Följ det här avsnittet för att lära dig hur du kör Cloud Readiness Analyzer:

1. Välj Adobe Experience Manager och navigera till verktyg -> **Åtgärder** -> **Cloud Readiness Analyzer**.

### Visa resultaten {#viewing-the-results}

Det finns två sätt att visa CRA-utdata:

1. Använda den strukturerade rapporten

   >[!NOTE]
   >Den ordnade rapporten finns på AEM version 6.3 och senare.

Se CRA-dokumentplanering och status för att beskriva prioritetsnivåer i rapporten

1. Visa CRA-utdata (kan användas med AEM version 6.1 och senare):

   1. Navigera till AEM Web Console genom att gå till.

   1. Välj Status - Cloud Readiness Analyzer enligt bilden nedan.

#### Om prioritetsnivåer i rapporten {#importance-levels}

I följande tabell beskrivs innebörden av de olika prioritetsnivåerna för Mönsteravkännare och Molnberedskapsanalys.

| Prioritetsnivå | Beskrivning |
|--- |--- |
| INFO/0 | Denna slutsats lämnas i informationssyfte. |
| RÅDGIVNING/1 | Detta kan vara ett uppgraderingsproblem. Ytterligare undersökningar rekommenderas. |
| MAJOR/2 | Denna slutsats är sannolikt ett uppgraderingsproblem som bör åtgärdas. |
| KRITISK/3 | Detta är sannolikt ett uppgraderingsproblem som måste åtgärdas för att förhindra funktionsförlust eller prestanda. |