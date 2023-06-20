---
title: AEM as a Cloud Service team- och produktprofiler
description: Lär dig hur AEM as a Cloud Service team och produktprofiler kan ge och begränsa åtkomst till era licensierade Adobe-lösningar.
exl-id: 7b1474c9-aca0-4354-8798-1abdcda2f6dd
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 0%

---

# AEM as a Cloud Service team- och produktprofiler {#product-profiles}

Lär dig hur AEM as a Cloud Service team och produktprofiler kan ge och begränsa åtkomst till era licensierade Adobe-lösningar.

## Produktprofiler {#profiles}

När du ger en användare åtkomst till en viss Adobe-lösning behöver du inte nödvändigtvis ge dem fullständig åtkomst. Med produktprofiler kan varje lösning ha en egen uppsättning användarbehörigheter. Dessa är tillgängliga via [Admin Console.](/help/journey-onboarding/admin-console.md)

## AEM as a Cloud Service produktprofiler {#aem-product-profiles}

AEM as a Cloud Service är ett fullständigt molnbaserat erbjudande som ger AEM som en tjänst. AEM levereras på ett inbyggt sätt i molnet, med nya attribut som alltid på, alltid aktuella, alltid säkra och alltid i stor skala. Samtidigt behåller AEM det huvudsakliga mervärdet som ger kunderna en anpassningsbar plattform och gör det möjligt för företagsgrupper att integrera i sina utvecklings- och leveransrutiner. Se [Introduktion till Adobe Experience Manager as a Cloud Service](/help/overview/introduction.md) om du vill veta mer om AEM as a Cloud Service.

Dina AEM as a Cloud Service teammedlemmar läggs till och tilldelas en eller flera av följande produktprofiler via Admin Console under introduktionen.

* **AEM administratörer**: En AEM administratör tilldelas vanligtvis till utvecklare, särskilt utvecklare som måste ha tillgång till exempelvis utvecklingsmiljöerna. AEM administratörs produktprofil används för att ge administratörsbehörighet i den associerade AEM.

* **AEM**: AEM användare är de användare i organisationen som i allmänhet använder AEM as a Cloud Service för att skapa innehåll. Dessa användare måste ha åtkomst till AEM för att kunna utföra sina uppgifter. AEM produktprofil tilldelas vanligtvis till en författare som skapar och granskar innehåll AEM. Det här innehållet kan vara av många typer, till exempel sidor, resurser, publikationer och så vidare. De AEM användarnas produktprofil som visas nedan tilldelas dessa medlemmar.

![Produktprofiler](/help/onboarding/assets/admin-console-profiles.png)

>[!NOTE]
>
>Alla användare som tilldelats en AEM as a Cloud Service produktprofil har skrivskyddad åtkomst till Cloud Manager via **Cloud Manager-användare** roll.
>
>Användare med endast **Cloud Manager-användare** kan du logga in i Cloud Manager och navigera till AEM (om det finns någon) med hjälp av **Program** menyalternativ. The **Cloud Manager-användare** rollen räcker inte för att komma åt programinformationen. Om sådan åtkomst behövs måste användarna tilldelas ytterligare roller av systemadministratören.

>[!WARNING]
>
>The **AEM administratörer** produktprofilens namn får inte ändras. Ändra namnet på **AEM administratörer** produktprofilen tar bort administratörsrättigheter för alla användare som har tilldelats den profilen.

>[!TIP]
>
>* Läs mer om AEM produktprofiler i dokumentet [Tilldela AEM produktprofiler.](/help/journey-onboarding/assign-profiles-aem.md)
>* Mer information om introduktionsprocessen finns i [Startresa.](/help/journey-onboarding/overview.md)

## Produktprofiler för Cloud Manager {#cloud-manager-product-profiles}

Cloud Manager har förkonfigurerade produktprofiler som kan ses som rollbaserade behörigheter. Din systemadministratör ansvarar för att konfigurera ditt Cloud Manager-team genom att tilldela dem till dessa produktprofiler.

>[!TIP]
>
>Se dokumentet [Rollbaserade behörigheter i Cloud Manager](/help/onboarding/cloud-manager-introduction.md#role-based-permissions) för mer information.

Var och en av produktprofilerna har särskilda behörigheter kopplade till sig.

* **Företagsägare** - I den här rollen har du behörighet att lägga till ett nytt program eller redigera ett program, lägga till eller uppdatera en miljö, distribuera kod AEM miljön eller utföra kvalitetskontroller av kod.
* **Distributionshanteraren** - I den här rollen har du behörighet att lägga till eller uppdatera en miljö, köra valfri pipeline och distribuera kod till AEM eller utföra kodkvalitetskontroller.
* **Utvecklare** - I den här rollen har du behörighet att skapa personliga åtkomsttoken för åtkomst till Git.
* **Programhanteraren** - I den här rollen har du behörighet att schemalägga rörledningar, åsidosätta de tre skiktens kvalitetsgates och ge produktionsgodkännande.

En användare kan tilldelas till flera produktprofiler. Du kan till exempel tilldela båda **Företagsägare** och **Distributionshantering** r roller till en användare ger dem summan av dessa behörigheter.

Ditt Cloud Manager-team kommer att innehålla minst:

* Ett **Företagsägare**, som vanligtvis också är systemadministratör, och måste vara den första personen som loggar in på och får åtkomst till Cloud Manager
* Ett **Distributionshanteraren**
* Ett **Utvecklare**

>[!NOTE]
>
>För att få åtkomst till AEM as a Cloud Service måste användarna tillhöra en av två produktprofiler: `AEM Users` eller `AEM Administrators`. Behörigheter att administrera Cloud Manager räcker inte.

>[!TIP]
>
>* Läs mer om produktprofiler för Cloud Manager i dokumentet [Tilldela teammedlemmar till Cloud Manager-produktprofiler.](/help/journey-onboarding/assign-profiles-cloud-manager.md)
>* Mer information om introduktionsprocessen finns i [Startresa.](/help/journey-onboarding/overview.md)
