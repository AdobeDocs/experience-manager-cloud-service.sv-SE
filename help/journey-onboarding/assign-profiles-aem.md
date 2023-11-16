---
title: Tilldela AEM produktprofiler
description: När du har konfigurerat dina molnresurser kan du ge ditt team åtkomst till AEM med hjälp av AEM produktprofiler.
feature: Onboarding
role: Admin, User, Developer
exl-id: c00f5d28-85af-4bd3-a50c-913d1342241c
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 0%

---

# Tilldela AEM produktprofiler {#assign-profiles-aem}

>[!CONTEXTUALHELP]
>id="assets_user_entitlements"
>title="Tilldela AEM produktprofiler"
>abstract="Du har inte rätt att använda Experience Manager Assets. Kontakta administratören."

I den här delen av [startresan,](overview.md) får du lära dig att ge ditt team tillgång till AEM med hjälp av AEM produktprofiler.

## Syfte {#objective}

När du har läst det föregående dokumentet under den här introduktionsresan, [Skapa miljöer,](create-environments.md) och få dina molnresurser konfigurerade kan du ge ditt team åtkomst till AEM med AEM produktprofiler. Som systemadministratör gör du detta genom att tilldela AEM produktprofiler.

När du har läst det här dokumentet bör du förstå:

* Vad AEM produktprofiler är.
* Så här lägger du till teammedlemmar AEM användarproduktprofilen.
* Så här lägger du till teammedlemmar AEM administratörernas produktprofil.

## AEM produktprofiler {#aem-product-profiles}

Om du vill använda AEM måste teammedlemmarna tilldelas till minst en AEM produktprofil. Behörigheter för åtkomst till Cloud Manager räcker inte. Användarna måste tillhöra en av två produktprofiler:

* `AEM Users` - Den här gruppen innehåller vanliga användare som arbetar med vardagsarbete med innehåll.
* `AEM Administrators` - Den här gruppen innehåller användare som ansvarar för avancerade funktioner eller AEM.

>[!NOTE]
>
>Alla användare som tilldelats en AEM as a Cloud Service produktprofil har skrivskyddad åtkomst till Cloud Manager via **Cloud Manager-användare** roll.
>
>Användare med **Cloud Manager** Användarrollen kan bara logga in i Cloud Manager och navigera till AEM författarmiljöer (om sådana finns) med hjälp av alternativen på menyn Program. The **Cloud Manager-användare** rollen räcker inte för att komma åt programinformationen. Om sådan åtkomst behövs måste användarna tilldelas ytterligare roller av systemadministratören.
>Se [Avsnittet Ytterligare resurser nedan](#additional-resources) för mer information om användarroller i Cloud Manager.

>[!CAUTION]
>
>Redigera eller ta inte bort produktprofilerna AEM administratörer eller AEM användare. Om du redigerar profilnamnen kan inloggningen till AEM molninstans brytas.

## Förutsättningar {#prerequisites}

Innan du börjar läsa det här avsnittet bör du ha tillgång till följande information om ditt team som kommer att använda AEM.

* Namn
* E-postadresser
* Roller och ansvarsområden

>[!TIP]
>
>För att komma igång rekommenderar Adobe att du till att börja med lägger till användare som ska delta i de omedelbara uppgifterna, till exempel administratörer, utvecklare och innehållsförfattare. Du kan fortsätta med resten av introduktionen utan att lägga till alla användare. När du är klar med introduktionen kan du skala till ett större antal användare senare.

## Visa AEM produktprofiler {#view-profiles}

Följ de här stegen för att se de AEM produktprofilerna från Admin Console.

1. Logga in Admin Console på [`https://adminconsole.adobe.com`.](https://adminconsole.adobe.com)

1. Från **Ökning** sida, markera **Adobe Experience Manager as a Cloud Service** från **Produkter och tjänster** kort.

   ![Produkter och tjänstekort](/help/journey-onboarding/assets/assign-team1.png)

1. Navigera till och markera instansen.

   ![Markera instans](/help/journey-onboarding/assets/cloud-profiles-1.png)

1. Du kan se en lista över AEM as a Cloud Service produktprofiler som kan tilldelas en användare baserat på deras roller.

   ![Produktprofiler](/help/journey-onboarding/assets/cloud-profiles-2.png)

## Lägg till teammedlemmar i produktprofiler {#add-team-members}

Nu när du är bekant med de tillgängliga profilerna kan du tilldela dem till dina teammedlemmar efter behov.

Dessa uppgifter kräver att du är systemadministratör för **Företagsägare** Cloud Manager-produktprofil.

1. Navigera till ditt program från Cloud Manager och välj **Hantera åtkomst** i den miljö som är av intresse.

   ![Hantera åtkomst](/help/journey-onboarding/assets/add-team1.png)

1. En ny flik används för att navigera till Admin Console från den plats där du har tillgång till författarinstansen av miljön. Välj **AEM administratörer** eller **AEM** baserat på de tillstånd som personen måste få.

   ![Tilldela åtkomst](/help/journey-onboarding/assets/add-team2.png)

1. Välj `AEM Administrator` eller `AEM User` och klicka **Lägg till användare** som visas nedan och skicka in den information som behövs för att lägga till teammedlemmen.

   ![Lägg till teammedlem](/help/journey-onboarding/assets/add-team3.png)

1. Upprepa dessa steg för alla miljöer, inklusive utveckling, staging och produktion, om du har information om teammedlemmar som behöver åtkomst till dem.

Användaren du lade till har nu tillgång till AEM as a Cloud Service redigeringstjänster!

## Slut på resan? {#the-end}

Grattis! De användare du har tilldelat till AEM as a Cloud Service produktprofiler kan nu komma åt den AEM redigeringsmiljön och börja skapa innehåll med AEM as a Cloud Service. På samma sätt kan utvecklare nu komma åt Cloud Manager för att använda Git för att lagra anpassad programkod och distribuera den. I det här sammanhanget är introduktionsresan färdig och användarna kan nu använda AEMaaCS.

Men om du bättre vill förstå hur författare och utvecklare använder systemet kan du fortsätta med två valfria delar av den här introduktionsresan:

* [Uppgifter för utvecklare och distributionsansvarig](developers.md) - Där får du lära dig hur utvecklare får tillgång till Git för att lagra sin egen kod och distribuera den med hjälp av Cloud Manager-pipelines.
* [AEM användaruppgifter](aem-users.md) - Där du lär dig hur du kommer åt den AEM miljön där du kan börja skapa innehåll.

## Ytterligare resurser {#additional-resources}

Här följer ytterligare, valfria resurser om du vill gå längre än vad som ingår i introduktionsresan.

* [AEM as a Cloud Service team- och produktprofiler](/help/onboarding/aem-cs-team-product-profiles.md) - Lär dig hur AEM as a Cloud Service team och produktprofiler kan ge och begränsa åtkomst till era licensierade Adobe-lösningar.
* [Hantera produkter och användaråtkomst i Admin Console](/help/security/ims-support.md#managing-products-and-user-access-in-admin-console) - Lär dig hur du använder Admin Console för att hantera åtkomsten.
* [Konfigurera åtkomst till AEM genomgång](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/walk-through.html) - Kolla in den här förkortade genomgången om du vill veta mer om hur du konfigurerar Adobe IMS-användare, användargrupper och produktprofiler i Admin Console.

