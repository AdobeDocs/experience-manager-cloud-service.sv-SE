---
title: Konfigurera molnresurser via Cloud Manager
description: Lär dig hur du använder Cloud Manager för att konfigurera och hantera dina egna molnresurser.
role: Admin, User, Developer
exl-id: de3a33b7-b459-4e47-b232-a0f88e2ce22e
source-git-commit: 0db24518610fccf0d2ea5e0620a0c6a5f8009ea8
workflow-type: tm+mt
source-wordcount: '1365'
ht-degree: 0%

---

# Konfigurera molnresurser via Cloud Manager {#setup-cloud-resources}

Lär dig hur du använder Cloud Manager för att konfigurera och hantera dina egna molnresurser.

## Syfte {#objective}

Det här dokumentet hjälper dig att förstå hur dina molnresurser skapas och vem som kan skapa dem. När du har läst det här avsnittet bör du förstå:

* En systemadministratör som tilldelats **Företagsägare** rollen måste vara den första i din organisation som kan logga in och komma åt Cloud Manager.
* Hur ditt molnprogram och dina miljöer skapas.

## Introduktion {#introduction}

Din molnresurs läggs till via Cloud Manager av din teammedlem som är tilldelad till **Företagsägare** produktprofil. Den här personen är vanligtvis en person som förstår affärsbehoven och som slutför den ursprungliga installationen av Cloud Manager.

