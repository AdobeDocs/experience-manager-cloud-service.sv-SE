---
title: Replikering
description: Distribution och felsökning av replikering.
translation-type: tm+mt
source-git-commit: 8fba31951276d7e0de1f3bd079e42e431edaff4e
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 3%

---


# Replikering {#replication}

Adobe Experience Manager som molntjänst använder funktionen [Sling Content Distribution](https://sling.apache.org/documentation/bundles/content-distribution.html) för att flytta innehållet som ska replikeras till en pipeline-tjänst som körs på Adobe I/O utanför AEM-miljön.

>[!NOTE]
>
> Läs [Distribution](/help/core-concepts/architecture.md#content-distribution) för mer information.

## Metoder för publicering av innehåll {#methods-of-publishing-content}

### Snabb borttagning/publicering - planerad avstängning/publicering {#publish-unpublish}

Dessa AEM-standardfunktioner för författarna ändras inte med AEM Cloud-tjänsten.

### Aktivering av träd {#tree-activation}

Så här utför du en trädaktivering:

1. Navigera från AEM Start-menyn till **Verktyg > Distribution > Distribution**
2. Välj kortet **forwardPublisher**
3. I användargränssnittet för webbkonsolen **väljer du Distribuera**
   ![](assets/distribute.png "DistribueraDistribuera")
4. Markera sökvägen i sökvägsläsaren, välj att lägga till en nod, ett träd eller att ta bort efter behov och välj **Skicka**

## Felsökning {#troubleshooting}

Om du vill felsöka replikering går du till replikeringsköerna i webbgränssnittet för AEM Author Service:

1. Navigera från AEM Start-menyn till **Verktyg > Distribution > Distribution**
2. Välj kortet **forwardPublisher**
   ![](assets/status.png "StatusStatus")
3. Kontrollera köstatusen som ska vara grön
4. Du kan testa anslutningen till replikeringstjänsten
5. Välj fliken **Loggar** som visar historiken för innehållspublikationer

![](assets/logs.png "LogsLogs")

Om innehållet inte kunde publiceras återställs hela publikationen från AEM Publish Service.
I så fall bör köerna ses över för att identifiera vilka objekt som orsakade att offentliggörandet avbröts. Om du klickar på en kö med röd status visas kön med väntande objekt, från vilken enskilda eller alla objekt kan rensas vid behov.
