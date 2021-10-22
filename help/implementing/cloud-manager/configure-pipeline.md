---
title: Konfigurera CI/CD-pipeline - Cloud Services
description: Konfigurera CI/CD-pipeline - Cloud Services
exl-id: d2024b42-9042-46a0-879e-110b214c7285
source-git-commit: f3743451f7aeadae26e8a6814cfbed9667c4a242
workflow-type: tm+mt
source-wordcount: '1447'
ht-degree: 0%

---

# Konfigurera CI-CD-pipeline {#configure-ci-cd-pipeline}

I Cloud Manager finns det två typer av pipeline:

* **Produktionspipeline**:

   En produktionspipeline kan bara läggas till när en produktions- och scenmiljöuppsättning har skapats.

   Se [Ställ in produktionspipeline](configure-pipeline.md#setting-up-the-pipeline) för mer information.

* **Icke-produktionsförlopp**:

   En icke-produktionspipeline kan läggas till från **Översikt** från Cloud Managers användargränssnitt.

   Se [Icke-produktion och endast kodkvalitet, rörledningar](configure-pipeline.md#non-production-pipelines) för mer information.

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

När du har konfigurerat programmet och har minst en miljö som använder [!UICONTROL Cloud Manager] UI, du är redo att lägga till en produktionspipeline.

Så här konfigurerar du beteendet och inställningarna för produktionsflödet:

1. Navigera till **Pipelines** från **Programöversikt** sida.
Klicka på **+Lägg till** och markera **Lägg till produktionspipeline**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-1.png)

1. **Lägg till produktionspipeline** visas. Ange pipelinenamnet.

   Dessutom kan du konfigurera **Utlösare för distribution** och **Beteende vid viktiga måttfel** från **Distributionsalternativ**. Klicka på **Fortsätt**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-add2.png)


   Du kan definiera distributionsutlösarna för att starta pipelinen.

   * **Manuell** - med användargränssnittet startar du pipelinen manuellt.
   * **Vid Git-ändringar** - startar CI/CD-pipeline när implementeringar har lagts till i den konfigurerade Git-grenen. Även om du väljer det här alternativet kan du alltid starta pipelinen manuellt.

      Under pipeline-konfigurationen eller -redigeringen kan Deployment Manager välja att definiera pipeline-beteendet när ett viktigt fel påträffas i någon av kvalitetsportarna.

      Detta är användbart för kunder som vill ha mer automatiserade processer. De tillgängliga alternativen är:
   Du kan definiera det viktiga felmåttets beteende för att starta pipelinen.

   * **Fråga varje gång** - Det här är standardinställningen och kräver manuell åtgärd vid viktiga fel.
   * **Misslyckas omedelbart** - Om du väljer det här alternativet avbryts pipelinen när ett viktigt fel inträffar. Detta emulerar i princip en användare som manuellt avvisar varje fel.
   * **Fortsätt omedelbart** - Om du väljer det här alternativet fortsätter pipeline automatiskt när ett viktigt fel inträffar. Detta emulerar i princip en användare som manuellt godkänner varje fel.


1. The **Lägg till produktionspipeline** innehåller en andra flik med etiketten **Källkod**. **Full Stack-kod** är markerat. Du kan välja **Databas** och **Git-gren**. Välj alternativ för produktionsdistribution enligt nedan. Klicka på **Fortsätt**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-fullstack1.png)

   Alternativ för produktionsdistribution:

   * **Pausa före distribution till produktion**: Med det här alternativet kan distributionen pausa pausen före produktion.
   * **Schemalagd**: Med det här alternativet kan användaren aktivera den schemalagda produktionsdistributionen.

