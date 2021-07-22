---
title: Konfigurera molnresurser via Cloud Manager
description: Följ den här sidan för att lära dig hur du konfigurerar molnresurser via Cloud Manager
hide: true
hidefromtoc: true
index: false
source-git-commit: 9caf3447fedf13fa81bb616cc54b7cb6a08ff159
workflow-type: tm+mt
source-wordcount: '1023'
ht-degree: 0%

---

# Konfigurera molnresurser via Cloud Manager {#setup-cloud-resources}

Den systemadministratör som tilldelats rollen *Business Owner* bör ha åtkomst till och logga in på Cloud Manager. Därefter måste en teammedlem som tilldelats produktprofilen *Business Owner* logga in i Cloud Manager och skapa ditt molnprogram och dina miljöer så att ditt expertteam kan komma igång.

## Syfte {#objective}

Det här dokumentet hjälper dig att förstå hur dina molnresurser skapas och vem som kan göra det.

När du har läst det här avsnittet bör du förstå:

* En systemadministratör som tilldelats rollen *Business Owner* måste vara den första som får åtkomst till och loggar in på Cloud Manager.
* Hur ditt molnprogram och dina miljöer skapas.

## Introduktion {#introduction}

Din teammedlem som är tilldelad till produktprofilen för Cloud Manager Business Owner lägger till dina molnresurser via Cloud Manager. Den här personen är vanligtvis en person som förstår affärsbehoven och som slutför den ursprungliga installationen av Cloud Manager.

