---
title: Tilldela teammedlemmar till Cloud Manager-produktprofiler
description: Följ den här sidan för att lära dig hur du tilldelar teammedlemmar till produktprofiler för Cloud Manager
feature: Onboarding
role: Admin, User, Developer
exl-id: 555688e5-f937-462c-9fcc-b90685f1882b
source-git-commit: 22a08a0cb80052485309ce3d33537e9fe303c6f5
workflow-type: tm+mt
source-wordcount: '1154'
ht-degree: 0%

---

# Tilldela teammedlemmar till Cloud Manager-produktprofiler {#assign-team-members}

I det föregående steget på denna resa [Kom igång med introduktionsprocessen](/help/journey-onboarding/sysadmin/get-started-onboarding-journey.md)loggar du nu in på Admin Console och ser dina behörigheter som systemadministratör. Du kan nu tilldela teammedlemmar till produktprofiler för Cloud Manager.

## Syfte {#objective}

I det här dokumentet sammanfattas hur du tilldelar teammedlemmar till Cloud Manager-produktprofiler från Adobe Admin Console. När de har tilldelats kan dessa medlemmar skapa en åtkomstmolnresurs enligt beskrivningen i nästa steg i den här resan.

När du har läst det här avsnittet ska du kunna:

* Förstå varför och hur ni måste lägga till teammedlemmar.
* Läs om tre viktiga produktprofiler för Cloud Manager: **Företagsägare**, **Distributionshanteraren** och **Utvecklare**.
* Tilldela teammedlemmar till Cloud Manager-produktprofiler.

>[!TIP]
>
>För att komma igång rekommenderar Adobe att du till att börja med lägger till användare som ska delta i de omedelbara uppgifterna, till exempel administratörer, utvecklare och innehållsförfattare. Du kan fortsätta med introduktionsprocessen utan att lägga till alla användare. När du är klar med introduktionen kan du lägga till fler användare.

## Förutsättningar {#prerequisites}

Följande krav måste vara uppfyllda innan du startar det här avsnittet. Du måste:

* Bli systemadministratör och förstå Cloud Managers produktprofiler.
   * Återgå till [Översikt över introduktionsresan](onboarding-journey-overview.md) om du inte känner till dessa begrepp.
* Förstå grunderna i Adobe Admin Console.
   * Återgå till [Översikt över introduktionsresan](onboarding-journey-overview.md) om du inte känner till dessa begrepp.
* Har information om teammedlemmarna som behöver AEM as a Cloud Service, inklusive
   * Namn
   * E-postadresser
   * Roller och ansvarsområden

## Granska produktprofiler för Cloud Manager {#review-product-profiles}

Från Adobe Admin Console visas en lista med Cloud Manager-profiler.