1. The **Lägg till produktionspipeline** innehåller en tredje flik med etiketten **Experience Audit**. Det här alternativet innehåller en tabell för de URL-sökvägar som alltid ska inkluderas i Experience Audit.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit.png)

   >[!IMPORTANT]
   >Du måste klicka på **Lägg till sida** för att definiera en egen länk. Sidsökvägen måste börja med `/`.
   >![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit2.png)


   Klicka **Lägg till ny sida** för att ange en URL-sökväg som ska inkluderas i Experience Audit.

   Om du till exempel vill inkludera `https://wknd.site/us/en/about-us.html` Ange sökvägen i Experience Audit `/us/en/about-us.html` i det här fältet och klicka **Spara**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit3.png)

   Den URL som visas i tabellen är:

   `https://publish-p12361-e112003.adobeaemcloud.com/us/en/about-us.html`

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit4.png)

   Högst 25 rader kan inkluderas. Om användaren inte har skickat in några sidor i det här avsnittet, kommer webbplatsens hemsida som standard att inkluderas i Experience Audit.

   Se [Upplevelsegranskningsresultat](/help/implementing/cloud-manager/experience-audit-testing.md) för mer information.

   >[!NOTE]
   > De konfigurerade sidorna skickas till tjänsten och utvärderas utifrån prestanda, tillgänglighet, SEO (Search Engine Optimization), bästa praxis och PWA (Progressive Web App)-tester.

1. Klicka på **Spara**. Produktionspipelinen som skapades visas nu i **Pipelines** kort.

   Rörledningen visas på kortet på startskärmen med tre åtgärder, som visas nedan:

   * **Lägg till** - gör det möjligt att lägga till en ny pipeline.
   * **Åtkomst till svarsinformation** - ger användaren tillgång till den information som krävs för att få åtkomst till Git-databasen i Cloud Manager.
   * **Läs mer** - navigerar till att förstå CI/CD-pipeline-dokumentationsresursen.

### Redigera en produktionspipeline {#editing-prod-pipeline}

Du kan redigera pipeline-konfigurationerna från **Programöversikt** sida.

Följ stegen nedan för att redigera den konfigurerade pipeline:

1. Navigera till **Pipelines** från **Programöversikt** sida.

1. Klicka på **...** från **Pipelines** kort och klicka på **Redigera**, vilket visas i figuren nedan.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-edit1.png)

1. The **Redigera produktionspipeline** visas.

   1. The **Konfiguration** kan du uppdatera **Pipelinenamn**, **Utlösare för distribution** och **Beteende vid fel i viktiga mått**.

      >[!NOTE]
      >Se [Lägga till och hantera databaser](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) om du vill lära dig hur du lägger till och hanterar databaser i Cloud Manager.

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-edit2.png)


   1. The **Källa** -fliken ger dig möjlighet att markera eller avmarkera **Pausa innan du distribuerar till produktion** och **Schemalagd** alternativ från **Alternativ för produktionsdistribution**.

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-editnotier.png)

   1. The **Experience Audit** kan du uppdatera eller lägga till nya sidor.

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-edit4.png)

1. Klicka på **Uppdatera** när du är klar med redigeringen.

### Ytterligare produktionsförloppsåtgärder {#additional-prod-actions}

#### Köra en produktionspipeline {#run-prod}

Du kan köra produktionsflödet från pipelines-kortet:

1. Navigera till **Pipelines** från **Programöversikt** sida.

1. Klicka på **...** från **Pipelines** kort och klicka på **Kör**, vilket visas i figuren nedan.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-run.png)

#### Ta bort en produktionspipeline {#delete-prod}

Du kan ta bort produktionsflödet från pipelines-kortet:

1. Navigera till **Pipelines** från **Programöversikt** sida.

1. Klicka på **...** från **Pipelines** kort och klicka på **Ta bort**, vilket visas i figuren nedan.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-delete.png)

   >[!NOTE]
   >En användare i rollen Distributionshanterare kan nu ta bort produktionsflödet via självbetjäning via **Ta bort** från Pipeline-kortet.


## Icke-produktion och endast kodkvalitet, rörledningar {#non-production-pipelines}

