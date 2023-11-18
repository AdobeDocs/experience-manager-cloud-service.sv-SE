---
title: Tilldela teammedlemmar till Cloud Manager-produktprofiler
description: Följ den här sidan för att lära dig hur du tilldelar teammedlemmar till produktprofiler för Cloud Manager
feature: Onboarding
role: Admin, User, Developer
exl-id: 555688e5-f937-462c-9fcc-b90685f1882b
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '1527'
ht-degree: 0%

---


# Tilldela teammedlemmar till Cloud Manager-produktprofiler {#assign-team-members}

I den här delen av [startresan,](overview.md) om du vill lära dig hur du tilldelar teammedlemmar till Cloud Managers produktprofiler.

## Syfte {#objective}

I det föregående steget på denna resa [som har åtkomst till Admin Console,](admin-console.md) du har lärt dig logga in på Admin Console och verifiera dina behörigheter som systemadministratör. Nu kan du ge teammedlemmarna tillgång till Cloud Manager. Det gör du genom att tilldela produktprofiler.

När du ger användare åtkomst till en Adobe-lösning behöver du inte nödvändigtvis ge dem full åtkomst. Med produktprofiler kan varje lösning ha en egen uppsättning användarbehörigheter. Du använder Admin Console för att tilldela produktprofiler.

Det första steget är att ge användarna åtkomst till Cloud Manager. Cloud Manager har stöd för företagsutvecklingsmiljöer och de specialbyggda CI/CD-pipelines som är utrustade för grundlig testning och högsta kodkvalitet för att leverera enastående upplevelser.

När du har läst det här dokumentet bör du:

* Förstå vilka produktprofiler som är.
* Förstå vad Cloud Manager är.
* Lär dig de tre viktiga produktprofilerna för Cloud Manager: **Företagsägare**, **Distributionshanteraren** och **Utvecklare**.
* Du kan tilldela teammedlemmar till Cloud Manager-produktprofiler.

## Förutsättningar {#prerequisites}

Om du vill tilldela teammedlemmar till produktprofiler måste du ha information om teammedlemmarna, som måste ha tillgång AEM as a Cloud Service, inklusive:

* Namn
* E-postadresser
* Roller och ansvarsområden

>[!TIP]
>
>För att komma igång rekommenderar Adobe att du till att börja med lägger till användare som ska delta i de omedelbara uppgifterna, till exempel administratörer, utvecklare och innehållsförfattare.
>
>Du kan fortsätta med introduktionsprocessen utan att lägga till alla användare. När du är klar med introduktionen kan du lägga till fler användare.

## Produktprofiler {#product-profiles}

När du ger användare åtkomst till en Adobe-lösning behöver du inte nödvändigtvis ge dem full åtkomst. Med produktprofiler kan varje lösning ha en egen uppsättning användarbehörigheter som ställs in med Admin Console.

Senare under den här resan kommer du till exempel att använda Admin Console för att ge användare åtkomst till AEM genom att tilldela produktprofiler till AEM administratörer och AEM författare.

Nästa steg är dock att tilldela produktprofiler så att teammedlemmarna först får tillgång till Cloud Manager.

## Cloud Manager {#cloud-manager}

Som systemadministratör vet du att ett lyckat AEM as a Cloud Service projekt inte bara handlar om att skapa fantastiskt innehåll med hjälp av AEM, utan även om att utveckla och driftsätta egen, anpassad kod och program för att leverera AEM innehåll.

Cloud Manager är en integrerad del av AEM as a Cloud Service och används för att hantera dina CI/CD-pipelines för koddistribution, hantera dina koddatabaser och hantera dina miljöer.

Innan ditt team kan göra något annat måste de integreras i Cloud Manager genom att ge dem de produktprofiler de behöver. I nästa steg visas var du hittar Cloud Manager-produktprofilen med Admin Console och hur du tilldelar dem till dina teammedlemmar.

## Granska produktprofiler för Cloud Manager {#review-product-profiles}

Med Admin Console kan du se en lista över Cloud Manager-profiler.

