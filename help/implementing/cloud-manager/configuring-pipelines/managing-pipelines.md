---
title: Hantera pipelines
description: Lär dig hur du hanterar dina befintliga rörledningar, inklusive redigering, körning och borttagning av dem.
index: true
exl-id: 4aff5a84-134a-43fa-8de8-8d564f4edd16
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '928'
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

## Fönstret Pipelines {#pipelines}

The **Pipelines** visas en fullständig lista över alla pipelines för det valda programmet. Detta är användbart eftersom det ger mer omfattande information än vad som finns i [Pipelinekort.](#pipeline-card)

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation och lämpligt program.

1. Från **Programöversikt** väljer du **Pipelines** för att växla till **Pipelines** -fönstret.

1. Här visas en lista med alla pipelines för programmet och hur du startar och stoppar pipelinekörningen som i **Förloppskort**.

Om en pipeline körs håller du pekaren över den **Status** -kolumnen visar information om körningen.

![Information om pipeline-körning](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-status.png)

Tryck eller klicka **Visa detaljer** tar dig till [information om pipelinekörningen.](#view-details)

## Aktivitetsfönster {#activity}

The **Verksamhet** visas en fullständig lista över alla pipelines-körningar för det valda programmet.

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation och lämpligt program.

1. Från **Programöversikt** väljer du **Aktivitet** för att växla till **Aktivitet** -fönstret.

1. Här visas en lista över alla pipeline-körningar för programmet, inklusive aktuella och historiska körningar.

Om en pipeline körs håller du pekaren över den **Status** -kolumnen visar information om körningen.

![Information om pipeline-körning](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-activity.png)

Tryck eller klicka **Visa detaljer** tar dig till [information om pipelinekörningen.](#view-details)

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

   * På följande sidor finns mer information om fälten och konfigurationsalternativen för pipelines.
      * [Konfigurera produktionsförlopp](configuring-production-pipelines.md)
      * [Konfigurera icke-produktionsförlopp](configuring-non-production-pipelines.md)

1. Klicka **Uppdatera** när du är klar med redigeringen.

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

Alla steg i en pipeline-körning visas med de som ännu inte har startats nedtonade. De färdiga stegen visar varaktigheten.

När ett pipeline-steg är klart visas en sammanfattning.

![Stegsammanfattning](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-step.png)

Välj **Visa detaljer** länk för att visa **Varaktighet** -avsnitt. Detta inbegriper den genomsnittliga rörledningens varaktighet på grundval av den historiska trenden för det programmet.

![Varaktighet](/help/implementing/cloud-manager/assets/configure-pipeline/duration.png)

>[!NOTE]
>
>Du kan bara visa information om en pipeline som körs eller har körts minst en gång.

## Avbryt pipelines {#cancel}

Om en pipeline befinner sig i validerings- eller byggarfasen kan du avbryta pipelinekörningen.

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation och lämpligt program.

1. Klicka på ellipsknappen för pipeline som du vill avbryta på sidan med programöversikten **Pipelines** kort.

   ![Avbryta en pipeline](/help/implementing/cloud-manager/assets/cancel-pipeline.png)

1. Välj **Avbryt**.

Du kan även avbryta en pipeline från informationssidan för pipeline.

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation och lämpligt program.

1. Navigera till **Pipelines** -fliken från **Programöversikt** och välj den pipeline som du vill avbryta.

1. Du dirigeras till informationssidan för den aktuella pipelinen.

   ![Avbryt pipeline-information](/help/implementing/cloud-manager/assets/cancel-pipeline-details.png)

1. Välj **Avbryt**.
