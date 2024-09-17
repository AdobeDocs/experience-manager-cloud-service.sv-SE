---
title: SLA Reports
description: Lär dig hur du kan se hur din AEM fungerar i förhållande till det avtalade servicenivåavtalet.
exl-id: 03932415-a029-4703-b44a-f86a87edb328
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: c46b6df488722fe750e524ad2bb383f25bf00b0f
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---


# SLA Reports {#sla-reporting}

Lär dig hur du kan se hur din AEM presterar i förhållande till den avtalade SLA (servicenivåavtal).

## Visa en SLA-rapport {#introduction}

SLA rapportdata spårar resultatvärden för två produktionsnivåer: Författarnivå och Publish Tier.

Raddiagrammet för ett valt år innehåller datapunkter för varje månad från januari till december. Följande mätvärden spåras.

| Spårat mått | Linjefärg | Beskrivning |
| --- | --- | --- |
| Författarnivå faktisk | Ljusgrön | Den uppmätta drifttiden för tillverkningsutvecklarens fasfactoringincidenter som orsakas av Adobe eller Adobe. |
| Författaravtal | Mörk blå | SLA som definieras i ditt avtal med Adobe för Author Tier. |
| Publish Tier Actual | Orange | Den uppmätta drifttiden för produktionen av Publish Tier, factoringincidenter som orsakas av Adobe eller Adobe. |
| Publish Tier Contract | Röd | SLA som definieras i ditt avtal med Adobe för Publish Tier. |

**Så här visar du en SLA-rapport:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.

1. Välj programmet på konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)**.

1. Klicka på **Rapporter** på sidan **Programöversikt** i den vänstra navigeringspanelen.

1. Klicka på **SLA Reports**.

   ![SLA rapportlinjediagram](/help/implementing/cloud-manager/assets/cm-sla-report.png)

1. Klicka på året när du vill se ett linjediagram över SLA-data.

1. (Valfritt) Gör något av följande:

   * Rulla markören över en datapunkt i linjediagrammet för att visa specifika värden för den punkten.
   * Under linjediagrammets årtal klickar du på ikonen Hämta för att spara en PNG-bildfil av linjediagrammet.
   * Klicka på ett måttnamn om du bara vill se måttets data. Du kan också trycka på `Shift` på tangentbordet när du markerar eller avmarkerar ett eller flera mätnamn.

   ![Visar detaljerade data](/help/implementing/cloud-manager/assets/cm-sla-download.png)

## Händelseanalys {#event-analysis}

Avsnittet **Händelseanalys** under diagrammet visar den uppsättning incidenter som har inträffat för programmet under det valda året.

Var och en av incidenterna har ett tidsintervall, en orsak och en uppsättning kommentarer.

![Exempel på händelseanalys](assets/sla-reporting-c.png)

## Uppdateringsintervall för SLA-rapporter {#refresh}

SLA rapportering ger er insikt i hur väl er AEM produktionsmiljö fungerar och är aktuell, men inte direkt. SLA rapportgenerering sker månadsvis och genereras för nya program som markerats som `Production previous month`. Det är inte omedelbart. På grund av den här fördröjningen bör du tänka på följande när du granskar din SLA-rapport:

* Den rapporterade SLA-versionen är den som fanns i början av månaden, även om SLA ändrades under den månaden.
* Om det inte fanns någon SLA i början av månaden på grund av att programmet inte existerade gäller den SLA som existerade den dag då programmet skapades.

## Förhandsvisningsmiljöer {#preview}

Förhandsvisningsmiljön är avsedd som ett verktyg som författare av innehåll kan använda för att verifiera innehållets slutliga upplevelse innan det publiceras. På grund av den här funktionaliteten är förhandsvisningsmiljöer inte utformade med hög tillgänglighet och har inte någon tillhörande SLA.
