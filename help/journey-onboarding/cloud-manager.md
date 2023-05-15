---
title: Access Cloud Manager
description: Lär dig hur du får åtkomst till Cloud Manager så att du kan konfigurera dina projektresurser.
role: Admin, User, Developer
exl-id: c9476ac9-8318-493e-a48d-94ff5a6433a7
source-git-commit: 5c9dbaa25f0142afdae8b09dc18d1e1aaaf4c1fb
workflow-type: tm+mt
source-wordcount: '1044'
ht-degree: 0%

---

# Access Cloud Manager {#cloud-resources}

I den här delen av [startresan,](overview.md) får du lära dig hur du får tillgång till Cloud Manager så att du kan konfigurera dina projektresurser.

## Syfte {#objective}

I föregående artikel på denna introduktionsresa [Tilldela teammedlemmar till Cloud Manager-produktprofiler,](assign-profiles-cloud-manager.md) du har gett ditt AEMaaCS-team rätt roller. Lär dig nu hur du får tillgång till Cloud Manager så att du kan konfigurera dina projektresurser som teamet använder.

Sedan du slutförde föregående steget på den här resan har ditt team tillgång till Cloud Manager. Cloud Manager används för att skapa och hantera projektresurser som program och miljöer.

När du har läst det här dokumentet bör du förstå följande:

* Att en systemadministratör har tilldelats **Företagsägare** rollen måste vara den första i organisationen som loggar in och får tillgång till Cloud Manager.
* Logga in på Cloud Manager.

## Cloud Manager {#cloud-manager}

Cloud Manager är en viktig komponent i AEM as a Cloud Service och fungerar som en enda startpunkt för ditt team. Den stöder kunder med företagsutvecklingsmiljöer med specialbyggda CI/CD-ledningar, som är utrustade för att säkerställa grundlig testning och högsta kodkvalitet för att leverera enastående upplevelser. Cloud Manager innehåller allt som krävs för att komma igång på ett självbetjäningssätt, inklusive möjligheten att skapa molnresurser och miljöer.

Vanligtvis är en teammedlem tilldelad till **Företagsägare** produktprofilen ansvarar för att lägga till molnresurser som program och miljöer. Den här personen förstår affärsbehoven och vem som slutför den ursprungliga installationen av Cloud Manager.

Som systemadministratör har du redan tilldelat dig själv till **Företagsägare** produktprofil och kan konfigurera molnresurserna. Beroende på de faktiska projektkraven kan det hända att företagsägarna inte är samma som systemadministratören.

## Använd Cloud Manager som systemadministratör och företagsägare {#access-sysadmin-bo}

Före de gruppmedlemmar som du tilldelade **Företagsägare** kan komma åt molnhanteraren och börja skapa molnresurser måste systemadministratören tilldelas **Företagsägare** roll. De måste också logga in i Cloud Manager på samma sätt som du gjorde i det föregående steget i den här introduktionsresan.

1. Se till att du som systemadministratör har **Företagsägare** tilldelad roll.

   * Återgå till föregående steg på denna resa. [Tilldela teammedlemmar till Cloud Manager-produktprofiler,](assign-profiles-cloud-manager.md) för mer information om hur du tilldelar **Företagsägare** till systemadministratören.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och presenteras med den normala landningssidan.

Genom att logga in som systemadministratör med **Företagsägare** roll, du initierar Cloud Manager för användning av andra användare med **Företagsägare** roll. Du får ingen bekräftelse eller något meddelande. Det räcker att bara logga in.

Tills du loggar in på Cloud Manager som systemadministratör med **Företagsägare** roll, andra användare med **Företagsägare** kan inte skapa program i Cloud Manager. Den här regeln gäller även om de har tilldelats rätt roller.

## Navigera till Cloud Manager {#navigate-cloud-manager}

Användare med **Företagsägare** rollen får ett välkomstmeddelande med en länk för att komma igång. Följ stegen nedan för att navigera till Cloud Manager med det här välkomstmeddelandet.

1. Klicka på **Kom igång**, vilket visas i figuren nedan.
   ![E-postexempel](/help/journey-onboarding/assets/get-started-email.png)

