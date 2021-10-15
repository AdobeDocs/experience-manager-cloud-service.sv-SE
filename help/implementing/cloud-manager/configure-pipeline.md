---
title: Konfigurera CI/CD-pipeline - Cloud Services
description: Konfigurera CI/CD-pipeline - Cloud Services
exl-id: d2024b42-9042-46a0-879e-110b214c7285
source-git-commit: 03c058c17e8a9ff5a0be9203a65207bb367a02a6
workflow-type: tm+mt
source-wordcount: '1398'
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

### Lägga till en ny produktionspipeline {#adding-production-pipeline}

När du har konfigurerat programmet och har minst en miljö med användargränssnittet [!UICONTROL Cloud Manager] är du redo att lägga till en produktionspipeline.

Så här konfigurerar du beteendet och inställningarna för produktionsflödet:

1. Gå till **Pipelines**-kortet från sidan **Programöversikt**.
Klicka på **+Lägg till** och välj **Lägg till produktionspipeline**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-1.png)

1. **Dialogrutan Lägg till** produktionspipeline visas. Ange pipelinenamnet.

   Dessutom kan du ställa in **Distributionutlösare** och **Beteende för viktiga måttfel** från **Distributionsalternativ**. Klicka på **Fortsätt**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-add2.png)


   Du kan definiera distributionsutlösarna för att starta pipelinen.

   * **Manuell**  - använd gränssnittet för att starta pipelinen manuellt.
   * **På Git Changes**  - startar CI/CD-flödet när implementeringar läggs till i den konfigurerade Git-grenen. Även om du väljer det här alternativet kan du alltid starta pipelinen manuellt.

      Under pipeline-konfigurationen eller -redigeringen kan Deployment Manager välja att definiera pipeline-beteendet när ett viktigt fel påträffas i någon av kvalitetsportarna.

      Detta är användbart för kunder som vill ha mer automatiserade processer. De tillgängliga alternativen är:
   Du kan definiera det viktiga felmåttets beteende för att starta pipelinen.

   * **Fråga varje gång**  - Det här är standardinställningen och kräver manuell åtgärd vid viktiga fel.
   * **Misslyckas omedelbart**  - Om du väljer det här alternativet avbryts pipelinen när ett viktigt fel inträffar. Detta emulerar i princip en användare som manuellt avvisar varje fel.
   * **Fortsätt omedelbart** - Om du väljer det här alternativet fortsätter pipelinen automatiskt när ett viktigt fel inträffar. Detta emulerar i princip en användare som manuellt godkänner varje fel.


1. Dialogrutan **Lägg till produktionspipeline** innehåller en andra flik med namnet **Källkod**. **Fullständig** stackkod har valts. Du kan välja **databasen** och **Git-grenen**. Välj alternativ för produktionsdistribution enligt nedan. Klicka på **Fortsätt**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-fullstack1.png)

   Alternativ för produktionsdistribution:

   * **Pausa före distribuering till produktion**: Med det här alternativet kan distributionen pausa pausen före produktion.
   * **Schemalagd**: Med det här alternativet kan användaren aktivera den schemalagda produktionsdistributionen.

1. Dialogrutan **Lägg till produktionspipeline** innehåller en tredje flik med namnet **Experience Audit**. Det här alternativet innehåller en tabell för de URL-sökvägar som alltid ska inkluderas i Experience Audit.

   >[!NOTE]
   >Du måste klicka på **Lägg till sida** för att definiera en egen anpassad länk.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit.png)

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

1. Klicka på **Spara**. Produktionspipelinen som skapades visas nu på kortet **Pipelines**.

   Rörledningen visas på kortet på startskärmen med tre åtgärder, som visas nedan:

   * **Lägg till**  - tillåter tillägg av en ny pipeline.
   * **Åtkomst till replikinformation**  - gör att användaren kan få den information som behövs för att komma åt Cloud Manager Git-databasen.
   * **Lär dig mer**  - navigerar till att förstå CI/CD-pipeline-dokumentationsresursen.

### Redigera en produktionspipeline {#editing-prod-pipeline}

Du kan redigera pipelinekonfigurationerna på sidan **Programöversikt**.

Följ stegen nedan för att redigera den konfigurerade pipeline:

1. Navigera till **Pipelines**-kortet från sidan **Programöversikt**.

1. Klicka på **..** på **Pipelines**-kortet och klicka på **Redigera**, som bilden nedan visar.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-edit1.png)

1. Dialogrutan **Redigera produktionspipeline** visas.

   1. På fliken **Konfiguration** kan du uppdatera **pipelinenamnet**, **Distributionutlösaren** och **Beteendet Viktigt mätningsfel**.

      >[!NOTE]
      >Mer information om hur du lägger till och hanterar databaser i Cloud Manager finns i [Lägga till och hantera databaser](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md).

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-edit2.png)


   1. På fliken **Källa** kan du kontrollera eller avmarkera alternativen **Paus innan du distribuerar till produktion** och **Schemalagda** från **Alternativ för produktionsdistribution**.

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-editnotier.png)

   1. Med alternativet **Experience Audit** kan du uppdatera eller lägga till nya sidor.

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-edit4.png)

