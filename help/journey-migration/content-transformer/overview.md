---
title: Översikt över innehållstransformeraren
description: Översikt över innehållstransformeraren
source-git-commit: 55eedd342f048e19bad5c6fbfdd16a468ff1f4f9
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---

# Översikt {#overview-ct}

CT (Content Transformer) är ett verktyg som utvecklats av Adobe och som kan användas för att automatiskt upptäcka och åtgärda innehållsrelaterade problem som rapporterats av [Best Practices Analyzer (BPA)](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md) innan du migrerar innehåll från den aktuella AEM-implementeringen (lokal eller Managed Services) till AEM as a Cloud Service.

Innehållsomvandlaren kan hjälpa dig att lösa problem som kan uppstå under följande [Kategorier för BPA-mönster](https://experienceleague.adobe.com/docs/experience-manager-pattern-detection/table-of-contents/aso.html) (visas i tabellen nedan) genom att tillåta användare att utföra massåtgärder som att flytta eller ta bort. Detta kan avsevärt minska tiden och minska komplexiteten i ett migreringsprojekt.

## Mönsterkategorier som omfattas av Content Transformer och föreslagna lösningar {#pattern-categories-and-benefits}

| Mönsterkod | Suspicion Type / Subtype | Potentiell korrigering innan innehåll migreras till AEM as a Cloud Service |
|--------------|--------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------|
| ACV | missing.jcrcontent <br> missing.original.rendering <br> metadata.descendants.errors | Flytta dessa resurser till en annan plats eller ta bort dem för att vara säker på att de inte migreras till AEM as a Cloud Service. |
| CAV | content.area.violation | Flytta banorna tillfälligt till `/etc/packages/content-transformation/paths` för att säkerställa att de inte migreras till AEM as a Cloud Service. |
| DOPI | deprecated.ordered.index | Ta bort de föråldrade indexen. |
| OAUI | non.migrated.oauth.users | Ta bort de här användarna för att se till att de inte migreras till AEM as a Cloud Service. |
| PCX | page.complex.medium <br> page.complex.high | Ta bort sidor/underordnade sidor eller flytta dem till en annan plats för att vara säker på att de inte migreras till AEM as a Cloud Service. |
| REP | forward.replication <br> reverse.replication <br> standard.replication.agent.modification <br> custom.replication.agent.detection | Ta bort de replikeringsagenter som nyligen har skapats. <br> ELLER <br> Ta bort de ändrade/tillagda egenskaperna. |
| URS | clientlibs.location <br> file.location <br> node.location <br> workflow.location | Gå till rätt plats för att undvika problem under migreringen. |
| URS | node.size | Flytta noderna tillfälligt till`/etc/packages/content-transformation/paths` för att säkerställa att de inte migreras till AEM as a Cloud Service. |

## Fördelar med Content Transformer {#benefits}

Innehållstransformeraren har följande fördelar:

* Felsäker: ett paket skapas av innehållstreraren varje gång den gör ändringar i databasen för att åtgärda problem. Om det behövs kan du återgå till det tidigare läget genom att installera paketet.
* Lättanvänt: Content Transformer har integrerats med Content Transfer Tool och har ett enkelt, intuitivt användargränssnitt.
* Sparar tid: När du har ett stort antal innehållsproblem som faller under en mönsterkategori kan du lösa alla med bara ett par klick med hjälp av Innehållsomvandlaren.
