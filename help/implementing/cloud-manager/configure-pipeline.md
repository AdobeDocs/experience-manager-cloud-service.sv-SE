---
title: Konfigurera CI/CD-pipeline - Cloud Services
description: Konfigurera CI/CD-pipeline - Cloud Services
exl-id: d2024b42-9042-46a0-879e-110b214c7285
source-git-commit: 90d75ddd0ace3eff8c3e1cde68208cf0a483ef86
workflow-type: tm+mt
source-wordcount: '953'
ht-degree: 0%

---

# Konfigurera CI-CD-pipeline {#configure-ci-cd-pipeline}

I Cloud Manager finns det två typer av pipeline:

* **Produktionspipeline**:

   En produktionspipeline kan bara läggas till när en produktions- och scenmiljöuppsättning har skapats.

   Mer information finns i [Konfigurera produktionspipeline](configure-pipeline.md#setting-up-the-pipeline).

* **Icke-produktionsförlopp**:

   En icke-produktionsförlopp kan läggas till från sidan **Översikt** i användargränssnittet för Cloud Manager.

   Mer information finns i [Icke-produktion och Endast kodkvalitet i pipeline](configure-pipeline.md#non-production-pipelines).

>[!NOTE]
>Om du vill konfigurera din pipeline måste du:
> * Definiera den utlösare som ska starta pipelinen.
> * Definiera parametrarna som styr produktionsdistributionen.
> * konfigurera prestandatestparametrarna.


## Ställ in produktionspipeline {#setting-up-production-pipeline}

Distributionshanteraren ansvarar för att ställa in produktionspipelinen.

>[!NOTE]
>Det går inte att konfigurera en produktionspipeline förrän ett program har skapats, Git-databasen har minst en gren och en Production- och Stage-miljöuppsättning har skapats.

Innan du börjar distribuera koden måste du konfigurera dina pipeline-inställningar från [!UICONTROL Cloud Manager].

>[!NOTE]
>
>Du kan ändra pipeline-inställningarna efter den första konfigurationen.

## Konfigurera förloppsinställningarna från [!UICONTROL Cloud Manager] {#configuring-the-pipeline-settings-from-cloud-manager}

När du har konfigurerat ditt program och har minst en miljö med användargränssnittet [!UICONTROL Cloud Manager] är du redo att konfigurera din distributionskanal.

Följ de här stegen för att konfigurera beteendet och inställningarna för din pipeline:

1. Klicka på **Konfigurera pipeline** för att konfigurera och konfigurera din pipeline.

   ![](assets/set-up-pipeline1.png)

1. Skärmen **Setup Pipeline** visas. Markera grenen och klicka på **Nästa**.

   ![](assets/setup-1.png)

1. Konfigurera distributionsalternativen.

   ![](assets/setup-pipeline.png)

   Du kan definiera utlösaren för att starta pipelinen:

   * **Manuell**  - använd gränssnittet för att starta pipelinen manuellt.
   * **På Git Changes**  - startar CI/CD-flödet när implementeringar läggs till i den konfigurerade Git-grenen. Även om du väljer det här alternativet kan du alltid starta pipelinen manuellt.

   Under pipeline-konfigurationen eller -redigeringen kan Deployment Manager välja att definiera pipeline-beteendet när ett viktigt fel påträffas i någon av kvalitetsportarna.

   Detta är användbart för kunder som vill ha mer automatiserade processer. De tillgängliga alternativen är:

   * **Fråga varje gång**  - Det här är standardinställningen och kräver manuell åtgärd vid viktiga fel.
   * **Avbryt omedelbart** - Om du väljer det här alternativet avbryts pipelinen när ett viktigt fel inträffar. Detta emulerar i princip en användare som manuellt avvisar varje fel.
   * **Godkänn omedelbart**  - Om du väljer det här alternativet fortsätter pipeline automatiskt när ett viktigt fel inträffar. Detta emulerar i princip en användare som manuellt godkänner varje fel.


1. Produktionens pipeline-inställningar innehåller en tredje flik med namnet **Experience Audit**. Det här alternativet innehåller en tabell för de URL-sökvägar som alltid ska inkluderas i Experience Audit.

   >[!NOTE]
   >Du måste klicka på **Lägg till ny sida** för att definiera en egen anpassad länk.

   ![](assets/setup-3.png)

   Klicka på **Lägg till ny sida** för att ange en URL-sökväg som ska inkluderas i Experience Audit.

   Om du till exempel vill inkludera `https://wknd.site/us/en/about-us.html` i Experience Audit (Upplevelsegranskning) anger du sökvägen `us/en/about-us.html` i det här fältet och klickar på **Save**.

   ![](assets/exp-audit4.png)

   Den URL som visas i tabellen är:

   `https://publish-p14253-e43686.adobeaemcloud.com/us/en/about-us.html`

   ![](assets/exp-audit5.png)

   Högst 25 rader kan inkluderas. Om användaren inte har skickat in några sidor i det här avsnittet, kommer webbplatsens hemsida som standard att inkluderas i Experience Audit.

   Mer information finns i [Understanding Experience Audit Results](/help/implementing/cloud-manager/experience-audit-testing.md).

   >[!NOTE]
   > De konfigurerade sidorna skickas till tjänsten och utvärderas utifrån prestanda, tillgänglighet, SEO (Search Engine Optimization), bästa praxis och PWA (Progressive Web App)-tester.

1. Klicka på **Spara** på skärmen **Redigera pipeline**. Sidan **Översikt** visar nu **Distribuera ditt program**-kort. Klicka på **Distribuera** för att distribuera programmet.

   ![](assets/configure-pipeline5.png)

### Redigera en produktionspipeline {#editing-prod-pipeline}

Du kan redigera pipelinekonfigurationerna på sidan **Programöversikt**.

Följ stegen nedan för att redigera den konfigurerade pipeline:

1. Navigera till **Pipelines**-kortet från sidan **Programöversikt**.

1. Klicka på **Redigera** på **Pipelines**-kortet.

   ![](assets/configure-pipeline/edit-pipeline-1.png)

1. På fliken **Källkod** kan du uppdatera databasen. Klicka på **Öppna repo-information** för att uppdatera databasen.

   >[!NOTE]
   >Mer information om hur du lägger till och hanterar databaser i Cloud Manager finns i [Lägga till och hantera databaser](/help/implementing/cloud-manager/cloud-manager-repositories.md#add-manage-repos).

   ![](assets/configure-pipeline/edit-pipeline-2.png)


1. På fliken **Miljö** kan du uppdatera scen- och produktionsalternativen.

   ![](assets/configure-pipeline/edit-pipeline-3.png)

1. Med alternativet **Experience Audit** kan du uppdatera eller lägga till nya sidor.

   ![](assets/configure-pipeline/edit-pipeline-4.png)

1. Klicka på **Spara** när du är klar med redigeringen av pipeline.

## Icke-produktion och endast kodkvalitet, rörledningar {#non-production-pipelines}

Förutom den huvudsakliga rörledningen som distribueras till stadium och produktion kan kunderna lägga upp ytterligare rörledningar, som kallas **icke-produktionsförlopp**. Dessa pipelines kör alltid stegen för bygg- och kodkvalitet. De kan också distribueras till AEM som en Cloud Service.

På startskärmen visas dessa rörledningar i ett nytt kort:

1. Gå till panelen **Icke-produktionspipelines** från startskärmen i Cloud Manager.

   ![](/help/implementing/cloud-manager/assets/non-prod-add.png)

1. Klicka på knappen **Lägg till** för att ange namnet på pipeline, typen av pipeline och Git-grenen.

   Dessutom kan du konfigurera utlösare för distribution och Beteende för viktigt fel i alternativen för pipeline.

   ![](assets/non-prod-pipe1.png)

1. Klicka på **Spara** så visas pipeline på startskärmen med fem åtgärder, som visas nedan:

   ![](/help/implementing/cloud-manager/assets/prod-one.png)

   * **Redigera**  - tillåter redigering av pipeline-inställningarna
   * **Detaljer**  - innehåller information om pipelinekörningen
   * **Build** - navigerar till körningssidan, från vilken pipelinen kan köras
   * **Åtkomst till**  upprepningsinformation - gör att användaren kan få den information som behövs för att komma åt Cloud Manager Git-databasen
   * **Lär dig mer**  - navigerar till att förstå CI/CD-pipeline-dokumentationsresursen.

### Redigera en icke-produktionspipeline {#editing-nonprod-pipeline}

Du kan redigera pipelinekonfigurationerna på sidan **Programöversikt**.

Följ stegen nedan för att redigera den konfigurerade icke-produktionsflödet:

1. Navigera till **Pipelines**-kortet från sidan **Programöversikt**.

1. Välj fliken **Icke-produktion** och klicka på **Redigera** när du har valt önskade pipelines.

   ![](assets/configure-pipeline/non-prod-edit-1.png)

1. Välj önskad databas och andra nödvändiga uppdateringar och klicka på **Spara**.

   ![](assets/configure-pipeline/edit-nonprodenv.png)

## Nästa steg {#the-next-steps}

När du har konfigurerat pipeline måste du distribuera koden.

Mer information finns i [Distribuera koden](deploy-code.md).
