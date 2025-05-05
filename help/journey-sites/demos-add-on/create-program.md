---
title: Skapa program
description: Lär dig hur du konfigurerar ett nytt program och en ny pipeline för att distribuera tillägget.
exl-id: 06287618-0328-40b1-bba8-84002283f23f
feature: Onboarding
role: Admin, User, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 0%

---


# Skapa program {#creating-a-program}

Lär dig hur du konfigurerar ett nytt program och en ny pipeline för att distribuera tillägget.

## Story hittills {#story-so-far}

I det föregående dokumentet om tillägget Adobe Experience Manager (AEM) Reference Demos, [Understanding Reference Demo Add-on Installation](installation.md), fick du veta hur installationsprocessen för tillägget Reference Demos fungerar och visar hur de olika delarna fungerar tillsammans. Nu bör du:

* Få en grundläggande förståelse för Cloud Manager.
* Förstå hur rörledningar levererar innehåll och konfigurationer till AEM.
* Se hur mallarna kan skapa webbplatser med demomaterial med bara några klick.

Den här artikeln bygger på dessa grundläggande funktioner och tar det första konfigurationssteget för att skapa ett program för testning och använder en pipeline för att distribuera tilläggsinnehållet.

## Syfte {#objective}

Det här dokumentet hjälper dig att förstå hur du konfigurerar ett nytt program och en ny pipeline för att distribuera tillägget. Efter läsning bör du kunna göra följande:

* Förstå och förklara hur man använder Cloud Manager för att skapa ett program.
* Aktivera tillägget Referensdemonstrationer för det nya programmet.
* Kör en pipeline så att du kan distribuera tilläggsinnehållet.

## Skapa ett program {#create-program}

När du har loggat in på Cloud Manager kan du skapa ett sandlådeprogram för testning och demo.

>[!NOTE]
>
>Användaren måste vara medlem i rollen **Business Owner** i Cloud Manager i din organisation för att kunna skapa program.

1. Logga in på Adobe Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/).

1. När du är inloggad kontrollerar du att du är i rätt ordning genom att kontrollera den i skärmens övre högra hörn. Om du bara är medlem i en organisation är det här steget inte nödvändigt.

   ![Cloud Manager - översikt](assets/cloud-manager.png)

1. Välj **Lägg till program** längst upp till höger i fönstret.

1. I dialogrutan **Skapa ditt program**:

   1. Ange ett **programnamn** som beskriver ditt program.
   1. Välj **Konfigurera en sandlåda** för ditt **programmål**
   1. Välj **Fortsätt**.

   ![Dialogrutan Skapa program](assets/create-program.png)

1. I dialogrutan **Konfigurera din sandlåda** i tabellen **Lösningar och tillägg** expanderar du posten **Platser** i listan genom att trycka eller klicka på den och sedan markera **Referensdemonstrationer**.

   * Om du även vill skapa demos för AEM Screens markerar du alternativet **Screens** i listan. Välj **Uppdatera**.

   ![Väljer tillägg för referensdemo i programkonfiguration](assets/select-reference-demo-add-on.png)


1. Välj **Skapa** så börjar Cloud Manager konfigurera ditt sandlådeprogram. Du kommer nu till programöversikten och ett kort banderollmeddelande anger att processen har startats. Ett kort har lagts till på översiktssidan för ditt nya program. Installationsprocessen tar några minuter.

1. När konfigurationen är klar visas miljökortets status som **Klar** på översiktssidan. Markera kortet så att du kan öppna miljön.

   ![Programmet har skapats](assets/ready.png)

1. Miljön är klar och tillägget är nu aktiverat som ett alternativ, men innehållet i demon måste distribueras för att AEM ska vara tillgängligt. Det gör du genom att markera ellipsknappen bredvid pipelinen Distribuera till utvecklare på kortet **Pipelines** och välja **Kör**.

   ![Start](assets/run.png)

1. Pipelinen börjar och du dirigeras till en sida med information om distributionsförloppet. Du kan navigera bort från den här skärmen när programmet skapas och returnera det senare om det behövs.

   ![Distribution](assets/deployment.png)

Det kan ta flera minuter att slutföra pipelinen. När det är klart är tillägget och dess demoinnehåll tillgängliga för användning i AEM redigeringsmiljö.

## What&#39;s Next {#what-is-next}

Nu när du har slutfört den här delen av AEM Reference Demo Add-on ska du:

* Lär dig hur du använder Cloud Manager för att skapa ett program.
* Lär dig hur du aktiverar tillägget Referensdemonstrationer för programmet.
* Du kan köra en pipeline så att du kan distribuera tilläggsinnehållet.

Bygg vidare på den här kunskapen och fortsätt din AEM Reference Demo Add-on-resa genom nästa granskning av [Skapa en demowebbplats](create-site.md). Där lär du dig att skapa en demowebbplats i AEM baserat på ett bibliotek med förkonfigurerade mallar som distribuerades via pipeline.

## Ytterligare resurser {#additional-resources}

* [Cloud Manager-dokumentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/onboarding-concepts/cloud-manager-introduction.html?lang=sv-SE) - Om du vill ha mer information om Cloud Manager funktioner kan det vara bra att läsa den detaljerade tekniska dokumentationen.
