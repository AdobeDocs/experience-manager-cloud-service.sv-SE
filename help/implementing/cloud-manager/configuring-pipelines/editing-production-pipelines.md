---
title: Redigera en produktionspipeline
description: Redigera en produktionspipeline
index: true
source-git-commit: d090329c46155d77a7b132583c777c09555a03c9
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 0%

---


# Redigera en produktionspipeline {#edit-prod-pipeline}

Du kan redigera pipeline-konfigurationerna från **Programöversikt** sida.

>[!IMPORTANT]
>Du kan inte redigera en pipeline som körs.

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

## Ytterligare produktionsförloppsåtgärder {#additional-prod-actions}

### Köra en produktionspipeline {#run-prod}

Du kan köra produktionsflödet från pipelines-kortet:

1. Navigera till **Pipelines** från **Programöversikt** sida.

1. Klicka på **...** från **Pipelines** kort och klicka på **Kör**, vilket visas i figuren nedan.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-run.png)

### Ta bort en produktionspipeline {#delete-prod}

Du kan ta bort produktionsflödet från pipelines-kortet:

1. Navigera till **Pipelines** från **Programöversikt** sida.

1. Klicka på **...** från **Pipelines** kort och klicka på **Ta bort**, vilket visas i figuren nedan.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-delete.png)

   >[!NOTE]
   >En användare i rollen Distributionshanterare kan nu ta bort produktionsflödet via självbetjäning via **Ta bort** från Pipeline-kortet.