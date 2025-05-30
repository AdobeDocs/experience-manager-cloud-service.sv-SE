---
title: Översikt över Best Practices Analyzer
description: Lär dig hur du använder Best Practices Analyzer för att bedöma om din AEM-implementering uppfyller de rekommenderade bästa metoderna
exl-id: 46c567f8-91e2-4d85-98bd-61d183b887d5
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 27%

---

# Ökning {#overview-best-practices-analyzer}

>[!CONTEXTUALHELP]
>id="aemcloud_bpa_overview"
>title="Översikt över Best Practices Analyzer"
>abstract="Best Practices Analyzer ger en bedömning av din nuvarande AEM-implementering genom att ange områden som inte följer AEM bästa praxis. Där finns också vägledning om nästa steg för att anta AEM bästa praxis. Dessutom går det snabbare att bedöma om man är redo att gå över från en befintlig Adobe Experience Manager-driftsättning (AEM) till AEM as a Cloud Service."

Best Practices Analyzer ger en bedömning av din nuvarande AEM-implementering genom att ange områden som inte följer AEM bästa praxis. Där finns också vägledning om nästa steg för att anta AEM bästa praxis. Dessutom går det snabbare att bedöma om man är redo att gå över från en befintlig Adobe Experience Manager-driftsättning (AEM) till AEM as a Cloud Service.

Verktyget genererar en rapport som identifierar områden med potentiell refaktorisering, vilket är det första steget i övergångsprocessen till AEM as a Cloud Service.

## Best Practices Analyzer Report {#bpa-report}

Best Practices Analyzer-rapporten används för att få en god förståelse för den allmänna uppgraderingsberedskapen. Rapporten innehåller information i olika kategorier om saker som måste åtgärdas innan en distribution till AEM as a Cloud Service kan genomföras.

Rapporten Best Practices Analyzer innehåller följande kategorier:

* Programfunktioner som måste refaktoriseras
* Databasobjekt som måste flyttas till en plats som stöds
* Äldre dialogrutor och komponenter i användargränssnittet som måste moderniseras
* Problem med distribution och konfiguration
* AEM 6.x-funktioner som har ersatts av nya funktioner eller som för närvarande inte stöds av AEM as a Cloud Service

Mer information om kategorierna och eventuella konsekvenser och lösningar som är kopplade till dessa kategorier finns via länkar i rapporten Best Practices Analyzer.

>[!NOTE]
>Rapporten Best Practices Analyzer snabbar upp processen att beräkna den tid och kostnad som krävs för övergången till AEM as a Cloud Service genom att tillhandahålla information som annars skulle behöva samlas in och utvärderas manuellt.

Du kan även hämta rapporten Best Practices Analyzer från din AEM-instans. Mer information finns i [Visa rapporten om Best Practices Analyzer](/help/journey-migration/best-practices-analyzer/using-best-practices-analyzer.md#viewing-report).
