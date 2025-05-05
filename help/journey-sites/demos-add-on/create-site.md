---
title: Skapa demowebbplats
description: Skapa en demowebbplats i AEM baserat på ett bibliotek med förkonfigurerade mallar.
exl-id: e76fd283-12b2-4139-9e71-2e145b9620b1
feature: Onboarding
role: Admin, User, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '809'
ht-degree: 0%

---

# Skapa demowebbplats {#creating-a-site}

Skapa en demowebbplats i AEM baserat på ett bibliotek med förkonfigurerade mallar.

## Story hittills {#story-so-far}

I det föregående dokumentet om AEM Reference Demos Add-On-resan, [Create Program](create-program.md), tog du det första konfigurationssteget för att skapa ett program för testningsändamål och använde en pipeline för att distribuera tilläggsinnehållet. Nu bör du:

* Lär dig hur du använder Cloud Manager för att skapa ett program.
* Lär dig hur du aktiverar tillägget Referensdemonstrationer för det nya programmet.
* Du kan köra en pipeline för att distribuera tilläggsinnehållet.

I den här artikeln beskrivs nästa steg i processen genom att skapa en webbplats eller ett AEM Screens-projekt i AEM baserat på mallarna i tillägget Referensdemo.

## Syfte {#objective}

Det här dokumentet hjälper dig att förstå hur du skapar en webbplats baserat på mallarna för tillägget Referensdemo. När du har läst bör du:

* Lär dig hur du kommer åt AEM.
* Lär dig hur du skapar en webbplats baserad på en mall.
* Förstå grunderna för navigering i webbplatsstrukturen och redigering av en sida.

## Skapa en demowebbplats eller Screens Project {#create-site}

När pipeline har distribuerat tillägget för referensdemo kan du komma åt AEM redigeringsmiljö och skapa demowebbplatser baserat på tilläggsinnehållet.

1. På programöversiktssidan i Cloud Manager väljer du länken till AEM.

   ![Åtkomst till redigeringsmiljön](assets/access-author.png)

1. Välj **Webbplatser** på AEM huvudmeny.

   ![Åtkomst till webbplatser](assets/access-sites.png)

1. I webbplatskonsolen väljer du **Skapa** längst upp till höger på skärmen och väljer **Plats från mall** i listrutan.

   ![Skapa webbplats från mall](assets/create-site-from-template.png)

1. Guiden Skapa webbplats startar. I den vänstra kolumnen ser du demomallarna som pipeline distribuerade till din redigeringsinstans. Markera den och visa information i den högra kolumnen. Om du vill testa eller demonstrera AEM Screens måste du välja webbplatsmallen **We.Cafe**. Välj **Nästa**.

   ![Guiden Skapa webbplats](assets/site-creation-wizard.png)

1. På nästa skärm anger du en titel för din webbplats eller ditt Screens-projekt. Om det utelämnas kan du ange eller generera ett platsnamn från titeln. Välj **Skapa**.

   * Platsens titel visas i webbläsarens namnlist.
   * Webbplatsnamnet blir en del av webbadressen.
   * Webbplatsnamnet måste uppfylla AEM regler för sidnamngivning, som det finns mer information om i avsnittet [Ytterligare resurser](#additional-resources).

   ![Webbplatsinformation](assets/site-details.png)

1. Webbplatsen har skapats med en dialogruta. Välj **Klar**.

   ![Webbplatsen har skapats](assets/site-creation-complete.png)

Nu har du skapat en egen demosajt!

## Använd demowebbplats {#use-site}

Nu när demowebbplatsen har skapats kan du navigera och använda den på samma sätt som andra webbplatser i AEM.

1. Platsen visas nu i webbplatskonsolen.

   ![Ny demowebbplats i webbplatskonsolen](assets/new-demo-site.png)

1. Kontrollera att konsolvyn är inställd på **Kolumnvy** i skärmens övre högra hörn.

   ![Kolumnvy](assets/column-view.png)

1. Välj webbplatsen för att utforska dess struktur och innehåll. Kolumnvyn utökas kontinuerligt när du navigerar i innehållsträdet på demowebbplatsen.

   ![Platsstruktur](assets/site-structure.png)

1. Markera en sida som du vill markera och välj sedan **Redigera** i verktygsfältet.

   ![Välj sida](assets/select-page.png)

1. Du kan redigera sidan som vilken annan AEM innehållssida som helst, till exempel lägga till eller redigera komponenter eller resurser och testa AEM funktioner.

   ![Redigera sida](assets/edit-page.png)

Grattis! Nu kan du utforska innehållet på din demowebbplats ytterligare och upptäcka allt som AEM har att erbjuda via det bästa innehållet i tillägget för referensdemo.

Skapa ytterligare sajter baserade på andra mallar för att utforska mer AEM funktionalitet.

## What&#39;s Next {#what-is-next}

Nu när du har slutfört den här delen av AEM Reference Demo Add-On-resan bör du:

* Lär dig hur du kommer åt AEM.
* Lär dig hur du skapar en webbplats baserad på en mall.
* Förstå grunderna för navigering i webbplatsstrukturen och redigering av en sida.

Nu kan du testa funktionerna i AEM med tilläggsinnehåll. Du har två alternativ för att fortsätta din resa:

* Om du vill demonstrera och testa AEM Screens-innehåll till fullo kontrollerar du att du har distribuerat en webbplats baserad på webbplatsmallen **We.Cafe** enligt beskrivningen ovan och fortsätter med [Aktivera AEM Screens för din demowebbplats](screens.md).
* Om du bara använder för att demonstrera webbplatsinnehåll kan du fortsätta med [Hantera dina demowebbplatser](manage.md), där du får lära dig mer om de verktyg som finns för att hantera dina demowebbplatser och hur du tar bort dem.

## Ytterligare resurser {#additional-resources}

* [Cloud Manager-dokumentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html?lang=sv-SE) - Om du vill ha mer information om Cloud Manager funktioner kan det vara bra att läsa den detaljerade tekniska dokumentationen.
* [Skapa plats](/help/sites-cloud/administering/site-creation/create-site.md) - Lär dig hur du använder AEM för att skapa en webbplats med hjälp av webbplatsmallar för att definiera webbplatsens format och struktur.
* [AEM sidnamnkonventioner](/help/sites-cloud/authoring/sites-console/organizing-pages.md#page-name-restrictions-and-best-practices). - På den här sidan finns information om hur du organiserar AEM sidor.
* [AEM Grundläggande hantering](/help/sites-cloud/authoring/basic-handling.md) - Utforska det här dokumentet om du inte AEM förstå grundläggande begrepp som navigering och konsolorganisation.
