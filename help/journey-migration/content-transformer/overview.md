---
title: Översikt över innehållstransformeraren
description: Lär dig hur du identifierar och åtgärdar innehållsrelaterade problem som rapporteras av BPA med hjälp av Content Transformer.
exl-id: aa3397ff-3dd6-4c67-9064-cb9b19bf1c73
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 0%

---

# Ökning {#overview-ct}

CT (Content Transformer) är ett verktyg som utvecklats av Adobe och som kan användas för att automatiskt identifiera och åtgärda innehållsrelaterade problem som rapporterats av [Best Practices Analyzer ](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md) innan innehåll migreras från den aktuella AEM (lokal eller Managed Services) till AEM as a Cloud Service.

Innehållstransformeraren kan hjälpa till att lösa problem som faller under följande [BPA-mönsterkategorier](https://experienceleague.adobe.com/docs/experience-manager-pattern-detection/table-of-contents/aso.html) (visas i tabellen nedan) genom att tillåta användare att utföra massåtgärder som att flytta eller ta bort. Detta kan avsevärt minska tiden och minska komplexiteten i ett migreringsprojekt.

## Mönsterkategorier som omfattas av Content Transformer och föreslagna lösningar {#pattern-categories-and-benefits}

| Mönsterkod | Suspicion Type / Subtype | Potentiell korrigering innan du migrerar innehåll till AEM as a Cloud Service |
|--------------|--------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------|
| ACV | missing.jcrcontent <br> missing.original.rendition <br> metadata.descendants.Violate | Flytta dessa resurser till en annan plats eller ta bort dem för att vara säker på att de inte migreras till AEM as a Cloud Service. |
| CAV | content.area.violation | Flytta sökvägarna tillfälligt till `/etc/packages/content-transformation/paths` för att se till att de inte migreras till AEM as a Cloud Service. |
| DOPI | deprecated.ordered.index | Ta bort de föråldrade indexen. |
| OAUI | non.migrated.oauth.users | Ta bort de här användarna för att vara säker på att de inte migreras till AEM as a Cloud Service. |
| PCX | page.complex.medium <br> page.complex.high | Ta bort sidor/underordnade sidor eller flytta dem till en annan plats för att vara säker på att de inte migreras till AEM as a Cloud Service. |
| REP | forward.replication <br> reverse.replication <br> standard.replication.agent.modification <br> custom.replication.agent.detection | Ta bort de skapade replikeringsagenterna. <br> ELLER <br> Ta bort de ändrade/tillagda egenskaperna. |
| URS | clientlibs.location <br> file.location <br> node.location <br> workflow.location | Gå till rätt plats för att undvika problem under migreringen. |
| URS | node.size | Flytta noderna tillfälligt till `/etc/packages/content-transformation/paths` för att kontrollera att de inte migreras till AEM as a Cloud Service. |

## Fördelar med Content Transformer {#benefits}

Innehållstransformeraren har följande fördelar:

* Felsäker: ett paket skapas av innehållstreraren varje gång det ändras i databasen för att åtgärda problem. Om det behövs kan du återgå till det tidigare läget genom att installera paketet.
* Lättanvänt: Content Transformer har integrerats med Content Transfer Tool och har ett enkelt, intuitivt användargränssnitt.
* Sparar tid: när du har ett stort antal innehållsproblem som faller under en mönsterkategori kan du lösa dem alla med flera klick med hjälp av Innehållsomvandlaren.
