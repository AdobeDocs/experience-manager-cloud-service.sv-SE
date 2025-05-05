---
title: Tilldela teammedlemmar till Cloud Manager produktprofiler
description: Följ den här sidan för att lära dig hur du tilldelar teammedlemmar till Cloud Manager produktprofiler
feature: Onboarding
role: Admin, User, Developer
exl-id: 555688e5-f937-462c-9fcc-b90685f1882b
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '1520'
ht-degree: 0%

---


# Tilldela teammedlemmar till Cloud Manager produktprofiler {#assign-team-members}

I den här delen av [introduktionsresan](overview.md) får du lära dig hur du tilldelar teammedlemmar till Cloud Manager produktprofiler.

## Syfte {#objective}

I det föregående steget i den här resan, [Åtkomst till Admin Console](admin-console.md), lärde du dig att logga in på Admin Console och verifiera dina behörigheter som systemadministratör. Nu kan du ge dina teammedlemmar tillgång till Cloud Manager. Det gör du genom att tilldela produktprofiler.

När du ger användare åtkomst till en Adobe-lösning behöver du inte nödvändigtvis ge dem full åtkomst. Med produktprofiler kan varje lösning ha en egen uppsättning användarbehörigheter. Du använder Admin Console för att tilldela produktprofiler.

Det första steget är att ge användare tillgång till Cloud Manager. Cloud Manager har stöd för företagsutvecklingsmiljöer och de specialbyggda CI/CD-pipelines som är utrustade för grundlig testning och högsta kodkvalitet för att leverera enastående upplevelser.

När du har läst det här dokumentet bör du:

* Förstå vilka produktprofiler som är.
* Förstå vad Cloud Manager är.
* Lär dig de tre viktiga Cloud Manager-produktprofilerna: **Business Owner**, **Deployment Manager** och **Developer**.
* Du kan tilldela teammedlemmar till Cloud Manager produktprofiler.

## Förutsättningar {#prerequisites}

Om du vill tilldela teammedlemmar till produktprofiler måste du ha information om teammedlemmarna, som måste ha tillgång till AEM as a Cloud Service, inklusive:

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

Som systemadministratör vet du att ett framgångsrikt AEM as a Cloud Service-projekt inte bara är beroende av att du skapar fantastiskt innehåll med hjälp av AEM, utan också av att du utvecklar och distribuerar din egen anpassade kod och program för att leverera ditt AEM.

Cloud Manager är en viktig del av AEM as a Cloud Service och används för att hantera dina CI/CD-pipelines för koddistribution, hantera kodarkiv och hantera miljöer.

Innan teamet kan göra något annat måste de bli medlemmar i Cloud Manager genom att ge dem de produktprofiler de behöver. I nästa steg visas var du kan hitta Cloud Manager produktprofil med Admin Console och hur du tilldelar den till dina teammedlemmar.

## Granska Cloud Manager produktprofiler {#review-product-profiles}

Med Admin Console kan du se en lista över Cloud Manager-profiler.

