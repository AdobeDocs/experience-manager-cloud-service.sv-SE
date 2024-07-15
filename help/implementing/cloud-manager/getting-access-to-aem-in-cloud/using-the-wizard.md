---
title: Guiden Skapa projekt
description: Lär dig mer om guiden för att skapa projekt så att du snabbt kan konfigurera projektet efter att du har skapat produktionsprogrammet.
exl-id: 03736ca7-1345-4faf-a61a-f9213ab5c89a
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---

# Guiden Skapa projekt {#project-creation-wizard}

När du har skapat ditt produktionsprogram erbjuder Cloud Manager en guide för att skapa ett AEM projekt baserat på [AEM Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) för att snabbt komma igång.

Följ de här stegen för att skapa ett AEM programprojekt i Cloud Manager med hjälp av guiden.

1. Skapa ett produktionsprogram genom att följa stegen i dokumentet [Skapa produktionsprogram](creating-production-programs.md)

1. När programkonfigurationen är klar går du till skärmen **Översikt** för ditt program och tittar på anropskortet **Skapa gren och projekt** längst upp.

   ![Call-to-action-vård för guiden](assets/create-wizard1.png)

1. Klicka på **Skapa** för att starta guiden och bekräfta projektets **namn** och **namn på ny gren** i fönstret **Skapa en gren och ett projekt**.

   ![Skapa en gren och ett projekt](assets/create-wizard2.png)

1. Du kan också klicka på avgränsaren för att visa ytterligare parametrar för projektet. Standardvärdena anges av AEM Project Archettype och behöver vanligtvis inte ändras.

   ![Ytterligare projektparametrar](assets/create-wizard5.png)

1. Klicka på **Skapa** för att börja skapa projektet.


Ett **pågående projekt**-kort ersätter nu anropskortet **Skapa gren och projekt** som överst på skärmen **Programöversikt**.

![Projektskapande pågår](assets/create-wizard3.png)

När programmet har skapats ersätter ett **Lägg till miljö** kortet **Projekt under arbete** högst upp på skärmen **Programöversikt**.

![Lägg till miljö](assets/create-wizard4.png)

Nu har du ett AEM baserat på den AEM typen av arkiv som lagts till i Git-databasen och som kan användas som grund för utveckling för ditt eget projekt. Därefter kan du skapa miljöer där du kan distribuera projektkoden.

Mer information om hur du lägger till eller hanterar miljöer finns i [Hantera dina miljöer](/help/implementing/cloud-manager/manage-environments.md).

>[!NOTE]
>
>Guiden är bara tillgänglig för produktionsprogram. Eftersom [sandlådeprogram](introduction-sandbox-programs.md#auto-creation) innehåller automatisk projektgenerering behövs inte guiden.