1. Logga in på Adobe Admin Console på [adminconsole.adobe.com](https://adminconsole.adobe.com/) och från **Ökning** sida, markera **Adobe Experience Manager as a Cloud Service** från **Produkter och tjänster** kort.

   ![AEM som produkt](/help/journey-onboarding/assets/assign-team1.png)

1. Navigera till **Cloud Manager** -instans i listan över alla instanser.

   ![Cloud Manager](/help/journey-onboarding/assets/assign-team2.png)

1. Du kan se en lista över förkonfigurerade Cloud Manager-produktprofiler.

   ![Produktprofiler](/help/journey-onboarding/assets/assign-team3.png)

De viktigaste profilerna att tilldela som en del av den inledande processen är:

* **Företagsägare** - Dessa användare hanterar olika program.
* **Distributionshanteraren** - Dessa användare distribuerar kod från dina databaser till miljöer där AEM körs.
* **Utvecklare** - Dessa användare utvecklar dina anpassade AEM och implementerar kod i dina databaser.

Ta reda på vad rollerna är och vad de gör genom att gå igenom din lista med teammedlemmar för att avgöra vem som behöver vilken profil. Tänk på att användare kan ha och ofta ha flera roller i ditt team och därför även behöver flera profiler.

## Tilldela produktprofilen för företagsägare {#assign-business-owner}

Nu kan du lägga till användare och tilldela dem till **Företagsägare** produktprofil.

1. Identifiera de användare som behöver hantera Cloud Manager-program. De här är dina **Affärsägare**.

1. Logga in på Admin Console vid `[adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview)` och **Ökning** sida, markera **Adobe Experience Manager as a Cloud Service** produkt från **Produkter och tjänster** kort.

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

Dina **Företagsägare** har tilldelats och har nu åtkomst till Cloud Manager. Glöm inte att utse dig själv till systemadministratör för **Företagsägare** profil.

## Tilldela produktprofilen för Distributionshanteraren {#assign-deployment-manager}

1. Identifiera de användare som behöver distribuera kod.

1. Logga in på Admin Console vid `[adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview)` och **Ökning** sidmarkering **Adobe Experience Manager as a Cloud Service** produkten från **Produkter och tjänster** kort.

   ![Produkter och tjänster](/help/journey-onboarding/assets/assign-team1.png)

1. Välj **Användare** i den övre navigeringen och sedan väljer **Lägg till användare**.

   ![Lägg till användare](/help/journey-onboarding/assets/assign-team4.png)

1. I **Lägg till användare i ditt team** anger du e-post-ID för den användare som du vill lägga till.

   * Om det federerade ID:t för dina teammedlemmar inte har konfigurerats än väljer du **Adobe ID** för **ID-typ**.

   ![Ange ID](/help/journey-onboarding/assets/assign-team5.png)

1. Klicka på plusknappen under **Välj produkter eller användargrupper** rubrik för att börja produktval och välja **Adobe Experience Manager as a Cloud Service** och tilldela **Distributionshanteraren** produktprofil för användaren.

   ![Tilldela profil](/help/journey-onboarding/assets/assign-team6.png)

Dina **Distributionshanteraren** har tilldelats och har nu åtkomst till Cloud Manager. Beroende på ditt framtida ansvar kan du behöva utse dig själv som systemadministratör till **Distributionshanteraren** profil.

## Tilldela produktprofilen för utvecklare {#assign-developer}

1. Identifiera de användare som behöver utveckla AEM program och hantera kod.

1. Logga in på Admin Console vid `[adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview)` och **Ökning** sidmarkering **Adobe Experience Manager as a Cloud Service** produkten från **Produkter och tjänster** kort.

   ![Produkter och tjänster](/help/journey-onboarding/assets/assign-team1.png)

1. Välj **Användare** i den övre navigeringen och sedan väljer **Lägg till användare**.

   ![Lägg till användare](/help/journey-onboarding/assets/assign-team4.png)

1. I **Lägg till användare i ditt team** anger du e-post-ID för den användare som du vill lägga till.

   * Om det federerade ID:t för dina teammedlemmar inte har konfigurerats än väljer du **Adobe ID** för **ID-typ**.

   ![Lägg till användar-ID](/help/journey-onboarding/assets/assign-team5.png)

1. Klicka på plusknappen under **Välj produkter eller användargrupper** rubrik för att börja produktval och välja **Adobe Experience Manager as a Cloud Service** och tilldela **Utvecklare** produktprofil för användaren.

   ![Tilldela profil](/help/journey-onboarding/assets/assign-team6.png).

Dina **Utvecklare** har tilldelats och har nu åtkomst till Cloud Manager. Beroende på ditt framtida ansvar kan du behöva utse dig själv som systemadministratör till **Utvecklare** profil.

## What&#39;s Next {#whats-next}

Grattis! Ditt nybildade Cloud Manager-team (inklusive dig själv som tilldelats till **Företagsägare** profil) har konfigurerats. I rollen **Företagsägare**&#x200B;är du nu bara ett steg ifrån att logga in i Cloud Manager och skapa dina molnresurser.

Under den här delen av introduktionsresan lärde du dig att tilldela teammedlemmar till profiler i Admin Console. Nu bör du:

* Förstå vilka produktprofiler som är.
* Förstå vad Cloud Manager är.
* Lär dig de tre viktiga produktprofilerna för Cloud Manager: **Företagsägare**, **Distributionshanteraren** och **Utvecklare**.
* Du kan tilldela teammedlemmar till Cloud Manager-produktprofiler.

Du är nu redo att fortsätta din introduktionsresa genom att granska dokumentet nästa gång [Access Cloud Manager,](cloud-manager.md) där du får lära dig att komma åt Cloud Manager och skapa dina projektresurser.

## Ytterligare resurser {#additional-resources}

Vi rekommenderar att du fortsätter med introduktionsresan enligt beskrivningen ovan. Det här är ytterligare resurser om du vill göra en djupdykning i ett visst ämne från den här resan.

* [Introduktion till Cloud Manager](/help/onboarding/cloud-manager-introduction.md) - Lär dig mer om Cloud Manager, Cloud Manager-program och miljöer.
* [Produktprofiler för Cloud Manager](/help/onboarding/aem-cs-team-product-profiles.md) - Läs mer om AEM as a Cloud Service team- och produktprofiler.
* [Identitetstyper på Adobe Admin Console](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/identity.ug.html) - Adobe identitetshanteringssystem hjälper administratörer att skapa och hantera användarnas åtkomst till program och tjänster. Adobe erbjuder dessa identitetstyper eller konton för att autentisera och auktorisera användare.

