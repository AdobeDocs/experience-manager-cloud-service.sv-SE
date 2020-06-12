---
title: Använda Cloud Readiness Analyzer
description: Använda Cloud Readiness Analyzer
translation-type: tm+mt
source-git-commit: f0e69dba5d670d141c82e762069f4831c2527dbe
workflow-type: tm+mt
source-wordcount: '506'
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

   ![image](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-1.png)

1. När du klickar på **Cloud Readiness Analyzer** börjar verktyget generera rapporten och efter några minuter visas den genererade rapporten.

   >[!NOTE]
   >Du måste rulla nedåt på sidan för att se hela rapporten.

   ![image](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-2.png)

### Visa resultaten i sammanfattningsrapporten {#viewing-the-results}

>[!IMPORTANT]
>Rapporterna som genereras från Cloud Readiness Analyzer baseras på mönsteridentifierare. Mer information finns i [Mönsteridentifierare](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/upgrading/pattern-detector.html) .

När du rullar nedåt på sidan för att visa den fullständiga sammanfattningsrapporten kan du se följande information för varje kategori som markeras i rapporten:

1. **Prioritetsnivå**

   I följande tabell beskrivs innebörden av de olika prioritetsnivåerna för Mönsteravkännare och Molnberedskapsanalys.

   | Prioritetsnivå | Beskrivning |
   |--- |--- |
   | INFO/0 | Denna slutsats lämnas i informationssyfte. |
   | RÅDGIVNING/1 | Detta kan vara ett uppgraderingsproblem. Ytterligare undersökningar rekommenderas. |
   | MAJOR/2 | Denna slutsats är sannolikt ett uppgraderingsproblem som bör åtgärdas. |
   | KRITISK/3 | Detta är sannolikt ett uppgraderingsproblem som måste åtgärdas för att förhindra funktionsförlust eller prestanda. |

1. **Beskrivning** Beskrivningen innehåller information om den rapporterade kategorin.

1. **Dokumentations-URL** Med dokumentations-URL kan du visa den tekniska dokumentationen för den associerade typen.

1. **Meddelande** En beskrivning av sökningen i ett enda meddelande.

### Visa resultaten i ett CSV-format {#viewing-the-results-csv}

Sammanfattningsrapporten finns i AEM-användargränssnittet. Du kan hämta den fullständiga rapporten i ett kommaseparerat värdeformat (CSV) som är användbart under omfaktoriseringsprocessen.

Följ stegen nedan för att skapa ett CSV-format för sammanfattningsrapporten:

1. 
   1. Välj Adobe Experience Manager och navigera till verktyg -> **Åtgärder** -> **Cloud Readiness Analyzer**.

1. När rapporten har skapats klickar du på **CSV** för att hämta den fullständiga sammanfattningsrapporten i CSV-format (kommaavgränsade värden), vilket visas i bilden nedan.

![image](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-3.png)


#### Visa rapporten i AEM 6.1-instanser {#aem-instances-report}

Du kan hämta CSV-rapporten för AEM 6.1. Detta väntar.

