---
title: SLA-rapportering
description: Lär dig hur du kan se hur din AEM fungerar i förhållande till det avtalade serviceavtalet (SLA).
exl-id: 03932415-a029-4703-b44a-f86a87edb328
source-git-commit: 90250c13c5074422e24186baf78f84c56c9e3c4f
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---


# SLA-rapportering {#sla-reporting}

Lär dig hur du kan se hur din AEM fungerar i förhållande till det avtalade serviceavtalet (SLA).

## Introduktion {#introduction}

SLA-rapporteringsdata är tillgängliga för alla produktionsprogram via **Rapporter** -fliken. Följ de här stegen för att komma åt.

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation.

1. På **[Mina program](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#my-programs)** väljer du programmet.

1. Navigera till **Rapporter** -fliken från **Ökning** sida.

1. Klicka på året du vill se.

![Exempel på SLA-diagram](assets/sla-reporting-1.png)

Rulla markören över en datapunkt för att visa specifika värden för den punkten.

![Visa detaljerade data](assets/sla-reporting-b.png)

## SLA-mått {#sla-metrics}

Diagrammet för det valda året innehåller flera datauppsättningar.

* **Publicera nivåkontrakt** - Det här är SLA-avtalet som definieras i ditt avtal med Adobe för publiceringsnivån.

* **Faktisk publiceringsnivå** - Detta är den uppmätta drifttiden för produktionsnivåfaktoriseringsincidenter som orsakas av Adobe eller Adobe.

* **Författaravtal** - Det här är SLA-avtalet som definieras i ditt kontrakt med Adobe för författarnivån.

* **Författarnivå faktisk** - Detta är den uppmätta drifttiden för produktionsförfattarens nivåfactoringincidenter som orsakas av Adobe eller Adobe produktleverantörer.

## Händelseanalys {#event-analysis}

The **Händelseanalys** i diagrammet visar vilka incidenter som har inträffat för programmet under det valda året.

Var och en av incidenterna har ett tidsintervall, en orsak och en uppsättning kommentarer.

![Exempel på händelseanalys](assets/sla-reporting-c.png)