1. Navigera till Cloud Managers **Program och produkter** sida.

   >[!TIP]
   >
   >Du kan även navigera direkt till inloggningssidan för Cloud Manager från `[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)`. Bokmärk den här sidan för framtida referens.

1. Du dirigeras till Cloud Managers landningssida.

Du kan även navigera till Cloud Managers **Program och produkter** från Adobe Experience Cloud hemsida genom att följa dessa steg

1. Navigera direkt till [Adobe Experience Cloud](https://experience.adobe.com) och logga in med din Adobe ID.

1. På Adobe Experience Cloud hemsida väljer du **Experience Manager** för att öppna AEM startsida.

   ![Experience Cloud hemsida](/help/journey-onboarding/assets/setup-resources2.png)

1. På **Cloud Manager** platta, markera **Starta**.

   ![AEM startsida](/help/journey-onboarding/assets/setup-resources3.png)

1. När du har loggat in dirigeras du till landningssidan för Cloud Manager. Se [Visa Cloud Managers program](#viewing-programs) för mer information.

Det är upp till dig och det påverkar inte hur du använder Cloud Manager eller hur du hanterar dina program.

>[!NOTE]
>
>Beroende på vilka roller som har tilldelats i Cloud Manager och programmets status visas olika skärmar när du använder användargränssnittet i Cloud Manager.

## Visningsprogram {#viewing-programs}

När du har lyckats få tillgång till Cloud Manager beror det du ser på hur dina program är, vilket beskrivs i följande avsnitt.

### När inga program finns {#no-programs}

Om det inte finns några program i din organisation instruerar landningssidan dig att skapa ditt första program.

![Inga program](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin0.png)

### När program redan finns {#programs-exist}

Om det finns program i organisationen visar landningssidan dina befintliga program och erbjuder även en knapp för att lägga till ytterligare program.

![Program finns](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

### När ett program finns och du är systemadministratör {#programs-exist-sysadmin}

Om det finns program i organisationen och du är systemadministratör visas landningssidan **Hantera åtkomst** med **Lägg till program** alternativ.

![Systemadministratörsvy](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/admin-console-4.png)

## Verifiera dina användarroller {#verify-user-roles}

När du har loggat in i Cloud Manager kan du verifiera att du har tilldelats **Företagsägare** produktprofil.

1. Välj din profil längst upp till höger i fönstret.

   ![Användarprofil](/help/journey-onboarding/assets/setup-resources5.png)

1. Om du vill visa rollerna som tilldelats din användare väljer du **Användarroller**.

   ![Användarroller](/help/journey-onboarding/assets/setup-resources6.png)

1. Dialogrutan bör bekräfta att din användare har **Företagsägare** roll.

   ![Lista över användarroller](/help/journey-onboarding/assets/setup-resources7.png)

Du har loggat in på Cloud Manager som företagsägare! Om du inte har tilldelats **Företagsägare** ska du kontakta systemadministratören.

## What&#39;s Next {#whats-next}

Nu när du har tillgång till Cloud Manager som systemadministratör kan du skapa ditt första program.

Fortsätt din introduktionsresa genom att nästa gång du granskar dokumentet [Skapa ett program](create-program.md) där du lär dig hur man gör det.

## Ytterligare resurser {#additional-resources}

Här följer ytterligare, valfria resurser om du vill gå längre än vad som ingår i introduktionsresan.

* [Introduktion till Cloud Manager](/help/onboarding/cloud-manager-introduction.md) - Lär dig mer om Cloud Manager, Cloud Manager-program och miljöer.
* [AEM as a Cloud Service team- och produktprofiler](/help/onboarding/aem-cs-team-product-profiles.md) - Lär dig hur AEM as a Cloud Service team och produktprofiler kan ge och begränsa åtkomst till era licensierade Adobe-lösningar.
<!-- ERROR: Not Found (HTTP error 404) * [AEM Champion Tips and Tricks - Cloud Manager UI](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/expert-resources/aem-champions/cloud-manager-ui.md) - Watch this video for an overview of Cloud Manager's UI from an AEM champion. -->
