---
title: Använd Cloud Manager
description: Lär dig hur du får tillgång till Cloud Manager så att du kan konfigurera dina projektresurser.
role: Admin, User, Developer
exl-id: c9476ac9-8318-493e-a48d-94ff5a6433a7
feature: Onboarding
source-git-commit: 4cad0ea1be4cba1c7f1af55cc760fb65fdc3cc4a
workflow-type: tm+mt
source-wordcount: '1033'
ht-degree: 0%

---

# Använd Cloud Manager {#cloud-resources}

I den här delen av [introduktionsresan](overview.md) får du lära dig hur du kommer åt Cloud Manager så att du kan konfigurera dina projektresurser.

## Syfte {#objective}

I den föregående artikeln i den här introduktionsresan, [Tilldela teammedlemmar till Cloud Manager produktprofiler](assign-profiles-cloud-manager.md), har du gett ditt AEMaaCS-team rätt roller. Lär dig nu hur du får tillgång till Cloud Manager så att du kan ställa in projektresurser som teamet tänker använda.

Sedan du slutförde föregående steget på den här resan kan ditt team få tillgång till Cloud Manager. Cloud Manager används för att skapa och hantera projektresurser som program och miljöer.

När du har läst det här dokumentet bör du förstå följande:

* En systemadministratör som tilldelats rollen **Business Owner** måste vara den första i organisationen som kan logga in och komma åt Cloud Manager.
* Logga in på Cloud Manager.

## Cloud Manager {#cloud-manager}

Cloud Manager är en viktig komponent i AEM as a Cloud Service och fungerar som en gemensam startpunkt för ert team. Den stöder kunder med företagsutvecklingsmiljöer med specialbyggda CI/CD-ledningar som är utrustade för grundlig testning och högsta kodkvalitet för att leverera enastående upplevelser. Cloud Manager tillhandahåller allt som krävs för att komma igång på ett självbetjäningssätt, inklusive möjligheten att skapa molnresurser och miljöer.

Vanligtvis är det en teammedlem som har tilldelats produktprofilen **Business Owner** som ansvarar för att lägga till dina molnresurser, till exempel program och miljöer. Denna person förstår vilka behov företaget har och vem som slutför den första Cloud Manager-installationen.

För den här introduktionsresan har du som systemadministratör redan tilldelat dig till produktprofilen **Business Owner** och kan konfigurera molnresurserna. Beroende på de faktiska projektkraven kan det hända att företagsägarna inte är samma som systemadministratören.

## Använd Cloud Manager som systemadministratör och företagsägare {#access-sysadmin-bo}

Innan teammedlemmarna som du tilldelade rollen **Business Owner** kan komma åt Cloud Manager och börja skapa molnresurser måste systemadministratören tilldelas rollen **Business Owner**. De måste också logga in på Cloud Manager på samma sätt som du gjorde i det föregående steget i den här introduktionsresan.

1. Kontrollera att du som systemadministratör har rollen **Affärsägare** tilldelad.

   Återgå till föregående steg, [Tilldela teammedlemmar till Cloud Manager produktprofiler](assign-profiles-cloud-manager.md), om du vill ha mer information om hur du tilldelar systemadministratören rollen **Affärsägare**.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/).

Genom att logga in som systemadministratör med rollen **Affärsägare** initierar du Cloud Manager för användning av andra användare med rollen **Affärsägare**. Du får ingen bekräftelse eller något meddelande. Det räcker att bara logga in.

Innan du har loggat in på Cloud Manager som systemadministratör med rollen **Business Owner** kan andra användare med rollen **Business Owner** inte skapa program i Cloud Manager. Den här regeln gäller även om de har tilldelats rätt roller.

## Navigera till Cloud Manager {#navigate-cloud-manager}

Användare med rollen **Affärsägare** får ett välkomstmeddelande med en länk för att komma igång. Följ stegen nedan för att navigera till Cloud Manager med det här välkomstmeddelandet.

1. Klicka på **Kom igång** från ditt välkomstmeddelande, vilket visas i bilden nedan.
   ![Exempel på e-post](/help/journey-onboarding/assets/get-started-email.png)

