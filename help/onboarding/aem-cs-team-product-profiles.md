---
title: AEM as a Cloud Service Team- och produktprofiler
description: Läs om hur AEM as a Cloud Service team och produktprofiler kan ge och begränsa åtkomst till era licensierade Adobe-lösningar.
exl-id: 7b1474c9-aca0-4354-8798-1abdcda2f6dd
feature: Onboarding
role: Admin, User, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '847'
ht-degree: 0%

---


# AEM as a Cloud Service Team- och produktprofiler {#product-profiles}

Läs om hur AEM as a Cloud Service team och produktprofiler kan ge och begränsa åtkomst till era licensierade Adobe-lösningar.

## Produktprofiler {#profiles}

När du ger en användare åtkomst till en viss Adobe-lösning behöver du inte nödvändigtvis ge dem fullständig åtkomst. Med produktprofiler kan varje lösning ha en egen uppsättning användarbehörigheter. Dessa är tillgängliga och tillgängliga via [Admin Console](/help/journey-onboarding/admin-console.md).

## AEM as a Cloud Service produktprofiler {#aem-product-profiles}

AEM as a Cloud Service är ett fullständigt molnbaserat erbjudande som ger AEM som en tjänst. AEM levereras på ett inbyggt sätt i molnet, med nya attribut som alltid på, alltid aktuella, alltid säkra och alltid i stor skala. Samtidigt behåller AEM det huvudsakliga mervärdet som utgör en anpassningsbar plattform för kunder och gör det möjligt för företagsgrupper att integrera i sina utvecklings- och leveransrutiner. Mer information om AEM as a Cloud Service finns i [Introduktion till Adobe Experience Manager as a Cloud Service](/help/overview/introduction.md).

Dina AEM as a Cloud Service-teammedlemmar läggs till och tilldelas en eller flera av följande produktprofiler via Admin Console under introduktionen.

* **AEM Administratörer**: En AEM administratör tilldelas vanligtvis till utvecklare, särskilt utvecklare som behöver åtkomst till till till exempel utvecklingsmiljöerna. AEM administratörs produktprofil används för att ge administratörsbehörighet i den associerade AEM.

* **AEM användare**: AEM användare är de användare i din organisation som använder AEM as a Cloud Service i allmänhet för att skapa innehåll. Dessa användare måste ha åtkomst till AEM för att kunna utföra sina uppgifter. AEM produktprofil tilldelas vanligtvis till en författare som skapar och granskar innehåll AEM. Det här innehållet kan vara av många typer, till exempel sidor, resurser, publikationer och så vidare. De AEM användarnas produktprofil som visas nedan tilldelas dessa medlemmar.

![Produktprofiler](/help/onboarding/assets/admin-console-profiles.png)

>[!NOTE]
>
>Alla användare som tilldelats en AEM as a Cloud Service-produktprofil har skrivskyddad åtkomst till Cloud Manager via rollen **Cloud Manager-användare**.
>
>Användare med endast rollen **Cloud Manager-användare** kan logga in på Cloud Manager och navigera till AEM författarmiljöer (om sådana finns) med hjälp av menyalternativen på **Program** . Rollen **Cloud Manager-användare** har inte tillräcklig åtkomst till programinformation. Om sådan åtkomst behövs måste användarna tilldelas ytterligare roller av systemadministratören.

>[!WARNING]
>
>**AEM Administrators** produktprofilnamnet får inte ändras. Om du ändrar namnet på produktprofilen **AEM Administratörer** tas administratörsrättigheter bort från alla användare som tilldelats den profilen.

>[!TIP]
>
>* Mer information om AEM produktprofiler finns i [Tilldela AEM produktprofiler](/help/journey-onboarding/assign-profiles-aem.md).
>* Mer information om introduktionsprocessen finns i [Startresa](/help/journey-onboarding/overview.md).

## Cloud Manager produktprofiler {#cloud-manager-product-profiles}

Cloud Manager har förkonfigurerade produktprofiler som kan tolkas som rollbaserade behörigheter. Din systemadministratör ansvarar för att konfigurera ditt Cloud Manager-team genom att tilldela dem till dessa produktprofiler.

>[!TIP]
>
>Mer information finns i [Rollbaserade behörigheter i Cloud Manager](/help/onboarding/cloud-manager-introduction.md#role-based-permissions).

Var och en av produktprofilerna har särskilda behörigheter kopplade till sig.

* **Affärsägare**
   * I den här rollen har du behörighet att lägga till ett nytt program eller redigera ett program, lägga till eller uppdatera en miljö, distribuera kod AEM miljön eller utföra kodkvalitetskontroller.
   * Den här användaren ansvarar för att definiera KPI:er, godkänna produktionsdistributioner och åsidosätta viktiga 3-nivåfel vid behov.
* **Distributionshanteraren**
   * I den här rollen har du behörighet att lägga till eller uppdatera en miljö, köra valfri pipeline och distribuera kod till AEM eller utföra kodkvalitetskontroller.
   * Den här användaren hanterar driftsättningsåtgärder och använder Cloud Manager för att utföra mellanlagrings-/produktionsdistributioner, redigera CI/CD-pipelines, godkänna viktiga 3-skiktsfel vid behov och har åtkomst till Git-databasen.
* **Utvecklare**
   * I den här rollen har du behörighet att skapa personliga åtkomsttoken för åtkomst till Git.
   * Den här användaren utvecklar och testar anpassad programkod och använder främst Cloud Manager för att visa distributionsstatus och har åtkomst till Git-databasen för kodimplementeringar.
* **Programhanteraren**
   * I den här rollen har du behörighet att schemalägga pipelines, åsidosätta de tre skiktens kvalitetsgates och tillhandahålla produktionsgodkännande.
   * Den här användaren använder Cloud Manager för att utföra gruppkonfiguration, granska status, visa KPI:er och kan godkänna viktiga 3-nivåfel när det behövs.

En användare kan tilldelas till flera produktprofiler. Om du till exempel tilldelar en användare både rollen **Affärsägare** och rollen **Distributionshantering** r får användaren summan av dessa behörigheter.

Cloud Manager-teamet kommer att innehålla minst:

* En **Business Owner**, som vanligtvis också är systemadministratör, och som måste vara den första personen som loggar in och får åtkomst till Cloud Manager
* En **Distributionshanterare**
* En **utvecklare**

>[!NOTE]
>
>För att få åtkomst till AEM as a Cloud Service måste användarna tillhöra en av två produktprofiler: `AEM Users` eller `AEM Administrators`. Behörigheter att administrera Cloud Manager räcker inte.

>[!TIP]
>
>* Mer information om Cloud Manager produktprofiler finns i [Tilldela teammedlemmar till Cloud Manager produktprofiler](/help/journey-onboarding/assign-profiles-cloud-manager.md).
>* Mer information om introduktionsprocessen finns i [Startresa](/help/journey-onboarding/overview.md).
