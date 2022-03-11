---
title: Tilldela teammedlemmar till AEM as a Cloud Service produktprofiler
description: Följ den här sidan för att lära dig hur du tilldelar teammedlemmar AEM as a Cloud Service produktprofiler
feature: Onboarding
role: Admin, User, Developer
exl-id: c00f5d28-85af-4bd3-a50c-913d1342241c
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 2%

---

# Tilldela teammedlemmar till AEM as a Cloud Service produktprofiler {#assign-team-members-cloud-service}

## Syfte {#objective}

Det här dokumentet hjälper dig att förstå de steg som systemadministratören måste ta för att tilldela dina teammedlemmar AEM as a Cloud Service produktprofiler och varför det är viktigt att dina AEM-författare kan ge sig ut på sin resa med AEM.

När du har läst det här avsnittet bör du förstå:

* Varför och hur teammedlemmarna tilldelas till AEM as a Cloud Service produktprofiler.
* Så här lägger du till teammedlemmar AEM användarproduktprofilen.
* Så här lägger du till teammedlemmar AEM administratörernas produktprofil.


## Introduktion {#introduction}

För att beviljas åtkomst till AEM as a Cloud Service användare måste de tillhöra en av två produktprofiler:  `AEM Users` eller `AEM Administrators`. Teammedlemmarna måste beviljas behörigheter till AEM eftersom behörighet att administrera Cloud Manager inte räcker.

>[!NOTE]
>Alla användare som tilldelas AEM användarproduktprofilen av systemadministratören har (skrivskyddad) åtkomst till Cloud Manager.

## Krav {#prerequisites}

Innan du börjar läsa det här avsnittet bör du överväga följande krav:

* Förstå [AEM as a Cloud Service produktprofiler](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#aem-product-profiles)
* Bekanta dig med [Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/admin-console.html?lang=en)
* Produktprofiler för Cloud Manager har tilldelats dina teammedlemmar efter behov, och molnresurserna har konfigurerats
* Information om teammedlemmen: Systemadministratören måste ha namn och e-postadresser samt roller och ansvar för de teammedlemmar som behöver åtkomst till AEM as a Cloud Service.

   >[!NOTE]
   >För att komma igång rekommenderar vi att du först lägger till användare som ska delta i de omedelbara uppgifterna, till exempel administratörer, utvecklare och innehållsförfattare. Du kan fortsätta med resten av introduktionen utan att lägga till alla användare. När du är klar med introduktionen kan du skala till ett större antal användare senare.


   >[!IMPORTANT]
   >Innan du börjar granska stegen för hur du tilldelar teammedlemmar till AEM as a Cloud Service produktprofiler måste du följa dessa två steg:
   >
   >1. Logga in på [Adobe Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/admin-console.html?lang=en). Mer information finns i Logga in på Admin Console.
   >
   >1. Granska [AEM as a Cloud Service produktprofiler](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#aem-product-profiles).


Följ stegen nedan för att se en lista över profiler för Cloud Manager från Adobe Admin Console:

1. Logga in på [Adobe Admin Console](https://adminconsole.adobe.com/). Från **Översikt** sida, markera **Adobe Experience Manager as a Cloud Service** från **Produkter och tjänster** kort.

   ![](/help/journey-onboarding/assets/assign-team1.png)

1. Navigera till och markera instansen (Author instance of Development environment) som visas i bilden nedan.

   ![](/help/journey-onboarding/assets/cloud-profiles-1.png)


1. Du ser en lista AEM as a Cloud Service produktprofiler som ska tilldelas en användare baserat på deras roll.

   >[!NOTE]
   >Mer information om detta finns i [AEM as a Cloud Service produktprofiler](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#aem-product-profiles).

   ![](/help/journey-onboarding/assets/cloud-profiles-2.png)


## Lägg till teammedlemmar i AEM användar- eller AEM administratörsproduktprofil {#add-team-members}

För att beviljas åtkomst till AEM as a Cloud Service instansen måste användarna tillhöra en av två produktprofiler `AEM Users` eller `AEM Administrators`.

>[!NOTE]
>Du måste ha behörighet för instansen. Behörigheter att administrera Cloud Manager räcker inte. Läs mer.

Stegen nedan måste följas av en systemadministratör som också har rollen Business Owner.

1. Navigera till ditt program från Cloud Manager och välj **Hantera åtkomst** knappen i den miljö som är av intresse enligt nedan.

   ![](/help/journey-onboarding/assets/add-team1.png)

1. En ny flik används för att navigera till Adobe Admin Console där du har tillgång till författarinstansen av miljön. Välj **AEM administratörer** eller **AEM** baserat på de behörigheter som personen måste ge. Läs mer om [AEM as a Cloud Service produktprofiler](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#aem-product-profiles).

   ![](/help/journey-onboarding/assets/add-team2.png)

1. Välj `AEM Administrator` eller `AEM User` och klicka på **Lägg till användare** som visas nedan och skicka in den information som behövs för att lägga till teammedlemmen.

   ![](/help/journey-onboarding/assets/add-team3.png)

   Användaren du lade till har nu tillgång till AEM as a Cloud Service redigeringstjänster!

   >[!NOTE]
   >Du vill upprepa dessa steg för alla miljöer, inklusive utveckling, scen och produktion, om du har information om teammedlemmar som behöver åtkomst till dem.


## What’s Next {#whats-next}

De användare du har tilldelat till AEM as a Cloud Service produktprofiler kan nu lära sig hur du kommer åt Författaren och bekanta dig med redigeringssidor på AEM as a Cloud Service. Du bör följa sökvägen genom att nästa gång du granskar dokumentets utbildningsväg för [AEM](/help/journey-onboarding/sysadmin/learning-path-aem-users.md) eller för [Utvecklare och driftsättningschefer](/help/journey-onboarding/sysadmin/learning-path-developers-deploymentmanagers.md).

## Ytterligare resurser {#additional-resources}

* [Hantera produkter och användaråtkomst i Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=en#managing-products-and-user-access-in-admin-console)
* [Konfigurera åtkomst till AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/walk-through.html?lang=en)
* [Snabbstartsguide till redigering av sidor](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/getting-started/quick-start.html?lang=en)
