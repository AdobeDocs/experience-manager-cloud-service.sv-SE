---
title: Översikt över Cloud Readiness Analyzer
description: Översikt över Cloud Readiness Analyzer
translation-type: ht
source-git-commit: 2064dd6c647780dc149c51b7ff166779ba0a2212
workflow-type: ht
source-wordcount: '256'
ht-degree: 100%

---


# Översikt {#overview-cloud-readiness-analyzer}

Cloud Readiness Analyzer gör det enklare att bedöma beredskap för att gå från en befintlig Adobe Experience Manager-distribution (AEM) till AEM as a Cloud Service.

Verktyget genererar en rapport som identifierar områden med potentiell refaktorisering, vilket är det första steget i övergångsprocessen till AEM as a Cloud Service.

## Rapport från Cloud Readiness Analyzer {#cra-report}

Cloud Readiness Analyzer-rapporten används för att få en övergripande förståelse av den allmänna uppgraderingsberedskapen. Rapporten innehåller information i olika kategorier om saker som måste åtgärdas innan en distribution till AEM as a Cloud Service kan genomföras.

Cloud Readiness Analyzer-rapporten innehåller följande kategorier:

* Programfunktioner som måste refaktoriseras
* Databasobjekt som måste flyttas till en plats som stöds
* Äldre dialogrutor och komponenter i användargränssnittet som måste moderniseras
* Problem med distribution och konfiguration
* AEM 6.x-funktioner som har ersatts av nya funktioner eller som för närvarande inte stöds av AEM as a Cloud Service

Mer information om kategorier och möjliga konsekvenser och lösningar som är kopplade till dessa kategorier finns via länkar i Cloud Readiness Analyzer-rapporten.

>[!NOTE]
>Cloud Readiness Analyzer-rapporten förenklar processen för att beräkna den tid och kostnad som krävs för att gå över till AEM as a Cloud Service genom att tillhandahålla information som annars måste samlas in och utvärderas manuellt.

Du kan även hämta Cloud Readiness Analyzer-rapporten från din AEM-instans. Mer information finns i [Visa Cloud Readiness Analyzer-rapporten](/help/move-to-cloud-service/cloud-readiness-analyzer/using-cloud-readiness-analyzer.md#viewing-report).