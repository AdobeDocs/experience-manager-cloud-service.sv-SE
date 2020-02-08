---
title: Skapa ett program - molntjänst
description: Skapa ett program - molntjänst
translation-type: tm+mt
source-git-commit: 57206e36725e28051b2468d47da726e318bd763b

---


# Skapa ett program {#create-a-program}

Den molnbaserade lösningen ger användaren de behörigheter som krävs och möjlighet att skapa ett program på en självbetjäningsmodell.

Guiden för att skapa ett program ber användaren att skicka in information beroende på vad användaren vill göra för att skapa programmet inom gränserna för vad som är tillgängligt för kunden eller organisationen.

Om det är första gången du får tillgång till Cloud Manager eller om det inte finns några program i klienten visas **Skapa ditt första program** -fönster. Om användaren väljer *Esc* eller klickar utanför dialogrutan visas följande skärm:

![](assets/create-program1.png)


## Använda guiden Skapa program {#using-create-program-wizard}

Beroende på vad användaren har för avsikt att skapa programmet inom gränserna för vad som är tillgängligt för den specifika kunden/organisationen, uppmanas användaren att skicka in en eller flera uppgifter.

![](assets/create-program-2.png)

>[!NOTE]
>Om det redan finns ett program visas **Lägg till program** överst till höger på landningssidan, vilket visas i bilden nedan.

![](assets/create-program-add.png)

## Skapa ett demoprogram {#create-demo-program}

>[!NOTE]
>
Ett demonstrationsprogram är detsamma som ett sandlådeprogram i användargränssnittet i Cloud Manager.

Följ stegen nedan för att skapa ett sandlådeprogram:

1. Välj **Konfigurera en demo** i guiden Skapa program. Användaren skickar programnamnet innan han/hon väljer **Skapa**.

   ![](assets/create-program-setupdemo.png)

1. Användaren ser det nya sandlådeprogramkortet på landningssidan och kan hovra över det för att välja molnhanterarikonen för att navigera till översiktssidan för Cloud Manager. Kortet informerar användaren om status för automatisk installation av det nyskapade sandlådeprogrammet. Användaren ser förloppet.

   ![](assets/program-create-setupdemo2.png)

1. När programmet har konfigurerats och projektskapandet är klart kan användaren få åtkomst till **länken Hantera Git** , vilket visas i bilden nedan:

   ![](assets/create-program4.png)

   >[!NOTE]
   >
   >Mer information om hur du får åtkomst till och hanterar Git-databasen med hjälp av Git-kontohantering för självbetjäning från användargränssnittet i Cloud Manager finns i [Åtkomst till Git](/help/implementing/cloud-manager/accessing-git.md).


1. När utvecklingsmiljön har skapats kan användaren **komma åt AEM** -länken, vilket visas i bilden nedan:

   ![](assets/create-program-5.png)

1. När icke-produktionsflödet som distribueras till utvecklingsfasen är klart vägleder guiden användaren till antingen åtkomst till AEM (under utveckling) eller distribution av kod till utvecklingsmiljön:

   ![](assets/create-program-setup-deploy.png)


## Skapa ett vanligt program {#create-regular-program}

Ett *Regelbundet* program är avsett för användare som är bekanta med AEM och Cloud Manager och som är redo att börja skriva, bygga och testa kod i syfte att distribuera den till Production.

Följ stegen nedan för att skapa ett vanligt program:

1. Välj **Konfigurera för produktion** i guiden Skapa program för att skapa ett vanligt program. Användaren kan godkänna standardprogramnamnet eller redigera det innan du väljer **Fortsätt**.

   ![](assets/set-up-prod1.png)

1. Användaren väljer lösningar som ska inkluderas i programmet på skärmen som visas efter skärmen ovan.



   >[!NOTE]
   >
   >Skärmen nedan visas endast för de kunder som har köpt mer än en lösning. För kunder som bara köpt en lösning visas inte skärmen för val av lösning nedan.

   ![](assets/set-up-prod2.png)

1. När du har valt lösningarna klickar du på **Skapa**.

   ![](assets/set-up-prod3.png)

1. När du ser ditt programkort på landningssidan för du pekaren över det och väljer ikonen Cloud Manager för att navigera till **översiktssidan** för Cloud Manager.

   ![](assets/set-up-prod4.png)

1. Det huvudsakliga anropskortet leder användaren till att skapa en miljö, skapa ett icke-produktionsflöde och slutligen till en produktionsprocess.
   ![](assets/set-up-prod5.png)


   >[!NOTE]
   >
   >Ett vanligt program har ingen **autoinstallationsfunktion** .





