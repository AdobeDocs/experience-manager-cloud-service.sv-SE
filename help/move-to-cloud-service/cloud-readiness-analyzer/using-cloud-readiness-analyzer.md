---
title: Använda Cloud Readiness Analyzer
description: Använda Cloud Readiness Analyzer
translation-type: tm+mt
source-git-commit: 47773a56f8bb24342281068a8c4d03d6edfb9277
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---


# Använda Cloud Readiness Analyzer {#using-cloud-readiness-analyzer}

## Viktigt att tänka på när du använder molnberedskapsanalysen {#imp-considerations}

Följ avsnittet nedan om du vill veta mer om de viktiga sakerna att tänka på när du kör Cloud Readiness Analyzer (CRA):

* CRA stöds på AEM-källinstanser med version 6.1 och senare
* CRA kan köras i alla miljöer (helst *scenmiljöer* )

   >[!NOTE]
   >För att öka avkänningsfrekvensen och undvika flaskhalsar i affärskritiska instanser rekommenderar vi att CRA körs i källförfattarens stagningsmiljöer som ligger så nära produktionsmiljöer som möjligt när det gäller anpassningar, konfigurationer, innehåll och användarprogram. Den kan även köras på en klon av *publiceringsmiljön* .

## Tillgänglighet {#availability}

Cloud Readiness Analyzer kan laddas ned som en zip-fil från Software Distribution Portal. Du kan installera paketet via Package Manager på din källinstans av Adobe Experience Manager (AEM).

>[!NOTE]
>Hämta Cloud Readiness Analyzer från portalen för programvarudistribution som *väntar*.

## Köra Cloud Readiness Analyzer {#running-tool}

Följ det här avsnittet för att lära dig hur du kör Cloud Readiness Analyzer:

1. Välj Adobe Experience Manager och navigera till verktyg -> **Åtgärder** -> **Cloud Readiness Analyzer**.

### Visa resultaten {#viewing-the-results}

>[!IMPORTANT]
>Rapporterna som genereras från Cloud Readiness Analyzer baseras på mönsteridentifierare. Mer information finns i [Mönsteridentifierare](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/upgrading/pattern-detector.html) .

Det finns två sätt att visa utdata från Cloud Readiness Analyzer:

1. **Använda den sorterade rapporten**

   >[!NOTE]
   >Den ordnade rapporten finns på AEM version 6.3 och senare.

   Eller

1. **Visa CRA:s utdata**

   Följ stegen nedan för att visa utdata från Cloud Readiness Analyzer:

   >[!NOTE]
   >Stegen nedan gäller för AEM version 6.1 och senare.

   1. Navigera till **AEM Web Console** med `https://serveraddress:serverport/system/console/configMgr`.

   1. Välj **Status - Mönsteravkännare** enligt bilden nedan.

#### Visa rapporten i AEM 6.1-instanser {#aem-instances-report}

Du kan hämta CSV-rapporten för AEM 6.1. Detta väntar.

#### Om prioritetsnivåer i rapporten {#importance-levels}

I följande tabell beskrivs innebörden av de olika prioritetsnivåerna för Mönsteravkännare och Molnberedskapsanalys.

| Prioritetsnivå | Beskrivning |
|--- |--- |
| INFO/0 | Denna slutsats lämnas i informationssyfte. |
| RÅDGIVNING/1 | Detta kan vara ett uppgraderingsproblem. Ytterligare undersökningar rekommenderas. |
| MAJOR/2 | Denna slutsats är sannolikt ett uppgraderingsproblem som bör åtgärdas. |
| KRITISK/3 | Detta är sannolikt ett uppgraderingsproblem som måste åtgärdas för att förhindra funktionsförlust eller prestanda. |