1. Gå till Cloud Manager **Program- och produktsida**.

   >[!TIP]
   >
   >Du kan även navigera direkt till Cloud Manager inloggningssida från `[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)`. Bokmärk den här sidan för framtida referens.

1. Du dirigeras till Cloud Manager landningssida.

Du kan också navigera till Cloud Manager **Program- och produktsida** från Adobe Experience Cloud hemsida med dessa steg.

1. Navigera direkt till [Adobe Experience Cloud](https://experience.adobe.com) och logga in med din Adobe ID.

1. På Adobe Experience Cloud hemsida väljer du **Experience Manager** för att öppna AEM hemsida.

   ![Experience Cloud hemsida](/help/journey-onboarding/assets/setup-resources2.png)

1. Välj **Starta** på panelen **Cloud Manager**.

   ![AEM hemsida](/help/journey-onboarding/assets/setup-resources3.png)

1. När du har loggat in dirigeras du till Cloud Manager landningssida. Mer information finns i [Visa Cloud Manager-program](#viewing-programs).

Det är upp till dig och det påverkar inte hur du använder Cloud Manager eller hur du hanterar dina program.

>[!NOTE]
>
>Beroende på vilka roller som har tilldelats i Cloud Manager och programmets status visas olika skärmar när du använder Cloud Manager användargränssnitt.

## Visningsprogram {#viewing-programs}

När du har fått tillgång till Cloud Manager beror det hur programmen ser ut, vilket beskrivs i följande avsnitt.

### När inga program finns {#no-programs}

Om det inte finns några program i din organisation instruerar landningssidan dig att skapa ditt första program.

![Inga program](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin0.png)

### När program redan finns {#programs-exist}

Om det finns program i organisationen visar landningssidan dina befintliga program och erbjuder även en knapp för att lägga till ytterligare program.

![Program finns](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

### När ett program finns och du är systemadministratör {#programs-exist-sysadmin}

Om det finns program i organisationen och du är systemadministratör, visas knappen **Hantera åtkomst** på landningssidan tillsammans med alternativet **Lägg till program** på sidan.

![Systemadministratörsvy](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/admin-console-4.png)

## Verifiera dina användarroller {#verify-user-roles}

När du har loggat in på Cloud Manager kan du verifiera att du har tilldelats produktprofilen **Business Owner**.

1. Välj din profil längst upp till höger i fönstret.

1. Om du vill visa rollerna som tilldelats din användare väljer du **Användarroller**.

   ![Användarroller](/help/journey-onboarding/assets/setup-resources6.png)

1. Dialogrutan bör bekräfta att din användare har rollen **Affärsägare**.

   ![Lista över användarroller](/help/journey-onboarding/assets/setup-resources7.png)

Du har loggat in på Cloud Manager som företagsägare! Kontakta systemadministratören om du inte har tilldelats rollen **Affärsägare**.

## What&#39;s Next {#whats-next}

Nu när du har åtkomst till Cloud Manager som systemadministratör kan du skapa ditt första program.

Fortsätt din introduktionsresa genom att nästa gång granska dokumentet [Skapa ett program](create-program.md) där du får lära dig hur du gör det.

## Ytterligare resurser {#additional-resources}

Här följer ytterligare, valfria resurser om du vill gå längre än vad som ingår i introduktionsresan.

* [Introduktion till Cloud Manager](/help/onboarding/cloud-manager-introduction.md) -
Läs om Cloud Manager, Cloud Manager program och miljöer.
* [AEM as a Cloud Service Team- och produktprofiler](/help/onboarding/aem-cs-team-product-profiles.md) - Lär dig hur AEM as a Cloud Service team och produktprofiler kan ge och begränsa åtkomst till licensierade Adobe-lösningar.
<!-- ERROR: Not Found (HTTP error 404) * [AEM Champion Tips and Tricks - Cloud Manager UI](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/expert-resources/aem-champions/cloud-manager-ui.md) - Watch this video for an overview of Cloud Manager's UI from an AEM champion. -->
