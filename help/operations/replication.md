---
title: Replikering
description: Distribution och felsökning av replikering.
translation-type: tm+mt
source-git-commit: abb45225e880f3d08b9d26c29e243037564acef0
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 2%

---


# Replikering {#replication}

Adobe Experience Manager som Cloud Service använder funktionen [Sling Content Distribution](https://sling.apache.org/documentation/bundles/content-distribution.html) för att flytta innehållet som ska replikeras till en pipeline-tjänst som körs på Adobe I/O utanför AEM.

>[!NOTE]
>
>Läs [Distribution](/help/core-concepts/architecture.md#content-distribution) för mer information.

## Metoder för publicering av innehåll {#methods-of-publishing-content}

### Snabb borttagning/publicering - planerad avstängning/publicering {#publish-unpublish}

De här AEM standardfunktionerna för författarna ändras inte med AEM Cloud Service.

### På- och avaktiveringstider - utlösarkonfiguration {#on-and-off-times-trigger-configuration}

Ytterligare möjligheter för **På-tid** och **Fråntid** finns på fliken [Grundläggande i Sidegenskaper](/help/sites-cloud/authoring/fundamentals/page-properties.md#basic).

Om du vill genomföra den automatiska replikeringen för detta måste du aktivera **automatisk replikering** i [OSGi-konfigurationen](/help/implementing/deploying/configuring-osgi.md) **vid utlösarkonfiguration**:

![Konfiguration av OSGi på av utlösare](/help/operations/assets/replication-on-off-trigger.png)

### Aktivering av träd {#tree-activation}

Så här utför du en trädaktivering:

1. Navigera AEM Start-menyn till **Verktyg > Distribution > Distribution**
2. Välj kortet **forwardPublisher**
3. I användargränssnittet för webbkonsolen **väljer du Distribuera**

   ![](assets/distribute.png "DistribueraDistribuera")
4. Markera sökvägen i sökvägsläsaren, välj att lägga till en nod, ett träd eller att ta bort efter behov och välj **Skicka**

## Felsökning {#troubleshooting}

Om du vill felsöka replikering går du till replikeringsköerna i webbgränssnittet för AEM Author Service:

1. Navigera AEM Start-menyn till **Verktyg > Distribution > Distribution**
2. Välj kortet **forwardPublisher**
   ![](assets/status.png "StatusStatus")
3. Kontrollera köstatusen som ska vara grön
4. Du kan testa anslutningen till replikeringstjänsten
5. Välj fliken **Loggar** som visar historiken för innehållspublikationer

![](assets/logs.png "LogsLogs")

Om innehållet inte kunde publiceras återställs hela publikationen från AEM Publish Service.
I så fall bör köerna ses över för att identifiera vilka objekt som orsakade att offentliggörandet avbröts. Om du klickar på en kö med röd status visas kön med väntande objekt, från vilken enskilda eller alla objekt kan rensas vid behov.
