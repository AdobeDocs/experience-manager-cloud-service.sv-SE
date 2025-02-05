---
title: Uppgifter för utvecklare och distributionsansvarig
description: När systemadministratören har konfigurerat de molnresurser som behövs kan du lära dig hur utvecklare och distributionsansvariga kan få åtkomst till Git för att utveckla program och använda rörledningar för att distribuera dem.
feature: Onboarding
role: Admin, User, Developer
exl-id: f57a856b-0932-4e8f-be59-a19fe692e2ab
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '1397'
ht-degree: 0%

---


# Uppgifter för utvecklare och distributionsansvarig {#developer-deployment-manager}

I den här valfria delen av [introduktionsresan](overview.md) får du lära dig hur utvecklare och distributionsansvariga kan komma åt Git för att utveckla program och använda rörledningar för att distribuera dem.

## Story hittills {#story-so-far}

Du har kommit långt på din startresa! Grattis! Systemadministratören har slutfört introduktionsresan genom att konfigurera nödvändiga molnresurser och bevilja åtkomst i dokumentet [Tilldela AEM produktprofiler](assign-profiles-aem.md).

Nu kan utvecklare och distributionsansvariga börja skapa egna program medan AEM kan börja skapa innehåll. I det här fallet är introduktionen klar och nu är det dags att använda ditt nya AEM as a Cloud Service-system, som det här dokumentet visar.

## Målgrupp {#audience}

Det här dokumentet är därför skrivet från perspektivet för **utvecklaren** och **distributionshanteraren**.

Systemadministratören kan även utföra samma uppgifter, men i allmänhet innehas de här rollerna av olika användare.

## Syfte {#objective}

Det här dokumentet är ett komplement till introduktionsresan som demonstrerar de grundläggande uppgifterna för en utvecklare och en driftsättningshanterare när systemadministratören har anslutit sig till alla användare och skapat de molnresurser som krävs.

När du har läst det här dokumentet bör du:

* Som utvecklare kan du förstå hur du får åtkomst till och hanterar dina Cloud Manager Git-databaser.
* Som driftsättningshanterare kan du konfigurera pipelines och driftsätta koden i Cloud Manager.

## Utvecklare och driftsättningschefer {#roles}

När systemadministratören har slutfört de huvudsakliga startåtgärderna för att skapa användare och konfigurera molnresurser är de användare som vanligtvis är mest angelägna om att få tillgång till systemet utvecklare och distributionschefer. Det beror på att de är de som ansvarar för att skapa dina anpassade program ovanpå AEM as a Cloud Service.

* **Utvecklare** - De här användarna får åtkomst till Cloud Manager Git-databaser där de hanterar koden för dina AEM anpassade program.
* **Distributionshanterare** - De här användarna använder Cloud Manager för att skapa och köra pipelines som distribuerar koden från Git-databaserna till dina AEM miljöer.

Beroende på organisationens behov kan samma användare ha båda rollerna.

## Förutsättningar {#prerequisites}

Innan du börjar de uppgifter som beskrivs i det här dokumentet som utvecklare eller distributionshanterare måste du se till att systemadministratören har slutfört alla steg i den här introduktionsresan. Detta innebär att

* Din systemadministratör har tilldelat utvecklare och distributionsansvariga till sina respektive produktprofiler.
* Utvecklare måste dessutom tilldelas produktprofilerna **AEM Användare** eller **AEM Administratörer** för att kunna använda AEM.
* Molnresurser har konfigurerats.

## Åtkomst till Git {#accessing-git}

Du kan komma åt och hantera dina Git-databaser med hjälp av självbetjäningskonto från Cloud Manager.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. Navigera till **Pipelines**-kortet från sidan **Programöversikt** och leta upp knappen **Åtkomstinformation** för att komma åt och hantera din Git-databas.

   ![Knappen Åtkomst till information om upprepning på miljökortet](/help/implementing/cloud-manager/assets/repos/access-repo1.png)

1. Klicka på knappen **Visa information om upprepning** för att öppna en dialogruta för att visa:

   * URL:en till Cloud Manager Git-databasen.
   * Git-användarnamn.
   * Git-lösenordet, vars värde visas när användaren klickar på knappen **Skapa lösenord**.

   ![Databasinformation](/help/implementing/cloud-manager/assets/repos/access-repo-create.png)

Med dessa inloggningsuppgifter kan användaren klona en lokal kopia av databasen och göra ändringar i den lokala databasen, och när den är klar kan han eller hon implementera kodändringar i fjärrkoddatabasen i Cloud Manager.

## Inställningar för pipeline {#setup-pipeline}

När utvecklarna har lagt till egen kod i Git-databaserna kan driftsättningshanteraren skapa och köra pipelines för att distribuera koden till dina AEM miljöer.

