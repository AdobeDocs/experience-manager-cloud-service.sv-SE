---
title: AEM som Cloud Service team och produktprofiler
description: Följ den här sidan om du vill veta mer om AEM som Cloud Service Team och produktprofiler.
source-git-commit: 976fc51be0ba8c407ff7d6f7c1a6efecbbdad5c9
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 0%

---


# AEM som Cloud Service Team och produktprofiler {#product-profiles}

## Produktprofiler {#profiles}

När du ger en användare åtkomst till en viss Adobe-lösning behöver du inte nödvändigtvis ge dem fullständig åtkomst. Produktprofiler gör att varje lösning kan ha en egen uppsättning användarbehörigheter. Dessa är tillgängliga och tillgängliga via [Adobe Admin Console](/help/onboarding/learn-concepts/admin-console.md).

Läs mer om [AEM som en Cloud Service produktprofiler](#aem-product-profiles) och [Cloud Manager-produktprofiler](#cloud-manager-product-profiles) för att förstå hur dessa fungerar tillsammans medan teamet är konfigurerat.

## AEM som en Cloud Service produktprofiler {#aem-product-profiles}

AEM som Cloud Service är det helt molnbaserade erbjudandet som tillhandahåller AEM som en tjänst. AEM levereras på ett inbyggt sätt i molnet, med nya attribut som alltid på, alltid aktuella, alltid säkra och alltid i stor skala. Samtidigt behåller AEM det huvudsakliga mervärdet som utgör en anpassningsbar plattform för kunder och gör det möjligt för företagsgrupper att integrera i sina utvecklings- och leveransrutiner. Se [Introduktion till Adobe Experience Manager som Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/introduction.html?lang=en) om du vill veta mer om AEM som Cloud Service.

AEM som teammedlemmar i Cloud Servicen läggs till och tilldelas en eller flera av följande produktprofiler via Admin Console under introduktionen.

* **AEM administratörer**: En AEM administratör tilldelas vanligtvis till utvecklare, särskilt utvecklare som måste ha tillgång till exempelvis utvecklingsmiljöerna. AEM administratörsproduktprofil används för att ge administratörsbehörighet i den associerade AEM.

* **AEM**: AEM användare är de användare i organisationen som använder AEM som Cloud Service i avtalet med Adobe. Dessa medlemmar måste ha åtkomst till AEM för att kunna utföra sina uppgifter. Produktprofilen AEM användare tilldelas vanligen till en AEM innehållsförfattare som skapar och granskar innehållet (detta kan vara av flera typer). till exempel sidor, resurser, publikationer o.s.v.) innan den publiceras på webbplatsen. AEM användarprofil som visas nedan är tilldelad dessa medlemmar.

   ![](/help/onboarding/learn-concepts/assets/admin-console-profiles.png)

   >[!NOTE]
   >Alla användare som tilldelats en AEM som en produktprofil för en Cloud Service har (skrivskyddad) åtkomst till Cloud Manager.

## Produktprofiler för Cloud Manager {#cloud-manager-product-profiles}

Cloud Manager har förkonfigurerade produktprofiler, eller mer enkelt, rollbaserade behörigheter. Din systemadministratör ansvarar för att konfigurera ditt Cloud Manager-team genom att tilldela dem till dessa produktprofiler, och måste bekanta sig med dessa produktprofiler och vilka gruppmedlemmar de ska tilldelas till.
>[!NOTE]
>Mer information finns i [Rollbaserade behörigheter i Cloud Manager](/help/onboarding/what-is-required/user-roles-permissions.md).

Var och en av produktprofilerna har tillhörande behörigheter. Om du till exempel har rollen som

* **Business Owner**, du har behörighet att lägga till ett nytt program eller redigera ett program, lägga till eller uppdatera en miljö, lägga till/redigera/ta bort pipelinen och köra valfri pipeline samt distribuera kod AEM miljö eller kodkvalitet.

* **Distributionshanteraren** har behörighet att lägga till eller uppdatera en miljö, köra valfri pipeline och distribuera kod AEM miljön eller kodkvaliteten.

* **Utvecklare**: du har behörighet att skapa en personlig åtkomsttoken för åtkomst till Git.

* **Programhanteraren** har du behörighet att schemalägga pipelines, åsidosätta kvalitetsportar i tre nivåer och tillhandahålla produktionsgodkännande.

En användare kan tilldelas till flera produktprofiler. Om du till exempel tilldelar en användare både Business Owner och Deployment Manager-roller får användaren kombinationen eller summan av dessa behörigheter.

Ditt Cloud Manager-team kommer att innehålla minst:

* En Business Owner, som vanligtvis också är systemadministratör, och måste vara den första personen som loggar in på och får åtkomst till Cloud Manager
* En distributionshanterare
* En utvecklare

   >[!NOTE]
   >För att få tillgång till AEM som Cloud Service måste användarna tillhöra en av två produktprofiler: `AEM Users` eller `AEM Administrators`. Du måste ha behörighet för instansen. Behörigheterna för att administrera den associerade Cloud Manager räcker inte.