---
title: Redigera en icke-produktionspipeline
description: Redigera en icke-produktionspipeline
index: true
source-git-commit: 7dc9f9a189927f3522445fac36a1606521f410b2
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---


# Redigera en icke-produktionspipeline {#edit-non-prod-pipeline}

Du kan redigera pipeline-konfigurationerna från **Förloppskort** från **Programöversikt** sida.

>[!IMPORTANT]
>Du kan inte redigera en pipeline som körs.

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

## Ytterligare icke-produktionsförloppsindikatorer {#additional-nonprod-actions}

### Köra en icke-produktionspipeline {#run-nonprod}

Du kan köra produktionsflödet från pipelines-kortet:

1. Navigera till **Pipelines** från **Programöversikt** sida.

1. Klicka på **...** från **Pipelines** kort och klicka på **Kör**, vilket visas i figuren nedan.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-run1.png)

### Ta bort en icke-produktionspipeline {#delete-nonprod}

Du kan ta bort produktionsflödet från pipelines-kortet:

1. Navigera till **Pipelines** från **Programöversikt** sida.

1. Klicka på **...** från **Pipelines** kort och klicka på **Ta bort**, vilket visas i figuren nedan.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-delete.png)
