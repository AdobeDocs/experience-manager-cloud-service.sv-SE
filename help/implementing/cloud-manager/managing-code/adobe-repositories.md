---
title: Lägga till Adobe-databaser i Cloud Manager
description: Lär dig hur du skapar databaser som hanteras med Adobe i Cloud Manager.
exl-id: 6c32c4ae-f48d-4440-bfc2-cdc1a3d59599
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 5d6d3374f2dd95728b2d3ed0cf6fab4092f73568
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---

# Lägga till Adobe-databaser i Cloud Manager {#adobe-repositories}

Lär dig hur du skapar databaser som hanteras med Adobe i Cloud Manager.

## Lägga till en Adobe-hanterad databas {#add-adobe-repository}

Fönstret **Databaser** gör det enkelt att lägga till fler Adobe-hanterade databaser för ditt program.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. På sidan **Programöversikt** väljer du fliken **Databaser** för att växla till sidan **Databaser**.

1. Klicka på **Lägg till databas** i verktygsfältet.

   ![Knappen Lägg till databas](assets/add-repository.png)

1. Ange namn och beskrivning enligt begäran och klicka på **Spara**.

   ![Dialogrutan Lägg till databas](assets/add-adobe-repository.png)

När guiden stängs visas din nya databas i tabellen i fönstret **Databaser**. Du kan nu associera en [CI/CD-pipeline](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) med den eller hantera den i fönstret [**Databaser**](managing-repositories.md).

>[!TIP]
>
>Du kan också lägga till GitHub-databaser som du hanterar själv som [privata databaser](private-repositories.md).
