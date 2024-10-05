---
title: Hantera pipelines
description: Lär dig hur du hanterar dina befintliga rörledningar, inklusive redigering, körning och borttagning av dem.
index: true
exl-id: 4aff5a84-134a-43fa-8de8-8d564f4edd16
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 500e1b78fb9688601848fc17f312fc23be83bcb0
workflow-type: tm+mt
source-wordcount: '1109'
ht-degree: 0%

---


# Hantera pipelines {#managing-pipelines}

Lär dig hur du hanterar dina befintliga rörledningar, inklusive redigering, körning och borttagning av dem.

## Pipeline-kort {#pipeline-card}

Kortet **Pipelines** på sidan **Programöversikt** i Cloud Manager ger dig en översikt över alla dina pipelines och deras aktuella status.

![Förloppskort i Cloud Manager](/help/implementing/cloud-manager/assets/configure-pipeline/pipelines-card.png)

Genom att klicka på ellipsknappen bredvid varje pipeline kan du utföra följande åtgärder.

* [Kör pipeline](#running-pipelines)
* [Redigera pipeline](#editing-pipelines)
* [Ta bort pipeline](#deleting-pipelines)
* [Visa detaljer](#view-details)

Längst ned i listan med rörledningar finns allmänna alternativ.

* **Lägg till** - Om du vill [lägga till en ny produktionspipeline](configuring-production-pipelines.md) eller [lägga till ny icke-produktionspipeline](configuring-non-production-pipelines.md)
* **Visa alla** - Tar användaren till skärmen Pipelines för att visa alla pipelines i en mer detaljerad tabell.
* **Åtkomst till repo-information** - Visar den information som krävs för åtkomst till Cloud Manager Git-databasen
* **Läs mer** - Navigerar till resurser för pipeline-dokumentation för CI/CD.

## Fönstret Pipelines {#pipelines}

I fönstret **Pipelines** visas en fullständig lista över alla pipelines för det valda programmet. Detta är användbart eftersom det ger mer omfattande information än vad som finns tillgängligt i [pipeline-kortet](#pipeline-card).

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.

1. Välj programmet på konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)**.

1. Gå till sidan **Programöversikt** och välj fliken **Pipelines** för att växla till fönstret **Pipelines**.

1. Här visas en lista med alla pipelines för programmet och du kan starta och stoppa pipelinekörning på samma sätt som i **pipelines-kortet**.

Om en pipeline körs visas information om körningen om du klickar på informationsikonen i kolumnen **Status** .

![Information om pipeline-körning](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-status.png)

Om du klickar på **Visa information** visas [information om pipelinekörningen](#view-details).

Du kan också klicka på ellipsknappen för pipelinen om du vill vidta ytterligare åtgärder som är lämpliga för pipelineläget, till exempel [redigera](#editing-pipelines) det eller [avbryta körningen](#cancel).

![Pipeline-åtgärder](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-actions.png)

## Aktivitetsfönster {#activity}

Fönstret **Aktivitet** visar en fullständig lista över alla pipelines-körningar för det valda programmet samt andra viktiga programhändelser.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. På sidan **Programöversikt** väljer du fliken **Aktivitet** för att växla till fönstret **Aktivitet** .

1. Här visas en lista över alla pipeline-körningar för programmet, inklusive aktuella och historiska körningar.

Om en pipeline körs visas information om körningen om du klickar på informationsikonen i kolumnen **Status** .

![Information om pipeline-körning](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-activity.png)

Om du trycker eller klickar på raden som representerar pipelinekörningen kommer du till [informationen för pipelinekörningen](#view-details).

Du kan också klicka på ellipsknappen om du vill vidta ytterligare åtgärder för pipelinekörningen, till exempel visa information om den eller hämta loggen, som tar dig till [informationssidan för pipeline](#view-details).

![Körningsåtgärder för pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-execution-actions.png)

## Löpande rörledningar {#running-pipelines}

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. Navigera till kortet **Pipelines** på sidan **Programöversikt** och klicka på ellipsknappen bredvid den pipeline du kör. Välj **Kör** på menyn.

1. Pipeline-körningen börjar och anges av kolumnen **Status**.

Du kan se information om körningen genom att klicka på ellipsknappen igen och välja **[Visa information](#view-details)**.

Beroende på typen av pipeline kan du eventuellt avbryta körningen genom att klicka på ellipsknappen igen och välja **Avbryt**.

## Redigera en pipeline {#editing-pipelines}

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. Navigera till kortet **Pipelines** på sidan **Programöversikt** och klicka på ellipsknappen bredvid den pipeline du vill redigera och välj sedan **Redigera** på menyn.

1. Dialogrutan **Redigera produktionspipeline** eller **Redigera icke-produktionspipeline** visas. Du kan redigera samma information som du angav när du skapade pipelinen.

   * På följande sidor finns mer information om fälten och konfigurationsalternativen för pipelines.
      * [Konfigurera produktionsförlopp](configuring-production-pipelines.md)
      * [Konfigurera icke-produktionsförlopp](configuring-non-production-pipelines.md)

1. Klicka på **Uppdatera** när du är klar med redigeringen av pipeline.

>[!NOTE]
>
>Du kan inte redigera en pågående pipeline.

>[!NOTE]
>
>Rörledningar för webbnivå och konfiguration stöds inte i privata databaser. Mer information och en fullständig lista över begränsningar finns i [Lägg till en privat databas i Cloud Manager](/help/implementing/cloud-manager/managing-code/private-repositories.md).

## Tar bort pipelines {#deleting-pipelines}

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. Navigera till kortet **Pipelines** på sidan **Programöversikt** och klicka på ellipsknappen bredvid den pipeline du kör. Välj **Ta bort** på menyn.

>[!NOTE]
>
>Du kan inte ta bort en pågående pipeline.

## Visa information om pipeline {#view-details}

Du kan visa information om en pipeline för att se status och loggar för den senaste körningen.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. Navigera till kortet **Pipelines** på sidan **Programöversikt** och klicka på ellipsknappen bredvid pipelinen som du kör. Välj **Visa information** på menyn.

1. Du dirigeras till informationssidan för den aktuella pipelinen.

![Information om pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-running-details.png)

Här kan du se status för de olika stegen i pipeline och hämta byggloggar för diagnostik. Mer information om koddistribution och testkörning finns i dokumentet [Distribuera koden](/help/implementing/cloud-manager/deploy-code.md).

Alla steg i en pipeline-körning visas med de som ännu inte har startats nedtonade. De färdiga stegen visar varaktigheten.

När ett pipeline-steg är klart visas en sammanfattning.

![Stegsammanfattning](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-step.png)

Markera länken **Visa information** om du vill visa avsnittet **Varaktighet**. Detta inbegriper den genomsnittliga rörledningens varaktighet på grundval av den historiska trenden för det programmet.

![Varaktighet](/help/implementing/cloud-manager/assets/configure-pipeline/duration.png)

Om din pipeline innehöll ett **kodskanningssteg**, vilket orsakade problem, kan du trycka eller klicka på knappen **Hämta information** för att visa en lista med [kodkvalitetstester](/help/implementing/cloud-manager/code-quality-testing.md) som inte godkänts.

![Kodkvalitetsproblem](assets/managing-pipelines-code-quality-issues.png)

Det finns en **projektfilsplats**-kolumn i CSV-filen som anger platsen för den felaktiga koden. Den här kolumnen är den projektrelativa sökvägen, medan kolumnen **Filplats** är Maven-genererad.

![Information om problem med genomsökning av projektkod](assets/managing-pipelines-code-quality-details.png)

>[!NOTE]
>
>Du kan bara visa information om en pipeline som körs eller har körts minst en gång.

## Avbryt pipelines {#cancel}

Om en pipeline befinner sig i validerings- eller byggarfasen kan du avbryta pipelinekörningen.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. Klicka på ellipsknappen för den pipeline som du vill avbryta på kortet **Pipelines** på sidan med programöversikt.

   ![Avbryter en pipeline](/help/implementing/cloud-manager/assets/cancel-pipeline.png)

1. Välj **Avbryt**.

Du kan även avbryta en pipeline från informationssidan för pipeline.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. Navigera till fliken **Pipelines** på sidan **Programöversikt** och markera den pipeline som du vill avbryta.

1. Du dirigeras till informationssidan för den aktuella pipelinen.

   ![Avbryt pipeline-information](/help/implementing/cloud-manager/assets/cancel-pipeline-details.png)

1. Välj **Avbryt**.
