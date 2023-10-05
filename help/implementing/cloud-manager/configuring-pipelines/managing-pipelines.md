---
title: Hantera pipelines
description: Lär dig hur du hanterar dina befintliga rörledningar, inklusive redigering, körning och borttagning av dem.
index: true
exl-id: 4aff5a84-134a-43fa-8de8-8d564f4edd16
source-git-commit: b8d692e354851a31b4f66b24135c863b5ca723b4
workflow-type: tm+mt
source-wordcount: '667'
ht-degree: 0%

---


# Hantera pipelines {#managing-pipelines}

Lär dig hur du hanterar dina befintliga rörledningar, inklusive redigering, körning och borttagning av dem.

## Pipeline-kort {#pipeline-card}

The **Pipelines** på **Programöversikt** i Cloud Manager ger dig en översikt över alla dina pipelines och deras aktuella status.

![Förloppskort i Cloud Manager](/help/implementing/cloud-manager/assets/configure-pipeline/pipelines-card.png)

Genom att klicka på ellipsknappen bredvid varje pipeline kan du utföra följande åtgärder.

* [Kör pipeline](#running-pipelines)
* [Redigera pipeline](#editing-pipelines)
* [Ta bort pipeline](#deleting-pipelines)
* [Visa detaljer](#view-details)

Längst ned i listan med rörledningar finns allmänna alternativ.

* **Lägg till** - Till [lägg till en ny produktionspipeline](configuring-production-pipelines.md) eller [lägga till ny icke-produktionspipeline](configuring-non-production-pipelines.md)
* **Visa alla** - Tar användaren till skärmen Pipelines för att visa alla pipelines i en mer detaljerad tabell.
* **Åtkomst till svarsinformation** - Visar den information som krävs för att komma åt Cloud Managers Git-databas
* **Läs mer** - Navigerar till CI/CD pipeline-dokumentationsresurser.

## Löpande rörledningar {#running-pipelines}

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation och lämpligt program.

1. Navigera till **Pipelines** från **Programöversikt** och klicka på ellipsknappen bredvid den pipeline du kör, välj **Kör** på menyn.

1. Pipeline-körningen börjar och anges av **Status** kolumn.

Du kan se information om körningen genom att klicka på ellipsknappen igen och välja **[Visa information.](#view-details)**

Beroende på typen av pipeline kan du eventuellt avbryta körningen genom att klicka på ellipsknappen igen och välja **Avbryt**.

## Redigera rörledningar {#editing-pipelines}

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation och lämpligt program.

1. Navigera till **Pipelines** från **Programöversikt** och klicka på ellipsknappen bredvid den pipeline du vill redigera och välj sedan **Redigera** på menyn.

1. The **Redigera produktionspipeline** eller **Redigera icke-produktionsförlopp** visas så att du kan redigera samma information som du angav när du skapade pipelinen.

   * På följande sidor finns mer information om alla fält och konfigurationsalternativ som är tillgängliga för pipelines.
      * [Konfigurera produktionsförlopp](configuring-production-pipelines.md)
      * [Konfigurera icke-produktionsförlopp](configuring-non-production-pipelines.md)

1. Klicka på **Uppdatera** när du är klar med redigeringen.

>[!NOTE]
>
>Du kan inte redigera en pågående pipeline.

## Tar bort pipelines {#deleting-pipelines}

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation och lämpligt program.

1. Navigera till **Pipelines** från **Programöversikt** och klicka på ellipsknappen bredvid den pipeline du kör, välj **Ta bort** på menyn.

>[!NOTE]
>
>Du kan inte ta bort en pågående pipeline.

## Visa information om pipeline {#view-details}

Du kan visa information om en pipeline för att se status och loggar för den senaste körningen.

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation och lämpligt program.

1. Navigera till **Pipelines** från **Programöversikt** och klicka på ellipsknappen bredvid den pipeline du kör, välj **Visa detaljer** på menyn.

1. Du dirigeras till informationssidan för den aktuella pipelinen.

![Information om pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-running-details.png)

Här kan du se status för de olika stegen i pipeline och hämta byggloggar för diagnostik. Se dokumentet [Distribuera koden](/help/implementing/cloud-manager/deploy-code.md) för mer information om koddistribution och testkörning.

>[!NOTE]
>
>Du kan bara visa information om en pipeline som körs eller har körts minst en gång.

## Avbryt pipelines {#cancel}

Om en pipeline befinner sig i validerings- eller byggarfasen kan du avbryta pipelinekörningen.

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation och lämpligt program.

1. Klicka på ellipsknappen för pipeline som du vill avbryta på sidan med programöversikten **Pipelines** kort.

   ![Avbryta en pipeline](/help/implementing/cloud-manager/assets/cancel-pipeline.png)

1. Tryck eller klicka **Avbryt**.

Du kan även avbryta en pipeline från informationssidan för pipeline.

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation och lämpligt program.

1. Navigera till **Pipelines** -fliken från **Programöversikt** och tryck eller klicka på den pipeline som du vill avbryta.

1. Du dirigeras till informationssidan för den aktuella pipelinen.

   ![Avbryt pipeline-information](/help/implementing/cloud-manager/assets/cancel-pipeline-details.png)

1. Tryck eller klicka **Avbryt**.
