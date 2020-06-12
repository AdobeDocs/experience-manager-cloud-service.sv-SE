---
title: Översikt över Cloud Readiness Analyzer
description: Översikt över Cloud Readiness Analyzer
translation-type: tm+mt
source-git-commit: 64b685a7c9fbb105ed66dc4b3212b2bf91dee4af
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 0%

---


# Översikt {#overview-cloud-readiness-analyzer}

Cloud Readiness Analyzer hjälper till att snabba upp processerna för att bedöma beredskap att gå över från en befintlig Adobe Experience Manager-distribution (AEM) till AEM som en molntjänst.

Det här verktyget genererar en rapport som identifierar områden med potentiell omfaktorisering, vilket är det första steget i övergången till AEM som en molntjänst.

## Sammanfattningsrapport i Cloud Readiness Analyzer {#summary-report}

Sammanfattningsrapporten för Cloud Readiness Analyzer används för att få en bättre förståelse för den allmänna uppgraderingsberedskapen. Rapporten innehåller information i olika problemkategorier som måste åtgärdas innan en lyckad distribution till AEM som molntjänst kan genomföras.

Sammanfattningsrapporten innehåller följande kategorier:

* Programfunktioner som måste ändras
* Databasobjekt som måste flyttas till en plats som stöds
* Äldre dialogrutor och komponenter i användargränssnittet som måste moderniseras
* Problem med distribution och konfiguration
* AEM 6.x-funktioner som har ersatts av nya funktioner eller som för närvarande inte stöds av AEM som molntjänst

Ytterligare information om kategorierna och eventuella konsekvenser och lösningar som är kopplade till dessa kategorier finns via länkar i den sammanfattande rapporten.

>[!NOTE]
>Rapporten Cloud Readiness Analyzer snabbar upp processen att beräkna den tid och kostnad som krävs för att gå över till AEM som molntjänst genom att tillhandahålla information som annars skulle behöva samlas in och utvärderas manuellt.

Sammanfattningsrapporten finns i AEM-användargränssnittet. Det finns ett alternativ för att hämta den fullständiga rapporten i ett kommaavgränsat värdeformat (CSV) som är användbart under omfaktoriseringsprocessen.