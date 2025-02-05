---
title: Tilldela AEM produktprofiler
description: När du har konfigurerat dina molnresurser kan du ge ditt team åtkomst till AEM med hjälp av AEM produktprofiler.
feature: Onboarding
role: Admin, User, Developer
exl-id: c00f5d28-85af-4bd3-a50c-913d1342241c
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '878'
ht-degree: 0%

---

# Tilldela AEM produktprofiler {#assign-profiles-aem}

>[!CONTEXTUALHELP]
>id="assets_user_entitlements"
>title="Tilldela AEM produktprofiler"
>abstract="Du har inte rätt att använda Experience Manager Assets. Kontakta administratören."

I den här delen av [introduktionsresan](overview.md) får du lära dig att ge ditt team åtkomst till AEM med hjälp av AEM produktprofiler.

## Syfte {#objective}

När du har läst det föregående dokumentet på den här introduktionsresan, [Skapa miljöer](create-environments.md), och har konfigurerat dina molnresurser, kan du ge ditt team åtkomst till AEM med hjälp av AEM produktprofiler. Som systemadministratör gör du detta genom att tilldela AEM produktprofiler.

När du har läst det här dokumentet bör du förstå:

* Vad AEM produktprofiler är.
* Så här lägger du till teammedlemmar AEM användarproduktprofilen.
* Så här lägger du till teammedlemmar AEM administratörernas produktprofil.

## AEM produktprofiler {#aem-product-profiles}

Om du vill använda AEM måste teammedlemmarna tilldelas till minst en AEM produktprofil. Åtkomstbehörighet till Cloud Manager räcker inte. Användarna måste tillhöra en av två produktprofiler:

* `AEM Users` - Den här gruppen innehåller vanliga användare som utför vanliga innehållsredigeringsåtgärder.
* `AEM Administrators` - Den här gruppen innehåller användare som ansvarar för avancerade funktioner eller AEM.

>[!NOTE]
>
>Alla användare som tilldelats en AEM as a Cloud Service-produktprofil har skrivskyddad åtkomst till Cloud Manager via rollen **Cloud Manager-användare**.
>
>Användare med användarrollen **Cloud Manager** kan bara logga in i Cloud Manager och navigera till AEM författarmiljöer (om sådana finns) med hjälp av menyalternativen på menyn Program. Rollen **Cloud Manager-användare** har inte tillräcklig åtkomst till programinformation. Om sådan åtkomst behövs måste användarna tilldelas ytterligare roller av systemadministratören.
>Mer information om Cloud Manager användarroller finns i avsnittet [Ytterligare resurser nedan](#additional-resources).

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

1. Logga in på Admin Console på [`https://adminconsole.adobe.com`](https://adminconsole.adobe.com).

1. På sidan **Översikt** väljer du **Adobe Experience Manager as a Cloud Service** från kortet **Produkter och tjänster**.

   ![Kort för produkter och tjänster](/help/journey-onboarding/assets/assign-team1.png)

1. Navigera till och markera instansen.

   ![Markera instans](/help/journey-onboarding/assets/cloud-profiles-1.png)

1. Du kan se en lista över AEM as a Cloud Service produktprofiler som kan tilldelas till en användare baserat på deras roller.

   ![Produktprofiler](/help/journey-onboarding/assets/cloud-profiles-2.png)

## Lägg till teammedlemmar i produktprofiler {#add-team-members}

Nu när du är bekant med de tillgängliga profilerna kan du tilldela dem till dina teammedlemmar efter behov.

De här uppgifterna kräver att du är systemadministratör med Cloud Manager-produktprofilen **Business Owner**.

1. Navigera till ditt program från Cloud Manager och välj knappen **Hantera åtkomst** i den aktuella miljön.

   ![Hantera åtkomst](/help/journey-onboarding/assets/add-team1.png)

1. En ny flik används för att navigera till Admin Console från den plats där du har tillgång till författarinstansen av miljön. Välj **AEM Administratörer** eller **AEM Användare** baserat på de behörigheter som den här personen måste ha.

   ![Tilldela åtkomst](/help/journey-onboarding/assets/add-team2.png)

1. Välj `AEM Administrator` eller `AEM User` och klicka på **Lägg till användare** så som visas nedan och skicka nödvändig information för att lägga till teammedlemmen.

   ![Lägg till teammedlem](/help/journey-onboarding/assets/add-team3.png)

1. Upprepa dessa steg för alla miljöer, inklusive utveckling, staging och produktion, om du har information om teammedlemmar som behöver åtkomst till dem.

Användaren du lade till har nu tillgång till AEM as a Cloud Service Author-tjänsterna!

## Slut på resan? {#the-end}

Grattis! De användare du har tilldelat AEM as a Cloud Service produktprofiler kan nu komma åt AEM redigeringsmiljö och börja skapa innehåll med AEM as a Cloud Service. På samma sätt kan utvecklare nu komma åt Cloud Manager för att använda Git för att lagra anpassad programkod och distribuera den. I det här sammanhanget är introduktionsresan färdig och användarna kan nu använda AEMaaCS.

Men om du bättre vill förstå hur författare och utvecklare använder systemet kan du fortsätta med två valfria delar av den här introduktionsresan:

* [Aktiviteter för utvecklare och distributionsansvarig](developers.md) - Där får du lära dig hur utvecklare får åtkomst till Git för att lagra sin anpassade kod och distribuera den med hjälp av Cloud Manager-pipelines.
* [AEM Användaruppgifter](aem-users.md) - Där får du lära dig hur du kommer åt den AEM miljön där du kan börja skapa innehåll.

## Ytterligare resurser {#additional-resources}

Här följer ytterligare, valfria resurser om du vill gå längre än vad som ingår i introduktionsresan.

* [AEM as a Cloud Service Team- och produktprofiler](/help/onboarding/aem-cs-team-product-profiles.md) - Lär dig hur AEM as a Cloud Service team och produktprofiler kan ge och begränsa åtkomst till licensierade Adobe-lösningar.
* [Hantera produkter och användaråtkomst i Admin Console](/help/security/ims-support.md#managing-products-and-user-access-in-admin-console) - Lär dig hur du använder Admin Console för att hantera användaråtkomst.
* [Konfigurerar åtkomst till AEM-genomgång](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/walk-through.html) - Kolla in den här förkortade genomgången om du vill veta mer om hur du konfigurerar Adobe IMS-användare, användargrupper och produktprofiler i Admin Console.

