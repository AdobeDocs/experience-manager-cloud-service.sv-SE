---
title: Konfigurera molnresurser via Cloud Manager
description: Följ den här sidan för att lära dig hur du konfigurerar molnresurser via Cloud Manager
role: Admin, User, Developer
source-git-commit: d8ff6f4386ab0e5df4f770cdb566facc1cc0cc98
workflow-type: tm+mt
source-wordcount: '1424'
ht-degree: 0%

---

# Konfigurera molnresurser via Cloud Manager {#setup-cloud-resources}

Den systemadministratör som tilldelats rollen Business Owner ska ha åtkomst till och logga in i Cloud Manager. Därefter måste en teammedlem som tilldelats produktprofilen Business Owner logga in på Cloud Manager och skapa ditt molnprogram och miljöer så att ditt expertteam kan komma igång.

## Syfte {#objective}

Det här dokumentet hjälper dig att förstå hur dina molnresurser skapas och vem som kan göra det.

När du har läst det här avsnittet bör du förstå:

* En systemadministratör som tilldelats rollen Business Owner måste vara den första som har åtkomst till och loggar in på Cloud Manager.
* Hur ditt molnprogram och dina miljöer skapas.

## Introduktion {#introduction}

Din teammedlem som är tilldelad till produktprofilen för Cloud Manager Business Owner lägger till dina molnresurser via Cloud Manager. Den här personen är vanligtvis en person som förstår affärsbehoven och som slutför den ursprungliga installationen av Cloud Manager.