Förutom den huvudsakliga rörledningen som distribuerar till scenen och produktionen kan kunderna även lägga upp ytterligare rörledningar, så kallade icke-produktionsrörledningar.
Det finns två typer av icke-produktionsrörledningar:

1. Kodkvalitet: Kör kodkvalitetsgenomsökningar på koden i en Git-gren. Detta tillvägagångssätt utför stegen för bygg- och kodkvalitet.
1. Distribution: Förutom att utföra stegen för bygg- och kodkvalitet distribuerar den här pipelinen koden till den valda icke-produktionen till AEM as a Cloud Service miljön.

### Lägga till en ny icke-produktionspipeline {#adding-non-production-pipeline}

På startskärmen visas dessa rörledningar i ett nytt kort:

1. Öppna **Pipelines** från startskärmen i Cloud Manager. Klicka på **+Lägg till** och markera **Lägg till icke-produktionsförlopp**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. **Lägg till icke-produktionsförlopp**  visas. Välj den typ av pipeline som du vill skapa, antingen **Kodkvalitetspipeline** eller **Distributionsförlopp**.

   >[!NOTE]
   >För distributionspipelines måste du välja distributionsmiljö.

   Dessutom kan du konfigurera **Utlösare för distribution** och **Beteende vid viktiga måttfel** från **Distributionsalternativ**. Klicka på **Fortsätt**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add2.png)

1. **Full Stack-kod** är markerat. Du kan välja **Databas** och **Git-gren**. Klicka på **Spara**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add3.png)

1. Den nyligen skapade icke-produktionsflödet visas nu i **Pipelines** kort.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add4.png)


   Rörledningen visas på kortet på startskärmen med tre åtgärder, som visas nedan:

   * **Lägg till** - gör det möjligt att lägga till en ny pipeline.
   * **Åtkomst till svarsinformation** - ger användaren tillgång till den information som krävs för att få åtkomst till Git-databasen i Cloud Manager.
   * **Läs mer** - navigerar till att förstå CI/CD-pipeline-dokumentationsresursen.

### Redigera en icke-produktionspipeline {#editing-nonprod-pipeline}

Du kan redigera pipeline-konfigurationerna från **Förloppskort** från **Programöversikt** sida.

Följ stegen nedan för att redigera den konfigurerade icke-produktionsflödet:

1. Navigera till **Pipelines** från **Programöversikt** sida.

1. Välj icke-produktionsflödet och klicka på **...**. Klicka på **Redigera**, vilket visas i figuren nedan.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-edit1.png)

1. The **Redigera produktionspipeline** visas.

   1. The **Konfiguration** kan du uppdatera **Pipelinenamn**, **Utlösare för distribution** och **Beteende vid viktiga måttfel**.

      >[!NOTE]
      >Se [Lägga till och hantera databaser](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) om du vill lära dig hur du lägger till och hanterar databaser i Cloud Manager.

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-edit2.png)


   1. The **Källkod** -fliken innehåller information om hur du uppdaterar **Databas** och **Git-gren**.

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-edit3.png)

1. Klicka på **Uppdatera** när du är klar med redigeringen av icke-produktionsflödet.

### Ytterligare icke-produktionsförloppsindikatorer {#additional-nonprod-actions}

#### Köra en icke-produktionspipeline {#run-nonprod}

Du kan köra produktionsflödet från pipelines-kortet:

1. Navigera till **Pipelines** från **Programöversikt** sida.

1. Klicka på **...** från **Pipelines** kort och klicka på **Kör**, vilket visas i figuren nedan.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-run1.png)

#### Ta bort en icke-produktionspipeline {#delete-nonprod}

Du kan ta bort produktionsflödet från pipelines-kortet:

1. Navigera till **Pipelines** från **Programöversikt** sida.

1. Klicka på **...** från **Pipelines** kort och klicka på **Ta bort**, vilket visas i figuren nedan.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-delete.png)


## Nästa steg {#the-next-steps}

När du har konfigurerat pipeline måste du distribuera koden.

Se [Distribuera koden](deploy-code.md) för mer information.