Följ avsnitten nedan för att lära dig hur du skapar [molntjänstprogram](#create-cloud-service-program) och [miljöer.](#create-cloud-environments)

### Förutsättningar {#prerequisites}

* Systemadministratören som är tilldelad **Företagsägare** rollen måste ha loggat in i Cloud Manager innan andra användare med **Företagsägare** rollförsök att komma åt Cloud Manager för att utföra och utföra de steg som beskrivs i det här dokumentet.

   * Återgå till [Tilldela teammedlemmar till Cloud Manager-produktprofiler](/help/journey-onboarding/sysadmin/assign-team-members-cloud-manager.md) dokument för den här resan för mer information.

* Du måste förstå hur [navigera och logga in på Cloud Manager.](/help/onboarding/learn-concepts/cloud-manager-introduction.md)

* Du bör känna till [Produktprofiler för Cloud Manager.](/help/onboarding/learn-concepts/aem-cs-team-product-profiles.md#cloud-manager-product-profiles)

* Du bör förstå begreppen i Cloud Manager [program](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) och [miljöer.](/help/implementing/cloud-manager/manage-environments.md)

## Använd Cloud Manager som systemadministratör och företagsägare {#access-sysadmin-bo}

Före de gruppmedlemmar som du tilldelade **Företagsägare** kan komma åt molnhanteraren och börja skapa molnresurser måste systemadministratören tilldelas **Företagsägare** och logga in i Cloud Manager.

1. Se till att du som systemadministratör har **Företagsägare** tilldelad roll.

   * Återgå till föregående steg på denna resa. [Tilldela teammedlemmar till Cloud Manager-produktprofiler,](/help/journey-onboarding/sysadmin/assign-team-members-cloud-manager.md) för mer information om hur du tilldelar **Företagsägare** till systemadministratören om du inte redan har gjort detta.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och presenteras med den normala landningssidan.

Genom att logga in som systemadministratör med **Företagsägare** roll, du initierar Cloud Manager för användning av andra användare med **Företagsägare** roll. Du kommer inte att få någon bekräftelse på detta eller något meddelande. Det räcker med att bara logga in.

Tills du loggar in på Cloud Manager som systemadministratör med **Företagsägare** roll, andra användare med **Företagsägare** roller kommer inte att kunna skapa program i Cloud Manager även om de har tilldelats rätt roller.

## Navigera till Cloud Manager {#navigate-cloud-manager}

Användaren med **Företagsägare** en roll får ett välkomstmeddelande med en länk för att komma igång. Följ stegen nedan för att navigera till Cloud Manager med det här välkomstmeddelandet.

1. Klicka på **Kom igång**, vilket visas i figuren nedan.
   ![E-postexempel](/help/journey-onboarding/assets/get-started-email.png)

1. Du kommer att navigera till Cloud Managers **Program och produkter** sida.

   >[!TIP]
   >
   >Du kan även navigera direkt till inloggningssidan för Cloud Manager från [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/). Bokmärk den här sidan för framtida referens.

1. Du dirigeras till Cloud Managers landningssida. Se [Visa Cloud Managers program](#viewing-programs) för mer information.

Du kan även navigera till Cloud Managers **Program och produkter** från Adobe Experience Cloud hemsida genom att följa dessa steg

1. Navigera direkt till [Adobe Experience Cloud](https://experience.adobe.com) och logga in med din Adobe ID.

1. På Adobe Experience Cloud hemsida väljer du **Experience Manager**.

   ![Experience Cloud hemsida](/help/journey-onboarding/assets/setup-resources2.png)

1. Du kommer nu till AEM startsida. Klicka här **Starta** på **Cloud Manager** platta.

   ![AEM startsida](/help/journey-onboarding/assets/setup-resources3.png)

1. När inloggningen är klar dirigeras du till landningssidan för Cloud Manager. Se [Visa Cloud Managers program](#viewing-programs) för mer information.

Det är upp till dig och det påverkar inte hur du använder Cloud Manager eller hur du hanterar dina program.

>[!NOTE]
>
>Beroende på vilka roller som har tilldelats i [!UICONTROL Cloud Manager] och programmets status kommer du att se olika skärmar när du använder [!UICONTROL Cloud Manager] Gränssnitt.

### Visningsprogram {#viewing-programs}

När du har åtkomst till Cloud Manager beror det du ser på hur dina program är, vilket beskrivs i följande avsnitt.

#### När inga program finns {#no-programs}

Om det inte finns några program i din organisation instruerar landningssidan dig att skapa ditt första program.

![Inga program](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin0.png)

#### När program redan finns {#programs-exist}

Om det redan finns program i organisationen visas dina befintliga program på landningssidan och det finns även en knapp för att lägga till ytterligare program.

![Program finns](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

#### När ett program finns och du är systemadministratör {#programs-exist-sysadmin}

Om det redan finns program i organisationen och du är systemadministratör visas landningssidan **Hantera åtkomst** med **Lägg till program** alternativ.

![Systemadministratörsvy](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/admin-console-4.png)


## Verifiera dina användarroller {#verify-user-roles}

När du har loggat in i Cloud Manager kan du verifiera att du har tilldelats **Företagsägare** produktprofil.

1. Välj din profil längst upp till höger i fönstret.

   ![Användarprofil](/help/journey-onboarding/assets/setup-resources5.png)

1. Välj **Användarroller** för att visa de roller som tilldelats användaren.

   ![Användarroller](/help/journey-onboarding/assets/setup-resources6.png)

1. Bekräftar att användaren har **Företagsägare** roll.

   ![Lista över användarroller](/help/journey-onboarding/assets/setup-resources7.png)

Du har loggat in på Cloud Manager som företagsägare! Om du inte har tilldelats **Företagsägare** ska du kontakta systemadministratören.

## Skapa ett Cloud Service Program {#create-cloud-service-program}

Nu när du har säkerställt att du har rätt åtkomst kan du skapa ditt första program.

1. Navigera till landningssidan för Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och logga in.

1. På landningssidan för Cloud Manager klickar du på **Lägg till program** för att starta guiden Lägg till program.

   ![Landningssida](/help/journey-onboarding/assets/setup-resources4.png)

   >[!TIP]
   >
   >Stegvisa instruktioner om hur du använder guiden Lägg till program finns i dokumentet [Skapa produktionsprogram](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md) eller se detta [video](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html) om du vill lära dig att skapa AEM som ett molnprogram och lära dig mer om viktiga saker innan du skapar ditt program.


1. När ditt molnprogram har skapats kan du navigera till programmet från Cloud Managers landningssida för att se **Översikt** sidan med ditt program.

   ![Programöversikt](/help/journey-onboarding/assets/setup-resources8.png)

1. Medlemmar som är tilldelade till produktprofilen för utvecklare kan logga in på molnhanteraren och hantera Creative Manager-git-databaser.

   * Om du inte redan har gjort det är det ett bra tillfälle att tilldela medlemmar till **Utvecklare** i ditt Cloud Manager-team. Återgå till [Tilldela teammedlemmar till Cloud Manager-produktprofiler](/help/journey-onboarding/sysadmin/assign-team-members-cloud-manager.md) dokument för den här resan för mer information.

Nu har ditt program skapats och din Cloud Manager Git-databas är tillgänglig för utvecklarna!

## Skapa dina molnmiljöer {#create-cloud-environments}

När du har skapat ditt molnprogram kan du skapa dina molnmiljöer.

1. Navigera till landningssidan för Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och markera **Lägg till** från miljökortet.

   ![Knappen Lägg till miljö](/help/journey-onboarding/assets/setup-resources9.png)

1. Guiden för att lägga till miljö startar och guidar dig genom att lägga till din miljö. Lägg till utvecklingsmiljön först för att bekanta dig med guiden.

   >[!TIP]
   >
   >Se dokumentet [Lägga till en miljö](/help/implementing/cloud-manager/manage-environments.md#adding-environments) om du vill veta mer eller titta [den här korta videosjälvstudiekursen](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html) om du vill veta mer om Cloud Manager-miljöer och hur du kan lägga till dem i ditt program.

1. Medlemmar som har tilldelats **Utvecklare** produktprofilen kan logga in på Cloud Manager och hantera Creative Manager Git-databaser.

Nu har ditt program skapats och din Cloud Manager-git är tillgänglig för utvecklarna!

## What’s Next {#whats-next}

Nu när dina molnresurser har skapats och är tillgängliga för ditt team måste systemadministratören tilldela teammedlemmarna AEM as a Cloud Service produktprofiler från Adobe Admin Console för att få tillgång till dessa resurser.

Du bör fortsätta din introduktionsresa genom att granska dokumentet nästa gång [Tilldela teammedlemmar till AEM as a Cloud Service produktprofiler](/help/journey-onboarding/sysadmin/assign-team-members-aem-cloud-service.md) där du får lära dig att ge teammedlemmarna de rättigheter de behöver för att få tillgång till dina nya miljöer.

## Ytterligare resurser {#additional-resources}

Följ de andra resurserna för att lära dig mer om:

* [Programtyper och lägga till ett program](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html)
* [Miljötyper och tillägg av en miljö](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html)
* [Hantera Cloud Manager Git](/help/implementing/cloud-manager/managing-code/accessing-repos.md)
* [Konfigurera åtkomst till AEM as a Cloud Service från Admin Console](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/overview.html#adobe-ims-users)