1. Klicka på **Uppdatera** när du är klar med redigeringen av pipeline.

### Ytterligare produktionsförloppsåtgärder {#additional-prod-actions}

#### Köra en produktionspipeline {#run-prod}

Du kan köra produktionsflödet från pipelines-kortet:

1. Navigera till **Pipelines**-kortet från sidan **Programöversikt**.

1. Klicka på **..** på **Pipelines**-kortet och klicka på **Kör**, som bilden nedan visar.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-run.png)

#### Ta bort en produktionspipeline {#delete-prod}

Du kan ta bort produktionsflödet från pipelines-kortet:

1. Navigera till **Pipelines**-kortet från sidan **Programöversikt**.

1. Klicka på **..** på **Pipelines**-kortet och klicka på **Ta bort**, enligt bilden nedan.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-delete.png)

   >[!NOTE]
   >En användare i rollen Distributionshanterare kan nu ta bort produktionsflöde på ett självbetjäningssätt via alternativet **Ta bort** från pipeline-kortet.


## Icke-produktion och endast kodkvalitet, rörledningar {#non-production-pipelines}

Förutom den huvudsakliga rörledningen som distribueras till stadium och produktion kan kunderna lägga upp ytterligare rörledningar, som kallas **icke-produktionsförlopp**. Dessa pipelines kör alltid stegen för bygg- och kodkvalitet. De kan också distribueras till AEM as a Cloud Service miljö.

### Lägga till en ny icke-produktionspipeline {#adding-non-production-pipeline}

På startskärmen visas dessa rörledningar i ett nytt kort:

1. Gå till **Pipelines**-kortet från startskärmen i Cloud Manager. Klicka på **+Lägg till** och välj **Lägg till icke-produktionsförlopp**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. **Dialogrutan Lägg till icke-produktionsförlopp**  visas. Välj den typ av pipeline som du vill skapa, antingen **Kodkvalitetspipeline** eller **Distributionspipeline**.

   Dessutom kan du ställa in **Distributionutlösare** och **Beteende för viktiga måttfel** från **Distributionsalternativ**. Klicka på **Fortsätt**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add2.png)

1. **Fullständig** stackkod har valts. Du kan välja **databasen** och **Git-grenen**. Klicka på **Spara**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add3.png)

1. Den nyligen skapade icke-produktionspipelinen visas nu på **pipelines**-kortet.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add4.png)


   Rörledningen visas på kortet på startskärmen med tre åtgärder, som visas nedan:

   * **Lägg till**  - tillåter tillägg av en ny pipeline.
   * **Åtkomst till replikinformation**  - gör att användaren kan få den information som behövs för att komma åt Cloud Manager Git-databasen.
   * **Lär dig mer**  - navigerar till att förstå CI/CD-pipeline-dokumentationsresursen.

### Redigera en icke-produktionspipeline {#editing-nonprod-pipeline}

Du kan redigera pipelinekonfigurationerna från sidan **Pipelines card** från **Program Overview**.

Följ stegen nedan för att redigera den konfigurerade icke-produktionsflödet:

1. Navigera till **Pipelines**-kortet från sidan **Programöversikt**.

1. Markera produktionsflödet och klicka på **..**. Klicka på **Redigera**, vilket visas i bilden nedan.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-edit1.png)

1. Dialogrutan **Redigera produktionspipeline** visas.

   1. På fliken **Konfiguration** kan du uppdatera **pipelinenamnet**, **Distributionutlösaren** och **Beteendet Viktiga måttfel**.

      >[!NOTE]
      >Mer information om hur du lägger till och hanterar databaser i Cloud Manager finns i [Lägga till och hantera databaser](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md).

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-edit2.png)


   1. På fliken **Källkod** kan du uppdatera **databasen** och **Git-grenen**.

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-edit3.png)

1. Klicka på **Uppdatera** när du är klar med redigeringen av produktionsflödet.

### Ytterligare icke-produktionsförloppsindikatorer {#additional-nonprod-actions}

#### Köra en icke-produktionspipeline {#run-nonprod}

Du kan köra produktionsflödet från pipelines-kortet:

1. Navigera till **Pipelines**-kortet från sidan **Programöversikt**.

1. Klicka på **..** på **Pipelines**-kortet och klicka på **Kör**, som bilden nedan visar.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-run1.png)

#### Ta bort en icke-produktionspipeline {#delete-nonprod}

Du kan ta bort produktionsflödet från pipelines-kortet:

1. Navigera till **Pipelines**-kortet från sidan **Programöversikt**.

1. Klicka på **..** på **Pipelines**-kortet och klicka på **Ta bort**, enligt bilden nedan.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-delete.png)


## Nästa steg {#the-next-steps}

När du har konfigurerat pipeline måste du distribuera koden.

Mer information finns i [Distribuera koden](deploy-code.md).