1. Logga in på Adobe Admin Console på [adminconsole.adobe.com](https://adminconsole.adobe.com/) och **Översikt** sida, markera **Adobe Experience Manager as a Cloud Service** från **Produkter och tjänster** kort.

   ![AEM som produkt](/help/journey-onboarding/assets/assign-team1.png)

1. Navigera till **Cloud Manager** -instans i listan över alla instanser.

   ![Cloud Manager](/help/journey-onboarding/assets/assign-team2.png)

1. Du ser en lista över förkonfigurerade Cloud Manager-produktprofiler.

   ![Produktprofiler](/help/journey-onboarding/assets/assign-team3.png)

## Tilldela användare till företagsägarens produktprofil {#assign-users-business-owner}

Nu kan du lägga till användare och tilldela dem till **Företagsägare** produktprofil.

1. Identifiera de användare som ska hantera Cloud Manager-program och lägga till dem i produktprofilen för Business Owner.

1. Logga in på Admin Console vid [adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview) och **Översikt** sida, markera **Adobe Experience Manager as a Cloud Service** produkt från **Produkter och tjänster** kort.

   ![Produkter och tjänster](/help/journey-onboarding/assets/assign-team1.png)

1. Välj **Användare** i den övre navigeringen och sedan väljer **Lägg till användare**.

   ![Lägg till användare](/help/journey-onboarding/assets/assign-team4.png)

1. I **Lägg till användare i ditt team** anger du e-post-ID för den användare som du vill lägga till.

   * Om det federerade ID:t för dina teammedlemmar inte har konfigurerats än väljer du **Adobe ID** för **ID-typ**.

   ![Lägg till användarinformation](/help/journey-onboarding/assets/assign-team5.png)

1. Klicka på plusknappen under **Välj produkter eller användargrupper** rubrik för att börja produktval och välja **Adobe Experience Manager as a Cloud Service** och tilldela **Företagsägare** produktprofil för användaren.

   * Tilldela varje användare till minst en produktprofil så att användaren kan komma åt Cloud Manager.
   * Kom ihåg att tilldela dig själv som systemadministratör till **Företagsägare** roll.

   ![Tilldela användare](/help/journey-onboarding/assets/assign-team6.png)

1. Klicka **Spara** och ett välkomstmeddelande skickas till användaren som du har lagt till. Den inbjudna användaren kan komma åt Cloud Manager genom att klicka på länken i välkomstmeddelandet och logga in med sin Adobe ID.

1. Upprepa dessa steg för användarna i ditt team.

Ditt nybildade Cloud Manager-team (inklusive dig själv som är tilldelad till **Företagsägare** roll) har konfigurerats. I rollen **Företagsägare**&#x200B;är du nu bara ett steg ifrån att logga in i Cloud Manager och skapa dina molnresurser.

## Tilldela användare till produktprofilen för Distributionshanteraren {#assign-users-deployment-manager}

1. Identifiera de användare som ska hantera Cloud Manager-program och lägga till dem i produktprofilen för Deployment Manager.

1. Logga in på Admin Console vid [adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview) och **Översikt** sidmarkering **Adobe Experience Manager as a Cloud Service** produkten från **Produkter och tjänster** kort.

   ![Produkter och tjänster](/help/journey-onboarding/assets/assign-team1.png)

1. Välj **Användare** i den övre navigeringen och sedan väljer **Lägg till användare**.

   ![Lägg till användare](/help/journey-onboarding/assets/assign-team4.png)

1. I **Lägg till användare i ditt team** anger du e-post-ID för den användare som du vill lägga till.

   * Om det federerade ID:t för dina teammedlemmar inte har konfigurerats än väljer du **Adobe ID** för **ID-typ**.

   ![Ange ID](/help/journey-onboarding/assets/assign-team5.png)

1. Klicka på plusknappen under **Välj produkter eller användargrupper** rubrik för att börja produktval och välja **Adobe Experience Manager as a Cloud Service** och tilldela **Distributionshanteraren** produktprofil för användaren.

   ![Tilldela profil](/help/journey-onboarding/assets/assign-team6.png).

## Tilldela användare till produktprofil för utvecklare {#assign-users-developer}

1. Identifiera de användare som ska hantera Cloud Manager-program.

1. Logga in på Admin Console vid [adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview) och **Översikt** sidmarkering **Adobe Experience Manager as a Cloud Service** produkten från **Produkter och tjänster** kort.

   ![Produkter och tjänster](/help/journey-onboarding/assets/assign-team1.png)

1. Välj **Användare** i den övre navigeringen och sedan väljer **Lägg till användare**.

   ![Lägg till användare](/help/journey-onboarding/assets/assign-team4.png)

1. I **Lägg till användare i ditt team** anger du e-post-ID för den användare som du vill lägga till.

   * Om det federerade ID:t för dina teammedlemmar inte har konfigurerats än väljer du **Adobe ID** för **ID-typ**.

   ![Lägg till användar-ID](/help/journey-onboarding/assets/assign-team5.png)

1. Klicka på plusknappen under **Välj produkter eller användargrupper** rubrik för att börja produktval och välja **Adobe Experience Manager as a Cloud Service** och tilldela **Utvecklare** produktprofil för användaren.

   ![Tilldela profil](/help/journey-onboarding/assets/assign-team6.png).

## What’s Next {#whats-next}

Under den här delen av introduktionsresan lärde du dig allt om att tilldela teammedlemmar till roller i Admin Console. Nu bör du:

* Förstå varför och hur ni måste lägga till teammedlemmar.
* Tre viktiga produktprofiler för Cloud Manager: **Företagsägare**, **Distributionshanteraren** och **Utvecklare**.
* Du kan tilldela teammedlemmar till Cloud Manager-produktprofiler.

Du är nu redo att fortsätta din introduktionsresa genom att nästa gång du granskar dokumentet [Konfigurera molnresurser via Cloud Manager](/help/journey-onboarding/sysadmin/setup-cloud-resources-via-cloud-manager.md), där du får lära dig:

1. För att andra företagsägare ska kunna skapa program är du som systemadministratör tilldelad till **Företagsägare** roll, måste först få åtkomst till och logga in på Cloud Manager.
1. Så här använder du **Företagsägare** kan logga in och konfigurera dina molnresurser, inklusive ditt molnprogram och dina miljöer.
1. Så här använder du **Utvecklare** och **Distributionshanteraren** roller har åtkomst till Cloud Manager.

## Ytterligare resurser {#additional-resources}

Vi rekommenderar att du fortsätter med introduktionsresan enligt beskrivningen ovan. Det här är ytterligare resurser om du vill göra en djupdykning i ett visst ämne från den här resan.

* [Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html?lang=en)
* [Produktprofiler för Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles)
* [Admin Console Identity Overview](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/identity.ug.html)
