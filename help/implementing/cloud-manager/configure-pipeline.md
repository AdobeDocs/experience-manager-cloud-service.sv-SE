---
title: Konfigurera CI/CD-pipeline - Cloud Services
description: Konfigurera CI/CD-pipeline - Cloud Services
translation-type: tm+mt
source-git-commit: 8d82bb8ee2b7aa234fc6b9b8efe23f04f4c66c87
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 0%

---


# Konfigurera CI-CD-pipeline {#configure-ci-cd-pipeline}


## Förstå flödet {#understanding-the-flow}

You can configure your production pipeline from the **Pipeline Settings** tile in the [!UICONTROL Cloud Manager] UI.

Distributionshanteraren ansvarar för att ställa in pipeline. När du gör det väljer du först en gren i **Git-databasen**.

För att konfigurera din pipeline måste användaren:

* Definiera den utlösare som ska starta pipelinen.
* Definiera parametrarna som styr produktionsdistributionen.
* konfigurera prestandatestparametrarna.

## Konfigurera pipeline {#setting-up-the-pipeline}

>[!CAUTION]
>
>Det går inte att konfigurera pipeline förrän ett program har skapats och Git-databasen har minst en gren.

Innan du börjar distribuera koden måste du konfigurera dina pipeline-inställningar från [!UICONTROL Cloud Manager].

>[!NOTE]
>
>Du kan ändra pipeline-inställningarna efter den första konfigurationen.

## Konfigurera Pipeline-inställningarna från [!UICONTROL Cloud Manager] {#configuring-the-pipeline-settings-from-cloud-manager}

När du har konfigurerat programmet och har minst en miljö med [!UICONTROL Cloud Manager] användargränssnittet är du redo att konfigurera ditt distributionsflöde.

Följ de här stegen för att konfigurera beteendet och inställningarna för din pipeline:

1. Klicka på **Konfigurera pipeline** för att konfigurera och konfigurera din pipeline.

   ![](assets/set-up-pipeline1.png)

1. Skärmen **Konfigurera pipeline** visas. Markera grenen och klicka på **Nästa**.

   ![](assets/set-up-pipeline2.png)

1. Konfigurera distributionsalternativen.

   ![](assets/set-up-pipeline3.png)

   Du kan definiera utlösaren för att starta pipelinen:

   * **Manuell** - med användargränssnittet startar du pipelinen manuellt.
   * **På Git Changes** - startar CI/CD-pipeline när implementeringar har lagts till i den konfigurerade Git-grenen. Även om du väljer det här alternativet kan du alltid starta pipelinen manuellt.

   Under pipeline-konfigurationen eller -redigeringen kan Deployment Manager välja att definiera pipeline-beteendet när ett viktigt fel påträffas i någon av kvalitetsportarna.

   Detta är användbart för kunder som vill ha mer automatiserade processer. De tillgängliga alternativen är:

   * **Fråga varje gång** - Det här är standardinställningen och kräver manuell åtgärd vid viktiga fel.
   * **Misslyckas omedelbart** - Om du väljer det här alternativet avbryts pipelinen varje gång ett viktigt fel inträffar. Detta emulerar i princip en användare som manuellt avvisar varje fel.
   * **Fortsätt omedelbart** - Om du väljer det här alternativet fortsätter pipeline automatiskt när ett viktigt fel inträffar. Detta emulerar i princip en användare som manuellt godkänner varje fel.


1. Klicka på **Nästa** för att gå till fliken **Testning** och definiera testvillkoren för programmet.

   ![](assets/set-up-pipeline4.png)

1. Click **Save**. På sidan *Översikt* visas nu **Distribuera ditt program** . Klicka på **Distribuera** för att distribuera programmet.

   ![](assets/configure-pipeline5.png)


## Icke-produktion och endast kodkvalitet, rörledningar

Förutom den huvudsakliga rörledningen som distribuerar till scenen och produktionen kan kunderna även lägga upp ytterligare rörledningar, så kallade **icke-produktionsrörledningar**. Dessa pipelines kör alltid stegen för bygg- och kodkvalitet. De kan också distribuera till Adobes miljö för hanterade tjänster.

På startskärmen visas dessa rörledningar i ett nytt kort:

1. Gå till **icke-produktionsförloppsindikatorn** från startskärmen i Cloud Manager.

   ![](assets/configure-pipeline6.png)

1. Klicka på knappen **Lägg** till för att ange Pipelinenamn, Pipelinetyp och Git-grenen.

   Dessutom kan du konfigurera utlösare för distribution och Beteende för viktigt fel i alternativen för pipeline.

   ![](assets/non-prod-pipe1.png)

1. Klicka på **Spara** och pipeline visas på kortet på startskärmen med tre åtgärder, som visas nedan:

   ![](assets/configure-pipeline8.png)

   * **Redigera** - tillåter redigering av pipeline-inställningarna
   * **Build** - navigerar till körningssidan, från vilken pipeline kan köras
   * **Hantera Git** - ger användaren tillgång till den information som krävs för att få åtkomst till Cloud Manager Git-databasen

## Nästa steg {#the-next-steps}

När du har konfigurerat pipeline måste du distribuera koden.

Mer information finns i [Distribuera koden](deploy-code.md) .
