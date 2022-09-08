---
title: Access Cloud Manager
description: Lär dig hur du får åtkomst till Cloud Manager så att du kan konfigurera dina projektresurser.
role: Admin, User, Developer
exl-id: c9476ac9-8318-493e-a48d-94ff5a6433a7
source-git-commit: fbf1e0b7cefb1dc981d7ee106283280fb2225007
workflow-type: tm+mt
source-wordcount: '1099'
ht-degree: 0%

---

# Access Cloud Manager {#cloud-resources}

I den här delen av [startresan,](overview.md) så får du lära dig hur du får tillgång till Cloud Manager så att du kan konfigurera dina projektresurser.

## Syfte {#objective}

I föregående artikel på denna introduktionsresa [Tilldela teammedlemmar till Cloud Manager-produktprofiler,](assign-profiles-cloud-manager.md) du har gett ditt AEMaaCS-team rätt roller. Lär dig nu hur du får tillgång till Cloud Manager så att du kan konfigurera dina projektresurser som teamet kommer att använda.

Sedan du slutförde föregående steget på den här resan har ditt team tillgång till Cloud Manager. Cloud Manager används för att skapa och hantera projektresurser som program och miljöer.

När du har läst det här dokumentet bör du förstå:

* Att en systemadministratör har tilldelats **Företagsägare** rollen måste vara den första i din organisation som kan logga in och komma åt Cloud Manager.
* Logga in på Cloud Manager.

## Cloud Manager {#cloud-manager}

Cloud Manager är en viktig komponent i AEM as a Cloud Service och fungerar som en enda startpunkt för ditt team. Den stöder kunder med företagsutvecklingsmiljöer med specialbyggda CI/CD-ledningar, som är utrustade för att säkerställa grundlig testning och högsta kodkvalitet för att leverera enastående upplevelser. Cloud Manager innehåller allt som krävs för att komma igång på ett självbetjäningssätt, inklusive möjligheten att skapa molnresurser och miljöer.

Vanligtvis är en teammedlem tilldelad till **Företagsägare** produktprofilen ansvarar för att lägga till molnresurser som program och miljöer. Den här personen förstår affärsbehoven och vem som slutför den ursprungliga installationen av Cloud Manager.

Som systemadministratör har du redan tilldelat dig själv till **Företagsägare** produktprofil och konfigurerar molnresurserna. Beroende på de faktiska projektkraven kan det hända att företagsägarna inte är samma som systemadministratören.

>[!NOTE]
>
>Som standard har en användare som har åtkomst till en AEM även användarrollen Cloud >Manager. Den här rollen i och för sig själv är inte tillräcklig för att ge användaren åtkomst till vyn för programinformation. En sådan användare med endast användarrollen Cloud Manager kan navigera via programmenyalternativen till URL:en för AEM (om det finns miljöer). Dessa användare måste kontakta sin administratör om de vill ha åtkomst på programnivå.

## Använd Cloud Manager som systemadministratör och företagsägare {#access-sysadmin-bo}

Före de gruppmedlemmar som du tilldelade **Företagsägare** kan komma åt molnhanteraren och börja skapa molnresurser måste systemadministratören tilldelas **Företagsägare** och logga in i Cloud Manager på samma sätt som du gjorde i det föregående steget i den här introduktionsresan.

1. Se till att du som systemadministratör har **Företagsägare** tilldelad roll.

   * Återgå till föregående steg på denna resa. [Tilldela teammedlemmar till Cloud Manager-produktprofiler,](assign-profiles-cloud-manager.md) för mer information om hur du tilldelar **Företagsägare** till systemadministratören om du inte redan har gjort detta.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och presenteras med den normala landningssidan.

Genom att logga in som systemadministratör med **Företagsägare** roll, du initierar Cloud Manager för användning av andra användare med **Företagsägare** roll. Du kommer inte att få någon bekräftelse på detta eller något meddelande. Det räcker med att bara logga in.

Tills du loggar in på Cloud Manager som systemadministratör med **Företagsägare** roll, andra användare med **Företagsägare** roller kommer inte att kunna skapa program i Cloud Manager även om de har tilldelats rätt roller.

## Navigera till Cloud Manager {#navigate-cloud-manager}

Användare med **Företagsägare** en roll får ett välkomstmeddelande med en länk för att komma igång. Följ stegen nedan för att navigera till Cloud Manager med det här välkomstmeddelandet.

1. Klicka på **Kom igång**, vilket visas i figuren nedan.
   ![E-postexempel](/help/journey-onboarding/assets/get-started-email.png)

1. Du kommer att navigera till Cloud Managers **Program och produkter** sida.

   >[!TIP]
   >
   >Du kan även navigera direkt till inloggningssidan för Cloud Manager från `[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)`. Bokmärk den här sidan för framtida referens.

1. Du dirigeras till Cloud Managers landningssida.

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
>Beroende på vilka roller som har tilldelats i Cloud Manager och programmets status, visas olika skärmar när du använder användargränssnittet i Cloud Manager.

## Visningsprogram {#viewing-programs}

När du har åtkomst till Cloud Manager beror det du ser på hur dina program är, vilket beskrivs i följande avsnitt.

### När inga program finns {#no-programs}

Om det inte finns några program i din organisation instruerar landningssidan dig att skapa ditt första program.

![Inga program](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin0.png)

### När program redan finns {#programs-exist}

Om det redan finns program i organisationen visas dina befintliga program på landningssidan och det finns även en knapp för att lägga till ytterligare program.

![Program finns](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

### När ett program finns och du är systemadministratör {#programs-exist-sysadmin}

Om det redan finns program i organisationen och du är systemadministratör visas landningssidan **Hantera åtkomst** med **Lägg till program** alternativ.

![Systemadministratörsvy](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/admin-console-4.png)

## Verifiera dina användarroller {#verify-user-roles}

När du har loggat in i Cloud Manager kan du verifiera att du har tilldelats **Företagsägare** produktprofil.

1. Välj din profil längst upp till höger i fönstret.

   ![Användarprofil](/help/journey-onboarding/assets/setup-resources5.png)

1. Välj **Användarroller** för att visa de roller som tilldelats användaren.

   ![Användarroller](/help/journey-onboarding/assets/setup-resources6.png)

1. Dialogrutan bör bekräfta att din användare har **Företagsägare** roll.

   ![Lista över användarroller](/help/journey-onboarding/assets/setup-resources7.png)

Du har loggat in på Cloud Manager som företagsägare! Om du inte har tilldelats **Företagsägare** ska du kontakta systemadministratören.

## What’s Next {#whats-next}

Nu när du har tillgång till Cloud Manager som systemadministratör kan du skapa ditt första program.

Du bör fortsätta din introduktionsresa genom att granska dokumentet nästa gång [Skapa ett program](create-program.md) där du får lära dig hur man gör detta.

## Ytterligare resurser {#additional-resources}

Följ de andra resurserna för att lära dig mer om:

* [Introduktion till Cloud Manager](/help/onboarding/cloud-manager-introduction.md) - Lär dig mer om Cloud Manager, Cloud Manager-program och miljöer.