Följ nedanstående avsnitt för att lära dig hur du skapar dina [molntjänstprogram](#create-cloud-service-program) och [miljöer](#create-cloud-environments).

### Krav {#prerequisites}

* Den systemadministratör som tilldelats rollen *Business Owner* bör ha åtkomst till och logga in på Cloud Manager.

* Lär dig hur du [navigerar och loggar in på Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/what-is-required/navigate-to-cloud-manager.html?lang=en).

* Läs om [Cloud Manager-produktprofiler](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles).

* Förstå vad du bör tänka på när du skapar programmet. I den här videon får du veta mer.

* Förstå begreppen i Cloud Manager [program](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/understand-program-types.html?lang=en) och [miljöer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html?lang=en)

## Navigera till Cloud Manager {#navigate-cloud-manager}

1. *Business Owner*-användaren får ett välkomstmeddelande där de kan komma igång, eller om de inte kan hitta det går du direkt till [Adobe Experience Cloud](https://experience.adobe.com/#/@ccs/home) och loggar in med din Adobe ID.

   ![](/help/onboarding/onboarding-journey/assets/setup-resources1.png)

1. På Adobe Experience Cloud hemsida väljer du **Experience Manager**.

   ![](/help/onboarding/onboarding-journey/assets/setup-resources2.png)

1. Du kommer nu till AEM startsida. Starta **Cloud Manager** härifrån.

   ![](/help/onboarding/onboarding-journey/assets/setup-resources3.png)

1. Landningssidan för Cloud Manager visas, vilket visas i bilden nedan.

   ![](/help/onboarding/onboarding-journey/assets/setup-resources4.png)

1. Kontrollera att du har tilldelats produktprofilen Business Owner. Om du vill göra det väljer du din profil högst upp till höger, enligt nedan.

   ![](/help/onboarding/onboarding-journey/assets/setup-resources5.png)

1. Välj **Användarroller** och kontrollera att du är tilldelad till Business Owner.

   ![](/help/onboarding/onboarding-journey/assets/setup-resources6.png)

1. Detta bekräftar din användarroll som företagsägare.

   ![](/help/onboarding/onboarding-journey/assets/setup-resources7.png)

   Bra jobbat! Du har loggat in på Cloud Manager som företagsägare!

## Create Cloud Service Program {#create-cloud-service-program}

Följ stegen nedan för att skapa ditt molntjänstprogram från Cloud Manager:

1. Navigera till landningssidan för Cloud Manager enligt nedan.

   >[!NOTE]
   >Du måste vara en teammedlem som har tilldelats produktprofilen för Cloud Manager Business Owner för att kunna slutföra det här steget.

1. Här väljer du Lägg till program för att starta guiden Lägg till program. I videon får du lära dig hur du skapar AEMaaCS-programmet och viktiga överväganden innan du skapar programmet.

1. Om du vill ha steg-för-steg-anvisningar om hur du använder guiden Lägg till program går du hit.

   >[!CAUTION]
   >Kom ihåg att programnamnet inte kan ändras när det har skapats. Vi rekommenderar att du vet vilket namn du vill ge ditt program.

   Om du måste byta namn på ditt program måste du öppna ett ärende hos Adobe Support eller kontakta Adobe. De kommer att bidra till att effektivt ta bort programmet. Du måste börja om från början igen med potentiell förlust av arbete som teamet har gjort.

1. När ditt molnprogram har skapats kan du navigera till programmet och se programmets översiktssida enligt nedan:

1. Om du inte redan har gjort det är det ett bra tillfälle att lägga till dina utvecklarmedlemmar i ditt Cloud Manager-team, gå till Lägg till användare i Developer-produktprofilen och följ stegen som beskrivs.

1. Medlemmar som är tilldelade till produktprofilen för utvecklare kan logga in på Cloud Manager och Hantera Cloud Manager Git.


   Bra jobbat! Nu när ditt program har skapats är din Cloud Manager Git tillgänglig för dina utvecklare!


## Skapa dina molnmiljöer {#create-cloud-environments}

Följ stegen nedan för att skapa molnmiljöer från Cloud Manager:

1. När du har skapat ditt molnprogram kan du skapa dina molnmiljöer genom att gå till översiktssidan för Cloud Manager och välja Lägg till på miljökortet.

   >[!IMPORTANT]
   >En Cloud Manager-användare i rollen Business Owner eller Deployment Manager måste vara inloggad för att det här steget ska kunna slutföras.

   Titta dessutom på videosjälvstudiekursen för att lära dig mer om Cloud Manager-miljöer och hur du kan lägga till dem i ditt program.

1. Detta startar guiden för att lägga till miljö som hjälper dig att lägga till din miljö. Lägg till din utvecklingsmiljö först för att bekanta dig.

1. Om du inte redan har gjort det kan du lägga till dina utvecklarmedlemmar i ditt Cloud Manager-team nu, gå till Lägg till användare i Developer-produktprofilen och följa stegen som beskrivs. På så sätt kan utvecklarna komma igång med att navigera till Cloud Manager och Managing Cloud Manager Git.


   Grattis! Nu har dina molnmiljöer skapats och dina utvecklare har lagts till i teamet!

## What’s Next {#whats-next}

Teammedlemmarna måste beviljas behörighet för instansen eftersom behörighet att administrera Cloud Manager inte räcker. Nu när dina molnresurser har skapats och är tillgängliga för ditt team måste systemadministratören utse dina teammedlemmar till AEM som en Cloud Service produktprofiler från Admin Console.

Du bör fortsätta din introduktionsresa genom att gå igenom dokumentet Tilldela teammedlemmar till AEM som en Cloud Service produktprofiler.

>[!NOTE]
>För att få åtkomst till AEM som Cloud Service måste användare tillhöra någon av produktprofilerna AEM användare eller AEM administratörer. Läs mer.

## Ytterligare resurser {#additional-resources}

Följ de andra resurserna för att lära dig mer om:

* [Programtyper och lägga till ett program](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html?lang=en)
* [Miljötyper och tillägg av en miljö](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html?lang=en)
* [Hantera Cloud Manager Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/managing-code/accessing-git.html?lang=en)
* [Konfigurera åtkomst till AEM som en Cloud Service från Admin Console](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/overview.html?lang=en#adobe-ims-users)
