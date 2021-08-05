---
title: Navigera till Cloud Manager
description: Följ den här sidan för att lära dig hur du navigerar till startsidan för Cloud Manager
exl-id: 9cf25d1d-a351-4ea0-b2e9-1df6ca4915b7
source-git-commit: 058622fd2628656c7b2fb3a02445724ca6a62f3b
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 6%

---

# Navigera till Cloud Manager {#cloud-manager}

Cloud Manager är en viktig del av AEM som Cloud Service. Det gör det möjligt för organisationer att självhantera Experience Manager i molnet. Det innehåller ett ramverk för kontinuerlig integrering och kontinuerligt leverans (CI/CD) som gör att IT-team och implementeringspartners kan snabba upp leveransen av anpassningar eller uppdateringar utan att kompromissa med prestanda eller säkerhet. Med användargränssnittet kan du konfigurera och starta CI/CD-flödet.

När din systemadministratör har gett dig åtkomst till Cloud Manager får du ett e-postmeddelande som tar dig till startsidan för [Adobe Experience Cloud](https://experience.adobe.com).

>[!NOTE]
>Du måste läggas till som användare och måste tilldelas minst en molnhanterarroll (produktprofil i Admin Console) av din systemadministratör.

1. I välkomstmeddelandet klickar du på **Kom igång**, vilket visas i bilden nedan.
   ![](/help/onboarding/what-is-required/assets/get-started-email.png)


   >[!IMPORTANT]
   >Du kan också navigera direkt till inloggningssidan för Cloud Manager från [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/). Bokmärk den här sidan för framtida bruk och för att hjälpa dig att navigera direkt till Cloud Managers landningssida.

1. Du dirigeras till Cloud Managers landningssida.

Du kan även navigera till sidan **Program och produkter** i Cloud Manager från Adobe Experience Cloud hemsida. Följ stegen nedan:

1. Navigera direkt till [Adobe Experience Cloud](https://experience.adobe.com) och logga in med din Adobe ID.

1. Välj **Experience Manager**.
   ![](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/landing-page1.png)

1. Klicka på **Starta** från Cloud Manager-kortet. När du har loggat in på [!UICONTROL Cloud Manager] är du redo att använda användargränssnittet.
   ![](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/landing-page2.png)

1. När inloggningen är klar dirigeras du till landningssidan för Cloud Manager.


## Startsida för Cloud Manager {#cloud-manager-landing}

När inloggningen är klar dirigeras du till landningssidan för Cloud Manager.

>[!NOTE]
>Beroende på vilka roller som har tilldelats i [!UICONTROL Cloud Manager] och programmets status visas olika skärmar när du använder användargränssnittet för [!UICONTROL Cloud Manager].

Ett av de tre alternativen som beskrivs nedan visas:

* **När det inte finns några program i Cloud Manager**

   Om det inte finns några program i organisationen instruerar landningssidan dig att skapa ditt första program, vilket visas i bilden nedan.
   ![](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin0.png)

* **När program redan finns i Cloud Manager**

   Om det redan finns program i organisationen instruerar landningssidan dig att lägga till ett annat program och att visa alla befintliga program också, vilket visas i bilden nedan.

   ![](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

* **När ett program finns och användaren är systemadministratör**

   Om det redan finns program i organisationen, och du är systemadministratör, visar landningssidan knappen **Hantera åtkomst** tillsammans med alternativet **Lägg till program**, vilket visas i bilden nedan.

   ![](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/admin-console-4.png)

Härifrån kan en användare med rätt behörigheter, t.ex. en Business Owner-roll i Cloud Manager välja **Lägg till program** för att starta [guiden Lägg till program](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/production-programs/creating-production-program.html?lang=en#getting-access).

Mer information om hur du lägger till ett program i Cloud Manager finns i Skapa:

* [Produktionsprogram](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/production-programs/creating-production-program.html?lang=en)
* [Sandbox Program](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/sandbox-programs/creating-sandbox-program.html?lang=en)