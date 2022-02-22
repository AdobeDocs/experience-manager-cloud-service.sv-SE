---
title: 'Skapa sandlådeprogram '
description: Lär dig hur du använder Cloud Manager för att skapa ett eget sandlådeprogram för utbildning, demo, POC eller andra icke-produktionssyften.
exl-id: 10011392-3059-4bb0-88db-0af1d390742e
source-git-commit: cf6941759dfc1e50928009490c7c518a89ed093e
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 0%

---

# Skapa sandlådeprogram {#create-sandbox-program}

Ett sandlådeprogram skapas vanligtvis för att användas för utbildning, löpande demonstrationer, aktivering, POC:er eller dokumentation och är inte avsett för livstrafik.

Läs mer om programtyper i dokumentet [Program- och programtyper.](program-types.md)

## Skapa ett sandlådeprogram {#create}

Följ de här stegen för att skapa ett sandlådeprogram.

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation.

1. Klicka på **Lägg till program** i skärmens övre högra hörn.

   ![Startsida för Cloud Manager](assets/first_timelogin1.png)

1. Välj **Konfigurera en sandlåda**, ange ett programnamn och klicka sedan på **Skapa**.

   ![Skapa programtyper](assets/create-sandbox.png)

Du ser ett nytt sandlådeprogramkort på landningssidan med en statusindikator allt eftersom installationsprocessen fortskrider.

![Skapa sandlåda från översiktssida](assets/program-create-setupdemo2.png)

## Använd din sandlåda {#access}

Du kan visa information om sandlådekonfigurationen och få tillgång till miljön (när den är tillgänglig) genom att visa programöversiktssidan.

1. På landningssidan för Cloud Manager klickar du på ellipsknappen i det nya programmet.

   ![Åtkomst till programöversikt](assets/program-overview-sandbox.png)

1. När projektet är klart kan du öppna **Åtkomst till svarsinformation** för att kunna använda ditt Git-svar.

   ![Programkonfiguration](assets/create-program4.png)

   >[!TIP]
   >
   >Mer information om hur du får åtkomst till och hanterar Git-databasen finns i dokumentet [Åtkomst till Git.](/help/implementing/cloud-manager/managing-code/accessing-repos.md)

1. När utvecklingsmiljön har skapats kan du använda **AEM** för att logga in AEM.

   ![AEM](assets/create-program-5.png)

1. När icke-produktionsflödet som distribueras till utvecklingsfasen är klart vägleder guiden dig att antingen få åtkomst till AEM utvecklingsmiljö eller att distribuera kod till utvecklingsmiljön.

   ![Distribuera sandlåda](assets/create-program-setup-deploy.png)

Om du behöver växla till ett annat program eller gå tillbaka till översiktssidan för att skapa ett annat program klickar du på programnamnet längst upp till vänster på skärmen för att visa **Navigera till** alternativ.

![Navigera till](assets/create-program-a1.png)
