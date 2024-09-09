---
title: Pipeline med endast scener och endast prod
description: Lär dig hur du kan dela upp driftsättningar för staging och produktion med dedikerade pipelines.
source-git-commit: 5d6d3374f2dd95728b2d3ed0cf6fab4092f73568
workflow-type: tm+mt
source-wordcount: '942'
ht-degree: 0%

---


# Pipeline med endast scener och endast produktion {#stage-prod-only}

Lär dig hur du kan dela upp driftsättningar för staging och produktion med dedikerade pipelines.

>[!NOTE]
>
>Den här funktionen är bara tillgänglig för [det tidiga adopterprogrammet](/help/implementing/cloud-manager/release-notes/current.md#early-adoption).

## Ökning {#overview}

Mellanlagrings- och produktionsmiljöer är nära kopplade. Som standard är distributioner till dem länkade till en enda pipeline. Det är en driftsättningspipeline som distribueras till både testnings- och produktionsmiljöerna i det programmet. Även om denna koppling normalt är lämplig, finns det vissa användningsområden där det finns nackdelar:

* Om du vill distribuera till enbart scenen kan du bara göra detta genom att avvisa steget **Befordra till produktion** i pipeline. Körningen markeras dock som avbruten.
* Om du vill distribuera den senaste koden i en staging-miljö till produktion måste du distribuera om hela pipelinen, inklusive staging-distributionen, även om ingen kod har ändrats där.
* Eftersom miljöer inte kan uppdateras under distributioner och du vill pausa och testa i staging-miljön i flera dagar innan du marknadsför till produktion, kan produktionsmiljön inte uppdateras. Detta gör icke-beroende aktiviteter som att uppdatera [miljövariabler](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#environment-variables) omöjliga.

Enkla rörledningar för scener och enbart för produkter erbjuder lösningar för dessa användningsområden genom att tillhandahålla dedikerade driftsättningsalternativ.

* **Distributionsförlopp med endast scener** distribuerar bara till en staging-miljö där körningen är klar när distributionen och testerna är klara.
   * En pipeline som bara är i ett steg fungerar på samma sätt som den standardkopplade kompletta stackproduktionskanalen, men utan stegen för produktionsdistribution (godkännande, schema, driftsättning).
* **Driftsättningspipelines för enbart produkter** distribuerar bara till en produktionsmiljö med möjlighet att välja en körning som har slutförts och validerats på scenen och distribuera dess artefakter på produkten.
   * Med rörledningar som endast är avsedda för produktion återanvänds artefakterna från scendistributionerna, och byggnadsfasen hoppas över.

Vare sig rörledningar som bara är i stadiet eller endast i drift kommer att utföras medan en produktionsprocess med en hel hög körs och vice versa. Om utlösaren **On Git Changes** är konfigurerad för både produktionsflödet för enbart scenen och hela stacken och pekar på samma gren och databas, startas endast den enbart för scenen automatiskt. Rörledningar som endast är avsedda för produktion startas inte **vid Git-ändringar** eftersom de inte är direkt länkade till en databas.

De här dedikerade rörledningarna ger större flexibilitet, men notera följande detaljer om drift och rekommendationer.

## Begränsningar {#limitations}

I rörledningar som endast är avsedda för produktion används alltid artefakter från rörledningen som endast är i stadiet, oavsett vad som under tiden kan ha driftsatts på scenen via den kopplade standardproduktionsledningen.

* Detta kan leda till oönskade kodåterställningar.
* Adobe rekommenderar att du slutar använda den standardiserade kopplade produktionskanalen när du väl har börjat använda pipelines som bara är för prod och enbart för stage.
* Om du fortfarande bestämmer dig för att köra både standardrörledningarna och rörledningar för scen/endast för produkt, bör du tänka på att artefakter återanvänds för att undvika att koda om.

## Kända fel {#known-issues}

Observera även följande kända fel innan du börjar testa den här funktionen.

* När du väl har använt rörledningar som bara är avsedda för produktion kan det hända att du inte har nytta av de senaste AEM uppdateringarna
   * I vissa fall kan AEM återställa koden till den kod som senast distribuerades via hela stackpipeline.
* Du kan inte begära en [miljöåterställning](/help/operations/restore.md#offsite-backup) om du använder pipelines som bara är för produktion eller endast för mellanlagring.

## Skapa pipeline {#pipeline-creation}

Rörledningar som endast är avsedda för produktion och endast för scenen skapas på ungefär samma sätt som standardanslutna [produktionspipelines](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) och [icke-produktionspipelines](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md). Mer information finns i de dokumenten.

1. Klicka på **Lägg till pipeline** i fönstret **Pipelines**.

   * Välj **Lägg till icke-produktionsförlopp** om du vill skapa en pipeline som bara är avsedd för scenen.
   * Välj **Lägg till endast produktion i pipeline** om du vill skapa en pipeline som endast är avsedd för produktion.

   ![Skapar en pipeline enbart för produkt/scen](assets/prod-stage-pipelines.png)

>[!NOTE]
>
>Vissa alternativ kan vara nedtonade om motsvarande rörledningar redan finns.
>
>* **Lägg till endast produktion i pipeline** är inte tillgängligt om det inte finns någon pipeline som bara är för stadiet än.
>* **Lägg till produktionspipeline** är inte tillgängligt om det redan finns en kopplad standardpipeline.
>* Endast en prod- och endast en fasledning tillåts per program.

### Enbart Stage-förlopp {#stage-only}

1. När du har valt alternativet **Lägg till icke-produktionsförlopp** öppnas dialogrutan **Lägg till icke-produktionsförlopp** .
1. Om du vill skapa en pipeline som bara är för ett stadium väljer du scenmiljön i fältet **Godtagbara distributionsmiljöer** för din pipeline. Fyll i återstående fält och klicka på **Fortsätt**.

   ![Skapar en pipeline enbart för scenen](assets/stage-only.png)

1. På fliken **Scentestning** kan du definiera testning som ska utföras i mellanlagringsmiljön. Tryck eller klicka på **Spara** för att spara din nya pipeline.

### Prod-Only Pipelines {#prod-only}

1. När du väljer alternativet **Lägg till endast produktionspipeline** öppnas dialogrutan **Lägg till endast produktionspipeline** .
1. Ange ett **pipelinenamn**. De återstående alternativen och funktionerna i dialogrutan fungerar på samma sätt som i den vanliga dialogrutan för att skapa kopplad pipeline. Klicka på **Spara** för att spara pipeline.

## Köra endast prod- och Stage-pipelines {#running}

Rörledningar med endast prod och scenen körs på samma sätt som [alla andra pipelines körs](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#running-pipelines). Mer information finns i den dokumentationen.

Dessutom kan en pipelinekörning som bara är avsedd för produktion aktiveras direkt från körningsinformationen för en pipeline som bara är avsedd för en viss fas.

### Enbart Stage-förlopp {#stage-only-run}

En rörledning som bara fungerar på en scen fungerar på nästan samma sätt som vanliga kopplade rörledningar. Efter testningsstegen kan du emellertid med en **Promote Build**-knapp i slutet av körningen starta en produktspecifik pipeline-körning som använder artefakter som distribuerats på scenen av den här körningen och distribuerar dem i produktionen.

![En pipeline som endast är för scenen körs](assets/stage-only-pipeline-run.png)

Knappen **Befordra bygge** visas bara om du är på den senaste pipelinekörningen som bara fungerar på scenen. När du klickar på den uppmanas du att bekräfta körningen av den produktspecifika pipelinen eller att skapa en produktbaserad pipeline om det inte redan finns en.

### Prod-Only Pipelines {#prod-only-run}

För rörledningar som endast är avsedda för produktion är det viktigt att identifiera de källartefakter som ska distribueras till produktionen. Den här informationen finns i steget **Förberedelse av felaktigheter**. Du kan navigera till dessa körningar för mer information och loggar.

![Information om felaktigheter](assets/prod-only-pipeline-run.png)
