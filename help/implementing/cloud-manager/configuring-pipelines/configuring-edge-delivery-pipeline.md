---
title: Lägg till en Edge Delivery Pipeline
description: Lär dig hur du lägger till en Edge Delivery-pipeline för att bygga och driftsätta din kod i produktionsmiljöer.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
badge: label="Beta" type="Positive" url="/help/implementing/cloud-manager/release-notes/current.md#gitlab-bitbucket"
hide: false
index: false
hidefromtoc: false
exl-id: 5ad342fa-dd71-4105-a9cb-2d999d402780
source-git-commit: dbd4ef8d782c9d05e50cab7479adbbc16d6a247d
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---

# Lägg till en Edge Delivery-pipeline {#configure-production-pipeline}

Lär dig hur du konfigurerar Edge Delivery-pipelines för att bygga och driftsätta din kod i produktionsmiljöer. En produktionspipeline distribuerar kod först till scenmiljön. Vid godkännande distribueras samma kod till produktionsmiljön.

En användare måste ha rollen **[Distributionshanteraren](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)** för att kunna konfigurera produktionspipelines.

>[!NOTE]
>
>En Edge Delivery-pipeline kan inte konfigureras förrän följande har inträffat:
>
>* Ett program som innehåller en Edge Delivery Services-webbplats och en mappad domän skapas. I annat fall visas alternativet **Lägg till Edge Delivery Pipeline** inaktiverat i användargränssnittet och ett verktygstips förklarar saknade krav.
>* Git-databasen har minst en gren.
>* Produktions- och mellanlagringsmiljöerna skapas.

<!-- CMGR‑69680 -->


Innan du börjar distribuera koden måste du konfigurera dina pipeline-inställningar från [!UICONTROL Cloud Manager].

>[!NOTE]
>
>Du kan [redigera pipeline-inställningar](managing-pipelines.md) efter den första konfigurationen.

**Så här lägger du till en Edge Delivery-pipeline:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj önskad organisation.

1. På sidan **Mina program** väljer du det program du vill ha.

   ![Sidan Mina program i Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/assets/my-programs.png)

1. Gör något av följande:

   * **Lägg till en Edge Delivery-pipeline från pipelines-kortet**

      1. Klicka på ikonen **Översikt** **![Översikt](/help/implementing/cloud-manager/configuring-pipelines/assets/overview.svg) i den vänstra listen under [Program](/help/implementing/cloud-manager/navigation.md#my-programs)**.
      1. På sidan **Programöversikt**, under kortet **Pipelines**, klickar du på **![Plustecken](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Add_18_N.svg)Lägg till** och väljer sedan **Lägg till Edge Delivery Pipeline**.

         ![Rörledningskortet på sidan Programöversikt](/help/implementing/cloud-manager/configuring-pipelines/assets/pipelinescard-add-ed-pipeline.png)

   * **Lägg till en Edge Delivery-pipeline från sidan för pipeline**

      1. Klicka på ikonen **Arbetsflöde eller Pipelines** Pipelines **![i den vänstra listen under ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg)Program**.
      1. Klicka på **Lägg till pipeline** > **Lägg till Edge Delivery-pipeline** på sidan Pipelines, i det övre högra hörnet.

         ![Sidan Pipelines med knappen Lägg till pipeline](/help/implementing/cloud-manager/configuring-pipelines/assets/pipelinespage-add-ed-pipeline.png)

1. I dialogrutan **Lägg till Edge Delivery-pipeline** skriver du en beskrivande pipeline-etikett i textfältet **Pipelinenamn**.

   ![Dialogrutan Lägg till Edge Delivery-pipeline](/help/implementing/cloud-manager/configuring-pipelines/assets/add-edge-delivery-pipeline-configuration.png)

1. Markera alternativet **Distributionutlösare** som du vill använda.

   * **Manuell** - Du startar distributionen.
   * **Vid Git-ändringar** - Git startar distributionen automatiskt. Med det här alternativet kan du fortfarande starta pipelinen manuellt, om det behövs.

1. Klicka på **Fortsätt**.

1. Ange följande alternativ under **Source-kod**:

   * **Distributionsmiljö** - Visar målmiljöfältet, men är fortfarande skrivskyddat.

   * **Databas** - Använd den nedrullningsbara listan för att peka pipelinen mot den exakta Git-databasen som lagrar Edge Delivery-konfigurationen.

     Se även [Lägg till och hantera databaser](/help/implementing/cloud-manager/managing-code/managing-repositories.md) för att lära dig hur du lägger till och hanterar databaser i Cloud Manager.

   * **Git-gren** - Använd listrutan för att välja en specifik gren i den valda databasen. Om det behövs klickar du på ikonen ![Papperskorgen eller ikonen Uppdatera](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Refresh_18_N.svg) för att läsa in den nedrullningsbara listan för Git-grenen igen efter senaste push-meddelanden
   * **Kodplats** - Definierar mappsökvägen inuti databasen där pipeline-klar kod startar ( `/` är lika med databasroten).

   ![Konfigurera pipeline](/help/implementing/cloud-manager/configuring-pipelines/assets/add-edge-delivery-pipeline-sourcecode.png)

1. Klicka på **Spara**.

Du kan nu [hantera din pipeline](managing-pipelines.md) på **pipelines**-kortet på sidan **Programöversikt** eller från sidan **Pipelines**.
