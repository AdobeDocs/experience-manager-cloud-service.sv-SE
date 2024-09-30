---
title: Lägg till en Adobe-databas i Cloud Manager
description: Lär dig hur du lägger till en databas som hanteras med Adobe i Cloud Manager.
exl-id: 6c32c4ae-f48d-4440-bfc2-cdc1a3d59599
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 533fa72b7610f671a24461073112b7fb798ce166
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---

# Lägga till en Adobe-databas i Cloud Manager {#adobe-repositories}

Lär dig hur du lägger till en databas som hanteras med Adobe i Cloud Manager.

Sidan **Databaser** gör det enkelt att lägga till ytterligare databaser som hanteras med Adobe i ett valt program.

**Så här lägger du till en Adobe-databas i Cloud Manager:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj den organisation och det program som du vill lägga till en databas som hanteras med Adobe.

1. På sidan **Programöversikt** klickar du på fliken ![Mappikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) **Databaser** på sidomenyn. för att växla till sidan **Databaser**.

1. Klicka på **Lägg till databas** på sidan **Databaser** uppe till höger.

   ![Knappen Lägg till databas](assets/add-repository.png)

1. I dialogrutan **Lägg till databas** kontrollerar du att **Adobe-databas** är markerad som databastyp.

1. Ange följande i respektive textfält:

   * **Databasnamn** - Ett uttrycksfullt namn för den nya databasen.
   * **Förhandsgranskning av databas-URL** - Du behöver inte ange en URL-sökväg eller redigera den befintliga sökvägen eftersom infrastrukturen redan är på plats och helt integrerad och hanteras av Adobe.
   * **Beskrivning (valfritt)** - En detaljerad beskrivning av databasen.

   ![Dialogrutan Lägg till databas](assets/add-adobe-repository.png)

1. Klicka på **Spara**.
Din nya databas visas i tabellen på sidan **Databaser**.

Du kan nu associera en [CI/CD-pipeline](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) med den eller hantera den på sidan [**Databaser**](managing-repositories.md).

>[!TIP]
>
>Du kan också lägga till GitHub-databaser som du hanterar själv som [privata databaser](private-repositories.md).
