---
title: Hantera pipelines
description: Lär dig hur du hanterar dina befintliga rörledningar, inklusive redigering, körning och borttagning av dem.
index: true
exl-id: 4aff5a84-134a-43fa-8de8-8d564f4edd16
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f7a8e823f058115f11241f0864517432a7dea5ab
workflow-type: tm+mt
source-wordcount: '1164'
ht-degree: 0%

---


# Hantera rörledningar {#managing-pipelines}

Lär dig hur du hanterar dina befintliga rörledningar, inklusive redigering, körning och borttagning av dem.

## Förloppskort {#pipeline-card}

Kortet **Pipelines** på sidan **Programöversikt** i Cloud Manager ger dig en översikt över alla dina pipelines och deras aktuella status.

![Förloppskort i Cloud Manager](/help/implementing/cloud-manager/assets/configure-pipeline/pipelines-card.png)

Genom att klicka på ![Ellips - Mer ikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) bredvid varje pipeline kan du utföra följande åtgärder:

* [Köra en pipeline](#running-pipelines)
* [Avbryt en pipeline](#cancel)
* [Redigera en pipeline](#editing-pipelines)
* [Ta bort en pipeline](#deleting-pipelines)
* [Visa information om den senaste körningen av en pipeline](#view-details)

Längst ned i listan med rörledningar finns följande allmänna alternativ:

* **Lägg till** - Om du vill [lägga till en ny produktionspipeline](configuring-production-pipelines.md) eller [lägga till en ny icke-produktionspipeline](configuring-non-production-pipelines.md)
* **Visa alla** - Tar användaren till skärmen Pipelines för att visa alla pipelines i en mer detaljerad tabell.
* **Åtkomst till repo-information** - Visar den information som krävs för åtkomst till Cloud Manager Git-databasen
* **Läs mer** - Navigerar till resurser för pipeline-dokumentation för CI/CD.

## Sidan Pipelines {#pipelines}

Sidan **Pipelines** visar en fullständig lista över alla pipelines för det valda programmet. Den här informationen är användbar eftersom den ger mer omfattande information än vad som är tillgängligt på [pipeline-kortet](#pipeline-card).

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.

1. Välj programmet på konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)**.

1. På sidan **Programöversikt** klickar du på fliken ![Pipeline - ikonen Arbetsflöde](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg) **Pipelines** .

1. På sidan **Pipelines** kan du se en lista över alla pipelines för programmet och starta och stoppa pipelinekörningen på samma sätt som i **pipelines-kortet**.

Om en pipeline körs klickar du på ![Info - medieikon](https://spectrum.adobe.com/static/icons/ui_18/InfoMedium.svg) i kolumnen **Status** för att visa ett popup-fönster med information om körningen. Klicka på **Visa information** i popup-fönstret för att visa [information om pipelinekörningen](#view-details).

![Information om pipeline-körning](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-status.png)


Du kan också klicka på ![Ellips - Mer ikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) bredvid pipelinen om du vill vidta ytterligare åtgärder som är lämpliga för pipelineläget, till exempel [redigera](#editing-pipelines) eller [avbryta körningen](#cancel).

![Pipeline-åtgärder](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-actions.png)

## Aktivitetssida {#activity}

På sidan **Aktivitet** visas en fullständig lista över alla pipelines-körningar för det valda programmet samt andra viktiga programhändelser.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. På sidan **Programöversikt** klickar du på ikonen ![Bell](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Bell_18_N.svg) **Aktivitet** på sidmenyn.

1. På sidan **Aktivitet** kan du se en lista över alla pipeline-körningar för programmet, inklusive aktuella och historiska körningar.

Om en pipeline körs kan du klicka på ![Info - medieikon](https://spectrum.adobe.com/static/icons/ui_18/InfoMedium.svg) i kolumnen **Status** för att visa ett popup-fönster med information om körningen.

![Information om pipeline-körning](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-activity.png)

Klicka på raden som representerar pipelinekörningen för att visa [information om pipelinekörningen](#view-details).

Du kan också klicka på ![Ellips - Mer ikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) om du vill utföra ytterligare åtgärder för pipelinekörningen, till exempel visa information eller hämta loggen, som tar dig till [sidan med information om pipeline](#view-details).

![Körningsåtgärder för pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-execution-actions.png)

## Köra en pipeline {#running-pipelines}

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. Navigera till kortet **Pipelines** från sidan **Programöversikt**.

1. Klicka på ![Ellipsis - Mer ikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) bredvid den pipeline som du kör.

1. Klicka på ikonen ![Kör - Spela upp](https://spectrum.adobe.com/static/icons/workflow_18/Smock_PlayCircle_18_N.svg) **Kör** i listrutan.

   Pipeline-körningen startar och kolumnen **Status** visar förloppet.

Du kan visa information om körningen genom att klicka på ikonen ![Ellips - Mer](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) igen och klicka på **[Visa information](#view-details)**.

Beroende på vilken typ av pipeline det gäller kan du eventuellt avbryta körningen genom att klicka på ikonen ![Ellips - Mer](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) igen och klicka på **Avbryt**.

## Redigera en pipeline {#editing-pipelines}

Du kan redigera en pipeline om den inte körs.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. Navigera till kortet **Pipelines** från sidan **Programöversikt**.

1. Klicka på ![Ellips - Mer ikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) bredvid den pipeline som du vill redigera.

1. Klicka på **Redigera** i listrutan.

1. Redigera samma information som du angav när du skapade pipelinen i dialogrutan **Redigera produktionspipeline** eller **Redigera icke-produktionspipeline**.

   På följande sidor finns mer information om fälten och konfigurationsalternativen för pipelines.
   * [Konfigurera en produktionspipeline](configuring-production-pipelines.md)
   * [Konfigurera en icke-produktionspipeline](configuring-non-production-pipelines.md)

1. Klicka på **Uppdatera** när du är klar.

>[!NOTE]
>
>Rörledningar för webbnivå och konfiguration stöds inte i privata databaser. Mer information och en fullständig lista över begränsningar finns i [Lägg till en privat GitHub-databas i Cloud Manager](/help/implementing/cloud-manager/managing-code/private-repositories.md).

## Ta bort en pipeline {#deleting-pipelines}

Du kan ta bort en pipeline om den inte körs.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. Navigera till kortet **Pipelines** från sidan **Programöversikt**.

1. Klicka på ![Ellipsis - Mer ikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) bredvid den pipeline som du kör.

1. Klicka på **Ta bort** i listrutan.


## Visa information om den senaste körningen av en pipeline {#view-details}

Du kan kontrollera detaljerna för en pipeline för att visa status och loggar från den senaste körningen. Du kan dock bara komma åt informationen om pipelinen körs eller har körts minst en gång.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. Navigera till kortet **Pipelines** från sidan **Programöversikt**.

1. I listrutan klickar du på ikonen ![Ellips - Mer](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) bredvid den pipeline som du kör.

1. Klicka på **Visa senaste körning** i listrutan.

   Du dirigeras till informationssidan för den aktuella pipelinen.

   ![Information om pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-running-details.png)

   Här kan du se status för de olika stegen i pipeline och hämta byggloggar för diagnostik. Mer information om koddistribution och testkörning finns i [Distribuera koden](/help/implementing/cloud-manager/deploy-code.md).

   Alla steg i en pipeline-körning visas med de som ännu inte har startats nedtonade. De färdiga stegen visar varaktigheten.

   När ett pipeline-steg är klart visas en sammanfattning.

   ![Stegsammanfattning](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-step.png)

1. Klicka på **Visa information** om du vill expandera avsnittet **Varaktighet**, där du kan se den genomsnittliga tiden för pipelinen baserat på programmets historiska trender.

   ![Varaktighet](/help/implementing/cloud-manager/assets/configure-pipeline/duration.png)

1. Om din pipeline innehöll ett **kodskanningssteg** som flaggade problem klickar du på **Hämta detaljer** för att få en lista över [kodkvalitetstester](/help/implementing/cloud-manager/code-quality-testing.md) som misslyckades.

   ![Kodkvalitetsproblem](assets/managing-pipelines-code-quality-issues.png)

   CSV-filen innehåller en **projektfilsplats**-kolumn som visar sökvägen till den problematiska koden i förhållande till projektet. Kolumnen **Filplats** återspeglar däremot den Maven-genererade sökvägen.

   ![Information om problem med genomsökning av projektkod](assets/managing-pipelines-code-quality-details.png)

## Avbryt en pipeline {#cancel}

Du kan avbryta pipeline-körningen om den är i validerings- eller byggarfasen.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. Klicka på ikonen ![Ellips - Mer](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) för pipeline som du vill avbryta på **pipelines**-kortet på programöversiktssidan.

   ![Avbryter en pipeline](/help/implementing/cloud-manager/assets/cancel-pipeline.png)

1. Klicka på **Avbryt**.

Du kan också avbryta en pipeline från informationssidan för pipeline.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. Navigera till fliken ![Förloppsindikatorer - ikonen för arbetsflöde](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg) **Förberedelser** på sidan **Programöversikt** och markera den pipeline som du vill avbryta.

   Du dirigeras till informationssidan för den aktuella pipelinen.

   ![Avbryt pipeline-information](/help/implementing/cloud-manager/assets/cancel-pipeline-details.png)

1. Klicka på **Avbryt**.