Följ de här stegen för att skapa din första icke-produktionspipeline.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. Gå till kortet **Pipelines** från Cloud Manager hemskärm. Klicka på **+Lägg till** och välj **Lägg till icke-produktionsförlopp**.

   ![Lägg till icke-produktionsflöde](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. På fliken **Konfiguration** i dialogrutan **Lägg till icke-produktionsförlopp** väljer du den typ av icke-produktionsförlopp du ska lägga till. I det här exemplet väljer du **Distributionspipeline**.

   ![Lägg till icke-produktion-pipeline-dialogruta](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config.png)

1. Ange ett **icke-produktionsförloppsnamn** för att identifiera din pipeline tillsammans med följande ytterligare information.

1. För **utlösaren för distribution** väljer du **Manuell** så att pipelinen endast körs när du startar den.

1. Klicka på **Fortsätt**.

1. På fliken **Source Code** i dialogrutan **Add Non-Production Pipeline** måste du välja vilken typ av kod som pipeline ska bearbeta. I det här exemplet väljer du **Fullständig stackkod**.

1. På fliken **Source Code** måste du definiera följande alternativ.

   * **Berättigade distributionsmiljöer** - Du måste välja vilken miljö pipelinen ska distribueras till.
   * **Databas** - Det här alternativet definierar från vilken Git-repo pipelinen ska hämta koden.
   * **Git Branch** - Det här alternativet definierar från vilken gren i den valda pipeline som ska hämta koden.
      * Ange de första tecknen i förgreningsnamnet och funktionen Komplettera automatiskt i det här fältet hittar de grenar som matchar dig.

   ![Pipeline i full hög](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-full-stack.png)

1. Klicka på **Spara**.

Nu har du skapat din första pipeline! Användare med rollen som distributionshanterare kan nu starta pipeline från Cloud Manager-gränssnittet.

## Distribuera {#deploy}

Nu när utvecklarna har lagt till sin egen kod i Git-databaserna och du har skapat en pipeline för att distribuera koden är det dags att köra pipeline för att faktiskt flytta koden från Git till din miljö.

![Förloppskort i Cloud Manager](/help/implementing/cloud-manager/assets/configure-pipeline/pipelines-card.png)

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. Navigera till kortet **Pipelines** på sidan **Programöversikt** och klicka på ellipsknappen bredvid den pipeline du skapade i föregående avsnitt och välj **Kör** på menyn.

1. Pipeline-körningen börjar och anges av kolumnen **Status**.

Du kan se information om körningen genom att klicka på ellipsknappen igen och välja **Visa information**.

Grattis! Nu har du distribuerat kod från din Git-databas till en icke-produktionsmiljö!

## What&#39;s Next {#whats-next}

Nu när du har läst det här dokumentet bör du:

* Som utvecklare kan du förstå hur du får åtkomst till och hanterar dina Cloud Manager Git-databaser.
* Som driftsättningshanterare kan du konfigurera pipelines och driftsätta koden i Cloud Manager.

Du har kommit igång som utvecklare eller driftsättningshanterare och inte bara har kunskap om Cloud Manager utan även om arbetsmiljöer, databaser och rörledningar! Men det finns mer att lära sig om AEM as a Cloud Service kraftfulla verktyg för CI/CD. Mer information finns i avsnittet [Ytterligare resurser](#additional-resources).

Om du är intresserad av hur innehållsförfattare får åtkomst till och använder AEM som en molntjänst kan du fortsätta till den sista delen av introduktionsresan, [AEM Användaruppgifter](aem-users.md).

>[!TIP]
>
>Nu när du har anslutit dig kan du [lära dig hur du enkelt lägger till AEM Reference Demos Add-On](/help/journey-sites/demos-add-on/overview.md) i en sandlådemiljö med minimal AEM och kan testa de kraftfulla funktionerna i AEM med detaljerade exempel baserade på bästa praxis.

## Ytterligare resurser {#additional-resources}

Här följer ytterligare, valfria resurser om du vill gå längre än vad som ingår i introduktionsresan.

* [Åtkomst till databaser](/help/implementing/cloud-manager/managing-code/accessing-repos.md) - Lär dig hur du får åtkomst till och hanterar din Git-databas med hjälp av Git-kontohantering för självbetjäning från Cloud Manager.
* [Använda Git med Cloud Manager](/help/implementing/cloud-manager/managing-code/integrating-with-git.md) - Lär dig hur du använder Cloud Manager Git-databaser och hur du integrerar din egen kundhanterade Git-databas med Cloud Manager.
* [Lokal utvecklingsmiljö - konfigurera](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html) - I den här självstudiekursen får du hjälp med att konfigurera en lokal utvecklingsmiljö för Adobe Experience Manager (AEM) med AEM as a Cloud Service SDK.
* [Komma igång med AEM Sites - WKND-självstudiekurs](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html) - Den här självstudiekursen i flera delar är utformad för utvecklare som är nybörjare i Adobe Experience Manager (AEM). Den här självstudiekursen går igenom implementeringen av en AEM sajt för ett fiktivt livsstilsmärke, WKND. Självstudiekursen behandlar grundläggande ämnen som projektinställningar, kärnkomponenter, redigerbara mallar, klientbibliotek och komponentutveckling med Adobe Experience Manager Sites.
* [Komma igång med SPA i AEM med Reagera](/help/implementing/developing/hybrid/getting-started-react.md) - I den här artikeln visas ett exempel SPA programmet, hur det sätts ihop och hur du snabbt kommer igång med ditt eget SPA med React Framework.
* [Komma igång med SPA i AEM med Angular](/help/implementing/developing/hybrid/getting-started-angular.md) - I den här artikeln visas ett exempel SPA programmet, hur det är sammansatt och hur du snabbt kommer igång med ditt eget SPA med hjälp av Angularnas ramverk.
* [Headless Developer Journey](/help/journey-headless/developer/overview.md) - Börja här om du vill ha en guidad kurs om hur du utvecklar headless-program med AEM.