1. Logga in på Adobe Admin Console på [adminconsole.adobe.com](https://adminconsole.adobe.com/) och på sidan **Översikt** väljer du **Adobe Experience Manager as a Cloud Service** från kortet **Produkter och tjänster**.

   ![AEM som en produkt](/help/journey-onboarding/assets/assign-team1.png)

1. Navigera till **Cloud Manager**-instansen från listan med alla instanser.

   ![Cloud Manager](/help/journey-onboarding/assets/assign-team2.png)

1. Du kan se en lista över förkonfigurerade Cloud Manager-produktprofiler.

   ![Produktprofiler](/help/journey-onboarding/assets/assign-team3.png)

De viktigaste profilerna att tilldela som en del av den inledande processen är:

* **Affärsägare** - De här användarna hanterar olika program.
* **Distributionshanteraren** - De här användarna distribuerar kod från dina databaser till miljöer AEM körs.
* **Utvecklare** - Dessa användare utvecklar dina anpassade AEM och implementerar kod i dina databaser.

Ta reda på vad rollerna är och vad de gör genom att gå igenom din lista med teammedlemmar för att avgöra vem som behöver vilken profil. Tänk på att användare kan ha och ofta ha flera roller i ditt team och därför även behöver flera profiler.

## Tilldela produktprofilen för företagsägare {#assign-business-owner}

Du kan nu lägga till användare och tilldela dem till produktprofilen **Business Owner**.

1. Identifiera de användare som behöver hantera Cloud Manager-program. Detta är dina **företagsägare**.

1. Logga in på Admin Console på `[adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview)` och välj **Adobe Experience Manager as a Cloud Service**-produkt från **Produkter och tjänster** på **översiktssidan**.

   ![Produkter och tjänster](/help/journey-onboarding/assets/assign-team1.png)

1. Välj fliken **Användare** i den övre navigeringen och välj sedan **Lägg till användare**.

   ![Lägg till användare](/help/journey-onboarding/assets/assign-team4.png)

1. I dialogrutan **Lägg till användare i ditt team** anger du e-post-ID:t för den användare som du vill lägga till.

   * Om det federerade ID:t för dina teammedlemmar ännu inte har konfigurerats väljer du **Adobe ID** som **ID-typ**.

   ![Lägg till användarinformation](/help/journey-onboarding/assets/assign-team5.png)

1. Klicka på plusknappen under rubriken **Välj produkter eller användargrupper** för att börja produktvalet och välj **Adobe Experience Manager as a Cloud Service** och tilldela **företagsägare** produktprofilen till användaren.

   * Tilldela varje användare minst en produktprofil så att användaren kan komma åt Cloud Manager.
   * Kom ihåg att tilldela dig själv som systemadministratör till rollen **Affärsägare**.

   ![Tilldela användare](/help/journey-onboarding/assets/assign-team6.png)

1. Klicka på **Spara** och ett välkomstmeddelande skickas till användaren som du lade till. Den inbjudna användaren kan komma åt Cloud Manager genom att klicka på länken i välkomstmeddelandet och logga in med sin Adobe ID.

1. Upprepa dessa steg för användarna i ditt team.

Din **Business Owner** s har tilldelats och kan nu komma åt Cloud Manager. Glöm inte att tilldela dig själv som systemadministratör till **Business Owner** -profilen.

## Tilldela produktprofilen för Distributionshanteraren {#assign-deployment-manager}

1. Identifiera de användare som behöver distribuera kod.

1. Logga in på Admin Console på `[adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview)` och på sidan **Översikt** väljer du **Adobe Experience Manager as a Cloud Service**-produkt från kortet **Produkter och tjänster**.

   ![Produkter och tjänster](/help/journey-onboarding/assets/assign-team1.png)

1. Välj fliken **Användare** i den övre navigeringen och välj sedan **Lägg till användare**.

   ![Lägg till användare](/help/journey-onboarding/assets/assign-team4.png)

1. I dialogrutan **Lägg till användare i ditt team** anger du e-post-ID:t för den användare som du vill lägga till.

   * Om det federerade ID:t för dina teammedlemmar ännu inte har konfigurerats väljer du **Adobe ID** som **ID-typ**.

   ![Ange ID](/help/journey-onboarding/assets/assign-team5.png)

1. Klicka på plusknappen under rubriken **Välj produkter eller användargrupper** för att börja produktvalet och välj **Adobe Experience Manager as a Cloud Service** och tilldela **Distributionshanteraren** produktprofil till användaren.

   ![Tilldela profil](/help/journey-onboarding/assets/assign-team6.png)

**Distributionshanteraren** har tilldelats och kan nu komma åt Cloud Manager. Beroende på ditt framtida ansvar kan du behöva tilldela dig själv som systemadministratör till profilen **Distributionshanteraren** eller inte.

## Tilldela produktprofilen för utvecklare {#assign-developer}

1. Identifiera de användare som behöver utveckla AEM program och hantera kod.

1. Logga in på Admin Console på `[adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview)` och på sidan **Översikt** väljer du **Adobe Experience Manager as a Cloud Service**-produkt från kortet **Produkter och tjänster**.

   ![Produkter och tjänster](/help/journey-onboarding/assets/assign-team1.png)

1. Välj fliken **Användare** i den övre navigeringen och välj sedan **Lägg till användare**.

   ![Lägg till användare](/help/journey-onboarding/assets/assign-team4.png)

1. I dialogrutan **Lägg till användare i ditt team** anger du e-post-ID för den användare som du vill lägga till.

   * Om det federerade ID:t för dina teammedlemmar ännu inte har konfigurerats väljer du **Adobe ID** som **ID-typ**.

   ![Lägg till användar-ID](/help/journey-onboarding/assets/assign-team5.png)

1. Klicka på plusknappen under rubriken **Välj produkter eller användargrupper** för att börja produktvalet och välj **Adobe Experience Manager as a Cloud Service** och tilldela **utvecklarproduktprofilen** till användaren.

   ![Tilldela profil](/help/journey-onboarding/assets/assign-team6.png).

**Utvecklaren** har tilldelats och kan nu komma åt Cloud Manager. Beroende på ditt framtida ansvar kan du behöva tilldela dig själv som systemadministratör till profilen **Utvecklare** eller inte.

## What&#39;s Next {#whats-next}

Grattis! Ditt nybildade Cloud Manager-team (inklusive dig själv tilldelad profilen **Business Owner**) har konfigurerats. I rollen som **Affärsägare** är du nu bara ett steg från att logga in på Cloud Manager och aktivera skapandet av dina molnresurser.

Under den här delen av introduktionsresan lärde du dig att tilldela teammedlemmar till profiler i Admin Console. Nu bör du:

* Förstå vilka produktprofiler som är.
* Förstå vad Cloud Manager är.
* Lär dig de tre viktiga Cloud Manager-produktprofilerna: **Business Owner**, **Deployment Manager** och **Developer**.
* Du kan tilldela teammedlemmar till Cloud Manager produktprofiler.

Du kan nu fortsätta din introduktionsresa genom att nästa gång granska dokumentet [Åtkomst till Cloud Manager](cloud-manager.md) där du får lära dig hur du kommer åt Cloud Manager och skapar dina projektresurser.

## Ytterligare resurser {#additional-resources}

Vi rekommenderar att du fortsätter med introduktionsresan enligt beskrivningen ovan. Det här är ytterligare resurser om du vill göra en djupdykning i ett visst ämne från den här resan.

* [Cloud Manager Introduktion](/help/onboarding/cloud-manager-introduction.md) - Läs mer om Cloud Manager, Cloud Manager-program och miljöer.
* [Cloud Manager produktprofiler](/help/onboarding/aem-cs-team-product-profiles.md) - Lär dig mer om AEM as a Cloud Service team och produktprofiler.
* [Identitetstyper på Adobe Admin Console](https://helpx.adobe.com/se/enterprise/admin-guide.html/enterprise/using/identity.ug.html) - Med identitetshanteringssystemet i Adobe kan administratörer skapa och hantera användarnas åtkomst till program och tjänster. Adobe erbjuder dessa identitetstyper eller konton för att autentisera och auktorisera användare.

