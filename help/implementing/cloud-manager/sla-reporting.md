---
title: SLA-rapportering
description: Lär dig hur du kan se hur din AEM fungerar i förhållande till det avtalade serviceavtalet (SLA).
exl-id: 03932415-a029-4703-b44a-f86a87edb328
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---


# SLA-rapportering {#sla-reporting}

Lär dig hur du kan se hur din AEM fungerar i förhållande till det avtalade serviceavtalet (SLA).

## Introduktion {#introduction}

SLA-rapportdata är tillgängliga för alla produktionsprogram via fliken **Rapporter**. Följ de här stegen för att komma åt.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.

1. Välj programmet på konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)**.

1. Navigera till fliken **Rapporter** på sidan **Översikt** med hjälp av sidnavigeringspanelen.

1. Klicka på året du vill se.

![Exempel på SLA-diagram](assets/sla-reporting-1.png)

Rulla markören över en datapunkt för att visa specifika värden för den punkten.

![Visar detaljerade data](assets/sla-reporting-b.png)

## SLA-mått {#sla-metrics}

Diagrammet för det valda året innehåller flera datauppsättningar.

* **Publish-nivåkontrakt** - Detta är det SLA som definieras i ditt kontrakt med Adobe för publiceringsnivån.

* **Faktisk Publish-nivå** - Detta är den uppmätta drifttiden för faktoriseringsincidenter på produktionsnivå som orsakas av Adobe eller Adobe.

* **Författarnivåkontrakt** - Detta är det SLA som definieras i ditt kontrakt med Adobe för författarnivån.

* **Författarnivå faktisk** - Detta är den uppmätta drifttiden för produktionsförfattarens nivåfactoringincidenter som orsakas av Adobe eller Adobe.

## Händelseanalys {#event-analysis}

Avsnittet **Händelseanalys** under diagrammet visar den uppsättning incidenter som har inträffat för programmet under det valda året.

Var och en av incidenterna har ett tidsintervall, en orsak och en uppsättning kommentarer.

![Exempel på händelseanalys](assets/sla-reporting-c.png)

## Uppdateringsintervall {#refresh}

SLA-rapporter ger er insikt i hur väl er AEM produktionsmiljö fungerar och är aktuell, men inte direkt. Generering av SLA-rapporter sker månadsvis och genereras för nya program som markerats som Produktion förra månaden. Det är inte omedelbart. På grund av den här fördröjningen bör du tänka på följande när du granskar din SLA-rapport:

* Det rapporterade SLA-avtalet är det som fanns i början av månaden, även om SLA ändrades under den månaden.
* Om det inte fanns något SLA i början av månaden på grund av att programmet inte existerade då gäller det SLA som existerade den dag programmet skapades.

## Förhandsgranska miljöer {#preview}

Förhandsvisningsmiljön är avsedd som ett verktyg som författare av innehåll kan använda för att verifiera innehållets slutliga upplevelse innan det publiceras. Därför är förhandsvisningsmiljöer inte utformade med hög tillgänglighet och har inget associerat SLA.
