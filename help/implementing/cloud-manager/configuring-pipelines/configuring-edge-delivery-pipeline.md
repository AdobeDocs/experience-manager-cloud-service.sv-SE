---
title: Lägg till en Edge Delivery Pipeline
description: Lär dig hur du lägger till en Edge Delivery-pipeline för att bygga och driftsätta din kod i produktionsmiljöer.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
hide: false
index: false
hidefromtoc: false
exl-id: 5ad342fa-dd71-4105-a9cb-2d999d402780
source-git-commit: 9ad50747b46b75c33cb5b034e8b8e41d5079e967
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 0%

---

# Lägg till en Edge Delivery-pipeline {#configure-production-pipeline}

<!--badge: label="Beta" type="Positive" url="/help/implementing/cloud-manager/release-notes/current.md#gitlab-bitbucket" -->

Lär dig hur du konfigurerar Edge Delivery-pipelines för att bygga och driftsätta din kod i produktionsmiljöer. Med Edge Delivery-pipelines kan du konfigurera funktioner som vidarebefordran av loggfiler och Adobe-hanterat CDN.

En lista över konfigurationer som stöds finns i [Använda konfigurationspipelines - konfigurationer som stöds](/help/operations/config-pipeline.md#configurations).

En användare måste ha rollen **[Distributionshanteraren](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)** för att kunna konfigurera produktionspipelines.

>[!IMPORTANT]
>
>En Edge Delivery-pipeline kan inte konfigureras förrän följande har inträffat:
>
>* Ett program som innehåller en Edge Delivery Services-webbplats och en mappad domän skapas. Annars visas alternativet **Lägg till Edge Delivery Pipeline** inaktiverat i användargränssnittet och ett verktygstips förklarar saknade krav. Se [Skapa en Edge Delivery-webbplats i Cloud Manager](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md)
>* Git-databasen har minst en gren. Se [Hantera databaser i Cloud Manager](/help/implementing/cloud-manager/managing-code/managing-repositories.md).
>* Produktions- och mellanlagringsmiljöerna skapas. Se [Introduktion till CI/CD-pipeline](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md).

<!-- CMGR‑69680 -->

Innan du börjar distribuera koden måste du konfigurera dina pipeline-inställningar från [!UICONTROL Cloud Manager].

>[!NOTE]
>
>Du kan [redigera pipeline-inställningar](managing-pipelines.md) efter den första konfigurationen.

**Så här lägger du till en Edge Delivery-pipeline:**

1. Logga in på Cloud Manager på [experience.adobe.com](https://experience.adobe.com).
1. Klicka på **Experience Manager** i avsnittet **Snabbåtkomst**.
1. Klicka på **Cloud Manager** på den vänstra panelen.
1. Välj en organisation som du vill ha.
1. Klicka på ett program på konsolen **Mina program**.

   ![Sidan Mina program i Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/assets/my-programs.png)

1. Gör något av följande:

   * **Lägg till en Edge Delivery-pipeline från pipelines-kortet**

      1. Klicka på ikonen **Översikt** **![Översikt](/help/implementing/cloud-manager/configuring-pipelines/assets/overview.svg) i den vänstra listen under [Program](/help/implementing/cloud-manager/navigation.md#my-programs)**.
      1. På sidan **Programöversikt**, under kortet **Pipelines**, klickar du på **![Plustecken](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Add_18_N.svg)Lägg till** och väljer sedan **Lägg till Edge Delivery Pipeline**.

         ![Rörledningskortet på sidan Programöversikt](/help/implementing/cloud-manager/configuring-pipelines/assets/pipelinescard-add-ed-pipeline.png)

         >[!TIP]
         >
         >Förutom att använda kortet **Pipeline** så som det visas på skärmbilden ovan, kan du även hantera din pipeline från sidan **Pipelines**.
         >
         >![Edge Delivery pipeline-widget med pipeline-namn, status, databas och gren](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-widget.png)

   * **Lägg till en Edge Delivery-pipeline från sidan för pipeline**

      1. Klicka på ikonen **Arbetsflöde eller Pipelines** Pipelines **![i den vänstra listen under &#x200B;](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg)Program**.
      1. Klicka på **Lägg till pipeline** > **Lägg till Edge Delivery-pipeline** på sidan Pipelines, i det övre högra hörnet.

         ![Sidan Pipelines med knappen Lägg till pipeline](/help/implementing/cloud-manager/configuring-pipelines/assets/pipelinespage-add-ed-pipeline.png)

         >[!TIP]
         >
         >I närheten av det övre vänstra hörnet klickar du på **Filter** och under avsnittet **Leveranstyp** markerar du kryssrutan **Edge-leverans** för att filtrera listan till endast Edge Delivery-pipelines (d.v.s. rörledningar som använder Edge Delivery Services). <!-- (CMGR-69682) -->
         >
         >![Filterpanelen visar den nya leveranstypen för Edge-leverans och Publicera leverans](/help/implementing/cloud-manager/release-notes/assets/filter-delivery-type.png)

1. I dialogrutan **Lägg till Edge Delivery-pipeline** skriver du en beskrivande pipeline-etikett i textfältet **Pipelinenamn**.

   ![Dialogrutan Lägg till Edge Delivery-pipeline](/help/implementing/cloud-manager/configuring-pipelines/assets/add-edge-delivery-pipeline-configuration.png)

1. Välj alternativet **Distributionutlösare** som du vill använda.

   * **Manuell** - Du startar distributionen.
   * **Vid Git-ändringar** - Git startar distributionen automatiskt. Med det här alternativet kan du fortfarande starta pipelinen manuellt, om det behövs.

1. Klicka på **Fortsätt**.

1. Ange följande alternativ under **Source-kod**:

   * **Distributionsmiljö** - Visar målmiljöfältet, men är fortfarande skrivskyddat.

   * **Databas** - Använd den nedrullningsbara listan för att peka pipelinen mot den exakta Git-databasen som lagrar Edge Delivery-konfigurationen.

     Se även [Lägg till och hantera databaser](/help/implementing/cloud-manager/managing-code/managing-repositories.md) för att lära dig hur du lägger till och hanterar databaser i Cloud Manager.

   * **Git-gren** - Använd listrutan för att välja en specifik gren i den valda databasen. Om det behövs klickar du på ikonen ![Papperskorgen eller ikonen Uppdatera](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Refresh_18_N.svg) för att läsa in den nedrullningsbara listan för Git-grenen igen när du har använt den nyligen.
   * **Kodplats** - Definierar mappsökvägen inuti databasen där pipeline-klar kod startar ( `/` är lika med databasroten).

   ![Konfigurera pipeline](/help/implementing/cloud-manager/configuring-pipelines/assets/add-edge-delivery-pipeline-sourcecode.png)

1. Klicka på **Spara**.

Du kan nu [hantera din pipeline](managing-pipelines.md) från kortet **Pipelines** på sidan **Programöversikt** eller från sidan **Pipelines**.


![Edge Delivery pipeline-widget med pipeline-namn, status, databas och gren](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-widget.png)



