---
title: Skapa sandlådeprogram
description: Lär dig hur du använder Cloud Manager för att skapa ett eget sandlådeprogram för utbildning, demo, POC eller andra icke-produktionssyften.
exl-id: 10011392-3059-4bb0-88db-0af1d390742e
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---

# Skapa sandlådeprogram {#create-sandbox-program}

Ett sandlådeprogram skapas vanligtvis för att användas för utbildning, löpande demonstrationer, aktivering, POC:er eller dokumentation och är inte avsett för livstrafik.

Läs mer om programtyper i dokumentet [Om program- och programtyper.](program-types.md)

## Skapa ett sandlådeprogram {#create}

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.

1. På konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)** trycker eller klickar du på **Lägg till program** i skärmens övre högra hörn.

   ![Cloud Manager landningssida](assets/log-in.png)

1. Välj **Konfigurera en sandlåda** i guiden Skapa program och ange ett programnamn.

   ![Skapa programtyp](assets/create-sandbox.png)

1. Du kan också lägga till en bild i programmet genom att dra och släppa en bildfil till målet **Lägg till en programbild** eller genom att klicka på den och välja en bild i en filläsare. Välj **Fortsätt**.

   * Bilden fungerar bara som plattan i programöversiktsfönstret och hjälper till att identifiera programmet.

1. I dialogrutan **Konfigurera din sandlåda** väljer du vilka lösningar du vill aktivera i ditt sandlådeprogram genom att kontrollera alternativen i tabellen **Lösningar och tillägg** .

   * Använd ändringarna bredvid lösningsnamnen så att du kan se ytterligare valfria tillägg för lösningarna.

   * Lösningarna **Webbplatser** och **Assets** ingår alltid i sandlådeprogram och kan inte avmarkeras.

   ![Välj lösningar och tillägg för en sandlåda](assets/sandbox-solutions-add-ons.png)

1. När du har valt lösningar och tillägg för ditt sandlådeprogram klickar du på **Skapa**.

Du ser ett nytt sandlådeprogramkort på landningssidan med en statusindikator allt eftersom installationsprocessen fortskrider.

![Skapa sandlåda från översiktssida](assets/sandbox-setup.png)

## Sandlådeåtkomst {#access}

Du kan visa detaljerna i sandlådekonfigurationen och få tillgång till miljön (när den är tillgänglig) genom att visa programöversiktssidan.

1. På Cloud Manager landningssida klickar du på ellipsknappen på det skapade programmet.

   ![Åtkomst till programöversikt](assets/program-overview-sandbox.png)

1. När du har skapat projektet kan du komma åt länken **Åtkomst till informationen** och använda Git-svaret.

   ![Programkonfiguration](assets/create-program4.png)

   >[!TIP]
   >
   >Mer information om hur du får åtkomst till och hanterar Git-databasen finns i [Åtkomst till Git](/help/implementing/cloud-manager/managing-code/accessing-repos.md).

1. När utvecklingsmiljön har skapats kan du använda länken **Åtkomst AEM** för att logga in på AEM.

   ![AEM](assets/create-program5.png)

1. När den icke-produktionsprocess som distribueras till utvecklingsfasen är klar vägleder guiden i anropet dig till att antingen få åtkomst till AEM utvecklingsmiljö eller att distribuera kod till utvecklingsmiljön.

   ![Distribuerar sandlåda](assets/create-program-setup-deploy.png)

>[!TIP]
>
>Dokumentet [Navigera i Cloud Manager-gränssnittet](/help/implementing/cloud-manager/navigation.md) innehåller information om hur du navigerar i Cloud Manager och förstår **Mina program**-konsolen.
