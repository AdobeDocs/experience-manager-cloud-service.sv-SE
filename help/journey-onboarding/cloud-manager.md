---
title: Använd Cloud Manager
description: Lär dig hur du får tillgång till Cloud Manager så att du kan konfigurera dina projektresurser.
role: Admin, User, Developer
exl-id: c9476ac9-8318-493e-a48d-94ff5a6433a7
feature: Onboarding
source-git-commit: 858a9c4b61fd3a80a257313e48816b067ca77175
workflow-type: tm+mt
source-wordcount: '820'
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

1. Logga in på Cloud Manager på [experience.adobe.com](https://experience.adobe.com).
1. Klicka på **Experience Manager** i snabbåtkomstgruppen.
1. Klicka på **Cloud Manager** på den vänstra panelen.

   ![Cloud Manager på konsol](/help/journey-onboarding/assets/consol-cloud-manager.png)

En systemadministratör med rollen **Business Owner** måste logga in på Cloud Manager först. Denna första inloggning gör det möjligt för andra användare med rollen **Business Owner** att skapa program. Ingen bekräftelse visas.

<!--
By successfully signing in as a system administrator with the **Business Owner** role, you use Cloud Manager for use by the other users with the **Business Owner** role. You do not receive a confirmation or any message. Simply signing in is sufficient.

Until you sign in to Cloud Manager as a system administrator with the **Business Owner** role, other users with the **Business Owner** role cannot create programs in Cloud Manager. This rule is true even if they are assigned the correct roles. -->

## Navigera till Cloud Manager {#navigate-cloud-manager}

1. Gå till [experience.adobe.com/experiencemanager](https://experience.adobe.com/experiencemanager).
1. Klicka på **Cloud Manager** på den vänstra panelen.

>[!NOTE]
>
>Beroende på vilka roller som har tilldelats i Cloud Manager och programmets status visas olika skärmar när du använder Cloud Manager användargränssnitt.

<!--
Users with the **Business Owner** role receive a welcome email with a link to get started. Follow the steps below to navigate to Cloud Manager using this welcome email.

1. From your welcome email, click **Get started**, as shown in the figure below.
    ![Email example](/help/journey-onboarding/assets/get-started-email.png)

1. Navigate to Cloud Manager's **Programs & Products** page.

   >[!TIP]
   >
   >You can also navigate directly to Cloud Manager's login page from `[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)`. Bookmark this page for future reference.

1. You are directed to Cloud Manager's landing page. -->

<!-- OLD
Alternatively, you can navigate to Cloud Manager's **Programs and Products** page from the Adobe Experience Cloud home page using these steps.

1. Navigate directly to [Adobe Experience Cloud](https://experience.adobe.com) and login using your Adobe ID.

1. From the Adobe Experience Cloud home page, select **Experience Manager** to open the AEM home page.

   ![Experience Cloud homepage](/help/journey-onboarding/assets/setup-resources2.png)

1. On the **Cloud Manager** tile, select **Launch**.

   ![AEM home page](/help/journey-onboarding/assets/setup-resources3.png)

1. After successfully logging on, you are directed to the Cloud Manager landing page. See [Viewing Cloud Manager's Programs](#viewing-programs) for more details.

How you access your programs and products via Cloud Manager is up to you and has no effect on how you use Cloud Manager or how you manage your programs.

>[!NOTE]
>
>Depending on the roles assigned in Cloud Manager and the state of the application, you see different screens while using the Cloud Manager user interface. -->

## Visa program {#viewing-programs}

När du har fått tillgång till Cloud Manager beror det hur programmen ser ut, vilket beskrivs i följande avsnitt.

### När inga program finns {#no-programs}

Om det inte finns några program i din organisation instruerar landningssidan dig att skapa ditt första program.

![Inga program](/help/journey-onboarding/assets/cloud-manager-programs-do-not-exist.png)

### När program redan finns {#programs-exist}

Om det finns program i organisationen visar landningssidan dina befintliga program och erbjuder även en knapp för att lägga till ytterligare program.

![Program finns](/help/journey-onboarding/assets/cloud-manager-programs-exist.png)

### När ett program finns och du är systemadministratör {#programs-exist-sysadmin}

Om det finns program i organisationen och du är systemadministratör, visas knappen **Hantera åtkomst** på landningssidan tillsammans med alternativet **Lägg till program** på sidan.

![Systemadministratörsvy](/help/journey-onboarding/assets/cloud-manager-programs-as-sysadmin.png)

## Verifiera dina användarroller {#verify-user-roles}

När du har loggat in på Cloud Manager kan du verifiera att du har tilldelats produktprofilen **Business Owner**.

1. Klicka på ikonen **Konto** i sidans övre högra hörn.

1. Klicka på **Användarroller**.

   ![Användarroller](/help/journey-onboarding/assets/cloud-manager-user-roles.png)

1. Bekräfta att din användare har rollen **Affärsägare** i dialogrutan **Användarroller**.

   ![Lista över användarroller](/help/journey-onboarding/assets/cloud-manager-user-roles-business-owner.png)

Du har loggat in på Cloud Manager som företagsägare. Kontakta systemadministratören om du inte har tilldelats rollen **Affärsägare**.

## Vad kommer härnäst? {#whats-next}

Nu när du har åtkomst till Cloud Manager som systemadministratör kan du skapa ditt första program.

Fortsätt din introduktionsresa genom att nästa gång granska dokumentet [Skapa ett program](create-program.md) där du får lära dig hur du gör det.

## Ytterligare resurser {#additional-resources}

Här följer ytterligare, valfria resurser om du vill gå längre än vad som ingår i introduktionsresan.

* [Introduktion till Cloud Manager](/help/onboarding/cloud-manager-introduction.md) -
Läs om Cloud Manager, Cloud Manager program och miljöer.
* [AEM as a Cloud Service Team- och produktprofiler](/help/onboarding/aem-cs-team-product-profiles.md) - Lär dig hur AEM as a Cloud Service team och produktprofiler kan ge och begränsa åtkomst till licensierade Adobe-lösningar.
<!-- ERROR: Not Found (HTTP error 404) * [AEM Champion Tips and Tricks - Cloud Manager UI](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/expert-resources/aem-champions/cloud-manager-ui.md) - Watch this video for an overview of Cloud Manager's UI from an AEM champion. -->