Följ nedanstående avsnitt för att lära dig hur du skapar dina [molntjänstprogram](#create-cloud-service-program) och [miljöer](#create-cloud-environments).

### Krav {#prerequisites}

* Den systemadministratör som tilldelats rollen Business Owner ska ha åtkomst till och logga in i Cloud Manager.

* Lär dig hur du [navigerar och loggar in på Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/what-is-required/navigate-to-cloud-manager.html?lang=en).

* Läs om [Cloud Manager-produktprofiler](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles).

* Förstå begreppen i Cloud Manager [program](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/understand-program-types.html?lang=en) och [miljöer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html?lang=en)

## Navigera till Cloud Manager {#navigate-cloud-manager}

Business Owner-användaren får ett välkomstmeddelande med en länk för att komma igång, eller om de inte kan hitta det kan du komma åt [Cloud Manager](https://my.cloudmanager.adobe.com/) direkt genom att logga in med din Adobe ID.

Följ stegen nedan för att navigera till Cloud Manager:

1. I välkomstmeddelandet klickar du på **Kom igång**, vilket visas i bilden nedan.
   ![](/help/journey-onboarding/assets/get-started-email.png)

1. Du går till sidan **Program och produkter** i Cloud Manager.

   >[!IMPORTANT]
   >Du kan också navigera direkt till inloggningssidan för Cloud Manager från [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/). Bokmärk den här sidan för framtida referens och för att hjälpa dig att navigera direkt till Cloud Managers landningssida.

1. Du dirigeras till Cloud Managers landningssida. Mer information finns i [Visa Cloud Managers programavsnitt](#viewing-programs).

Dessutom kan du gå till sidan **Program och produkter** i Cloud Manager från Adobe Experience Cloud hemsida. Följ stegen nedan:

1. Navigera direkt till [Adobe Experience Cloud](https://experience.adobe.com) och logga in med din Adobe ID.

1. På Adobe Experience Cloud hemsida väljer du **Experience Manager**.

   ![](/help/journey-onboarding/assets/setup-resources2.png)

1. Du kommer nu till AEM startsida. Starta **Cloud Manager** härifrån.

   ![](/help/journey-onboarding/assets/setup-resources3.png)

1. När inloggningen är klar dirigeras du till landningssidan för Cloud Manager. Mer information finns i [Visa Cloud Managers programavsnitt](#viewing-programs).

   >[!NOTE]
   >Beroende på vilka roller som har tilldelats i [!UICONTROL Cloud Manager] och programmets status visas olika skärmar när du använder användargränssnittet för [!UICONTROL Cloud Manager].

### Visa program på Cloud Managers startsida {#viewing-programs}

När inloggningen är klar dirigeras du till landningssidan för Cloud Manager. Ett av de tre alternativen som beskrivs nedan visas:

#### När det inte finns några program i Cloud Manager {#no-programs}

Om det inte finns några program i organisationen instruerar landningssidan dig att skapa ditt första program, vilket visas i bilden nedan.

![](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin0.png)

#### När program redan finns i Cloud Manager {#programs-exist}

Om det redan finns program i organisationen instruerar landningssidan dig att lägga till ett annat program och att visa alla befintliga program också, vilket visas i bilden nedan.

![](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

#### När ett program finns och användaren är systemadministratör {#programs-exist-sysadmin}

Om det redan finns program i organisationen, och du är systemadministratör, visar landningssidan knappen **Hantera åtkomst** tillsammans med alternativet **Lägg till program**, vilket visas i bilden nedan.

![](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/admin-console-4.png)


## Verifiera dina användarroller {#verify-user-roles}

När du har loggat in på Cloud Manager följer du stegen nedan för att verifiera att du har tilldelats produktprofilen för företagsägare:

1. Välj din profil högst upp till höger, enligt nedan.

   ![](/help/journey-onboarding/assets/setup-resources5.png)

1. Välj **Användarroller** och kontrollera att du är tilldelad till Business Owner.

   ![](/help/journey-onboarding/assets/setup-resources6.png)

1. Detta bekräftar din användarroll som företagsägare.

   ![](/help/journey-onboarding/assets/setup-resources7.png)

   Bra jobbat! Du har loggat in på Cloud Manager som företagsägare!

## Create Cloud Service Program {#create-cloud-service-program}

Följ stegen nedan för att skapa ditt molntjänstprogram från Cloud Manager:

1. Navigera till landningssidan för Cloud Manager, som visas nedan.

   >[!NOTE]
   >Du måste vara en teammedlem som har tilldelats produktprofilen för Cloud Manager Business Owner för att kunna slutföra det här steget.

   Klicka här på **Lägg till program** för att starta guiden Lägg till program.

   ![](/help/journey-onboarding/assets/setup-resources4.png)

   >[!NOTE]
   >Titta på [videon](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html?lang=en) om du vill lära dig hur du skapar AEM som ett molnprogram och om viktiga saker att tänka på innan du skapar ditt program.

   >[!IMPORTANT]
   >Stegvisa instruktioner om hur du använder guiden Lägg till program finns [här](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/production-programs/creating-production-program.html?lang=en).
   >
   >* Kom ihåg att programnamnet inte kan ändras när det har skapats. Vi rekommenderar att du vet vilket namn du vill ge ditt program.
   >* Om du måste byta namn på ditt program måste du öppna ett ärende hos Adobe Support eller kontakta Adobe. De kommer att bidra till att effektivt ta bort programmet. Du måste börja om från början igen med potentiell förlust av arbete som teamet har gjort.


1. När ditt molnprogram har skapats kan du navigera till programmet för att se sidan **Översikt** för ditt program, som visas nedan.

   ![](/help/journey-onboarding/assets/setup-resources8.png)

   >[!NOTE]
   >Om du inte redan har gjort det är det ett bra tillfälle att lägga till dina utvecklarmedlemmar i ditt Cloud Manager-team nu. Se Lägga till användare i produktprofilen för utvecklare och följ stegen som beskrivs ovan.

1. Medlemmar som är tilldelade till produktprofilen för utvecklare kan logga in på Cloud Manager och [Hantera Cloud Manager Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/managing-code/accessing-git.html?lang=en).

   Bra jobbat! Nu när ditt program har skapats är din Cloud Manager Git tillgänglig för dina utvecklare!


## Skapa dina molnmiljöer {#create-cloud-environments}

När du har skapat ditt molnprogram kan du skapa dina molnmiljöer.

Följ stegen nedan för att skapa molnmiljöer från Cloud Manager:

1. Navigera till sidan **Översikt** i Cloud Manager och välj **Lägg till** från miljökortet.

   ![](/help/journey-onboarding/assets/setup-resources9.png)

   >[!IMPORTANT]
   >En Cloud Manager-användare i rollen Business Owner eller Deployment Manager måste vara inloggad för att det här steget ska kunna slutföras.

   Titta dessutom på den snabba självstudiekursen [video](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html?lang=en) för att lära dig mer om Cloud Manager-miljöer och hur du kan lägga till dem i ditt program.

1. Detta startar guiden för att lägga till miljö som vägleder dig genom att lägga till din miljö. Lägg till utvecklingsmiljön först för att bekanta dig med guiden. Mer information finns i [Lägga till en miljö](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html?lang=en#adding-environments).

   >[!NOTE]
   >Om du inte redan har gjort det är det ett bra tillfälle att lägga till dina utvecklarmedlemmar i ditt Cloud Manager-team nu. Se Lägga till användare i produktprofilen för utvecklare och följ stegen som beskrivs ovan.

1. Medlemmar som är tilldelade till produktprofilen för utvecklare kan logga in på Cloud Manager och [Hantera Cloud Manager Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/managing-code/accessing-git.html?lang=en).

   Bra jobbat! Nu har ditt program skapats och din Cloud Manager Git är tillgänglig för dina utvecklare!

   Grattis! Nu har dina molnmiljöer skapats och dina utvecklare har lagts till i teamet!

## What’s Next {#whats-next}

Teammedlemmarna måste beviljas behörighet för instansen eftersom behörighet att administrera Cloud Manager inte räcker. Nu när dina molnresurser har skapats och är klara att användas av ditt team måste systemadministratören utse dina teammedlemmar till AEM som produktprofiler för Cloud Service från Adobe Admin Console.

>[!NOTE]
>För att få åtkomst till AEM som Cloud Service måste användare tillhöra en av två produktprofiler `AEM Users` eller `AEM Administrators`. Mer information finns i [Hantera produkter och användaråtkomst i Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=en#managing-products-and-user-access-in-admin-console).

Du bör fortsätta din introduktionsresa genom att gå igenom dokumentet [Tilldela teammedlemmar AEM som en Cloud Service produktprofiler](/help/journey-onboarding/sysadmin/assign-team-members-aem-cloud-service.md).


## Ytterligare resurser {#additional-resources}

Följ de andra resurserna för att lära dig mer om:

* [Programtyper och lägga till ett program](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html?lang=en)
* [Miljötyper och tillägg av en miljö](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html?lang=en)
* [Hantera Cloud Manager Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/managing-code/accessing-git.html?lang=en)
* [Konfigurera åtkomst till AEM som en Cloud Service från Admin Console](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/overview.html?lang=en#adobe-ims-users)
