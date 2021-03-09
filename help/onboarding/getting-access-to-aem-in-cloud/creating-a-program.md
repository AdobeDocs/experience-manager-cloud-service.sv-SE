---
title: Skapa ett program - Cloud Service
description: Skapa ett program - Cloud Service
translation-type: tm+mt
source-git-commit: d85c0e9035ee09cf86aeea1cae20d545823eaca0
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 0%

---


# Skapa ett program {#create-a-program}

Den molnbaserade lösningen ger användaren de behörigheter som krävs och möjlighet att skapa ett program på en självbetjäningsmodell.

Guiden för att skapa ett program ber användaren att skicka in information beroende på vad användaren vill göra för att skapa programmet inom gränserna för vad som är tillgängligt för kunden eller organisationen.

Om det är första gången du använder Cloud Manager eller om det inte finns några program i klienten visas **skärmen Skapa ditt första program**. Om användaren väljer *Esc* eller klickar utanför dialogrutan visas följande skärm:

![](assets/create-program1.png)


## Använda guiden Skapa program {#using-create-program-wizard}

Beroende på vad användaren har för avsikt att skapa programmet inom gränserna för vad som är tillgängligt för den specifika kunden/organisationen, uppmanas användaren att skicka in en eller flera uppgifter.

![](assets/create-sandbox.png)


## Skapa ett sandlådeprogram {#create-sandbox-program}

Följ stegen nedan för att skapa ett sandlådeprogram:

1. Välj **Konfigurera en sandlåda** i guiden Skapa program. Användaren skickar programnamnet innan **Skapa** väljs.

   ![](assets/create-sandbox.png)

1. Användaren ser det nya sandlådeprogramkortet på landningssidan och kan hovra över det för att välja molnhanterarikonen för att navigera till översiktssidan för Cloud Manager. Kortet informerar användaren om status för automatisk installation av det nyskapade sandlådeprogrammet. Användaren ser förloppet.

   ![](assets/program-create-setupdemo2.png)

1. När programmet har konfigurerats och projektskapandet har slutförts kan användaren komma åt länken **Hantera Git**, vilket visas i bilden nedan:

   ![](assets/create-program4.png)

   >[!NOTE]
   >
   >Mer information om hur du får åtkomst till och hanterar Git-databasen med hjälp av Git-kontohantering för självbetjäning från användargränssnittet i Cloud Manager finns i [Åtkomst till Git](/help/implementing/cloud-manager/accessing-git.md).


1. När utvecklingsmiljön har skapats kan användaren **komma åt AEM**-länken, vilket visas i bilden nedan:

   ![](assets/create-program-5.png)

1. När icke-produktionsflödet som distribueras till utveckling är klart vägleder guiden användaren till antingen åtkomst AEM (under utveckling) eller distribution av kod till utvecklingsmiljön:

   ![](assets/create-program-setup-deploy.png)

   >[!NOTE]
   >Du kan också redigera, byta eller lägga till ett program från sidan Översikt över Cloud Manager, enligt nedan:

   ![](assets/create-program-a1.png)

## Tar bort ett sandlådeprogram {#delete-sandbox-program}

En användare av sandlådeprogrammet i *Business Owner* eller *Deployment Manager*-rollen i Cloud Manager kan ta bort sin produktions- och scenmiljö som angetts via användargränssnittet i molnhanteraren.

>[!NOTE]
>Om du väljer borttagningsalternativet för antingen produktion eller scen tas även det andra bort i uppsättningen.

Borttagningsalternativet är tillgängligt från landningssidan enligt nedan:

![](assets/delete-sandbox1.png)

Eller

Välj **Ta bort program** från sidan **Programöversikt** om du vill ta bort ditt Sandbox-program.

![](assets/delete-sandbox2.png)


## Skapa ett vanligt program {#create-regular-program}

Ett *Regelbundet*-program är avsett för användare som är bekanta med AEM och Cloud Manager och som är redo att börja skriva, bygga och testa kod i syfte att distribuera den till Production.

Följ stegen nedan för att skapa ett vanligt program:

1. Välj **Konfigurera för produktion** i guiden Skapa program för att skapa ett vanligt program. Användaren kan godkänna standardprogramnamnet eller redigera det innan **Fortsätt** väljs.

   ![](assets/create-prod1.png)

1. Användaren väljer lösningar som ska inkluderas i programmet på skärmen som visas efter skärmen ovan.



   >[!NOTE]
   >
   >Skärmen nedan visas endast för de kunder som har köpt mer än en lösning. För kunder som bara köpt en lösning visas inte skärmen för val av lösning nedan.

   ![](assets/set-up-prod2.png)

1. När du har valt lösningarna klickar du på **Skapa**.

   ![](assets/set-up-prod3.png)

1. När du ser ditt programkort på landningssidan för du pekaren över det och väljer ikonen Cloud Manager för att gå till sidan med Cloud Manager **Översikt**.

   ![](assets/set-up-prod4.png)

1. Det huvudsakliga anropskortet leder användaren till att skapa en miljö, skapa ett icke-produktionsflöde och slutligen till en produktionsprocess.
   ![](assets/set-up-prod5.png)


   >[!NOTE]
   >
   >Ett vanligt program har inte funktionen **Auto-setup**.





