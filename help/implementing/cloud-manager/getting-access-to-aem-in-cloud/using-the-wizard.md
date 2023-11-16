---
title: Guiden Skapa projekt
description: Lär dig mer om guiden för att skapa projekt så att du snabbt kan konfigurera projektet efter att du har skapat produktionsprogrammet.
exl-id: 03736ca7-1345-4faf-a61a-f9213ab5c89a
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---

# Guiden Skapa projekt {#project-creation-wizard}

När du har skapat ditt produktionsprogram kan du använda en guide för att skapa ett AEM baserat på [AEM Project Archettype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) för att snabbt komma igång.

Följ de här stegen för att skapa ett AEM programprojekt i Cloud Manager med hjälp av guiden.

1. Skapa ett produktionsprogram genom att följa stegen i dokumentet [Skapa produktionsprogram](creating-production-programs.md)

1. När programmet är klart kan du få åtkomst till **Ökning** -skärmen i programmet och se **Skapa gren och projekt** telefonsamtalskort överst.

   ![Call-to-action-vård för guiden](assets/create-wizard1.png)

1. Klicka **Skapa** för att starta guiden och bekräfta projektet **Titel** och **Nytt grennamn** i **Skapa en gren och ett projekt** -fönstret.

   ![Skapa en gren och ett projekt](assets/create-wizard2.png)

1. Du kan också klicka på avgränsaren för att visa ytterligare parametrar för projektet. Standardvärdena anges av AEM Project Archettype och behöver vanligtvis inte ändras.

   ![Ytterligare projektparametrar](assets/create-wizard5.png)

1. Klicka **Skapa** för att starta projektskapandet.


A **Projekt skapas** kortet ersätter nu **Skapa gren och projekt** telefonsvararkort som överst på **Programöversikt** skärm.

![Projektskapande pågår](assets/create-wizard3.png)

När programmet är klart **Lägg till miljö** kortet ersätter **Projekt skapas** överst på **Programöversikt** skärm.

![Lägg till miljö](assets/create-wizard4.png)

Nu har du ett AEM baserat på den AEM typen av arkiv som lagts till i Git-databasen och som kan användas som grund för utveckling för ditt eget projekt. Därefter kan du skapa miljöer där du kan distribuera projektkoden.

Se [Hantera dina miljöer](/help/implementing/cloud-manager/manage-environments.md) om du vill lära dig hur du lägger till eller hanterar miljöer.

>[!NOTE]
>
>Guiden är bara tillgänglig för produktionsprogram. För [sandlådeprogram](introduction-sandbox-programs.md#auto-creation) innehåller automatisk projektgenerering. Guiden behövs inte.